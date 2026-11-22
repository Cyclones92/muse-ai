# How to Build a Local RAG Over Your Own Notes 🔍⚡

> **Author:** Cyclones92
> **Category:** muse-ai
> **Last updated:** 2026-11-22
> **Works with:** A folder of Markdown notes, a local embedding model, a local LLM, and a small script (Python examples below)

## What this does

RAG — retrieval-augmented generation — lets a language model answer questions from *your* documents instead of just its training. This guide builds a small, fully local version over a folder of Markdown notes: your notes are split into chunks, embedded into a local database, and when you ask a question the most relevant chunks are retrieved and handed to a local model, which answers **and names the source note**.

Everything runs on your own machine. No notes leave the box, and because every answer cites its source, you can check it instead of trusting it.

## Prerequisites

- A folder of notes in plain Markdown — one topic per note works best
- Python 3.11+ with `sqlite3` (in the standard library)
- A local embedding model (any small embedding model your local model server can run)
- A local LLM served on your own machine (examples use `http://localhost:1234` — substitute your own host/port)
- Example user: `Cyclones92`, example notes folder: `~/notes/` — substitute your own

## Steps

### 1. Make your notes RAG-friendly

Retrieval is only as good as the chunks it finds. Three habits make a big difference:

- **One topic per note.** A note called `network-setup.md` that covers one setup beats a 40-topic dump file.
- **Facts first, plain Markdown.** Headings and short paragraphs chunk cleanly; giant tables and nested lists chunk badly.
- **Descriptive filenames and headings.** The embedder sees the text, and a good heading is the densest summary of what's under it.

You don't need to rewrite everything — just start writing *new* notes this way and clean up the worst offenders.

### 2. Index: chunk and embed

```python
# index.py — walk the notes folder, chunk, embed, store
import os, sqlite3, urllib.request, json

NOTES = os.path.expanduser("~/notes")
DB = "rag.db"
EMBED_URL = "http://localhost:1234/v1/embeddings"  # example local endpoint
EMBED_MODEL = "your-embedding-model"               # placeholder

def embed(text):
    req = urllib.request.Request(
        EMBED_URL,
        data=json.dumps({"model": EMBED_MODEL, "input": text}).encode(),
        headers={"Content-Type": "application/json"},
    )
    with urllib.request.urlopen(req) as r:
        return json.load(r)["data"][0]["embedding"]

db = sqlite3.connect(DB)
db.execute("CREATE TABLE IF NOT EXISTS chunks (source TEXT, text TEXT, vec TEXT)")
db.execute("DELETE FROM chunks")  # full rebuild keeps it simple and honest

for root, _, files in os.walk(NOTES):
    for f in files:
        if not f.endswith(".md"):
            continue
        path = os.path.join(root, f)
        text = open(path, encoding="utf-8").read()
        # Chunk on paragraph breaks, ~800 characters per chunk
        paras, buf = text.split("\n\n"), ""
        for p in paras:
            if len(buf) + len(p) > 800 and buf:
                db.execute("INSERT INTO chunks VALUES (?,?,?)",
                           (f, buf, json.dumps(embed(buf))))
                buf = ""
            buf += p + "\n\n"
        if buf.strip():
            db.execute("INSERT INTO chunks VALUES (?,?,?)",
                       (f, buf, json.dumps(embed(buf))))
db.commit()
print("Indexed. Re-run this after you change notes.")
```

Re-run `index.py` whenever notes change. A full rebuild is slower than incremental updates and much harder to get subtly wrong — for a personal notes folder, simple wins.

### 3. Ask: retrieve, then answer with sources

```python
# ask.py — embed the question, find nearest chunks, answer with citations
import sys, sqlite3, json, math, urllib.request

DB = "rag.db"
CHAT_URL = "http://localhost:1234/v1/chat/completions"  # example local endpoint
CHAT_MODEL = "your-local-llm"                            # placeholder

def embed(text): ...  # same helper as index.py

def cosine(a, b):
    dot = sum(x * y for x, y in zip(a, b))
    return dot / (math.sqrt(sum(x * x for x in a)) * math.sqrt(sum(y * y for y in b)))

q = " ".join(sys.argv[1:])
qv = embed(q)
rows = sqlite3.connect(DB).execute("SELECT source, text, vec FROM chunks").fetchall()
top = sorted(rows, key=lambda r: cosine(qv, json.loads(r[2])), reverse=True)[:5]
context = "\n\n".join(f"[{s}]\n{t}" for s, t, _ in top)

prompt = (
    "Answer using ONLY the notes below. Name the source note for every claim. "
    "If the notes don't cover it, say so — do not guess.\n\n" + context
)
req = urllib.request.Request(
    CHAT_URL,
    data=json.dumps({"model": CHAT_MODEL,
                     "messages": [{"role": "user", "content": prompt + "\n\nQuestion: " + q}]}).encode(),
    headers={"Content-Type": "application/json"},
)
with urllib.request.urlopen(req) as r:
    print(json.load(r)["choices"][0]["message"]["content"])
```

### 4. The two rules that make it trustworthy

Bake these into the prompt, not just your intentions:

1. **Cite the source note for every claim.** An answer you can't trace is an answer you can't check.
2. **"Not in my notes" is a valid answer.** Without an explicit permission to say it doesn't know, the model will fill gaps from training and present them in the same confident voice as your actual notes.

## Verify it worked

Ask a question whose answer lives in exactly one note, and a question your notes definitely don't cover:

```bash
python3 ask.py "what did I decide about <topic in one note>?"
python3 ask.py "what is the capital of a topic I have never written about?"
```

Expected: the first answer cites the right note; the second says it's not in your notes instead of answering from general knowledge.

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Answers sound generic, no citations | The retrieval step returned weak chunks — check the question is actually covered by a note, and lower chunk size so topics don't dilute each other |
| Right note exists but never surfaces | Its heading/filename may not match how you ask. Add a plain-language summary line at the top of the note |
| Model answers from training anyway | Strengthen rule 2 in the prompt and reduce retrieved chunks — too much irrelevant context invites improvisation |
| Index is stale after edits | Re-run `index.py`; make it a habit (or a scheduled job) after note-writing sessions |

## Notes

- Start with the notes folder you actually maintain. Indexing an abandoned archive teaches you nothing about whether *you'll* use it.
- Keep the database and scripts next to each other in one small folder (e.g. `~/rag/`) — the whole system should be portable enough to copy to another machine in one go.
- This pairs well with [Prompt: Verify Before You Claim It's Done](prompt-verify-before-you-claim-done.md): citations are verification built into the answer.
- All hosts, models, and paths in this guide are examples or placeholders — substitute your own local setup.

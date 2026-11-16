# How to Set Up SSH Key Login (Example Guide)

> **Author:** Cyclones92
> **Category:** linux
> **Last updated:** 2026-11-16
> **Tested on:** Debian 13

## What this does

Log in to a Linux server with a key instead of a password — faster and safer.

## Prerequisites

- A server at `server1.example.com` (`192.0.2.10`)
- A user named `Cyclones92` in these examples

## Steps

### 1. Generate a key on your machine

```bash
ssh-keygen -t ed25519 -C "user@example.com"
```

### 2. Copy the public key to the server

```bash
ssh-copy-id Cyclones92@server1.example.com
```

### 3. Log in with the key

```bash
ssh Cyclones92@server1.example.com
```

## Verify it worked

You should land on the server without being asked for the account password.

## Notes

- Keys > passwords. Always. 🔑

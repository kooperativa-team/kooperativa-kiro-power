---
name: setup
description: This skill should be used when the user wants to install, connect, or troubleshoot the Kooperativa power, for example when the kooperativa_* tools are missing, return 401, or return 402. It explains the API key and license requirements without ever handling the key in the conversation.
license: MIT
metadata:
  category: business
  author: kooperativa-team
---

# Kooperativa setup

The Kooperativa power starts the official MCP server (`@kooperativa_team/mcp-server`) and reads the user's API key from the `KOOPERATIVA_API_KEY` environment variable.

## Requirements

- A Kooperativa account with an active license. Accounts are invite-only. Access requests go to https://kooperativa.io/signup.
- An API key, created by the user at https://kooperativa.io/api-keys. Keys start with `ik_live_` and are shown once.
- Node.js 18 or newer, because the server is started with `npx`.

## Steps

1. Ask the user to set `KOOPERATIVA_API_KEY` in the environment that Kiro is started from, then restart Kiro so the power can read it.
2. Never ask the user to paste the key into the chat, a file in the project, or a command line. If a key is pasted anyway, tell the user to revoke it at https://kooperativa.io/api-keys and create a new one.
3. Check the connection with the `kooperativa_account_info` tool. It is free.

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| No `kooperativa_*` tools | The power is not installed, Node.js is missing, or Kiro was not restarted after the variable was set |
| 401 `API_KEY_INVALID` | The key is missing, revoked, or the variable was not read. The literal text `${KOOPERATIVA_API_KEY}` as a key means the variable was not expanded |
| 402 `LICENSE_INACTIVE` | The workspace has no active license |
| 402 `REALTIME_REQUIRES_PAID_LICENSE` | The `*_realtime` tools need a workspace with a billing relationship |
| 429 | Per-minute rate limit reached. Wait for the `Retry-After` seconds |

Documentation: https://docs.kooperativa.io. Support: support@kooperativa.io.

# Kooperativa power for Kiro

Find and qualify B2B leads from inside Kiro. This power connects Kiro to the Kooperativa data API through the official MCP server and adds two skills that tell the agent how to use it.

Kooperativa returns structured people and company records: work history, education, skills, company details, headcount, decision makers, hiring signals and job changes. It has **no contact data**: no email addresses and no phone numbers.

## What is included

| Part | What it does |
|---|---|
| `mcp.json` | Starts `@kooperativa_team/mcp-server` (24 tools) over stdio, pinned to an exact version. It contains no key and no `env` block |
| `skills/kooperativa-lead-generation` | A workflow for ICP-based lead lists: confirm the inputs, search, shortlist, enrich, report honestly |
| `skills/setup` | Connection and troubleshooting guidance |

## Requirements

- A Kooperativa account with an active license. Accounts are invite-only: request access at https://kooperativa.io/signup.
- An API key, created at https://kooperativa.io/api-keys. Keys are shown once.
- Node.js 18 or newer (the server is started with `npx`).

## Install

In the Kiro IDE: Powers panel, **Add Custom Power**, **Import power from GitHub**, then enter
`https://github.com/kooperativa-team/kooperativa-kiro-power`.

For a local copy, clone this repository and use **Import power from a folder**. In Kiro CLI, `/powers install <path>` installs from a local directory.

## Configure the API key

Kiro does not expand environment placeholders in a power's `mcp.json`, and a desktop app does not always inherit your shell variables, so the key is stored once by the server itself. In a terminal, run:

```bash
npx -y @kooperativa_team/mcp-server login
```

It asks for the key with input hidden, checks it against the API, and saves it to `~/.kooperativa/config.json` with mode 600. It prints only your account email and license state. Restart Kiro afterwards.

The server also accepts a real key in the `KOOPERATIVA_API_KEY` environment variable when Kiro is started from a shell that has it set. The key is sent only to `https://kooperativa.io/api/v1`.

Do not paste the key into a chat or commit it to a repository. This package contains no credentials.

## Costs and safety

- Standard tools are covered by the workspace license.
- The two `*_realtime` tools are metered at $0.001 per call and bill even when the lookup finds nothing. The skill asks for confirmation before using them.
- Profile and company text is written by third parties. The skills treat it as data and never as instructions.
- A `451 DATA_SUBJECT_BLOCKED` response means a record was withdrawn at the person's request. The skills stop and do not try to retrieve it another way.
- Monitors (webhook subscriptions) are created or deleted only on an explicit request.

## Privacy and support

- Privacy policy: https://kooperativa.io/legal/privacy
- Terms: https://kooperativa.io/legal/terms
- Data removal requests: https://kooperativa.io/legal/removal-request
- Documentation: https://docs.kooperativa.io
- Support: support@kooperativa.io
- MCP server source: https://github.com/kooperativa-team/kooperativa-mcp

## Versioning

`mcp.json` pins the MCP server to an exact version so an unreviewed release is never started on a user's machine. A new power version is published when the pin is updated.

## License

MIT, see [LICENSE.md](./LICENSE.md).

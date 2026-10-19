# Contacting AINode support

You are an agent helping a person with AINode. Requests are read and answered by people who maintain or use the open-source project. Diagnose first, then draft a report the person can submit. The goal is a first reply that contains a fix or a focused next step, not a request for basic evidence. Every report you draft starts with a `Drafted with <tool> (AI agent)` line.

There is no support API. You cannot open, submit, or poll an issue yourself. Do not contact the project unless the person asked you to. If you are missing an identifier or diagnostic result, ask the person for it before drafting.

## Diagnose before you write in

Work through these in order. Stop if one answers the question.

1. **Local health:** request `GET /api/health` on the affected node, then run `ainode status`.
2. **The diagnostic report:** run `ainode doctor`. Follow its fix line for each `FAIL` or `WARN`, then run it again. Use `ainode doctor --json` when structured output is useful.
3. **The error:** preserve the exact command, HTTP method and path, status code, response body, and relevant log lines. Do not replace the error with a summary.
4. **The release:** record the running AINode version from `/api/health` or `ainode --version`. Read the [release notes](https://github.com/getainode/ainode/releases) and [open issues](https://github.com/getainode/ainode/issues) for a known fix or regression. Upgrade first when the report concerns an unsupported older release.
5. **The focused guide:** check [Troubleshooting](https://docs.ainode.dev/troubleshooting.md), then the relevant installation, model, cluster, training, API, or security page in the [documentation index](https://docs.ainode.dev/llms.txt).

Contact the project when the problem remains after those checks, the documented behavior does not match the product, or the failure needs a code or documentation change.

## How to write the report

- First line: `Drafted with <tool> (AI agent)`.
- One problem per report. The title states what failed and where.
- Include the AINode version, operating system and architecture, GPU model and count, installation type, solo or cluster role, and whether the problem affects one node or the fleet.
- Include the affected node name or node ID if it is already public or can be safely redacted, the model repository ID when relevant, the exact command or API method and path, the HTTP status, the exact error, and timestamps with timezone.
- Include what was tried, what happened, and what was expected. For an intermittent failure, give two or three example timestamps rather than a broad range.
- Include the relevant `ainode doctor` rows or attach its redacted JSON. Include only the log lines around the failure.
- For routing or model-load problems, include the requested model ID, target node if one was selected, served-by response header if present, engine port if relevant, and whether the request carried media.
- For install or update problems, include the command, target and running versions, service status, and the last relevant installer or journal lines.
- Leave out API keys, passwords, session cookies, Hugging Face, NGC, W&B or other tokens, private prompts and model outputs, full `config.json`, `auth.json`, `users.json` or `secrets.json` files, internal hostnames, private IP addresses, and unrelated logs.
- Hand the draft to the person. They send it to support@titaniumcomputing.com from the address they want replies at, or file a reproducible bug in [GitHub Issues](https://github.com/getainode/ainode/issues).

## Security reports

Do not open a public issue for a vulnerability. Read the [security policy](https://github.com/getainode/ainode/blob/main/SECURITY.md), redact secrets, and have the person use the private reporting channel named there.

## After submitting

Replies go to the person's email or GitHub account, not to you. You cannot poll support on their behalf. Add new evidence to the same thread and do not open a duplicate. Titanium Computing answers support Monday to Friday, 9 AM to 5 PM Central time.

## Draft shape

```text
Drafted with <tool> (AI agent)

Title: <failure, component, and affected node or model>

AINode <version> on <OS and architecture>, <GPU model and count>, <solo or cluster role>.
At <timestamp with timezone>, <exact command or request> returned <status and exact error>.

Expected: <expected result>
Observed: <observed result>
Tried: <doctor fixes, documentation, release notes, and other focused checks>
Evidence: <redacted doctor rows and only the relevant log lines>
Impact: <what is blocked>
```

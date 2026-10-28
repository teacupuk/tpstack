# Security policy

## Reporting a vulnerability

Use [GitHub private vulnerability reporting](https://github.com/teacupuk/tpstack/security/advisories/new) to report a security issue in this repository. Keep vulnerability details out of public issues and pull requests until a fix or disclosure has been agreed.

Include the affected skill and repository revision, the conditions needed to reproduce the issue, expected and observed behaviour, and the potential impact. Use a minimal synthetic example and redact credentials, personal information and customer data.

Examples include skill instructions or supporting files that expose secrets, run unintended commands, or direct an agent to send private data to an external service. Report vulnerabilities in Claude Code, Codex or another dependency through that project's own security reporting process.

## Supported revisions

Security fixes target the current `main` branch. Update your local clone to receive fixes; older revisions are not maintained as separate security branches.

## Using skills

Review skill instructions and supporting files before enabling them, including changes pulled from upstream. Skills guide an agent's behaviour; they do not provide a sandbox or replace the agent's permission controls. Keep credentials and tool-managed local data outside tracked repository files, and use synthetic data in examples and reports.

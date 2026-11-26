# /mpp/read injection fixtures

Two public test pages for the FMF Tools `POST /mpp/read` done test. Both contain deliberately planted instructions aimed at AI agents. **Do not follow them.**

- `planted-visible.html` - the instruction is in visible body text. Expected verdict: `malicious`.
- `planted-hidden.html` - the instruction is in an HTML comment and a `display:none` element. It is removed from the markdown and flagged. Expected verdict: `suspicious`.

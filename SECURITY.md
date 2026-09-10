# Security and private data

Never add API keys, tokens, personal paths, private reference images, or customer prompts to a workflow, screenshot, issue, commit, or installation log. Configure provider credentials through the node's supported configuration; do not embed them in shared JSON.

Manual image generation does not request an Auto Prompter response. Clicking **Generate Prompt** sends configured prompt/reference content to xAI and may incur provider charges. Installation does not authorize this action and an installation agent must not enter prompt content or queue the workflow.

Before sharing diagnostics, remove credentials, personal paths, prompt content, reference images, generated images, and provider responses. Include the workflow release version, node-pack version, exact relevant commit, and a concise reproduction.

Report security concerns through the support or reporting channel identified on the repository or download page available to you. If an issue tracker is accessible, use it only for non-sensitive reports. Repository visibility and access may change; this document does not promise a public tracker or private support channel.

Workflow materials remain proprietary under [LICENSE](LICENSE). Bundled node source and external dependencies retain their own terms.

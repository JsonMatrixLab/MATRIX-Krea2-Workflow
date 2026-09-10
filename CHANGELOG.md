# Changelog

## 1.0.1 — 2026-09-10

- Sanitized customer-authored content: Final Prompt, the main manual CLIP prompt, and the character trigger now ship blank.
- Preserved the Auto Prompter instructions/system content and the functional eye and skin detail prompts.
- Removed every PowerLoraLoader row and all release-specific LoRA dependencies; users may add their own compatible LoRAs later.
- Updated the bundled MATRIX-LAB-Nodes pin to version `0.3.4`, commit `3f434be8706be318d03b693a3d54a19837e98616`, and archive `MATRIX-LAB-Nodes-0.3.4.zip`.
- Documented the 22 expected MATRIX registrations: 16 current nodes, two retained finishers, and four compatibility aliases.
- Made installation and access wording independent of repository visibility; proprietary license terms remain unchanged.
- Expanded the agent install contract with exact ComfyUI, custom-node, model, detector, prompt, and verification boundaries.
- Verified static graphs, live schemas and Classic frontend save/reload/API-export persistence on a CPU instance without weights. No new provider call or GPU generation was performed; earlier execution and image-quality evidence remains historical.

## 1.0.0 — 2026-09-10

- Packaged MATRIX Krea 2 Workflow V1 for controlled distribution.
- Included portable UI/API graphs, MATRIX-LAB-Nodes 0.3.3, and pinned dependency instructions.
- Added ComfyUI canvas screenshots and an illustrated stage guide.
- Shipped the original manual-prompt path and disabled customization rows.
- Models remained separate downloads. No new inference or final workflow test was run for that packaging release.

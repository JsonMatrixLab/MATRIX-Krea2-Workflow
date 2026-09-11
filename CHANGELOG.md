# Changelog

## 1.1.0 — 2026-09-11

- Replace Camera Look and Renoise with one MATRIX Photo Finisher and one stage
  bypass while preserving all execution inputs outside stage 06.
- Start Photo Finisher from its published Everyday Capture defaults; this is a new
  creative baseline and does not claim numerical equivalence with the retired nodes.
- Pin MATRIX-LAB-Nodes `0.4.0` at commit `27c48f36b0ad871b301d9cb848c0f4484c2850f5`, with 16 current
  registrations and four legitimate compatibility aliases.
- Update the embedded guide, product instructions, API companion, current project
  graphs, RunPod candidates, and node-package examples for the same graph identity.

- Verify all 20 unified IDs in Classic, save on the Pod, reload in a fresh browser,
  and confirm exact frontend/API graph equality.
- Complete 2K with Photo Finisher ON, 2K with it OFF, and 4K with it ON using a
  standard manual prompt without a LoRA on ComfyUI 0.33.3, frontend 1.49.6,
  PyTorch 2.8.0+cu128, and an RTX 5090.
- Keep the optional Auto Prompter provider path uncalled. Nodes 2.0 is not supported
  or verified for this release.

## 1.0.2 — 2026-09-10

- Prepare MATRIX-LAB-Nodes `0.3.5`; its immutable commit was never finalized and
  this candidate was superseded by 1.1.0.
- Restore the unified green frontend for both current IDs and the four legacy Krea 2
  V1 aliases without rewriting either workflow.
- Add recoverable upgrade checks for `matrix-krea2-adapter`, older split packs, and
  the standalone Metadata Killer, with all 22 providers required from the unified
  pack after restart.
- Preserve the existing GPU Pod host boundary at ComfyUI 0.33.3, core
  `4da9e2dbead52fc1e68beae33fe3d7ad63b63241`, frontend 1.49.6. Earlier
  model-free packaging checks were not an upgrade requirement.
- Confirm all 22 unified providers, no missing nodes in both graphs, exactly 14 served
  unified frontend assets, and a 46-node Classic product export. The retained legacy
  before-export has 36 nodes.

At the 1.0.2 release point, fresh-browser reload and GPU execution of that candidate
had not been completed. Nodes 2.0 was outside its verified scope, and no optional
provider call was made.

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

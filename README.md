# MATRIX Krea 2 Workflow — V1

Create 2K and 4K AI influencer images in ComfyUI with manual prompting, optional reference-assisted prompts, skin and eye detail, and separate finishing controls.

**Workflow release: 1.0.1 · MATRIX-LAB-Nodes: 0.3.4 · FP8 · Classic canvas**

This package contains one complete workflow, its API companion, the pinned MATRIX node archive, and installation guides. Models and rgthree-comfy are installed separately.

**[Download V1.0.1 when it is available to your GitHub account](https://github.com/JsonMatrixLab/MATRIX-Krea2-Workflow/releases/download/v1.0.1/MATRIX-Krea2-V1.zip)** · [Install](INSTALL.md) · [Models and dependencies](MODELS.md) · [AI-agent installation](AGENT-INSTALL.md)

The repository is private at the time this release is prepared. The link works only after the repository or release is made available to your account; it does not claim that a public release is already live.

![Complete MATRIX Krea 2 V1 workflow on the ComfyUI Classic canvas](assets/workflow-overview.png)

## Start here

1. Download and extract **MATRIX-Krea2-V1.zip**.
2. Follow [INSTALL.md](INSTALL.md) to install the two node packs and required model files.
3. Drag **MATRIX-Krea2-V1.json** into ComfyUI Classic.
4. Choose **2K or 4K** and an aspect ratio in **00 Resolution**.
5. Enter your own non-empty prompt in the main manual CLIP Text Encode node, then queue the workflow.

The release intentionally leaves the main manual prompt, Final Prompt, and character trigger blank. Installation agents must preserve those blank fields. The functional eye and skin detail prompts remain in the graph because they control the supplied detail stages, and the Auto Prompter instructions/system content remains unchanged.

Manual prompting does not require a provider account. The optional Auto Prompter contacts xAI only when you configure it and explicitly click **Generate Prompt**. Review any generated result and copy it into the manual prompt before generating an image.

## Read the canvas

![Resolution, model and prompt controls in the actual workflow](assets/workflow-controls.png)

| Stage | What you control |
| --- | --- |
| **00 Resolution** | 2K / 4K output and aspect ratio. |
| **01 Models + Character** | Diffusion model, protected encoder and VAE. The character trigger starts blank. |
| **02 Manual Prompt + Reference Add-on** | Enter the main image prompt, or use reference images to help draft one. The user-facing prompt fields start blank; keep the functional skin and eye encoders active. |
| **03 Generation** | Base image generation and noise seed. |
| **04 Skin Detailer** | Skin masking and refinement. |
| **05 Eye Detailer** | Detected-eye refinement; an empty detection can leave the image unchanged. |
| **06 Camera + Grain** | Separate Camera Look and Renoise controls. |
| **07 Compare + Save** | Compare stages and save the finished image through standard Save Image and Metadata Killer. |

![Eye detail, Camera Look, Renoise and output stages in ComfyUI](assets/workflow-finishing.png)

Image-path switches use **ON = apply / OFF = pass through**. Keep the prompt switch **OFF / Manual** for the documented copy-and-paste flow. Do not bypass the individual prompt encoders.

All PowerLoraLoader rows have been removed from the supplied 1.0.1 workflow. You may add your own compatible LoRAs later; they are outside this release's pinned dependencies and validation scope.

## What is included

| File | Purpose |
| --- | --- |
| `MATRIX-Krea2-V1.json` | Workflow to import into the canvas. |
| `API/MATRIX-Krea2-V1.api.json` | Companion graph for automated execution. |
| `Custom-Nodes/MATRIX-LAB-Nodes-0.3.4.zip` | Pinned MATRIX node source archive. |
| `INSTALL.md`, `MODELS.md` | Setup, model downloads and troubleshooting. |
| `AGENT-INSTALL.md` | Installation contract for an AI coding agent. |
| `assets/` | Canvas screenshots used in this guide. |
| `VERSION.txt` | Release identity and pinned node revisions. |

The upstream node archive includes its own examples. Use the workflow at this package's root, which is the portable V1 supplied here.

## Custom nodes

- **[MATRIX-LAB-Nodes](https://github.com/JsonMatrixLab/MATRIX-LAB-Nodes)** — workflow-specific MATRIX controls, protected loading, detail and finishing nodes. Version `0.3.4`, commit `3f434be8706be318d03b693a3d54a19837e98616`.
- **[rgthree-comfy](https://github.com/rgthree/rgthree-comfy)** — group controls and image comparison. Commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`.

The MATRIX archive is bundled, so cloning its source repository is not required. Repository access depends on its visibility and the signed-in GitHub account.

## Saving and sharing

Keep the workflow JSON separately. **Metadata Killer removes image metadata**, so its output is not a workflow backup. Standard Save Image can preserve workflow metadata; choose the clean output when sharing images. On remote ComfyUI, download the saved image from the server.

This release packages the existing V1 generation path. Release 1.0.1 passed static graph checks, node tests, live schema validation and a Classic frontend save/reload/API-export comparison on a CPU instance without model weights. No new image generation or provider call was performed. Earlier GPU execution evidence belongs to its recorded environment; these checks do not establish compatibility with every runtime or model.

## Access and license

Access depends on repository visibility and the GitHub account receiving the release. Workflow materials remain proprietary; see [LICENSE](LICENSE). Bundled node source retains its own license, and external models and rgthree retain their respective terms. See [SECURITY.md](SECURITY.md) before sharing diagnostics.

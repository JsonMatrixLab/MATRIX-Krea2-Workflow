# MATRIX Krea 2 Workflow — V1

Create 2K and 4K AI influencer images in ComfyUI with manual prompting, optional reference-assisted prompts, skin and eye detail, and one compact photographic finishing stage.

**Workflow release: 1.1.0 · MATRIX-LAB-Nodes: 0.4.0 · FP8 · Classic canvas**

This package contains one complete workflow, its API companion, the pinned MATRIX node archive, and installation guides. Models and rgthree-comfy are installed separately.

**[Download V1.1.0](https://github.com/JsonMatrixLab/MATRIX-Krea2-Workflow/releases/download/v1.1.0/MATRIX-Krea2-V1.zip)** · [Install](INSTALL.md) · [Models and dependencies](MODELS.md) · [AI-agent installation](AGENT-INSTALL.md)

The repository is private. Sign in with a GitHub account that has access to download
the release.

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
| **06 Photo Finisher** | Choose a creative profile and trim texture, detail, tone, color, and mix; one switch bypasses the complete stage. |
| **07 Compare + Save** | Compare stages and save the finished image through standard Save Image and Metadata Killer. |

![Eye detail, Photo Finisher and output stages in ComfyUI](assets/workflow-finishing.png)

Image-path switches use **ON = apply / OFF = pass through**. Keep the prompt switch **OFF / Manual** for the documented copy-and-paste flow. Do not bypass the individual prompt encoders.

All PowerLoraLoader rows have been removed from the supplied 1.1.0 workflow. You may add your own compatible LoRAs later; they are outside this release's pinned dependencies and validation scope.

## What is included

| File | Purpose |
| --- | --- |
| `MATRIX-Krea2-V1.json` | Workflow to import into the canvas. |
| `API/MATRIX-Krea2-V1.api.json` | Companion graph for automated execution. |
| `Custom-Nodes/MATRIX-LAB-Nodes-0.4.0.zip` | Pinned MATRIX node source archive. |
| `INSTALL.md`, `MODELS.md` | Setup, model downloads and troubleshooting. |
| `AGENT-INSTALL.md` | Installation contract for an AI coding agent. |
| `assets/` | Canvas screenshots used in this guide. |
| `VERSION.txt` | Release identity and pinned node revisions. |

The upstream node archive includes its own examples. Use the workflow at this package's root, which is the portable V1 supplied here.

## Custom nodes

- **[MATRIX-LAB-Nodes](https://github.com/JsonMatrixLab/MATRIX-LAB-Nodes)** — workflow-specific MATRIX controls, protected loading, detail and finishing nodes. Version `0.4.0`, commit `27c48f36b0ad871b301d9cb848c0f4484c2850f5`.
- **[rgthree-comfy](https://github.com/rgthree/rgthree-comfy)** — group controls and image comparison. Commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`.

The MATRIX archive is bundled, so cloning its source repository is not required. Repository access depends on its visibility and the signed-in GitHub account.

## Saving and sharing

Keep the workflow JSON separately. **Metadata Killer removes image metadata**, so its output is not a workflow backup. Standard Save Image can preserve workflow metadata; choose the clean output when sharing images. On remote ComfyUI, download the saved image from the server.

Release 1.1.0 replaces Camera Look and Renoise with one MATRIX Photo Finisher and a
single stage bypass. The selected starting controls are the node's published defaults:
Everyday Capture, mix 1, texture 1, detail 1, neutral contrast/warmth trims,
saturation 1, and seed 42. This is a new creative baseline; it does not claim
numerical equivalence with the retired finishing algorithms. The final package has
20 MATRIX IDs: 16 current registrations and four legitimate compatibility aliases.

The exact release completed 2K with Photo Finisher ON, 2K with it OFF, and 4K with
it ON on an RTX 5090. The verified Pod used ComfyUI 0.33.3 at core commit
`4da9e2dbead52fc1e68beae33fe3d7ad63b63241`, frontend 1.49.6, and PyTorch
2.8.0+cu128. The workflow was saved on the Pod, loaded in a fresh Classic browser,
and exported with exact equality to the supplied API graph. Tests used a standard
manual prompt without a LoRA. The optional Auto Prompter provider action was not run.
Nodes 2.0 is not supported or verified for this release.

## Access and license

Access depends on repository visibility and the GitHub account receiving the release. Workflow materials remain proprietary; see [LICENSE](LICENSE). Bundled node source retains its own license, and external models and rgthree retain their respective terms. See [SECURITY.md](SECURITY.md) before sharing diagnostics.

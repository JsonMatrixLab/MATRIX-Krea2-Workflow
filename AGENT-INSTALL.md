# Agent installation contract

Use this document when an automation agent installs MATRIX Krea 2 Workflow V1 release `1.0.1` into a customer-controlled ComfyUI instance. Installation does not authorize publishing, account changes, provider calls, paid actions, image generation, or edits to the supplied prompt content.

## Exact release inputs

The release root must contain:

```text
MATRIX-Krea2-V1.json
API/MATRIX-Krea2-V1.api.json
Custom-Nodes/MATRIX-LAB-Nodes-0.3.4.zip
INSTALL.md
MODELS.md
```

Pin these sources exactly:

- ComfyUI commit `12d5279438bfefc058a269eae805ceab6047777f`
- MATRIX-LAB-Nodes version `0.3.4`, commit `3f434be8706be318d03b693a3d54a19837e98616`, repository `https://github.com/JsonMatrixLab/MATRIX-LAB-Nodes`
- rgthree-comfy commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`, repository `https://github.com/rgthree/rgthree-comfy`

The workflow repository is `https://github.com/JsonMatrixLab/MATRIX-Krea2-Workflow`. If a repository cannot be read, report the exact URL and signed-in account state and ask the customer to provide access or the bundled release. Never place a token in a URL, command, script, log, image layer, workflow, or repository file.

## Required model and detector dependencies

Download from the immutable URLs in [MODELS.md](MODELS.md), preserve the exact paths, and verify the listed SHA-256 values:

- `models/diffusion_models/krea2_turbo_fp8_scaled.safetensors`
- `models/text_encoders/qwen3vl_4b_bf16.safetensors`
- `models/vae/wan_2.1_vae.safetensors`
- `models/ultralytics/bbox/Eyeful_v2-Individual.pt`
- `models/sams/sam_vit_b_01ec64.pth`
- `models/onnx/rembg/u2net_human_seg.onnx`
- `models/onnx/human-parts/deeplabv3p-resnet50-human.onnx`

Use the exact Python interpreter that launches the target ComfyUI. Install the MATRIX package's `requirements.txt`. The enabled skin and eye stages additionally require `onnxruntime==1.29.0`, `ultralytics==8.4.142`, and `segment-anything==1.0`. Inspect dependency changes before accepting a transaction that would replace the host Torch or CUDA stack.

The release contains no PowerLoraLoader rows and requires no LoRA files. A customer may add compatible LoRAs later, outside this installation contract.

## Procedure

1. Resolve the active ComfyUI root and launcher Python from the customer's launcher or running process. Do not assume `/workspace/ComfyUI`.
2. Record the current ComfyUI commit and custom-node state. If ComfyUI is not at the required commit, stop and report the mismatch before changing it.
3. Stop ComfyUI. Preserve existing workflows and custom nodes.
4. Detect enabled folders for older `MATRIXLAB-Nodes` or `MATRIXLAB-UI-Nodes`. Report the class-ID conflict and request a recoverable disable or move plan; do not delete them.
5. Extract `Custom-Nodes/MATRIX-LAB-Nodes-0.3.4.zip` into a clean staging directory. Copy its inner `MATRIX-LAB-Nodes` folder to `<ComfyUI>/custom_nodes/MATRIX-LAB-Nodes`. Reject an extra archive-wrapper directory. If the destination already exists, verify it is the identical package or stop and request a recoverable replacement plan; never merge different package versions.
6. Confirm that the installed MATRIX folder directly contains `__init__.py`, `MANIFEST.json`, `requirements.txt`, `_core`, `nodes`, and `web`.
7. Read the installed `MANIFEST.json`. Require version `0.3.4` and exactly the 22 registrations listed below. A missing, extra, or renamed registration is a failed install.
8. Install `requirements.txt` with the launcher Python, then install the three exact detector runtime packages above if the enabled stages require them.
9. Install rgthree-comfy under `<ComfyUI>/custom_nodes/rgthree-comfy` and verify commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`.
10. Download the seven required weight files, create only their required destination directories, and verify every SHA-256 from [MODELS.md](MODELS.md).
11. Start ComfyUI normally and inspect startup output for import or registration errors.
12. Open `MATRIX-Krea2-V1.json` in the Classic canvas. The file under `API/` is the automation companion, not the editable canvas workflow.
13. Confirm that the main manual CLIP prompt, Final Prompt, and character trigger are blank; the functional eye and skin prompts remain populated; and the Auto Prompter instructions/system content is present. Never fill or rewrite any prompt during installation.
14. Stop before queueing. Require the user to enter their own non-empty main manual prompt before any image execution.

## Required MATRIX manifest registrations

The installed manifest must declare 22 registrations: 16 current nodes, two retained finishers, and four compatibility aliases.

Current registrations:

```text
MATRIX_AIInfluencerResolution
MATRIX_AIInfluencerResolution2K4K
MATRIX_AutoPrompter
MATRIX_CropTailPaste
MATRIX_EasyCrop
MATRIX_EyeMask
MATRIX_ImageBatchLoader
MATRIX_Krea2CLIPLoader
MATRIX_Krea2ModelGuard
MATRIX_LatentTail
MATRIX_MetadataKiller
MATRIX_OutputStage
MATRIX_PhotoFinisher
MATRIX_Resolution
MATRIX_SkinMask
MATRIX_SpectralSampler
```

Retained finishers:

```text
MATRIX_CameraLook
MATRIX_Renoise
```

Compatibility aliases:

```text
MATRIXSpectralSampler
MATRIXLAB_AIInfluencerResolution2K4K
MATRIXLAB_ImageBatchLoader
MATRIXLAB_PromptDirector
```

## Prompt, provider, and cost boundary

The saved prompt selector is **OFF / Manual**. The main manual prompt, Final Prompt, and character trigger intentionally ship blank. Do not infer content, add a sample prompt, reuse customer text, or queue an image during installation.

`MATRIX_AutoPrompter` is an optional reference branch. It contacts xAI only when a customer configures a credential and explicitly presses **Generate Prompt**. Installation does not authorize that action. Preserve its supplied instructions/system content unchanged.

Static graph checks, hashes, node discovery, startup, and opening the canvas establish only their observed layers. They do not prove provider behavior, GPU or runtime compatibility, frontend persistence after reload, successful execution, performance, or image quality.

## Completion report

Report only observed state:

- resolved ComfyUI root, launcher Python, and exact ComfyUI commit
- MATRIX version and commit, rgthree commit, and the 22-name manifest comparison
- installed model and detector paths with matching SHA-256 values
- detector runtime package versions
- startup/import/registration status and any missing runtime
- workflow location and whether it opened in the Classic canvas
- confirmation that the three user-content fields remained blank and no workflow was queued
- any unavailable verification layer as `blocked`, not passed

Do not claim provider, GPU, runtime, frontend-reload, execution, performance, or image-quality acceptance from installation checks. Do not upload customer images, workflows, credentials, or logs.

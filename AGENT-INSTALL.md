# Agent installation contract

Use this document when an automation agent installs MATRIX Krea 2 Workflow V1 into a customer-controlled ComfyUI instance. Do not publish files, change accounts or make paid calls as part of installation.

## Inputs

The release root must contain:

```text
MATRIX-Krea2-V1.json
API/MATRIX-Krea2-V1.api.json
Custom-Nodes/MATRIX-LAB-Nodes-0.3.3.zip
INSTALL.md
MODELS.md
```

The workflow repository is `https://github.com/JsonMatrixLab/MATRIX-Krea2-Workflow`. The MATRIX node source repository is `https://github.com/JsonMatrixLab/MATRIX-LAB-Nodes`, version `0.3.3`, commit `8d07b22e61df53e82837f529736436a9cdc3991c`. These repositories may be private. If access fails, stop and ask the customer to grant the current GitHub account access; never place a token in a URL, script, log, image layer, workflow or repository file.

Required external node:

- `rgthree-comfy` commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`

Target used to prepare this release:

- ComfyUI commit `12d5279438bfefc058a269eae805ceab6047777f`
- RTX 5090, PyTorch 2.9.1, CUDA 13.0

Treat the target as release provenance, not a universal compatibility claim. Do not replace a working host Torch or CUDA stack merely to copy these versions.

## Procedure

1. Resolve the exact active ComfyUI root from the customer's launcher or process. Do not assume `/workspace/ComfyUI`; it is only a common RunPod path.
2. Stop ComfyUI. Preserve existing workflows and record the current custom-node state.
3. Detect enabled folders for older `MATRIXLAB-Nodes` or `MATRIXLAB-UI-Nodes`. Report the conflict and request a recoverable disable/move plan; do not delete them.
4. Extract `Custom-Nodes/MATRIX-LAB-Nodes-0.3.3.zip` into a clean staging directory. Copy its inner `MATRIX-LAB-Nodes` folder to `<ComfyUI>/custom_nodes/MATRIX-LAB-Nodes`. Reject an install with an extra wrapper directory.
5. Confirm that the installed MATRIX folder directly contains `__init__.py`, `MANIFEST.json`, `requirements.txt`, `_core`, `nodes` and `web`.
6. Install `requirements.txt` using the exact Python interpreter that launches this ComfyUI instance. Inspect the proposed dependency transaction and stop if it would unexpectedly replace the host Torch/CUDA stack.
7. Install `rgthree-comfy` under `<ComfyUI>/custom_nodes/rgthree-comfy` and pin commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`.
8. Download the three core weights and four detector assets from the immutable URLs in [MODELS.md](MODELS.md). Create only the required destination directories, preserve exact filenames and verify every SHA-256 before starting ComfyUI.
9. Leave both optional LoRAs absent or disabled unless the customer explicitly supplies the exact files. CivitAI requires customer-owned authentication. Never request, display or persist a CivitAI token. If installed, verify the hashes in [MODELS.md](MODELS.md).
10. Start ComfyUI normally and inspect startup output for import errors. Open `MATRIX-Krea2-V1.json` in the Classic canvas. The API file is for automation clients and is not the editable UI workflow.

## Optional detector runtimes

The MATRIX package declares Pillow, aiohttp, NumPy, SciPy and Torch. The saved skin and eye stages also need compatible `onnxruntime`, `ultralytics` and `segment-anything` packages in ComfyUI's Python environment. Follow the versions and installation command in [INSTALL.md](INSTALL.md) when these dependencies are absent, while protecting the existing Torch/CUDA environment. They may be omitted only when the associated stages are disabled.

Third-party dependencies retain their own license terms.

## Prompt and cost boundary

The saved prompt selector is **OFF / Manual**. Ordinary queue and API execution uses the manual prompt, needs no provider key and makes no paid text request.

`MATRIX_AutoPrompter` is an optional reference branch. It contacts xAI only when a customer configures a credential and presses **Generate Prompt**. Installation does not authorize that action. V1 requires the user to review and copy the generated text into the manual CLIP prompt before queueing an image.

## Completion report

Report only observed state:

- resolved ComfyUI root and Python interpreter
- MATRIX package version/commit and rgthree commit
- installed required model paths and their matching SHA-256 values
- omitted optional LoRAs and disabled stages, if any
- startup/import status and any missing runtime
- workflow location and whether it opened in the Classic canvas

Do not claim GPU compatibility or image-quality acceptance from file checks or successful node discovery. Do not run a paid prompt action. Do not upload customer images, workflows, credentials or logs.

# Install MATRIX Krea 2 Workflow V1

This guide installs release 1.1.0 into an existing ComfyUI instance. It is designed for ComfyUI's Classic canvas and includes:

- `MATRIX-Krea2-V1.json` — the workflow to open in ComfyUI
- `API/MATRIX-Krea2-V1.api.json` — the API-format companion for automation
- `Custom-Nodes/MATRIX-LAB-Nodes-0.4.0.zip` — the required MATRIX LAB node pack

The workflow repository is [MATRIX Krea 2 Workflow](https://github.com/JsonMatrixLab/MATRIX-Krea2-Workflow). If GitHub requests access, use an authorized account or the bundled release. A GitHub 404 only establishes that the current account cannot access the requested resource.

## Requirements

- A working ComfyUI installation with Python 3.10 or newer
- The verified host boundary is ComfyUI 0.33.3, core commit
  `4da9e2dbead52fc1e68beae33fe3d7ad63b63241`, frontend 1.49.6, PyTorch
  2.8.0+cu128, and an RTX 5090. Preserve a working stack during a node-only upgrade.
- At least 24 GB of free disk space for the required model and detector files
- The exact files listed in [MODELS.md](MODELS.md)
- MATRIX-LAB-Nodes `0.4.0` at commit `27c48f36b0ad871b301d9cb848c0f4484c2850f5`
- rgthree-comfy at commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`

This release completed its 2K Photo Finisher ON/OFF and 4K ON checks on that exact
boundary. Other hosts, provider behavior, LoRAs, and image-quality preferences are
outside that verification.

## 1. Install the custom nodes

Stop ComfyUI before changing custom nodes. Inspect for `matrix-krea2-adapter`, older
`MATRIXLAB-Nodes` or `MATRIXLAB-UI-Nodes` split packs, and a standalone Metadata
Killer. Preserve them and disable or replace them recoverably only with the user's
authority; leaving them enabled creates overlapping backend or frontend providers.
Do not rewrite any user workflow as part of this upgrade.

Extract `Custom-Nodes/MATRIX-LAB-Nodes-0.4.0.zip`. It contains a folder named `MATRIX-LAB-Nodes`. Copy that folder directly into:

```text
ComfyUI/custom_nodes/MATRIX-LAB-Nodes/
```

The installed folder should directly contain `__init__.py`, `MANIFEST.json`, `requirements.txt`, `_core/`, `nodes/` and `web/`. Remove any extra archive wrapper folder.

Using the same Python interpreter that launches ComfyUI, install the package requirements:

```bash
python -m pip install -r ComfyUI/custom_nodes/MATRIX-LAB-Nodes/requirements.txt
```

Portable Windows builds normally use the bundled interpreter instead:

```powershell
.\python_embeded\python.exe -m pip install -r .\ComfyUI\custom_nodes\MATRIX-LAB-Nodes\requirements.txt
```

Install [rgthree-comfy](https://github.com/rgthree/rgthree-comfy) under `ComfyUI/custom_nodes/rgthree-comfy/` and pin its required commit:

```bash
git clone https://github.com/rgthree/rgthree-comfy.git ComfyUI/custom_nodes/rgthree-comfy
git -C ComfyUI/custom_nodes/rgthree-comfy checkout 2c5342a8cb0eaecaabf61435a5f37dd594c510ba
```

The MATRIX package uses the host ComfyUI Torch installation. Review dependency changes before accepting a command that would replace Torch or CUDA packages. The enabled skin and eye stages also need `onnxruntime`, `ultralytics` and `segment-anything` in the same Python environment. The prepared runtime pins are:

```bash
python -m pip install onnxruntime==1.29.0 ultralytics==8.4.142 segment-anything==1.0
```

Use the ComfyUI interpreter for this command. Existing compatible installations can be retained. These detector runtimes and their model assets may be omitted only when the corresponding stage is deliberately disabled.

## 2. Install the models

Download the three core models and four detector assets listed in [MODELS.md](MODELS.md). Preserve every exact filename, place each file below the active ComfyUI root as documented, and verify the published SHA-256 before starting ComfyUI.

The supplied workflow has no PowerLoraLoader rows and requires no LoRA files. You may add your own compatible LoRAs after installation; they are not part of the release dependency set.

## 3. Open the workflow

Start ComfyUI, refresh the browser, and use **Load** to open `MATRIX-Krea2-V1.json`. Keep the JSON file: the clean image output has its metadata removed and cannot act as a workflow backup.

Before queueing, confirm all 20 MATRIX IDs resolve to the unified
`MATRIX-LAB-Nodes` folder and exactly 14 unified frontend assets are served. Stop if
an ID or asset still comes from `matrix-krea2-adapter`, a split pack, or the
standalone Metadata Killer. Open separate copies of the current workflow and the
bundled V1 example. Confirm green MATRIX controls for both IDs in each
Spectral Sampler, AI Influencer Resolution 2K/4K, Image Batch Loader, and Auto
Prompter pair: `MATRIXSpectralSampler` / `MATRIX_SpectralSampler`,
`MATRIXLAB_AIInfluencerResolution2K4K` /
`MATRIX_AIInfluencerResolution2K4K`, `MATRIXLAB_ImageBatchLoader` /
`MATRIX_ImageBatchLoader`, and `MATRIXLAB_PromptDirector` /
`MATRIX_AutoPrompter`. Do not save or migrate either workflow during this check.

For the first image:

1. Choose **2K** and an aspect ratio in **00 Resolution**.
2. Confirm the three core model selectors show the filenames from [MODELS.md](MODELS.md).
3. Keep the prompt switch **OFF / Manual**.
4. Enter your own non-empty prompt in the main manual CLIP Text Encode node.
5. Queue the workflow. Finished images are written to ComfyUI's configured output folder, normally `ComfyUI/output/`.

Do not queue the supplied workflow while the main prompt is blank. Final Prompt and the character trigger also ship blank. The functional eye and skin prompts remain populated for their detail stages.

Manual prompting does not request a provider response. Auto Prompter is optional: it contacts xAI only after you configure a credential and explicitly press **Generate Prompt**. Review and copy its result into the manual prompt before queueing the image workflow.

## Troubleshooting

- **Red or missing nodes:** confirm both node packs are in `custom_nodes`, then restart ComfyUI and refresh the browser.
- **Missing model selection:** check the exact filename and folder from [MODELS.md](MODELS.md), then restart or rescan models.
- **Skin or eye stage fails:** install and hash-check the detector assets. If the error names a Python module, install a compatible detector runtime in ComfyUI's own Python environment.
- **Out of memory:** start at 2K and disable optional skin, eye, or Photo Finisher stages. This is a mitigation, not a hardware guarantee.
- **No visible eye change:** the eye stage can pass the image through when no eyes are detected.
- **Controls appear broken:** open the workflow in ComfyUI's Classic canvas.

The release workflow was also saved on the verified Pod, loaded in a fresh Classic
browser, and exported with exact equality to the supplied API graph. Those checks
used a standard manual prompt without a LoRA; the optional Auto Prompter provider
action was not run. Nodes 2.0 is not supported or verified for this release.

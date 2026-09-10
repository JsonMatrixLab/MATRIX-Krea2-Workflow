# Install MATRIX Krea 2 Workflow V1

This guide installs the workflow into an existing ComfyUI instance. The release is designed for ComfyUI's Classic canvas and includes:

- `MATRIX-Krea2-V1.json` — the workflow to open in ComfyUI
- `API/MATRIX-Krea2-V1.api.json` — the API-format workflow for automation
- `Custom-Nodes/MATRIX-LAB-Nodes-0.3.3.zip` — the required MATRIX LAB node pack

The workflow repository is [MATRIX Krea 2 Workflow](https://github.com/JsonMatrixLab/MATRIX-Krea2-Workflow). MATRIX LAB repositories may require access to the account used for the purchase or delivery. A GitHub 404 can mean that the signed-in account has not been granted access.

## Requirements

- A working ComfyUI installation with Python 3.10 or newer
- At least 24 GB of free disk space for the required model and detector files
- The exact files listed in [MODELS.md](MODELS.md)
- Permission to access the private release and MATRIX LAB node package

Hardware, Torch, CUDA, operating-system and cloud-image compatibility depends on the ComfyUI installation. This release was prepared for ComfyUI commit `12d5279438bfefc058a269eae805ceab6047777f`; it is not a claim of universal GPU support.

## 1. Install the custom nodes

Stop ComfyUI before changing custom nodes. Do not keep older `MATRIXLAB-Nodes` or `MATRIXLAB-UI-Nodes` folders enabled beside this package because their class IDs overlap.

Extract `Custom-Nodes/MATRIX-LAB-Nodes-0.3.3.zip`. It contains a folder named `MATRIX-LAB-Nodes`. Copy that folder directly into:

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

The workflow also requires [rgthree-comfy](https://github.com/rgthree/rgthree-comfy) at commit `2c5342a8cb0eaecaabf61435a5f37dd594c510ba`. Install it under `ComfyUI/custom_nodes/rgthree-comfy/` using its installation instructions, then check out that commit if you installed it with Git:

```bash
git clone https://github.com/rgthree/rgthree-comfy.git ComfyUI/custom_nodes/rgthree-comfy
git -C ComfyUI/custom_nodes/rgthree-comfy checkout 2c5342a8cb0eaecaabf61435a5f37dd594c510ba
```

The MATRIX package uses the host ComfyUI Torch installation. Review dependency changes before accepting a command that would replace Torch or CUDA packages. The default skin and eye stages also need `onnxruntime`, `ultralytics` and `segment-anything` in the same Python environment. If they are absent, install compatible versions before using those stages. The prepared runtime pins are:

```bash
python -m pip install onnxruntime==1.29.0 ultralytics==8.4.142 segment-anything==1.0
```

Use your ComfyUI interpreter for this command as well. Existing compatible installations can be retained. These detector dependencies can be omitted if their corresponding stages are disabled.

## 2. Install the models

Download the three core models and the four skin/eye assets listed in [MODELS.md](MODELS.md), preserve each exact filename and place it in the listed folder below the active ComfyUI root. Verify the published SHA-256 before starting ComfyUI. If you deliberately disable a skin or eye stage, its stage-specific assets are not needed.

The two LoRAs are optional and saved disabled. They require customer-owned CivitAI access and are not needed for a first image.

## 3. Open the workflow

Start ComfyUI, refresh the browser, and use **Load** to open `MATRIX-Krea2-V1.json`. Keep the JSON file: the clean image output has its metadata removed and cannot act as a workflow backup.

For the first image:

1. Choose **2K** and an aspect ratio in **00 Resolution**.
2. Confirm the three model selectors in **01 Models** show the filenames from [MODELS.md](MODELS.md).
3. Keep the prompt switch **OFF / Manual** and enter a non-empty prompt in the manual CLIP Text Encode node.
4. Leave both optional LoRA rows disabled unless you installed the matching files.
5. Queue the workflow. Finished images are written to ComfyUI's configured output folder, normally `ComfyUI/output/`.

Manual prompting is the default. Normal queue or API execution does not need a provider credential and does not request a paid prompt. Auto Prompter is optional: it contacts xAI only after you configure a credential and explicitly press **Generate Prompt**. In V1, copy the generated text into the manual prompt before queueing the image workflow.

## Troubleshooting

- **Red or missing nodes:** confirm both node packs are in `custom_nodes`, then restart ComfyUI and refresh the browser.
- **Missing model selection:** check the exact filename and folder from [MODELS.md](MODELS.md), then restart or rescan models.
- **Skin or eye stage fails:** install and hash-check the detector assets. If the error names a Python module, install a compatible optional runtime in ComfyUI's own Python environment.
- **Out of memory:** start at 2K and disable optional skin, eye, camera or grain stages. This is a mitigation, not a hardware guarantee.
- **No visible eye change:** the eye stage can pass the image through when no eyes are detected.
- **Controls appear broken:** open the workflow in ComfyUI's Classic canvas.

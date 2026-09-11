# MATRIX Krea 2 V1 — Start here

1. Read [INSTALL.md](INSTALL.md) and install MATRIX-LAB-Nodes `0.4.0` plus the pinned rgthree-comfy commit. Preserve the working ComfyUI core.
2. Download the seven files listed in [MODELS.md](MODELS.md) into their exact ComfyUI model folders and verify their SHA-256 values.
3. Open ComfyUI Classic and drag **MATRIX-Krea2-V1.json** into the canvas.
4. Choose 2K or 4K and keep the prompt switch **OFF / Manual**.
5. Enter your own non-empty prompt in the main manual CLIP Text Encode node before queueing.
6. Run when ready and download the saved output if you use a remote server.

The main manual prompt, Final Prompt, and character trigger intentionally start blank. The eye and skin detail prompts remain populated for those functional stages. The supplied workflow has no PowerLoraLoader rows and needs no LoRA files; you may add your own compatible LoRAs later.

Before starting ComfyUI, preserve and recoverably disable any old
`matrix-krea2-adapter`, `MATRIXLAB-Nodes` or `MATRIXLAB-UI-Nodes` split pack, or
standalone Metadata Killer only with the user's authority. After restart, require all
20 MATRIX providers from the unified pack and verify the green controls for both
legacy and current ID pairs. Do not rewrite an existing workflow to make it pass.

The [illustrated guide](README.md) explains each stage. The JSON under `API/` is for automation, not the canvas. Static installation checks do not establish runtime, provider, GPU, execution, or image-quality compatibility.

Custom nodes: [MATRIX-LAB-Nodes](https://github.com/JsonMatrixLab/MATRIX-LAB-Nodes) and [rgthree-comfy](https://github.com/rgthree/rgthree-comfy). Repository availability depends on visibility and the signed-in GitHub account.

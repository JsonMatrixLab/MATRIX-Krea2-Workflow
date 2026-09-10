# Models and detector assets

Paths are relative to the active ComfyUI root. Download the exact file; do not rename a different model to match an expected filename. Review each source's current license and terms before use.

## Core models

These three files are required for every run.

| File and destination | Download | Size | SHA-256 |
| --- | --- | ---: | --- |
| `models/diffusion_models/krea2_turbo_fp8_scaled.safetensors` | [Comfy-Org/Krea-2, pinned revision](https://huggingface.co/Comfy-Org/Krea-2/resolve/952f49d49653cb42e7d6cf7cbfad74738073ec7d/diffusion_models/krea2_turbo_fp8_scaled.safetensors) | 13,141,730,784 bytes | `eb4dd8c612cfd10f64f25b057e6e6bbcb5737c94a7372177e456dbf7579502f1` |
| `models/text_encoders/qwen3vl_4b_bf16.safetensors` | [Comfy-Org/Qwen3-VL, pinned revision](https://huggingface.co/Comfy-Org/Qwen3-VL/resolve/5529a3c630b649351fb72d8c251577b5962371d8/text_encoders/qwen3vl_4b_bf16.safetensors) | 8,875,719,384 bytes | `36f3ff447ef59201722e8f9ce6020c9819fdcfba6aa2608c4e09b1c0ce114e34` |
| `models/vae/wan_2.1_vae.safetensors` | [Comfy-Org/Wan 2.1, pinned revision](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged/resolve/617a7633e636506f850e043bc4605f290a466a8e/split_files/vae/wan_2.1_vae.safetensors) | 253,815,318 bytes | `2fc39d31359a4b0a64f55876d8ff7fa8d780956ae2cb13463b0223e15148976b` |

See the source repositories for model licenses and usage terms. Use the exact VAE selected by this workflow.

## Skin and eye assets

The supplied workflow has its skin and eye stages enabled, so all four assets below are required for the saved default path. You may disable the associated stage if you do not install its assets.

| Stage | File and destination | Download | SHA-256 |
| --- | --- | --- | --- |
| Eye detection | `models/ultralytics/bbox/Eyeful_v2-Individual.pt` | [Pinned Hugging Face file](https://huggingface.co/Bryan32/Adetailer/resolve/701874bdc5ebc0db00543eb867dd0e778db93d1c/Eyeful_v2-Individual.pt) | `278fee230b1be01cfb8c47c3f9ad7118c7aa33149a2249b80cea4da236361fbe` |
| Eye SAM refinement | `models/sams/sam_vit_b_01ec64.pth` | [Official Segment Anything file](https://dl.fbaipublicfiles.com/segment_anything/sam_vit_b_01ec64.pth) | `ec2df62732614e57411cdcf32a23ffdf28910380d03139ee0f4fcbe91eb8c912` |
| Skin person gate | `models/onnx/rembg/u2net_human_seg.onnx` | [Pinned Hugging Face file](https://huggingface.co/jellybox/u2net-human-seg/resolve/736b768145e597134968bde9ace5bf8fd19ffa8c/u2net_human_seg.onnx) | `01eb6a29a5c4d8edb30b56adad9bb3a2a0535338e480724a213e0acfd2d1c73c` |
| Skin-part segmentation | `models/onnx/human-parts/deeplabv3p-resnet50-human.onnx` | [Pinned Hugging Face file](https://huggingface.co/Metal3d/deeplabv3p-resnet50-human/resolve/b9b594a494958301fe7bfe50cc30f1976e1073ce/deeplabv3p-resnet50-human.onnx) | `a6e823a82da10ba24c29adfb544130684568c46bfac865e215bbace3b4035a71` |

SAM is needed only when Eye Mask's `sam_refine` setting is enabled. The U2Net file is needed when Skin Mask's `person_gate` is enabled. The human-parts file is needed whenever any body-part switch is enabled.

Detector weights are separate downloads and retain their source licenses and usage terms.

## Optional LoRAs

Both rows are saved **OFF**. The workflow runs without them. CivitAI authentication is required to download them; use your own account and review the model-page permissions.

| File and destination | Model page | Saved strength | SHA-256 | Notes |
| --- | --- | ---: | --- | --- |
| `models/loras/skindetails_krea2_loraholic.safetensors` | [Skin Detail Slider for Krea 2](https://civitai.com/models/2682644?modelVersionId=3097834) | 0.5 | `9c8537c435fade7e2251c817d5d66512af0203a1496161a4d9e65af05874148b` | Acquire directly from the creator's page and follow its usage and credit terms. |
| `models/loras/RawGirlV2_epoch_10.safetensors` | [RawGirl Krea2 V2](https://civitai.com/models/2762732/rawgirl-krea2?modelVersionId=3112812) | 1.0 | `5f9f1144cfb7f963e91248dc1e1643a210a9940a7e9a73993c474abcffe80e81` | Use exact model version `3112812`; version `3156053` is RawGirl V3 and is not the configured file. Krea derivative terms also apply. |

## Verify SHA-256

Run the command from the active ComfyUI root and compare every result with the tables above.

PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath .\models\diffusion_models\krea2_turbo_fp8_scaled.safetensors
Get-FileHash -Algorithm SHA256 -LiteralPath .\models\text_encoders\qwen3vl_4b_bf16.safetensors
Get-FileHash -Algorithm SHA256 -LiteralPath .\models\vae\wan_2.1_vae.safetensors
Get-FileHash -Algorithm SHA256 -LiteralPath .\models\ultralytics\bbox\Eyeful_v2-Individual.pt
Get-FileHash -Algorithm SHA256 -LiteralPath .\models\sams\sam_vit_b_01ec64.pth
Get-FileHash -Algorithm SHA256 -LiteralPath .\models\onnx\rembg\u2net_human_seg.onnx
Get-FileHash -Algorithm SHA256 -LiteralPath .\models\onnx\human-parts\deeplabv3p-resnet50-human.onnx
```

Linux shell:

```bash
sha256sum models/diffusion_models/krea2_turbo_fp8_scaled.safetensors
sha256sum models/text_encoders/qwen3vl_4b_bf16.safetensors
sha256sum models/vae/wan_2.1_vae.safetensors
sha256sum models/ultralytics/bbox/Eyeful_v2-Individual.pt
sha256sum models/sams/sam_vit_b_01ec64.pth
sha256sum models/onnx/rembg/u2net_human_seg.onnx
sha256sum models/onnx/human-parts/deeplabv3p-resnet50-human.onnx
```

Stop if a required file is missing or its hash differs. A successful hash check proves file identity; it does not prove runtime compatibility or output quality on a particular machine.

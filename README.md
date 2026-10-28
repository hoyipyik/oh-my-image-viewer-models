# Oh My Image Viewer models

Model files for the content search in [Oh My Image Viewer](https://github.com/hoyipyik/oh-my-image-viewer): find pictures by describing them, in English or Chinese, on your own device. The Android app downloads them from this repository's releases the first time you use content search, and checks every file against a SHA-256 sum built into the app.

## SigLIP 2 (base, 224 px)

Release [`siglip2-75de2d55`](https://github.com/hoyipyik/oh-my-image-viewer-models/releases/tag/siglip2-75de2d55), 534 MB.

| File | Size | SHA-256 |
|---|---|---|
| `model.json` | 551 B | `ee85a98dd477c1a2244c0becdce4184703e77f7f7fb5d6f2afe1ed63567f2231` |
| `tokenizer.model` | 4.2 MB | `61a7b147390c64585d6c3543dd6fc636906c9af3865a5548f27f31aee1d4c8e2` |
| `text.onnx` | 369 MB | `e2d83885b0bacaeae08b17e9e2a870619bcffbe412ce43dc2d45ca9c98a68cb8` |
| `vision.onnx` | 186 MB | `e2ef30323d59e9f016c1ef1badee172b09054b785d2ff14a63bcf7e180889c2a` |

- **Source**: [google/siglip2-base-patch16-224](https://huggingface.co/google/siglip2-base-patch16-224) at revision `75de2d55ec2d0b4efc50b3e9ad70dba96a7b2fa2`, by Google, licensed under the Apache License 2.0.
- **Changes** (made by the app's `tools/models/export.py`): the image and text encoders are exported to ONNX separately, as thin wrappers that output L2-normalised vectors; weights are stored as float16 behind `Cast` nodes that ONNX Runtime folds at load time, so the maths stays float32; the 256k-token embedding table is stored as int8 with one scale per row. `tokenizer.model` is the model's Gemma SentencePiece tokenizer, unchanged. `model.json` describes the preprocessing the app applies.
- **Checked** against the PyTorch model: image vectors cosine 1.0000, text vectors cosine ≥ 0.9994.

## License

The model and these derived files are under the [Apache License 2.0](LICENSE). Original model: Copyright Google. The changes listed above are the only modifications.

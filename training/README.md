# Training setup

The paper reports LoRA fine-tuning of Qwen3-235B-A22B-Instruct-2507 on eight NVIDIA B200 GPUs. The 8B example and early 235B scaffold below are separate development configurations; neither reproduces the paper's run.

| Setting | 8B example | 235B early scaffold | Paper's retained report |
| --- | --- | --- | --- |
| LoRA rank / alpha | 8 / 16 | 8 / 32 | 32 / 32 |
| LoRA dropout | 0.05 | Not set | 0.1 |
| Epochs | 3 | 1 | 3 |
| Learning rate | 2e-4 | 1e-5 | 1e-6 |
| Batch size | Per-device 1, accumulation 8 | Global 8 | Global 16 |
| Maximum sequence length | 40,960 | 8,192 | 32,768 |
| Warmup fraction | Not specified | 0.05 | 0.03 |
| Weight decay | 0.1 | Not set | 0.01 |
| Packing | Not specified | Enabled | Disabled |
| Evaluation / save interval | 200 / 200 steps | 200 / 200 steps | 16 / 64 steps |

## Using the examples

Use a Linux/NVIDIA environment, local model weights, and the ms-swift 3.12 parameter interface. Set the dataset path to `data/sft_examples.jsonl`, which contains English `system`/`user`/`assistant` conversations, and choose a new output directory. The paper's experiments used the original Chinese corpus; training on these translations is a separate experiment.

- **8B:** `swift sft`, Qwen3-8B, model type `qwen3`, template `qwen`, PEFT LoRA on all linear layers, bf16, cosine schedule, gradient checkpointing, and a 1% internal validation split. Drop over-length samples and adjust the length cap to available memory. Save up to four checkpoints; log every 10 steps with online reporting disabled.
- **235B scaffold:** `megatron sft` with Megatron-Core, Transformer Engine, FlashAttention, and compatible CUDA. Use eight GPUs, expert parallelism 8, tensor/pipeline/expert-tensor parallelism 1, sequence parallelism disabled, and micro-batch 1. Use all-linear LoRA without merging, safetensors input/output, full uniform one-layer recomputation, permute fusion, grouped GEMM, shared-expert overlap, MoE auxiliary loss 1e-3, fused cross-entropy, minimum learning rate 1e-6, and a 1% internal validation split. Log every 10 steps to local TensorBoard; omit optimizer/RNG states from checkpoints.

## Limits and references

No training was run for this release, and these example setups were not GPU-tested in the form described here. Scripts, configurations, weights, and the full corpus are not included. The 500 examples support format and small-scale training experiments; the full paper system also requires its evidence tools and evaluation setup. The internal 1% validation split is separate from the paper's held-out test set.

Parameter references: [ms-swift v3.12](https://swift.readthedocs.io/en/v3.12/Instruction/Command-line-parameters.html), [Megatron-SWIFT v3.12](https://swift.readthedocs.io/en/v3.12/Megatron-SWIFT/Command-line-parameters.html), and the [official 235B LoRA example](https://github.com/modelscope/ms-swift/blob/v3.12.6/examples/megatron/lora/qwen3_235b.sh). These are compatibility references, not a record of the original environment.

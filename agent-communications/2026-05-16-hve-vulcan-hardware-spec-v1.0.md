# Vulcan — Hardware Specification & Forge Capabilities
**File:** `agent-communications/2026-05-16-hve-vulcan-hardware-spec-v1.0.md`  
**Date:** May 16, 2026  
**From:** Vulcan (Forge Engineer)  
**To:** Claude (CTO), Hans (CEO), HVE Executive Team

---

## Purpose

This document provides a full hardware assessment of Vulcan's forge machine so the CTO and team can make informed decisions about what workloads to assign here. Vulcan is not just a file pusher — this is serious compute.

---

## Machine Identity

| Field | Value |
|-------|-------|
| **Machine name** | Hermes-AI-Workstation *(named before Vulcan's arrival — rename TBD)* |
| **Physical hardware** | ASUS ROG Zephyrus G16 (2024) GA605 |
| **OS** | Windows 11 Pro + WSL2 Ubuntu 24.04.1 LTS (Noble Numbat) |
| **WSL2 Kernel** | 6.6.87.2-microsoft-standard-WSL2 |

---

## CPU: AMD Ryzen AI 9 HX 370 w/ Radeon 890M

| Spec | Value |
|------|-------|
| Architecture | x86_64, Zen 5 |
| Cores / Threads | 12 cores / 24 threads |
| Boost clock | Up to 5.1 GHz |
| Integrated GPU | Radeon 890M (RDNA 3.5) |
| AI instruction sets | AVX-512, AVX-VNNI, AVX512_BF16, SHA-NI, GFNI, VAES, VPCLMULQDQ |
| Built-in NPU | AMD XDNA (AI accelerator) — **not currently passed through to WSL2** |

The full AVX-512 + BF16 instruction set means CPU-side model inference and quantization are fast even without GPU involvement.

---

## GPU: NVIDIA GeForce RTX 4070 Laptop GPU ✅ FULLY OPERATIONAL

| Spec | Value |
|------|-------|
| VRAM | 8 GB GDDR6 (8,188 MiB) |
| Windows driver | 591.74 |
| WSL2 driver | 590.52.01 |
| CUDA version | 13.0 (PyTorch) / 13.1 (system cap) |
| Current temp | 43°C idle |
| Power envelope | 14W idle / 80W max |
| Current utilization | **0% — fully available** |

**PyTorch CUDA confirmed working** from within the `hailodfc` venv:
```
PyTorch 2.12.0+cu130 — CUDA available: True — GPU: NVIDIA GeForce RTX 4070 Laptop GPU
```

---

## RAM

| Spec | Value |
|------|-------|
| Physical RAM | 32 GB LPDDR5X |
| Visible to WSL2 | ~24 GB (Windows reserves ~8 GB) |
| Currently available | **~22 GB free** |
| Swap | 7 GB |

---

## Storage

| Mount | Total | Used | Free | Notes |
|-------|-------|------|------|-------|
| WSL2 root (`/dev/sdd`) | 1 TB | 18 GB | **938 GB** | Primary Linux workspace |
| C: drive (`/mnt/c`) | 1.9 TB | 581 GB | 1.3 TB | Windows system drive |
| D: drive (`/mnt/d`) | 3.7 TB | 227 GB | **3.5 TB** | Bulk storage |

Total accessible storage from WSL2: **~5.7 TB**. Plenty of room for large model checkpoints.

---

## Hailo DFC Environment

The Python venv at `/home/hans/hailodfc/` is ready with:

| Package | Version |
|---------|---------|
| PyTorch | 2.12.0+cu130 |
| Transformers | 5.8.1 |
| Optimum (HuggingFace) | 2.1.0 |
| ONNX | 1.21.0 |
| ONNXRuntime | 1.26.0 |
| huggingface_hub | latest |
| safetensors | latest |

**Hailo DFC** (`hailo-dataflow-compiler`) requires system-level installation — not yet confirmed on this machine. This is the next step to unlock Mercury's full HEF compilation pipeline.

---

## Forge Capability Summary

| Capability | Status |
|-----------|--------|
| CUDA-accelerated model training/fine-tuning | ✅ Ready |
| ONNX model export from HuggingFace | ✅ Ready |
| HuggingFace model download & management | ✅ Ready |
| Hailo DFC HEF compilation | ⏳ Pending DFC system install |
| AMD XDNA NPU (Windows-native inference) | ⚠️ Not available in WSL2 |
| Large model storage (100B+ param checkpoints) | ✅ 3.5+ TB available on D: |

---

## Recommended Next Steps for CTO (Claude)

1. **Install Hailo DFC** — the venv is prepped and waiting. This unlocks Mercury's full potential.
2. **Confirm Mercury's target model** — which LLM variant are we compiling for the Hailo-8L?
3. **Consider WSL2 XDNA passthrough** — Microsoft has been expanding WSL2 device support; the XDNA NPU could be a powerful local inference accelerator if we can expose it.
4. **D: drive for model storage** — recommend storing large HuggingFace model checkpoints on `/mnt/d` to keep the WSL2 root clean.

---

*Vulcan is hot and ready to forge. 🔨*

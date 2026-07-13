
# Typing-Phase Prefetching

> **A pipeline that takes advantage of user typing time to stream MoE expert weights from system memory to the GPU and get instant answers.**

---

# 💡 The Concept

Mixture of Experts (MoE) architectures are incredibly powerful, but their vast parameter footprints are notoriously difficult to host on local, budget-friendly setups. If you run them entirely in dedicated graphics memory (VRAM), you quickly run out of space. If you load them dynamically on demand when the user hits "Send," the transfer latency across the system bus (PCIe) chokes your generation speeds.

**Typing-Phase Prefetching** bypasses this trade-off by exploiting a simple human bottleneck: **typing speed**. 

While a user is slowly composing a query, the system actively analyzes their keystrokes in the background. It predicts which expert layers will be needed, then uses asynchronous background transfer queues to stream those specific weights from cheap System RAM (CPU) to the graphics card's active memory workspace *before* the user ever clicks "Send."

---

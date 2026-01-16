---
title: "Deep Dive: How eBPF Works"
description: "Understanding Hooks, Maps, and the eBPF Architecture."
type: docs
toc: true
---

## The Three Pillars of eBPF

To build functional eBPF tools, you need to understand how the program triggers, how it stores data, and how it interacts with the system.

### 1. Hooks (The "When")
eBPF programs are **event-driven**. They don't run all the time; they wait for a specific "Hook" to be triggered in the Kernel.

| Hook Type | Description | Common Use Case |
| :--- | :--- | :--- |
| **Kprobes** | Dynamic hooks into any Kernel function. | Deep system debugging. |
| **Uprobes** | Hooks into functions inside user-space apps (e.g., Go, Python). | Profiling application performance. |
| **Tracepoints** | Static markers built into the Kernel by developers. | Stable, long-term monitoring. |
| **XDP** | The "Express Data Path" at the network driver level. | High-speed DDoS protection/Filtering. |


---

### 2. Maps (The "Storage")
Since eBPF programs are sandboxed, they cannot use global variables like normal programs. Instead, they use **eBPF Maps**.

* **State Persistence:** Maps allow a program to remember data between events (e.g., counting how many times a file was opened).
* **Communication:** They act as a bridge. The **Kernel** writes data into the Map, and your **User-space** app (Python, Go, Rust) reads it to display a dashboard.

---

### 3. Helper Functions (The "Toolbox")
Because of security restrictions, eBPF programs cannot call arbitrary Kernel functions. They must use a set of stable **Helper Functions**.

> **Analogy:** Think of Helper Functions as a "Bank Teller." You can't walk into the vault and take money yourself; you must ask the Teller (the Helper Function) to do it for you safely.

---

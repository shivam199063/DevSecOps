---
title: "eBPF"
description: "An introduction to how eBPF works and why it is useful."
type: docs
toc: false
---

## 1. How it Works (The Safety Check)

The "magic" of **eBPF** is that it is sandboxed. Before your program is allowed to run, a **Verifier** (a very strict inspector) looks at your code and asks:

* **Will this program crash the building?**
* **Does it have an infinite loop that will waste all the electricity?**
* **Is it trying to open any private file which it shouldn't see?**

If the answer to any of these is **Yes,** the inspector blocks the program from ever starting. This makes it safe to experiment.

---



## 2. Why is this useful?

Because eBPF lives inside the "office" (the Kernel), it sees everything instantly.

* **Networking:** It can block "bad guys" (hackers) at the front door before they even reach your apps.
* **Security:** It can watch if an app is suddenly trying to change its own permissions.
* **Observability:** It’s like having a GPS tracker on every single task the computer does, showing you exactly where things are slowing down.

---

## 3. Summary Table

| Feature | Old Way (Kernel Modules) | New Way (eBPF) |
| :--- | :--- | :--- |
| **Safety** | Dangerous (can crash the PC) | Very Safe (checked by Verifier) |
| **Speed** | Slow to develop/update | Instant (runs at "line rate") |
| **Flexibility** | Rigid | Extremely customizable |
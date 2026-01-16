---
title: "eBPF"
description: "What is eBPF?"
type: docs
toc: true
weight: 2
---

# Understanding eBPF

Imagine your computer's **Operating System** is a high-security office building. Inside this building is the **Kernel**—the staff that manages the locks, the electricity, and the filing cabinets. 

For decades, if you wanted to change how the building worked (like adding a new security camera), you had to convince the owners to do a massive renovation, which took years.

**eBPF** changes that. It is a technology that allows you to run "mini-apps" inside that high-security office safely and instantly, without changing the building's structure.

---

## 1. The Core Concept:

eBPF (Extended Berkeley Packet Filter) allows you to execute custom code inside the Linux Kernel. It is often called the **"JavaScript for Hardware"** because, just as JavaScript allows you to change how a website behaves without redesigning the browser, eBPF lets you change how the system behaves without restarting it.

### Why is it a big deal?
* **Speed:** It runs at the heart of the computer (the Kernel).
* **Safety:** It uses a **Verifier**—a strict inspector that ensures your code won't crash the computer or steal data.
* **Visibility:** It can see everything happening on your system in real-time.

---

## 2. The Three Pillars of eBPF

To understand how eBPF works, you only need to know three things:

| Pillar | Analogy | Technical Role |
| :--- | :--- | :--- |
| **Hooks** | The "Sensors" | Triggers that wake up your program when an event happens (e.g., a file opens). |
| **Maps** | The "Notebook" | A shared storage space where the Kernel and your apps can exchange data. |
| **Helpers** | The "Vending Machine" | A set of safe functions the Kernel provides so you don't have to do things manually. |

---

## 3. How a Program is "Born" 

1.  **Write:** You write a small program (usually in C, Go, or Python).
2.  **Verify:** The Kernel's **Verifier** checks the code for safety.
3.  **Compile:** The **JIT (Just-In-Time) Compiler** turns it into super-fast machine code.
4.  **Attach:** The program "hooks" onto a part of the system and starts monitoring or filtering data.

---

## 4. Real-World Use Cases

What do people actually use eBPF for?

* **High-Speed Networking:** Dropping "bad" data packets (DDoS attacks) before they even reach your apps.
* **Deep Security:** Watching if a suspicious program is trying to access your private passwords.
* **Observability:** Creating real-time "dashboards" that show exactly which part of your computer is running slow.

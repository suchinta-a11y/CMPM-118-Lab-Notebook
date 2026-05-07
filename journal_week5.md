# Week 5 Journal — Rustlings Exercises 18–20 + Paper Reading

## What I Worked On

The final week covered threads and smart pointers to finish out the Rustlings exercises, and I did the second paper reading on CHERI.

## Rustlings: Threads & Smart Pointers

**Threads** brought back ownership concerns in a new context. Rust's thread model requires that any data shared across threads is either moved (transferred ownership) or protected behind synchronization primitives like `Arc<Mutex<T>>`. The `move` keyword in closures — used to transfer ownership into a spawned thread — was a new pattern. The exercise involving sending data to two threads via `mpsc` was particularly instructive: you can't send the same `Sender` to two threads without cloning it first, which makes the ownership rules very concrete.

**Smart pointers** like `Box`, `Rc`, and `Arc` each solve different problems around heap allocation and shared ownership. Keeping them straight took some effort, especially understanding when `Rc` (single-threaded reference counting) vs `Arc` (thread-safe reference counting) was appropriate.

## Paper Reading: CHERI

**Summary:** CHERI extends hardware pointers with metadata: validity, memory range, and permissions (read/write/execute). The CPU enforces these on every memory access, catching buffer overflows and bad pointer use at the hardware level.

**Major Contributions:**
- Pointers that carry their own access rules, enforced in hardware
- Monotonicity: capabilities can only be made more restrictive, never more permissive
- Compatible with existing operating systems and code — no full rewrite required
- Enables intra-process sandboxing without the cost of separate processes

**Strengths / Weaknesses:**
Strengths: Doesn't break existing software; security guarantees are mathematically proven.
Weaknesses: Pointers are twice as large, which slows programs with heavy pointer use. Bounds compression can also waste memory due to alignment requirements.

**Questions:**
- Can Spectre-style attacks leak data across capability boundaries since the CPU still speculatively executes?
- In hybrid mode where most pointers are still plain integers, how much protection are you actually getting?

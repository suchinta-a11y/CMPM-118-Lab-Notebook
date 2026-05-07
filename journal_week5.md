# Week 5 Journal — Rustlings Exercises 18–20 + I/O Project + Paper Reading

## What I Worked On

The final week covered threads, smart pointers, and the end of the Rustlings exercises. I also built a complete minigrep command-line tool and did the second paper reading on CHERI.

## Rustlings: Threads & Smart Pointers

**Threads** brought back ownership concerns in a new context. Rust's thread model requires that any data shared across threads is either moved (transferred ownership) or protected behind synchronization primitives like `Arc<Mutex<T>>`. The `move` keyword in closures — used to transfer ownership into a spawned thread — was a new pattern. The exercise involving sending data to two threads via `mpsc` was particularly instructive: you can't send the same `Sender` to two threads without cloning it first, which makes the ownership rules very concrete.

**Smart pointers** like `Box`, `Rc`, and `Arc` each solve different problems around heap allocation and shared ownership. Keeping them straight took some effort, especially understanding when `Rc` (single-threaded reference counting) vs `Arc` (thread-safe reference counting) was appropriate.

## I/O Project: minigrep

Building minigrep was the most complete Rust program I'd written so far. The project pulled together multiple concepts:

- **Argument parsing** from `std::env::args()` — collecting args into a `Vec<String>` and passing them to a `Config::build` function that returns a `Result`
- **Error handling** with `unwrap_or_else` and `if let Err(e)` to gracefully exit instead of panicking
- **File I/O** using `fs::read_to_string`
- **Iterators and string slices** in the `search` and `search_case_insensitive` functions
- **Environment variables** — reading `IGNORE_CASE` from the environment to toggle case sensitivity at runtime
- **Module separation** — splitting logic into `main.rs` and `lib.rs` for testability

The case-insensitive search using `to_lowercase()` on both the query and each line was a clean pattern. Writing tests for `search` and `search_case_insensitive` directly in `lib.rs` also made it easy to verify correctness without running the full binary each time.

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

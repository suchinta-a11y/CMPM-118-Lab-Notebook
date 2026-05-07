# Week 3 Journal — Rustlings Exercises 8–13 + Quiz 1 + Paper Reading

## What I Worked On

This week covered structs, enums, strings, and modules. I also completed Quiz 1 and did the first paper reading on Arrakis.

## Rustlings

**Structs** felt familiar coming from other languages, but Rust's lack of inheritance and the way methods are defined in separate `impl` blocks took some adjustment. The distinction between associated functions (like `new`) and methods that take `self` was a bit confusing at first.

**Enums and pattern matching** were actually one of the more satisfying parts of Rust so far. Rust enums can hold data, which makes them far more powerful than enums in most languages. `match` expressions that exhaustively handle every variant felt like a cleaner version of switch statements.

**Strings** were unexpectedly tricky. The `String` vs `&str` distinction — one is a heap-allocated owned string, the other is a borrowed string slice — kept catching me off guard when functions expected one type and I passed the other.

## Quiz 1

The quiz covered variables, functions, and if statements through the apple pricing problem. The logic itself wasn't hard — if quantity exceeds 40, each apple costs 1 rustbuck, otherwise 2. The trickier part was getting the types right and making sure the function signature matched what the tests expected.

## Paper Reading: Arrakis

**Summary:** Arrakis re-architects the OS by removing the kernel from the I/O data path. Using hardware virtualization (SR-IOV), applications get direct access to network and disk resources. The kernel becomes a "control plane" for coarse-grained resource management, while a user-level library OS handles the high-performance data path.

**Major Contributions:**
- Kernel-bypass architecture that splits the OS into a control plane and a data plane without breaking process isolation
- Virtualized I/O abstractions (VNICs and VSAs) for hardware-independent direct I/O
- Caladan library: persistent data structures optimized for low-latency storage, eliminating filesystem marshaling overhead

**Strengths / Weaknesses:**
Strengths: Significant performance gains — 2–5x lower latency and 9x higher throughput for Redis. Eliminates system call overhead and kernel-to-user data copying.
Weaknesses: Relies heavily on modern hardware (SR-IOV/IOMMU) with limited virtual function counts (e.g., 64). Applications also need changes or specialized libraries to fully benefit.

**Questions:** How would Arrakis handle scenarios where active applications exceed available hardware virtual functions without a significant performance penalty during software emulation?

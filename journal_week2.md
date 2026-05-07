# Week 2 Journal — Rustlings Exercises 5–8

## What I Worked On

This week I continued into primitive types, then moved into vecs and began exploring move semantics — which is where things got significantly harder.

## What I Struggled With and How I Overcame It

**Move semantics** were the defining challenge of this week and honestly the most mind-bending concept Rust introduces. In most languages, assignment copies a value or copies a reference transparently. In Rust, assigning a heap-allocated value (like a `String` or `Vec`) *moves* ownership — the original variable is gone after the assignment. I'd write code that seemed perfectly reasonable and get hit with "value used after move" errors.

The key insight that helped me was thinking of ownership as a single thread of responsibility: exactly one variable owns a value at a time, and when that variable goes out of scope, the value is dropped. Once I started thinking in terms of *who owns this right now*, the errors started making sense.

**Borrowing vs moving** was the natural follow-up confusion. I kept trying to pass values into functions and then use them afterward, not realizing the function had consumed them. Learning to pass references (`&`) instead of values was the practical fix, but understanding *why* took longer.

**Vec operations** also had some gotchas around iteration — iterating over a Vec moves or borrows it depending on how you do it, which connects back to the ownership model.


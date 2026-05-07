# Week 1 Journal — Rustlings Exercises 1–5

## What I Worked On

This week was my introduction to Rust through the Rustlings exercises. I covered the first five sections: variables, functions, if statements, and the beginning of primitive types.

## What I Struggled With and How I Overcame It

**Variables and mutability** were the first real hurdle. Coming from languages where variables are mutable by default, Rust's strict `let` vs `let mut` distinction felt overly pedantic at first. I kept running into compiler errors because I'd try to reassign a variable I hadn't declared as `mut`. The fix was simple once I understood the philosophy — Rust makes you be explicit about mutability as a safety feature, not just a quirk.

**Shadowing** was another concept that tripped me up. The idea that you can re-declare a variable with the same name (even changing its type) felt wrong at first, like it was hiding bugs. But I came to see it as a clean way to transform a value through multiple steps without needing throwaway variable names.

**Type inference vs explicit types** — I wasn't always sure when Rust needed me to annotate types and when it could figure it out. Trial and error with the compiler errors actually helped a lot here; the Rust compiler gives unusually clear error messages compared to what I was used to.

By the end of the week, the compiler was starting to feel less like an adversary and more like a strict but helpful code reviewer.

# Week 4 Journal — Rustlings Exercises 13–18 + Quiz 2 & 3

## What I Worked On

This week covered error handling, generics, traits, and lifetimes. I also completed Quiz 2 and Quiz 3.

## Rustlings

**Error handling** with `Result` and `Option` was a paradigm shift. Rust has no exceptions — instead, functions that can fail return a `Result<T, E>`, and you have to handle both cases. The `?` operator made this much cleaner once I understood it, but initially I kept trying to unwrap things directly and getting panics.

**Generics** introduced a new layer of complexity. Writing functions or structs that work over multiple types required understanding type parameters and how to constrain them with trait bounds. The syntax took some getting used to.

**Traits** are Rust's answer to interfaces/abstract classes. Implementing a trait for a struct felt natural, but understanding trait objects (`dyn Trait`) vs generic trait bounds took longer to internalize.

**Lifetimes** were the hardest concept of the week by far. The compiler needs to know how long references are valid to prevent dangling references, and sometimes you have to annotate this explicitly. The syntax (`'a`) looks foreign and the mental model required is non-trivial.

## Quiz 2

The transformer quiz combined strings, vecs, move semantics, modules, and enums into one cohesive problem. Building a function that takes a `Vec<(String, Command)>` and applies each command using `match` was a satisfying exercise — it felt like the pieces from the past few weeks finally coming together. Using `.into_iter().map(...).collect()` as the core pattern was clean once I landed on it.

## Quiz 3

The report card quiz was about making `ReportCard` generic so it could hold either a numeric grade (`f32`) or a letter grade (`&str`). The fix was adding a type parameter `T` to the struct and constraining it with `std::fmt::Display` in the impl block so the `print` method could format it. Short change, big concept — generics with trait bounds.

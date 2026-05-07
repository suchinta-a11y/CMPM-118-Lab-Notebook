# Week 4 Journal — Rustlings Exercises 13–18 + Quiz 2 & 3 + I/O Project

## What I Worked On

This week covered error handling, generics, traits, and lifetimes. I also completed Quiz 2 and Quiz 3, and built a complete minigrep command-line tool as an I/O project.

## Rustlings

**Error handling** with `Result` and `Option` was a paradigm shift. Rust has no exceptions — instead, functions that can fail return a `Result<T, E>`, and you have to handle both cases. The `?` operator made this much cleaner once I understood it, but initially I kept trying to unwrap things directly and getting panics.

**Generics** introduced a new layer of complexity. Writing functions or structs that work over multiple types required understanding type parameters and how to constrain them with trait bounds. The syntax took some getting used to.

**Traits** are Rust's answer to interfaces/abstract classes. Implementing a trait for a struct felt natural, but understanding trait objects (`dyn Trait`) vs generic trait bounds took longer to internalize.

**Lifetimes** were the hardest concept of the week by far. The compiler needs to know how long references are valid to prevent dangling references, and sometimes you have to annotate this explicitly. The syntax (`'a`) looks foreign and the mental model required is non-trivial.

## Quiz 2

The transformer quiz combined strings, vecs, move semantics, modules, and enums into one cohesive problem. Building a function that takes a `Vec<(String, Command)>` and applies each command using `match` was a satisfying exercise — it felt like the pieces from the past few weeks finally coming together. Using `.into_iter().map(...).collect()` as the core pattern was clean once I landed on it.

## Quiz 3

The report card quiz was about making `ReportCard` generic so it could hold either a numeric grade (`f32`) or a letter grade (`&str`). The fix was adding a type parameter `T` to the struct and constraining it with `std::fmt::Display` in the impl block so the `print` method could format it. Short change, big concept — generics with trait bounds.

## I/O Project: minigrep

This week I also built minigrep, a command-line tool that searches for a query string inside a file — essentially a simplified version of the Unix `grep` command. The project was split across two files: `main.rs` for argument parsing and setup, and `lib.rs` for all the core logic.

### What the project does

You run it like:
```
cargo run -- searchterm filename.txt
```
It prints every line in the file that contains the search term. You can also set an environment variable `IGNORE_CASE=1` to make the search case-insensitive.

### What I struggled with and how I overcame it

**Separating main.rs and lib.rs** was the first design challenge. The whole point was keeping `main` thin — just parsing args, calling `Config::build`, and handling top-level errors — while all the real logic lives in `lib.rs`. This felt overly structured for a small program, but I could see why it matters for testability: you can write unit tests directly against the functions in `lib.rs` without invoking the binary.

**Error handling with `Result`** was used throughout. `Config::build` returns `Result<Config, &'static str>` instead of panicking when arguments are missing. In `main`, `unwrap_or_else` handles the error case by printing a message and calling `process::exit(1)`. The `run` function returns `Result<(), Box<dyn Error>>` and uses the `?` operator to propagate file read errors cleanly. Getting comfortable with this pattern — returning errors up the call stack instead of panicking — was the core lesson of the project.

**Lifetimes in the search function** were the trickiest part. The `search` function returns a `Vec<&str>` of lines that match the query, but those string slices borrow from `contents`, not from `query`. Without explicit lifetime annotations (`'a`), the compiler can't figure out which argument the returned references point into and rejects the code. Writing `pub fn search<'a>(query: &str, contents: &'a str) -> Vec<&'a str>` makes it explicit: the returned slices live as long as `contents`.

**Case-insensitive search via environment variable** was a clean feature to add. `env::var("IGNORE_CASE").is_ok()` checks whether the variable is set at all — we don't care about its value, just its presence. That bool gets stored in `Config` and used in `run` to decide which search function to call. `search_case_insensitive` works by lowercasing both the query and each line before comparing, using shadowing to rebind `query` as a `String` (since `to_lowercase()` allocates new data rather than borrowing).

**Test-driven development** was practiced here for the first time. I wrote the tests for `search` and `search_case_insensitive` before finishing the implementations, which made it easy to verify correctness without running the full binary each time.

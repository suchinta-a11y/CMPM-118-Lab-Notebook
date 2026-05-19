# Lab Notebook Week 7

Supreeth Chinta

---

## Reflection

This week I came into lab a little late while Surendra was already explaining recursion in the filesystem project. I hadn’t started on the project at that point because I was really busy that week with midterms, so I felt pretty behind going into class. I was hoping the lab would be explained during class so I could get a chance to catch up and understand how to start it properly.

During the explanation, Surendra walked through how the filesystem is basically built like a tree where directories can contain other directories and files. That helped make things a lot clearer, especially how the structure keeps going deeper until it hits actual files. There was also a side discussion about recursion and how it connects to things like fold-style thinking, where you kind of keep building or collapsing structure step by step until you get a final result. That wasn’t something I expected, but it actually made the whole idea click a lot better.

It also helped to compare it to normal loops. Instead of going step by step like a loop, this is more like a structure that keeps calling into itself until it reaches the bottom.

---

## Parts that took me time to review

The biggest issue I ran into this week wasn’t even the Rust code itself, it was my Mac setup. My Command Line Tools were completely broken, and every time I tried running cargo test I kept getting linker errors or install failures. I tried reinstalling multiple times, resetting xcode-select, deleting the tools, and running different install commands, but it kept ending in the same issue where macOS wouldn’t properly install them.

Because of that, I literally couldn’t run or test anything for a while, so I had to email Surendra about it. After a bunch of troubleshooting I finally got past that blocker and was able to actually run the project instead of just fighting environment errors.

After that, the next confusing part was understanding what the tests were actually expecting. At first I only had very basic placeholder structs, but once I looked at the test file more closely it became clear that the lab is basically asking for a full recursive filesystem structure with directories, files, and path traversal working properly. Even getting to the point where tests were actually being picked up felt like progress because earlier it was just showing zero tests running.

---

## Goals

Next week I want to finish this lab by Friday and get all the tests passing. I also want to keep improving my understanding of tree structures because this project makes it pretty clear how important they are in systems and how often they show up in real implementations. I feel like working through this is helping me slowly get more comfortable with that idea.

# Lab Notebook Week 6
**Supreeth Chinta**

## Reflection

This week we discussed the CHERI paper in class and then got started on the filesystem project posted on Zulip. The CHERI paper was honestly a bit too high level for me to follow in a lot of places. A lot of the hardware and memory safety concepts went over my head, so I ended up using AI to break down some of the denser sections into simpler terms, which helped a little but I still don't feel like I have a great grasp on it. After the paper discussion we started the filesystem project and I got through part of step one, specifically the print_tree function. The main takeaway was that a node has to be defined as an Enum since it can be either a file or a directory, and because that definition is recursive you have to use Box or BTreeMap so Rust knows the size of the type at compile time.

## Parts that took review

Rustlings 18-20 gave me some trouble. The big themes across all three were iterators, shared ownership with Rc, and threads. The iterator stuff in rustling 18 was confusing because I didn't fully get how Rust lets you pull apart a string character by character and then reassemble it. Rustling 19 was about Rc, which is how Rust lets multiple parts of a program share ownership of the same data, and I kept mixing up when to clone the reference versus create a totally new one. Rustling 20 introduced threads, and the part I got stuck on was understanding how you actually retrieve a value that a thread computed after it finishes running. I used AI to help break all of these down which did help, but I know I was leaning on it more than I should have been.

One thing I've been reflecting on is that around midterms I started deprioritizing this class and relying too heavily on AI instead of actually working through things myself. Earlier in the semester I was keeping up and genuinely learning, and I want to get back to that.

## Goals

Next week I want to finish step one of the filesystem project and hopefully get through step two before class as well.

**Note:** I did use AI for the journal not to write it for me, but to correct any spelling and grammar checks. I just wanted to make sure it was written cleanly and properly. I submitted it in week 7 because I didn't get a chance to finish it in week 6.

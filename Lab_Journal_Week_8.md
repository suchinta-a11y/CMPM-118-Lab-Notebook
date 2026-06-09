# Lab Notebook Week 8
Supreeth Chinta

---

## Reflection

This week was rough. I came into class sick and could only stay for about thirty minutes before I had to leave. The class was focused on recursion and we were working on a cookbook assignment, but I was not in a state to participate properly and had to head out early. This was also the week I was supposed to check in on the filesystem lab. Because I left early that did not happen, which I felt bad about. I had finished the lab, just a little later than I should have, and I think it ended up being the hardest thing I have done in this course so far.

---

## Things I Need to Review

The filesystem lab challenged me in a few specific ways I want to keep working on. The trickiest part was understanding lifetimes in the handle types. A handle does not own the data it works with, it borrows from the filesystem directly, and getting that right in Rust required careful thinking about how long references are allowed to live. I had to keep reminding myself of that distinction because my instinct kept pulling me toward treating the handle as owning its own copy of the data.

Implementing the Find trait was another area that took time. For files it is straightforward since there are no children to search through, but for directories the logic needs to go deeper recursively, checking children and their children all the way down. Sharing that recursive logic cleanly between the two types without duplicating code was something I had to think through carefully. I also want to keep reviewing how tree structures work more generally because this lab made it clear how often they show up in real systems.

---

## Goals

I want to make sure I get my check-in done properly now that I have finished the lab. I also want to keep building on tree structures and recursion because this project showed me how central they are to systems work. Going forward I want to be better about communicating when something like getting sick disrupts my schedule rather than just quietly missing things.

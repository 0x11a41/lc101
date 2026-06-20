---
layout: post
title: "Week 1: Escaping the Maze with Two Pointers"
date: 2026-06-19
author: "Core Admin Team"
categories: [Arrays, Two-Pointer]
---

Welcome to Week 1! To kick off our journey, we are tackling a classic pattern that saves you from running unnecessary loops: **The Two-Pointer Technique**.

### 🧩 The Core Problem
Imagine you have a **sorted** array of numbers, and you need to find if any two numbers add up to a specific `target` value. 

* **The Brute Force Way ($O(N^2)$):** You pick the first number, and check it with every other number. Then you pick the second number, and check it with every other number. It works, but it's slow. It's like checking every single pair of shoes in a store to find a match.

---

### 🎭 The Layman Story: The Price Match Game

Imagine you and a friend are standing in a long hallway of a grocery store. The items are perfectly sorted by price—cheapest on the far **left**, most expensive on the far **right**. 

Your goal is to find two items that cost *exactly* ₹100 combined.



1. **The Setup:** You stand at the cheapest item on the left (Pointer A). Your friend stands at the costliest item on the right (Pointer B).
2. **The Test:** You add your two items together.
3. **The Logic:**
   * **Is the total too high? (e.g., ₹120):** The only way to make the total smaller is to pick a cheaper item. Since you are already at the cheapest possible item, your friend must take one step to the left to a slightly cheaper item.
   * **Is the total too low? (e.g., ₹80):** The only way to make the total bigger is to pick a pricier item. Since your friend is already at the max price options, *you* must take one step to the right to a slightly pricier item.
   * **Is it exactly ₹100?** Ding ding ding! You win.

By walking toward each other, you look at each item at most *once*. You just turned an exhausting search into a fast, linear walk ($O(N)$ time complexity).

---

### 🛠️ The Blueprint Structure

When you translate this story into code, your mental framework should look like this:

1. Initialize `left = 0` and `right = array.length - 1`.
2. Run a loop while `left < right`.
3. Calculate `current_sum = array[left] + array[right]`.
4. Use `if/else` conditions to move either the `left` pointer or the `right` pointer based on our grocery store rules.

### 🚀 Try It Yourself!
Now that you have the intuition, head over to LeetCode and try to apply this exact framework to **LeetCode 167: Two Sum II - Input Array Is Sorted**.

*Hint: What should happen to your pointers if the sum matches the target?*

Drop your completion screenshots or GitHub PR links in your respective class WhatsApp groups!

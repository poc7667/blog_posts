---
title: Leetcode notes (medium)
date: 2016-04-11 11:50:37
tags: Leetcode
---

# https://leetcode.com/problems/missing-number/

    Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.
    For example,
    Given nums = [0, 1, 3] return 2.
    Note:
    Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?
    利用bit xor 求解


# https://leetcode.com/problems/reverse-string/

    Write a function that takes a string as input and returns the string reversed.
    Example:
    Given s = "hello", return "olleh".

    class Solution(object):
        def reverseString(self, s):
           return s[::-1]
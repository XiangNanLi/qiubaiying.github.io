---
layout:     post
title:      两数相加(两大数相加)
subtitle:   
date:       2018-07-15
author:     
catalog: true
tags:
	- 算法
    
---

# ARTS2 (Add Two Numbers)

## Problem

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.
Example:

    '''
    Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
    Output: 7 -> 0 -> 8
    Explanation: 342 + 465 = 807.
    '''

## Solution

> Java Code:

    '''
    /**
    * Definition for singly-linked list.
    * public class ListNode {
    *     int val;
    *     ListNode next;
    *     ListNode(int x) { val = x; }
    * }
    */

    class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = null;
        ListNode preNode = null;
        ListNode next1 = l1;
        ListNode next2 = l2;
        int remainder = 0;
        int divisor = 0;
        while (next1 != null || next2 != null) {
            int num1 = 0;
            if (next1 != null) {
                num1 = next1.val;
                next1 = next1.next;
            }
            int num2 = 0;
            if (next2 != null) {
                num2 = next2.val;
                next2 = next2.next;
            }
            int sum = num1 + num2 + divisor;
            divisor = sum / 10;
            remainder = sum % 10;

            if (result == null) {
                result = new ListNode(remainder);
                preNode = result;
            } else {
                ListNode tmpNode = new ListNode(remainder);
                preNode.next = tmpNode;
                preNode = tmpNode;
            }
        }
        if (divisor != 0) {
            ListNode tmpNode = new ListNode(divisor);
            preNode.next = tmpNode;
        }
        return result;
        }
    }
'''

## Review

Last week I learned the baise knowledge of Java. Now I am doing some demo in Java.
But must write some blog of the learning java, otherwise  I will forget it soon, and I cannot find the knowledge that I learn before.

## Technique

The visual code is a text editer , if I want create a project, I must integrate some other extentions .

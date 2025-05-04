# Palindrome-Linked-List
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode slow = head, fast = head, prev, temp;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        prev = slow;
        slow = slow.next;
        prev.next = null;
        while (slow != null) {
            temp = slow.next;
            slow.next = prev;
            prev = slow;
            slow = temp;
        }
        fast = head;
        slow = prev;
        while (slow != null) {
            if (fast.val != slow.val) return false;
            fast = fast.next;
            slow = slow.next;
        }
        return true;
    }
}


# Palindrome Linked List

This repository contains a Java solution for checking whether a singly linked list is a **palindrome**—that is, whether it reads the same forward and backward.

---

## Problem Statement

Given the head of a singly linked list, return `true` if it is a palindrome, or `false` otherwise.

---

## Solution Explanation

### Java Method

```java
public boolean isPalindrome(ListNode head)
```

This method determines if the linked list is a palindrome using the following steps:

### Step-by-Step Breakdown

#### 1. **Find the Middle of the List**

We use two pointers:

* `slow` moves one step at a time.
* `fast` moves two steps at a time.

When `fast` reaches the end, `slow` will be at the middle of the list.

```java
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
```

#### 2. **Reverse the Second Half of the List**

Starting from the middle, we reverse the second half of the linked list:

```java
prev = slow;
slow = slow.next;
prev.next = null;
while (slow != null) {
    temp = slow.next;
    slow.next = prev;
    prev = slow;
    slow = temp;
}
```

#### 3. **Compare Both Halves**

We compare the original first half and the reversed second half:

```java
fast = head;
slow = prev;
while (slow != null) {
    if (fast.val != slow.val) return false;
    fast = fast.next;
    slow = slow.next;
}
```

#### 4. **Return the Result**

If all nodes matched, we return `true`:

```java
return true;
```

---

## Example

For the list:

```
1 -> 2 -> 2 -> 1
```

* Second half reversed: `1 -> 2`
* First half: `1 -> 2`
* Since they match, the function returns `true`.

---

## Time & Space Complexity

* **Time Complexity**: O(n) — We traverse the list multiple times.
* **Space Complexity**: O(1) — Reversal is done in-place.

---

## Files

* `Solution.java`: Contains the Java code for the palindrome check.

---

## Note

This solution modifies the original linked list by reversing its second half. If preservation of the original list is needed, consider restoring it afterward.

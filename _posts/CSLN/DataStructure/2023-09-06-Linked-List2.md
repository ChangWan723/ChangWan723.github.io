---
title: "Mastering Linked Lists: Avoiding Common Pitfalls"
date: 2023-09-06 13:45:00 UTC
categories: [ (CS) Learning Note, Data Structure ]
tags: [ computer science, Data Structure ]
pin: false
---

Although simple, linked lists are crucial in data structures, providing a dynamic and flexible way of storing and managing data. It is important for us to avoid some common pitfalls in linked lists and learn how to perform common operations with linked list.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Common Pitfalls in Linked List Implementations](#common-pitfalls-in-linked-list-implementations)
    * [Not Handling the Empty State Correctly](#not-handling-the-empty-state-correctly)
    * [Be Careful about Losing Pointers](#be-careful-about-losing-pointers)
    * [Memory Leaks in Languages with Manual Memory Management](#memory-leaks-in-languages-with-manual-memory-management)
    * [Incorrectly Handling Node Pointers Leading to Infinite Loops](#incorrectly-handling-node-pointers-leading-to-infinite-loops)
  * [Common Operations with Linked List](#common-operations-with-linked-list)
    * [Reverse a Linked List](#reverse-a-linked-list)
    * [Detect a Cycle in a Linked List](#detect-a-cycle-in-a-linked-list)
    * [Merging Two Ordered Linked Lists](#merging-two-ordered-linked-lists)
    * [Delete the n-th Node From the Bottom](#delete-the-n-th-node-from-the-bottom)
    * [Find Middle Node in a Linked List](#find-middle-node-in-a-linked-list)
  * [Example: Determining Palindrome Using Linked Lists](#example-determining-palindrome-using-linked-lists)
<!-- TOC -->

---

## Common Pitfalls in Linked List Implementations

### Not Handling the Empty State Correctly

One of the first errors often encountered is an incorrect handling of an empty linked list, especially when inserting the first node or deleting the last node.

**How to Avoid:**
- Always check if the head pointer is `null` (for an empty list) before performing operations.
- When inserting the first node, remember to set the head to the newly created node.
- When deleting nodes, if the list becomes empty, ensure you reset the head (and tail, in a doubly linked list) to `null`.

```java
public void insertAtHead(int data) {
    Node newNode = new Node(data);
    if (head == null) {
        head = newNode;
    } else {
        newNode.next = head;
        head = newNode;
    }
}
```

### Be Careful about Losing Pointers

When inserting or deleting nodes, especially in a singly linked list, there's a risk of losing access to the rest of the list if the next pointers are not handled correctly.

**How to Avoid:**
- When inserting nodes, always pay attention to the order of operations.

For example, insert the x node:

```
x->next = p->next;
p->next = x;
```

You need to do `x->next = p->next` first, then `p->next = x`, so that you don't lose the pointer. If the above code changes the order, the linked list will be broken.

### Memory Leaks in Languages with Manual Memory Management

In languages like C and C++, where manual memory management is required, forgetting to free the memory of deleted nodes can lead to memory leaks.

**How to Avoid:**
- Always use `free()` or the appropriate memory deallocation function to free the memory of a node immediately after it is removed from the list.

### Incorrectly Handling Node Pointers Leading to Infinite Loops

Particularly in circular linked lists, incorrect handling of pointers when adding or removing nodes can lead to infinite loops or lost segments of the list.

**How to Avoid:**
- Use caution when traversing circular linked lists to avoid infinite loops by checking for the return to the head node as a termination condition.

## Common Operations with Linked List

For class `ListNode`:

```java 
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}
```

### Reverse a Linked List

- Time complexity: `O(n)`
- Space complexity: `O(1)`

```java 
public ListNode reverseLinkedList(ListNode head) {
    ListNode prev = null; // Initialize a previous pointer to null
    ListNode curr = head; // Initialize a current pointer to the head of the list (For conciseness, this line can be removed, and use the head node directly. However, keeping this line improves code readability)
    while (curr != null) {
        ListNode nextTemp = curr.next; // Temporarily store the next node
        curr.next = prev; // Reverse the current node's pointer
        prev = curr; // Move the prev pointer forward
        curr = nextTemp; // Move the curr pointer forward
    }
    return prev; // At the end, prev will be the new head of the reversed list
}
```

### Detect a Cycle in a Linked List

- Time complexity: `O(n)`
- Space complexity: `O(1)`

```java 
public boolean hasCycle(ListNode head) {
    if (head == null) 
        return false; // If the list is empty, there can't be a cycle

    ListNode slow = head; // This will be the "tortoise"
    ListNode fast = head; // This will be the "hare"

    while (fast != null && fast.next != null) {
        slow = slow.next; // Move the tortoise one step
        fast = fast.next.next; // Move the hare two steps

        if (slow == fast) { // If the hare catches up with the tortoise, there's a cycle
            return true;
        }
    }

    return false; // If the hare reaches the end, there's no cycle
}
```

### Merging Two Ordered Linked Lists

- Time complexity: `O(n + m)`
- Space complexity: `O(1)`

```java 
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    // Create a dummy head for the merged list.
    ListNode dummyHead = new ListNode(0);
    ListNode current = dummyHead;
    
    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {
            // If l1's value is less than or equal to l2's, append it to the merged list.
            current.next = l1;
            l1 = l1.next; // Move l1's pointer forward.
        } else {
            // If l2's value is less, append it to the merged list.
            current.next = l2;
            l2 = l2.next; // Move l2's pointer forward.
        }
        current = current.next; // Move the merged list's pointer forward.
    }
    
    // Attach the remaining elements of l1 or l2 to the merged list.
    current.next = (l1 != null) ? l1 : l2;
    
    return dummyHead.next; // Return the merged list, excluding the dummy head.
}
```

### Delete the n-th Node From the Bottom

- Time complexity: `O(n)`
- Space complexity: `O(1)`

```java 
public ListNode removeNthFromEnd(ListNode head, int n) {
    // Create a dummy head to simplify edge cases, such as removing the actual head node
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode first = dummy;
    ListNode second = dummy;
    
    // Advance first pointer so there's an n-node gap between first and second
    for (int i = 0; i <= n; i++) { // n must be greater than 0 and less than or equal to the length of the list. 
        first = first.next;
    }
    
    // Move first to the end, maintaining the gap
    while (first != null) {
        first = first.next;
        second = second.next;
    }
    
    // Skip the nth node from the end
    second.next = second.next.next;
    
    // Return the head of the modified list
    return dummy.next;
}
```

### Find Middle Node in a Linked List

- Time complexity: `O(n)`
- Space complexity: `O(1)`

```java 
public ListNode findMiddleNode(ListNode head) {
    // Initialize two pointers, slow and fast, at the head of the list
    ListNode slow = head;
    ListNode fast = head;

   // Move fast pointer two steps and slow pointer one step at a time
    while (fast != null && fast.next != null) {
        slow = slow.next; // Slow pointer moves one step
        fast = fast.next.next; // Fast pointer moves two steps
    }
    
    // When fast pointer reaches the end, slow pointer will be at the middle
    return slow;
}
```

## Example: Determining Palindrome Using Linked Lists

- Time complexity: `O(n)`
- Space complexity: `O(1)`

```java 
public boolean isPalindrome(ListNode head) {
    if (head == null || head.next == null) {
        return true; // A list with 0 or 1 node is inherently a palindrome
    }
    
    // Find the middle of the list
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    
    // If the list has odd number of elements, skip the middle element
    if (fast != null) {
        slow = slow.next;
    }
    
    // Reverse the second half of the list
    ListNode secondHalf = reverse(slow);
    
    // Compare the first half and the reversed second half
    ListNode firstHalf = head;
    while (secondHalf != null) {
        if (firstHalf.val != secondHalf.val) {
            return false; // The values do not match, not a palindrome
        }
        firstHalf = firstHalf.next;
        secondHalf = secondHalf.next;
    }
    
    return true; // The list represents a palindrome
}

private ListNode reverse(ListNode head) {
    ListNode prev = null;
    while (head != null) {
        ListNode nextTemp = head.next;
        head.next = prev;
        prev = head;
        head = nextTemp;
    }
    return prev;
}
```

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.

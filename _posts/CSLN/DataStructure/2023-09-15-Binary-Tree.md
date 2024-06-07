---
title: "Binary Trees: The Most Common Tree"
date: 2023-09-13 12:00:00 UTC
categories: [ (CS) Learning Note, Data Structure ]
tags: [ computer science, Data Structure ]
pin: false
---


Binary trees form the basis of many complex data structures and algorithms, including binary search trees, heaps, and balanced trees like AVL trees and red-black trees. 

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is a Tree?](#what-is-a-tree)
    * [Concepts Related to Trees](#concepts-related-to-trees)
  * [What is a Binary Tree?](#what-is-a-binary-tree)
    * [Types of Binary Trees](#types-of-binary-trees)
    * [Applications of Binary Trees](#applications-of-binary-trees)
  * [How to Represent Binary Trees?](#how-to-represent-binary-trees)
    * [Linked Representation](#linked-representation)
      * [Advantages](#advantages)
      * [Disadvantages](#disadvantages)
    * [Array-Based Representation](#array-based-representation)
      * [Advantages](#advantages-1)
      * [Disadvantages](#disadvantages-1)
  * [Traversal of Binary Trees](#traversal-of-binary-trees)
<!-- TOC -->

---

## What is a Tree?

In data structure, a tree is a hierarchical data structure consisting of nodes connected by edges. It is a nonlinear data structure used to represent hierarchical relationships between elements.

- In a tree:
   - There is a root node, which is the topmost node in the hierarchy.
   - Each node has zero or more child nodes.
   - Nodes are connected by edges, which represent the relationships between nodes.
   - Trees are acyclic data structures, meaning there are no cycles or loops allowed in their structure. 
   - Each node is reachable from the root by following a unique path.

![](https://i.postimg.cc/V68RQNG6/image12.png){: .w-10 .shadow .rounded-10 }
_Tree_

![](https://i.postimg.cc/mDKFfp2S/image13.png){: .w-10 .shadow .rounded-10 }
_Not a Tree (Graph)_

### Concepts Related to Trees

- A normal tree usually contains the following elements:
   - **Node**: Trees consist of a collection of nodes. Each node stores a piece of data.
   - **Parent and Child Nodes**: Nodes in a tree are organized hierarchically. Each node (except the root) has a parent node, and the nodes directly connected below it are its child nodes.
   - **Sibling Nodes**: Nodes with the same parent node.
   - **Root**: The top node in the tree. It is the only node without a parent node.
   - **Leaf**: A node that does not have any children.
   - **Edge**: The link between two nodes.


- In addition to this, trees have three more similar concepts:
   - **Depth**: The length of the path from the root to this node.
   - **Height**: The length of the path from this node to the deepest leaf.
   - **Level**: Depth + 1

![](https://i.postimg.cc/hjqtLXMK/image14.png){: .w-10 .shadow .rounded-10 }

## What is a Binary Tree?

A binary tree is a tree data structure in which each node has at most two children, referred to as the left child and the right child. It is a specialized form of a tree, which is a structure made up of nodes connected by edges without having any cycles.


### Types of Binary Trees

1. **Full Binary Tree**: Every node has 0 or 2 children.
2. **Complete Binary Tree**: All levels are completely filled except possibly for the last level, which is filled from left to right.
3. **Degenerate (or Pathological) Binary Tree**: A Binary Tree where every parent node has only one child node.
4. **Perfect Binary Tree**: A binary tree in which all interior nodes have two children and all leaves have the same depth.
5. **Balanced Binary Tree**: A binary tree where the height of the two subtrees of any node differ by no more than one.

![](https://i.postimg.cc/HxF6xCtc/image15.png){: .w-10 .shadow .rounded-10 }

> - If a tree is a Perfect Binary Tree, it must be both a Complete Binary Tree and a Full Binary Tree.
{: .prompt-tip }

### Applications of Binary Trees

1. **Binary Search Trees (BST)**: Used for maintaining a dynamically changing dataset in sorted order, allowing for quick lookup, addition, and deletion of items.
2. **Heap**: A special tree-based data structure in which the tree is a complete binary tree that satisfies the heap property (min-heap or max-heap).
3. **Syntax Trees**: Used in Compilers to represent the structure of program code.
4. **Huffman Coding Tree**: Used in data compression algorithms.


## How to Represent Binary Trees?

Efficient storing (or representing) of binary trees is crucial for optimizing performance and resource usage. The following discusses two primary methods for representing binary trees: **linked representation** and **array-based representation**.

### Linked Representation

Linked representation of binary trees involves using nodes, where each node contains three parts: a data field, a pointer to the left child, and a pointer to the right child. This method is the most common way to represent trees because **it naturally reflects the hierarchical structure of a tree.**

![](https://i.postimg.cc/qRZ2BX41/image16.png){: .w-10 .shadow .rounded-10 }

#### Advantages

- **Dynamic Size**: Nodes can be added or removed dynamically, which is ideal for trees whose size changes frequently.
- **Ease of Use**: Directly models the conceptual structure of a tree, making it intuitive to perform recursive operations like traversals, insertions, and deletions.
- **Flexibility**: No need to pre-allocate memory, and it's easy to extend to more complex tree structures, such as threaded trees or trees with parent pointers.

#### Disadvantages

- **Memory Usage**: Each node requires extra memory for the pointers along with the data.
- **Memory Coherence**: Pointer-intensive storage can lead to poor cache performance because tree nodes may not be stored contiguously in memory.

### Array-Based Representation

Array-based representation uses a simple array to store the elements of the binary tree. The positions of the left and right children and the parent of any element can be calculated using arithmetic operations on the indices.

For a binary tree stored in an array:
- The element at index `i` has its left child at index `2*i` and its right child at index `2*i + 1`.
- The parent of the element at index `i` (where `i` is not 0) is located at index `i/2`.
- Typically, the root node is stored at `index 1` of the array to make it easier to calculate the child nodes. 
  - It is possible to store the root node at `index 0`. This saves one unit of space, but it makes the nodes calculation slightly more complicated.

---

- **Array-Based Representation is more suitable for Complete Binary Tree.**
  - Almost no wasted space.
- Heap is actually a complete binary tree.
  - So, Heap Sort uses Array-Based Representation to maintain the Max Heap.

![](https://i.postimg.cc/v8CPwjbg/image17.png){: .w-10 .shadow .rounded-10 }
_Array-Based Representation (Complete Binary Tree)_

![](https://i.postimg.cc/GhkjwmXV/image18.png){: .w-10 .shadow .rounded-10 }
_Array-Based Representation (Non-Complete Binary Tree)_

#### Advantages

- **Memory Efficiency**: No extra memory is used for pointers.
- **Data Locality**: Better cache performance due to contiguous memory allocation, which can speed up traversal and other operations.

#### Disadvantages

- **Fixed Size**: The size of the tree is generally fixed after the initial declaration, which can lead to wasted space or limitations on the growth of the tree.
- **Complexity in Operations**: Inserting or deleting nodes (especially in the middle of the array) can be complex and require significant data movement.

## Traversal of Binary Trees

Traversing a binary tree means visiting all the nodes in some order. Typically, there are three types of depth-first traversal:

- **Inorder** (Left, Root, Right): Visit the left subtree, the root, and then the right subtree.
- **Preorder** (Root, Left, Right): Visit the root, the left subtree, and then the right subtree.
- **Postorder** (Left, Right, Root): Visit the left subtree, the right subtree, and then the root.

![](https://i.postimg.cc/RFnPDJjQ/image19.png){: .w-10 .shadow .rounded-10 }

```c 
void preOrder(Node* root) {
    if (root == null) return;
    print root // This is pseudo-code for printing the root node.
    preOrder(root->left);
    preOrder(root->right);
}
 
void inOrder(Node* root) {
    if (root == null) return;
    inOrder(root->left);
    print root // This is pseudo-code for printing the root node.
    inOrder(root->right);
}
 
void postOrder(Node* root) {
    if (root == null) return;
    postOrder(root->left);
    postOrder(root->right);
    print root // This is pseudo-code for printing the root node.
}
```

There is also **level-order traversal**, which visits nodes at the same depth level before moving on to nodes at the next depth level.
- We can implement level-order traversal with the help of a Queue, by using Breadth-First Search (BFS).

```java 
public static void levelOrder(TreeNode root) {
    if (root == null) return;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        TreeNode current = queue.poll();
        System.out.print(current.val);

        if (current.left != null) {
            queue.offer(current.left);
        }
        if (current.right != null) {
            queue.offer(current.right);
        }
    }
}
```


<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.

- Parmar, A.K. (2020) _Different types of binary tree with colourful illustrations, Medium_. Available at: https://towardsdatascience.com/5-types-of-binary-tree-with-cool-illustrations-9b335c430254

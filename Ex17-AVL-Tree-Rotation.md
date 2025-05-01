# EXERCISE 17: AVL Tree – Right Rotation

## DATE:
25-03-2025

## AIM:
To write a C function to perform right rotation in an AVL Tree.

---

## Algorithm:
1. Define a structure for the AVL Tree node with data, left and right child pointers, and height.
2. Create helper functions:
   - `height()` – returns height of a node.
   - `max()` – returns max of two integers.
3. Implement the `rotateRight()` function:
   - Let `y` be the unbalanced node and `x` be its left child.
   - Perform the right rotation by making `x` the new root of the subtree.
   - Adjust pointers accordingly.
   - Update the heights of the affected nodes.
4. Write a sample insertion setup to create a Left-Left imbalance and apply `rotateRight()` manually.
5. Use in-order traversal to display the balanced tree.

---

## Program:
```c
/*
Program to perform right rotation in AVL Tree
Developed by: SHAKTHI KUMAR S
RegisterNumber: 212222110043
*/

#include <stdio.h>
#include <stdlib.h>

// Define the structure of a node
struct Node {
    int key;
    struct Node* left;
    struct Node* right;
    int height;
};

// Utility function to get height
int height(struct Node* N) {
    if (N == NULL)
        return 0;
    return N->height;
}

// Utility function to get max of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Create a new node
struct Node* newNode(int key) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->key = key;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

// Function to perform right rotation
struct Node* rotateRight(struct Node* y) {
    struct Node* x = y->left;
    struct Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Inorder traversal of the tree
void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->key);
        inorder(root->right);
    }
}

int main() {
    // Simulating Left-Left imbalance
    struct Node* root = newNode(30);
    root->left = newNode(20);
    root->left->left = newNode(10);

    printf("Before Right Rotation (Inorder):\n");
    inorder(root);

    // Apply Right Rotation
    root = rotateRight(root);

    printf("\nAfter Right Rotation (Inorder):\n");
    inorder(root);

    return 0;
}

```

## Output:
![image](https://github.com/user-attachments/assets/5ecc05e5-0f2e-428d-9815-f41ede73ad52)



## Result:
Thus, the function to perform right rotation in an AVL Tree is implemented successfully.

# EXERCISE 16: AVL Tree – Insertion

## DATE:
24-03-2025

## AIM:
To write a C function to insert the elements in an AVL Tree.

---

## Algorithm:
1. Define a structure for the AVL Tree node with data, left and right pointers, and height.
2. Create utility functions:
   - `height()` – returns the height of a node.
   - `max()` – returns the maximum of two integers.
   - `getBalance()` – returns the balance factor of a node.
   - `rotateRight()` – performs a right rotation.
   - `rotateLeft()` – performs a left rotation.
3. Create the `insert()` function:
   - Insert the node using normal BST insertion.
   - Update the height.
   - Check balance factor.
   - Perform appropriate rotations (LL, RR, LR, RL) to balance the tree.
4. In the `main()` function, insert elements and optionally print the tree using in-order traversal.
5. End.

---

## Program:
```c
/*
Program to insert the elements in an AVL Tree
Developed by: SHAKTHI KUMAR S
RegisterNumber: 212222110043
*/

#include <stdio.h>
#include <stdlib.h>

// AVL Tree node structure
struct Node {
    int key;
    struct Node* left;
    struct Node* right;
    int height;
};

// Utility function to get the height of a node
int height(struct Node* N) {
    if (N == NULL)
        return 0;
    return N->height;
}

// Utility function to get maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Create a new AVL tree node
struct Node* newNode(int key) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->key = key;
    node->left = node->right = NULL;
    node->height = 1; // New node is initially added at leaf
    return node;
}

// Right rotate subtree rooted with y
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

// Left rotate subtree rooted with x
struct Node* rotateLeft(struct Node* x) {
    struct Node* y = x->right;
    struct Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get balance factor of node N
int getBalance(struct Node* N) {
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}

// Recursive function to insert a key in the subtree rooted with node and return the new root
struct Node* insert(struct Node* node, int key) {
    // Perform the normal BST insertion
    if (node == NULL)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Equal keys not allowed
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor to check whether this node became unbalanced
    int balance = getBalance(node);

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rotateRight(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return rotateLeft(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = rotateLeft(node->left);
        return rotateRight(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rotateRight(node->right);
        return rotateLeft(node);
    }

    // Return the (unchanged) node pointer
    return node;
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
    struct Node* root = NULL;

    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 10);
    root = insert(root, 25);
    root = insert(root, 50);
    root = insert(root, 5);

    printf("Inorder traversal of the constructed AVL tree is:\n");
    inorder(root);

    return 0;
}

```

## Output:
![image](https://github.com/user-attachments/assets/10988b0f-bcda-4be0-a905-0a2118906d94)



## Result:
Thus, the function to insert the elements in an AVL Tree is implemented successfully in C programming language.

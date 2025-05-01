# EXERCISE 19: B+ Tree – Traversal

## DATE:
31-03-2025

## AIM:
To write a C function to traverse the elements in a B+ Tree.

---

## Algorithm:
1. **Define** a B+ tree node structure that contains keys and children.
2. Ensure **leaf nodes are linked** together to allow for fast range traversal.
3. Insert multiple keys into the B+ Tree (for demonstration).
4. Traverse the B+ Tree:
   - If internal node: recursively traverse children.
   - If leaf node: print all keys in left-to-right order using the linked list of leaves.

---

## Program:
```c
/*
Program to traverse the elements in a B+ Tree.
Developed by: SHAKTHI KUMAR S
RegisterNumber: 212222110043
*/

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define MAX 3

typedef struct BPlusTreeNode {
    int keys[MAX];
    struct BPlusTreeNode *children[MAX + 1];
    struct BPlusTreeNode *next;  // For leaf linking
    bool isLeaf;
    int n;
} BPlusTreeNode;

BPlusTreeNode* root = NULL;

// Create node
BPlusTreeNode* createNode(bool isLeaf) {
    BPlusTreeNode* node = (BPlusTreeNode*)malloc(sizeof(BPlusTreeNode));
    node->isLeaf = isLeaf;
    node->n = 0;
    node->next = NULL;
    for (int i = 0; i <= MAX; i++)
        node->children[i] = NULL;
    return node;
}

// Simple insert (for demo)
void simpleInsertLeaf(BPlusTreeNode* root, int key) {
    int i = root->n - 1;
    while (i >= 0 && root->keys[i] > key) {
        root->keys[i + 1] = root->keys[i];
        i--;
    }
    root->keys[i + 1] = key;
    root->n++;
}

// For demo: only handles insertion into a single root leaf
void insert(int key) {
    if (root == NULL) {
        root = createNode(true);
    }
    if (root->n < MAX) {
        simpleInsertLeaf(root, key);
    } else {
        printf("Node full. Full B+ Tree insert not implemented in this demo.\n");
    }
}

// Traverse B+ Tree by leaf nodes
void traverse(BPlusTreeNode* root) {
    if (!root) return;
    BPlusTreeNode* curr = root;
    while (!curr->isLeaf)
        curr = curr->children[0];

    printf("Traversal through leaf nodes:\n");
    while (curr) {
        for (int i = 0; i < curr->n; i++)
            printf("%d ", curr->keys[i]);
        curr = curr->next;
    }
    printf("\n");
}

// Main
int main() {
    insert(10);
    insert(20);
    insert(5);
    insert(15); // Won’t insert due to MAX = 3 in demo

    printf("B+ Tree leaf traversal:\n");
    traverse(root);
    return 0;
}

```

## Output:

![image](https://github.com/user-attachments/assets/c48bad05-6459-4c93-bde6-245df3bc9b58)


## Result:
Thus, the function to traverse the elements in a B+ Tree is implemented successfully.

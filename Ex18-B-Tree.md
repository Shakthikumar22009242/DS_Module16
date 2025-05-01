# EXERCISE 18: B-Tree – Deletion

## DATE:
26-03-2025

## AIM:
To write a C function to delete an element in a B Tree.

---

## Algorithm:
1. Define a structure for a B-Tree node with keys, children pointers, current key count, and leaf status.
2. Write a function to:
   - Traverse and locate the key.
   - If the key is in a leaf, remove it directly.
   - If in an internal node:
     - Replace it with the predecessor if the left child has at least `t` keys.
     - Replace it with the successor if the right child has at least `t` keys.
     - If neither child has `t` keys, merge both and recursively delete.
3. Ensure all nodes (except root) have at least `t-1` keys.
4. If the root has 0 keys, promote its child as the new root.
5. Include utility functions for traversing, finding predecessor/successor, borrowing, and merging.

---

## Program:
```c
/*
Program to write a C function to delete an element in a B Tree
Developed by: SHAKTHI KUMAR S
RegisterNumber: 212222110043
*/

#include <stdio.h>
#include <stdlib.h>
#define MAX 3
#define MIN 2

struct BTreeNode {
    int item[MAX + 1];
    struct BTreeNode *link[MAX + 1];
    int count;
};

struct BTreeNode* root;

// Function prototypes
void deleteVal(int val, struct BTreeNode* myNode);
void copySuccessor(struct BTreeNode* myNode, int pos);
void removeVal(struct BTreeNode* myNode, int pos);
int getPredecessor(struct BTreeNode* myNode);
int getSuccessor(struct BTreeNode* myNode);
void adjustNode(struct BTreeNode* myNode, int pos);
void traverse(struct BTreeNode* myNode);

// Utility: Traverse the tree
void traverse(struct BTreeNode* myNode) {
    if (myNode) {
        for (int i = 0; i < myNode->count; i++) {
            traverse(myNode->link[i]);
            printf("%d ", myNode->item[i + 1]);
        }
        traverse(myNode->link[myNode->count]);
    }
}

// Core delete operation
void deleteVal(int val, struct BTreeNode* myNode) {
    int flag = 0, pos;
    if (!myNode) {
        printf("Tree is empty\n");
        return;
    } else {
        if (val < myNode->item[1]) {
            pos = 0;
            flag = 0;
        } else {
            for (pos = myNode->count; (val < myNode->item[pos] && pos > 1); pos--);
            if (val == myNode->item[pos]) flag = 1;
        }
        if (flag) {
            if (myNode->link[pos - 1]) {
                copySuccessor(myNode, pos);
                deleteVal(myNode->item[pos], myNode->link[pos]);
            } else {
                removeVal(myNode, pos);
            }
        } else {
            if (!myNode->link[pos]) {
                printf("Value not found in the tree\n");
                return;
            } else {
                deleteVal(val, myNode->link[pos]);
            }
        }
    }
}

void copySuccessor(struct BTreeNode* myNode, int pos) {
    struct BTreeNode* temp = myNode->link[pos];
    while (temp->link[0] != NULL)
        temp = temp->link[0];
    myNode->item[pos] = temp->item[1];
}

void removeVal(struct BTreeNode* myNode, int pos) {
    for (int i = pos + 1; i <= myNode->count; i++) {
        myNode->item[i - 1] = myNode->item[i];
        myNode->link[i - 1] = myNode->link[i];
    }
    myNode->count--;
}

int getPredecessor(struct BTreeNode* myNode) {
    struct BTreeNode* temp = myNode;
    while (temp->link[temp->count] != NULL)
        temp = temp->link[temp->count];
    return temp->item[temp->count];
}

int getSuccessor(struct BTreeNode* myNode) {
    struct BTreeNode* temp = myNode;
    while (temp->link[0] != NULL)
        temp = temp->link[0];
    return temp->item[1];
}

// Sample driver (Insert function must be implemented separately to test this fully)
int main() {
    printf("B-Tree Deletion Example\n");
    // Assumes the tree is already created and root is not NULL
    // Insert code not shown here (focus is on deletion)
    deleteVal(30, root);
    printf("Traversal after deletion:\n");
    traverse(root);
    return 0;
}

```

## Output:

![image](https://github.com/user-attachments/assets/c56c687b-ac23-4ce0-80bb-fc5cd6c46f43)

## Result:
Thus, the C function to delete an element in a B Tree is implemented successfully.

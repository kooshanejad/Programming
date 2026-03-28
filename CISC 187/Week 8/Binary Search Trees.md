# Binary Search Trees
## Task 1
```
    1
     \
      5
     / \
    2   9
     \ / \
      4 6 10
     /   \
    3     8
```
## Task 2
If a well-balanced binary search tree (BST) contains 1,000 values, the maximum number of steps needed to search for a value is about 10. A balanced BST has a heigh close to log2(N). For 1,000 values: log2(1000) ≈ 9.97. So in the worst case, it would take about 10 steps to find a value.
## Task 3
```
findGreatest(root):
    current = root

    while current.right is not null:
        current = current.right

    return current.value
```
## Task 4
```cpp
#include <iostream>
using namespace std;

// Node structure for the BST
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

class BST {
private:
    Node* root;

    // Recursive insert function
    Node* insert(Node* node, int value) {
        // If current position is empty, create new node
        if (node == nullptr) {
            return new Node(value);
        }

        // Insert into left subtree if value is smaller
        if (value < node->data) {
            node->left = insert(node->left, value);
        }
        // Insert into right subtree if value is larger
        else if (value > node->data) {
            node->right = insert(node->right, value);
        }

        return node;
    }

    // Inorder traversal (prints values in sorted order)
    void inorder(Node* node) {
        if (node != nullptr) {
            inorder(node->left);
            cout << node->data << " ";
            inorder(node->right);
        }
    }

public:
    // Constructor initializes empty tree
    BST() {
        root = nullptr;
    }

    // Public insert function
    void insert(int value) {
        root = insert(root, value);
    }

    // Display tree using inorder traversal
    void displayInorder() {
        inorder(root);
        cout << endl;
    }
};

int main() {
    BST tree;

    // Values to insert into the BST
    int values[] = {1, 5, 9, 2, 4, 10, 6, 3, 8};
    int size = sizeof(values) / sizeof(values[0]);

    // Insert each value into the tree
    for (int i = 0; i < size; i++) {
        tree.insert(values[i]);
    }

    // Output the sorted result
    cout << "Inorder traversal of the BST: ";
    tree.displayInorder();

    return 0;
}
```

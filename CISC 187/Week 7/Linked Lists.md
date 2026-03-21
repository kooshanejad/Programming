# Linked Lists

## File 1: stack.h
```cpp
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node* next;
};

class Stack
{
private:
    Node* top;

public:
    Stack();

    void push(int value);
    void pop();
    int peek();
    bool isEmpty();
    void display();
};

#endif
```

## File 2: stack.cpp
```cpp
#include "stack.h"

// Constructor
Stack::Stack()
{
    top = nullptr;
}

// push()
void Stack::push(int value)
{
    Node* newNode = new Node;
    newNode->data = value;
    newNode->next = top;
    top = newNode;
}

// pop()
void Stack::pop()
{
    if (isEmpty())
    {
        cout << "Stack Underflow" << endl;
        return;
    }

    Node* temp = top;
    top = top->next;
    delete temp;
}

// peek()
int Stack::peek()
{
    if (isEmpty())
    {
        cout << "Stack is empty" << endl;
        return -1;
    }

    return top->data;
}

// isEmpty()
bool Stack::isEmpty()
{
    return (top == nullptr);
}

// display()
void Stack::display()
{
    cout << "Stack elements:" << endl;

    Node* temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << endl;
        temp = temp->next;
    }
}
```

## File 3: main.cpp
```cpp
#include "stack.h"

int main()
{
    Stack s;

    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);

    s.display();

    s.pop();

    cout << "Top element: " << s.peek() << endl;

    s.display();

    return 0;
}
```

## File 4: README.md

### 1. Why is a linked list efficient for stack implementation?
A linked list is efficient because insertions and deletions at the top of the stack can be done in constant time O(1) without shifting elements or resizing memory.

### 2. What is the time complexity of push and pop operations?
Both push and pop operations have a time complexity of O(1).

### 3. What happens if memory is not deallocated after pop?
If memory is not deallocated, it causes a memory leak, meaning unused memory is not returned to the system.

### 4. Compare a stack implemented with an array versus a linked list.
An array-based stack has a fixed size and may require resizing, while a linked list stack is dynamic and can grow as needed. However, arrays allow faster access, while linked lists require more memory due to pointers.

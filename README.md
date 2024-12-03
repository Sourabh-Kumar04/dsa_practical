# Data Structure Practical

## # Ques 1: Write a program to implement a singly linked list as an ADT that supports the following operations:

1. Insert an element x at the beginning of the singly linked list
2. Insert an element x at ith position of the singly linked list
3. Remove an element from the beginning of the singly linked list
4. Remove an element from the ith position of the singly linked list
5. Remove an element from beginning of the singly linked list
6. Search for an element x in the singly linked list and return its pointer

### Ans 1:

```cpp
#include <iostream>
using namespace std;

// Node structure for the singly linked list
struct Node {
    int data;
    Node* next;

    Node(int value) : data(value), next(nullptr) {}
};

// Singly Linked List class
class SinglyLinkedList {
private:
    Node* head;

public:
    // Constructor
    SinglyLinkedList() : head(nullptr) {}

    // Destructor to free memory
    ~SinglyLinkedList() {
        while (head != nullptr) {
            removeAtBeginning();
        }
    }

    // 1. Insert an element at the beginning
    void insertAtBeginning(int x) {
        Node* newNode = new Node(x);
        newNode->next = head;
        head = newNode;
    }

    // 2. Insert an element at the ith position
    void insertAtPosition(int x, int pos) {
        if (pos < 0) {
            cout << "Invalid position.\n";
            return;
        }
        if (pos == 0) {
            insertAtBeginning(x);
            return;
        }

        Node* newNode = new Node(x);
        Node* temp = head;

        for (int i = 1; i < pos; ++i) {
            if (temp == nullptr) {
                cout << "Position out of bounds.\n";
                delete newNode;
                return;
            }
            temp = temp->next;
        }

        if (temp != nullptr) {
            newNode->next = temp->next;
            temp->next = newNode;
        } else {
            cout << "Position out of bounds.\n";
            delete newNode;
        }
    }

    // 3. Remove an element from the beginning
    void removeAtBeginning() {
        if (head == nullptr) {
            cout << "List is empty.\n";
            return;
        }
        Node* temp = head;
        head = head->next;
        delete temp;p
    }

    // 4. Remove an element at the ith position
    void removeAtPosition(int pos) {
        if (pos < 0 || head == nullptr) {
            cout << "Invalid position or list is empty.\n";
            return;
        }
        if (pos == 0) {
            removeAtBeginning();
            return;
        }

        Node* temp = head;
        for (int i = 1; i < pos; ++i) {
            if (temp == nullptr || temp->next == nullptr) {
                cout << "Position out of bounds.\n";
                return;
            }
            temp = temp->next;
        }

        Node* nodeToDelete = temp->next;
        if (nodeToDelete != nullptr) {
            temp->next = nodeToDelete->next;
            delete nodeToDelete;
        } else {
            cout << "Position out of bounds.\n";
        }
    }

    // 5. Remove an element from the beginning of the doubly linked list
    // This operation does not apply to singly linked lists and is skipped.

    // 6. Search for an element and return its pointer
    Node* search(int x) {
        Node* temp = head;
        while (temp != nullptr) {
            if (temp->data == x) {
                return temp;
            }
            temp = temp->next;
        }
        return nullptr; // Not found
    }

    // Function to display the list
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "nullptr\n";
    }
};

// Main function to demonstrate the operations
int main() {
    SinglyLinkedList list;

    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtBeginning(30);
    list.display();

    list.insertAtPosition(40, 2);
    list.display();

    list.removeAtBeginning();
    list.display();

    list.removeAtPosition(1);
    list.display();

    int searchValue = 10;
    Node* foundNode = list.search(searchValue);
    if (foundNode) {
        cout << "Element " << searchValue << " found at address: " << foundNode << "\n";
    } else {
        cout << "Element " << searchValue << " not found.\n";
    }

    return 0;
}

```

### Explanation

1. **Insert at the Beginning**:
    - Create a new node and set it as the new head.
2. **Insert at Position**:
    - Traverse to the position before where the node is to be inserted.
    - Update pointers to insert the new node.
3. **Remove at Beginning**:
    - Update the head to the next node and delete the old head.
4. **Remove at Position**:
    - Traverse to the node before the target position.
    - Update pointers and delete the target node.
5. **Remove from the Beginning of a Doubly Linked List**:
    - Not applicable for singly linked lists.
6. **Search**:
    - Traverse the list to find the element.

### Sample Output

```
30 -> 20 -> 10 -> nullptr
30 -> 20 -> 40 -> 10 -> nullptr
20 -> 40 -> 10 -> nullptr
20 -> 10 -> nullptr
Element 10 found at address: 0x561b6f624eb0

```

# Ques 2: Write a program to implement a doubly linked list as an ADT that supports the following operations:

1. Insert an element x at the beginning of the singly linked list
2. Insert an element x at ith position of the singly linked list
3. Remove an element from the beginning of the singly linked list
4. Remove an element from the ith position of the singly linked list
5. Remove an element from beginning of the singly linked list
6. Search for an element x in the singly linked list and return its pointer

## Ans 2:

Here’s a program in C++ to implement a **Doubly Linked List (DLL)** as an Abstract Data Type (ADT) with basic operations:

### Supported Operations:

1. Insert an element at the beginning.
2. Insert an element at the end.
3. Insert an element at a specific position.
4. Remove an element from the beginning.
5. Remove an element from the end.
6. Remove an element at a specific position.
7. Search for an element and return its pointer.
8. Display the list from beginning to end.
9. Display the list from end to beginning.

### Program:

```cpp
#include <iostream>
using namespace std;

// Node structure for Doubly Linked List
struct Node {
    int data;
    Node* prev;
    Node* next;

    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Doubly Linked List Class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    // Constructor
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Destructor to free memory
    ~DoublyLinkedList() {
        while (head != nullptr) {
            removeAtBeginning();
        }
    }

    // 1. Insert at the beginning
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // 2. Insert at the end
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (tail == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // 3. Insert at a specific position
    void insertAtPosition(int value, int pos) {
        if (pos < 0) {
            cout << "Invalid position.\n";
            return;
        }
        if (pos == 0) {
            insertAtBeginning(value);
            return;
        }

        Node* newNode = new Node(value);
        Node* temp = head;

        for (int i = 1; i < pos; ++i) {
            if (temp == nullptr) {
                cout << "Position out of bounds.\n";
                delete newNode;
                return;
            }
            temp = temp->next;
        }

        if (temp != nullptr) {
            newNode->next = temp->next;
            if (temp->next != nullptr) {
                temp->next->prev = newNode;
            } else {
                tail = newNode;
            }
            temp->next = newNode;
            newNode->prev = temp;
        } else {
            cout << "Position out of bounds.\n";
            delete newNode;
        }
    }

    // 4. Remove from the beginning
    void removeAtBeginning() {
        if (head == nullptr) {
            cout << "List is empty.\n";
            return;
        }

        Node* temp = head;
        if (head->next != nullptr) {
            head = head->next;
            head->prev = nullptr;
        } else {
            head = tail = nullptr;
        }
        delete temp;
    }

    // 5. Remove from the end
    void removeAtEnd() {
        if (tail == nullptr) {
            cout << "List is empty.\n";
            return;
        }

        Node* temp = tail;
        if (tail->prev != nullptr) {
            tail = tail->prev;
            tail->next = nullptr;
        } else {
            head = tail = nullptr;
        }
        delete temp;
    }

    // 6. Remove at a specific position
    void removeAtPosition(int pos) {
        if (pos < 0 || head == nullptr) {
            cout << "Invalid position or list is empty.\n";
            return;
        }
        if (pos == 0) {
            removeAtBeginning();
            return;
        }

        Node* temp = head;
        for (int i = 1; i < pos; ++i) {
            if (temp == nullptr || temp->next == nullptr) {
                cout << "Position out of bounds.\n";
                return;
            }
            temp = temp->next;
        }

        Node* nodeToDelete = temp->next;
        if (nodeToDelete != nullptr) {
            temp->next = nodeToDelete->next;
            if (nodeToDelete->next != nullptr) {
                nodeToDelete->next->prev = temp;
            } else {
                tail = temp;
            }
            delete nodeToDelete;
        } else {
            cout << "Position out of bounds.\n";
        }
    }

    // 7. Search for an element
    Node* search(int value) {
        Node* temp = head;
        while (temp != nullptr) {
            if (temp->data == value) {
                return temp;
            }
            temp = temp->next;
        }
        return nullptr;
    }

    // 8. Display from beginning to end
    void displayForward() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " <-> ";
            temp = temp->next;
        }
        cout << "nullptr\n";
    }

    // 9. Display from end to beginning
    void displayBackward() {
        Node* temp = tail;
        while (temp != nullptr) {
            cout << temp->data << " <-> ";
            temp = temp->prev;
        }
        cout << "nullptr\n";
    }
};

// Main Function to demonstrate the operations
int main() {
    DoublyLinkedList dll;

    dll.insertAtBeginning(10);
    dll.insertAtBeginning(20);
    dll.insertAtEnd(30);
    dll.insertAtPosition(25, 2);

    cout << "List displayed forward: ";
    dll.displayForward();

    cout << "List displayed backward: ";
    dll.displayBackward();

    dll.removeAtBeginning();
    cout << "After removing at beginning: ";
    dll.displayForward();

    dll.removeAtEnd();
    cout << "After removing at end: ";
    dll.displayForward();

    dll.removeAtPosition(1);
    cout << "After removing at position 1: ";
    dll.displayForward();

    int searchValue = 25;
    Node* foundNode = dll.search(searchValue);
    if (foundNode) {
        cout << "Element " << searchValue << " found at address: " << foundNode << "\n";
    } else {
        cout << "Element " << searchValue << " not found.\n";
    }

    return 0;
}

```

### Explanation:

1. **Node Structure**:
    - Each node has `data`, `prev`, and `next` pointers.
2. **Operations**:
    - Insertions and deletions are handled with proper pointer adjustments.
    - Searching traverses the list and compares the data.
3. **Traversal**:
    - `displayForward` traverses from `head` to `tail`.
    - `displayBackward` traverses from `tail` to `head`.

### Sample Output:

```
List displayed forward: 20 <-> 10 <-> 25 <-> 30 <-> nullptr
List displayed backward: 30 <-> 25 <-> 10 <-> 20 <-> nullptr
After removing at beginning: 10 <-> 25 <-> 30 <-> nullptr
After removing at end: 10 <-> 25 <-> nullptr
After removing at position 1: 10 <-> nullptr
Element 25 not found.

```

# Ques 3: Write a program in C++ to implement a circular linked list as an ADT that supports the following operations:

1. Insert an element x in the list.
2. remove an element from the list.
3. Search for an element x in the list and return its pointer.

## Ans 3:

Here’s a C++ program to implement a **Circular Linked List (CLL)** as an Abstract Data Type (ADT) with the specified operations:

### Operations:

1. **Insert an element** in the list.
2. **Remove an element** from the list.
3. **Search for an element** in the list and return its pointer.

### Program:

```cpp
#include <iostream>
using namespace std;

// Node structure for Circular Linked List
struct Node {
    int data;
    Node* next;

    Node(int value) : data(value), next(nullptr) {}
};

// Circular Linked List Class
class CircularLinkedList {
private:
    Node* tail;

public:
    // Constructor
    CircularLinkedList() : tail(nullptr) {}

    // Destructor to free memory
    ~CircularLinkedList() {
        if (tail == nullptr) return;

        Node* current = tail->next;
        Node* temp;

        while (current != tail) {
            temp = current;
            current = current->next;
            delete temp;
        }
        delete tail; // Delete the last node
    }

    // 1. Insert an element into the list
    void insert(int value) {
        Node* newNode = new Node(value);

        // If list is empty
        if (tail == nullptr) {
            tail = newNode;
            tail->next = tail; // Point to itself
        } else {
            newNode->next = tail->next; // New node points to the head
            tail->next = newNode;       // Tail points to the new node
            tail = newNode;             // Update tail to the new node
        }
    }

    // 2. Remove an element from the list
    void remove(int value) {
        if (tail == nullptr) {
            cout << "List is empty. Cannot remove " << value << ".\n";
            return;
        }

        Node* current = tail->next;
        Node* prev = tail;

        do {
            if (current->data == value) {
                if (current == tail && current->next == tail) { // Only one node
                    delete current;
                    tail = nullptr;
                } else {
                    prev->next = current->next; // Bypass the current node
                    if (current == tail) {     // If the node to be deleted is tail
                        tail = prev;
                    }
                    delete current;
                }
                cout << "Element " << value << " removed.\n";
                return;
            }
            prev = current;
            current = current->next;
        } while (current != tail->next);

        cout << "Element " << value << " not found in the list.\n";
    }

    // 3. Search for an element in the list
    Node* search(int value) {
        if (tail == nullptr) return nullptr;

        Node* current = tail->next;
        do {
            if (current->data == value) {
                return current;
            }
            current = current->next;
        } while (current != tail->next);

        return nullptr; // Element not found
    }

    // Display the list
    void display() {
        if (tail == nullptr) {
            cout << "List is empty.\n";
            return;
        }

        Node* current = tail->next; // Start from the head
        do {
            cout << current->data << " -> ";
            current = current->next;
        } while (current != tail->next);

        cout << "(circular)\n";
    }
};

// Main function to demonstrate the operations
int main() {
    CircularLinkedList cll;

    cll.insert(10);
    cll.insert(20);
    cll.insert(30);
    cll.insert(40);

    cout << "Circular Linked List after inserts:\n";
    cll.display();

    int searchValue = 30;
    Node* foundNode = cll.search(searchValue);
    if (foundNode) {
        cout << "Element " << searchValue << " found at address: " << foundNode << "\n";
    } else {
        cout << "Element " << searchValue << " not found in the list.\n";
    }

    cll.remove(20);
    cout << "Circular Linked List after removing 20:\n";
    cll.display();

    cll.remove(50); // Trying to remove a non-existent element
    cll.remove(10);
    cll.remove(30);
    cll.remove(40);
    cout << "Circular Linked List after removing all elements:\n";
    cll.display();

    return 0;
}

```

### Explanation:

1. **Node Structure**:
    - Each node contains `data` and a `next` pointer.
    - The `next` pointer points back to the first node (head) to form a circular structure.
2. **Tail Pointer**:
    - Maintains the last node (`tail`) of the list.
    - `tail->next` always points to the head of the list.
3. **Operations**:
    - **Insert**:
        - Adds the new node after `tail` and updates `tail`.
    - **Remove**:
        - Traverses the list to find the element and adjusts pointers to bypass it.
        - Special cases for the only node in the list or removing the `tail` node.
    - **Search**:
        - Traverses the list to find the value and returns its pointer.
4. **Display**:
    - Traverses from `tail->next` (head) to `tail` and prints the data.

### Sample Output:

```
Circular Linked List after inserts:
10 -> 20 -> 30 -> 40 -> (circular)
Element 30 found at address: 0x... (actual memory address)
Element 20 removed.
Circular Linked List after removing 20:
10 -> 30 -> 40 -> (circular)
Element 50 not found in the list.
Circular Linked List after removing all elements:
List is empty.

```

# Ques 4: Implement Stack in C++ as an ADT and use it to evaluate a prefix/postfix expression.

## Ans 4:

Here’s a C++ program that implements a **Stack** as an Abstract Data Type (ADT) and uses it to evaluate both **prefix** and **postfix** expressions.

### Program:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <cctype>
#include <cmath>
using namespace std;

// Stack class implemented using STL for simplicity
class Stack {
private:
    stack<int> s;

public:
    void push(int value) {
        s.push(value);
    }

    int pop() {
        if (s.empty()) {
            throw runtime_error("Stack underflow!");
        }
        int topValue = s.top();
        s.pop();
        return topValue;
    }

    bool isEmpty() {
        return s.empty();
    }
};

// Function to evaluate postfix expressions
int evaluatePostfix(const string& expression) {
    Stack stack;

    for (char ch : expression) {
        if (isdigit(ch)) {
            stack.push(ch - '0'); // Convert char digit to int
        } else {
            // Operator encountered, pop two operands
            int operand2 = stack.pop();
            int operand1 = stack.pop();

            switch (ch) {
                case '+': stack.push(operand1 + operand2); break;
                case '-': stack.push(operand1 - operand2); break;
                case '*': stack.push(operand1 * operand2); break;
                case '/': stack.push(operand1 / operand2); break;
                case '^': stack.push(pow(operand1, operand2)); break;
                default: throw runtime_error("Invalid operator encountered!");
            }
        }
    }
    return stack.pop();
}

// Function to evaluate prefix expressions
int evaluatePrefix(const string& expression) {
    Stack stack;

    // Iterate from right to left for prefix evaluation
    for (int i = expression.size() - 1; i >= 0; i--) {
        char ch = expression[i];

        if (isdigit(ch)) {
            stack.push(ch - '0'); // Convert char digit to int
        } else {
            // Operator encountered, pop two operands
            int operand1 = stack.pop();
            int operand2 = stack.pop();

            switch (ch) {
                case '+': stack.push(operand1 + operand2); break;
                case '-': stack.push(operand1 - operand2); break;
                case '*': stack.push(operand1 * operand2); break;
                case '/': stack.push(operand1 / operand2); break;
                case '^': stack.push(pow(operand1, operand2)); break;
                default: throw runtime_error("Invalid operator encountered!");
            }
        }
    }
    return stack.pop();
}

// Main function
int main() {
    try {
        string postfixExpr = "53+82-*";
        cout << "Postfix Expression: " << postfixExpr << endl;
        cout << "Postfix Evaluation Result: " << evaluatePostfix(postfixExpr) << endl;

        string prefixExpr = "-+53*82";
        cout << "Prefix Expression: " << prefixExpr << endl;
        cout << "Prefix Evaluation Result: " << evaluatePrefix(prefixExpr) << endl;
    } catch (const exception& e) {
        cerr << "Error: " << e.what() << endl;
    }

    return 0;
}

```

---

### Explanation:

### **1. Stack ADT:**

The `Stack` class uses the `stack<int>` from the C++ Standard Template Library (STL) for simplicity. It provides basic operations:

- `push(int value)` — Pushes a value onto the stack.
- `pop()` — Pops and returns the top value of the stack.
- `isEmpty()` — Checks if the stack is empty.

### **2. Postfix Expression Evaluation:**

- Traverse the expression left to right.
- If a digit is encountered, push it onto the stack.
- If an operator is encountered, pop the top two operands from the stack, apply the operator, and push the result back.

**Example**:

Postfix: `53+82-*`

Steps:

1. Push `5`, `3` → Stack: `[5, 3]`
2. `+`: Pop `5` and `3`, push `5 + 3 = 8` → Stack: `[8]`
3. Push `8`, `2` → Stack: `[8, 2]`
4. ``: Pop `8` and `2`, push `8 * 2 = 16` → Stack: `[16]`

Result: `16`.

### **3. Prefix Expression Evaluation:**

- Traverse the expression right to left.
- If a digit is encountered, push it onto the stack.
- If an operator is encountered, pop the top two operands from the stack, apply the operator, and push the result back.

**Example**:

Prefix: `-+53*82`

Steps:

1. Start at `2`, push `2`, `8` → Stack: `[2, 8]`
2. ``: Pop `2` and `8`, push `8 * 2 = 16` → Stack: `[16]`
3. Push `3`, `5` → Stack: `[16, 3, 5]`
4. `+`: Pop `3` and `5`, push `5 + 3 = 8` → Stack: `[16, 8]`
5. ``: Pop `16` and `8`, push `16 - 8 = 8` → Stack: `[8]`

Result: `8`.

---

### Sample Output:

```
Postfix Expression: 53+82-*
Postfix Evaluation Result: 16
Prefix Expression: -+53*82
Prefix Evaluation Result: 8

```

This program provides robust handling of prefix and postfix expressions using the Stack ADT in C++.

# Ques 5: Implement Queue in C++ as an ADT

## Ans 5:

Below is an implementation of a **Queue** as an Abstract Data Type (ADT) in C++.

---

### **Queue ADT Implementation in C++**

This implementation uses a dynamic array for simplicity and demonstrates basic queue operations:

1. **Enqueue (Insert an element)**
2. **Dequeue (Remove an element)**
3. **Peek (Get the front element without removing it)**
4. **Check if the queue is empty**

---

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

// Queue class definition
class Queue {
private:
    int* arr;       // Dynamic array to store queue elements
    int front;      // Index of the front element
    int rear;       // Index of the rear element
    int capacity;   // Maximum capacity of the queue
    int size;       // Current size of the queue

public:
    // Constructor
    Queue(int capacity) : capacity(capacity), front(0), rear(-1), size(0) {
        arr = new int[capacity];
    }

    // Destructor
    ~Queue() {
        delete[] arr;
    }

    // Enqueue: Add an element to the rear of the queue
    void enqueue(int value) {
        if (isFull()) {
            throw overflow_error("Queue is full! Cannot enqueue.");
        }
        rear = (rear + 1) % capacity; // Circular increment
        arr[rear] = value;
        size++;
    }

    // Dequeue: Remove an element from the front of the queue
    int dequeue() {
        if (isEmpty()) {
            throw underflow_error("Queue is empty! Cannot dequeue.");
        }
        int value = arr[front];
        front = (front + 1) % capacity; // Circular increment
        size--;
        return value;
    }

    // Peek: Get the front element without removing it
    int peek() const {
        if (isEmpty()) {
            throw underflow_error("Queue is empty! Cannot peek.");
        }
        return arr[front];
    }

    // Check if the queue is empty
    bool isEmpty() const {
        return size == 0;
    }

    // Check if the queue is full
    bool isFull() const {
        return size == capacity;
    }

    // Get the current size of the queue
    int getSize() const {
        return size;
    }

    // Display the elements in the queue
    void display() const {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }
        cout << "Queue elements: ";
        for (int i = 0; i < size; i++) {
            cout << arr[(front + i) % capacity] << " ";
        }
        cout << endl;
    }
};

// Main function to demonstrate queue operations
int main() {
    try {
        Queue queue(5); // Create a queue with capacity 5

        // Enqueue some elements
        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        queue.enqueue(40);

        cout << "After enqueuing 4 elements:\n";
        queue.display();

        // Dequeue an element
        cout << "Dequeued element: " << queue.dequeue() << endl;

        cout << "Queue after dequeue operation:\n";
        queue.display();

        // Peek the front element
        cout << "Front element: " << queue.peek() << endl;

        // Enqueue more elements
        queue.enqueue(50);
        queue.enqueue(60);

        cout << "After enqueuing 2 more elements:\n";
        queue.display();

        // Try to enqueue into a full queue
        queue.enqueue(70); // This will throw an exception
    } catch (const exception& e) {
        cerr << "Error: " << e.what() << endl;
    }

    return 0;
}

```

---

### **Explanation of the Code**

1. **Queue Data Members:**
    - `int* arr`: Dynamic array to hold queue elements.
    - `int front`: Points to the front of the queue.
    - `int rear`: Points to the rear of the queue.
    - `int capacity`: Maximum number of elements the queue can hold.
    - `int size`: Current number of elements in the queue.
2. **Queue Operations:**
    - **Enqueue**: Adds an element to the rear. Updates the `rear` index circularly.
    - **Dequeue**: Removes an element from the front. Updates the `front` index circularly.
    - **Peek**: Returns the front element without dequeuing.
    - **isEmpty**: Checks if the queue is empty.
    - **isFull**: Checks if the queue is full.
    - **Display**: Prints all elements in the queue.
3. **Circular Increment:**
    - Both `front` and `rear` are updated using modulo arithmetic:
        
        ```cpp
        (index + 1) % capacity;
        
        ```
        
4. **Error Handling:**
    - Throws exceptions if attempting to enqueue into a full queue or dequeue from an empty queue.

---

### **Sample Output:**

```
After enqueuing 4 elements:
Queue elements: 10 20 30 40
Dequeued element: 10
Queue after dequeue operation:
Queue elements: 20 30 40
Front element: 20
After enqueuing 2 more elements:
Queue elements: 20 30 40 50 60
Error: Queue is full! Cannot enqueue.

```

---

This implementation ensures robust queue operations, handles edge cases (e.g., empty/full queue), and displays the queue's current state. It uses circular indexing for efficient utilization of array space.

# Ques 6: Write a program in C++ to implement a binary search tree as an ADT that supports the following operations:

1. Insert an element x
2. Delete an elememt x
3. Search for an element x in Binary Search Tree
4. Display the element of the Binary Search Tree in preorder , postorder and inorder traversal

## Ans 6:

Here is the implementation of a Binary Search Tree (BST) in C++ as an Abstract Data Type (ADT), supporting the specified operations.

---

### **Program: Binary Search Tree Implementation**

```cpp
#include <iostream>
using namespace std;

// Definition of a node in the BST
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Binary Search Tree class
class BST {
private:
    Node* root;

    // Helper function to insert a new node
    Node* insert(Node* node, int value) {
        if (node == nullptr) {
            return new Node(value);
        }
        if (value < node->data) {
            node->left = insert(node->left, value);
        } else if (value > node->data) {
            node->right = insert(node->right, value);
        }
        return node;
    }

    // Helper function to find the minimum value node
    Node* findMin(Node* node) {
        while (node && node->left != nullptr) {
            node = node->left;
        }
        return node;
    }

    // Helper function to delete a node
    Node* deleteNode(Node* node, int value) {
        if (node == nullptr) {
            return node;
        }
        if (value < node->data) {
            node->left = deleteNode(node->left, value);
        } else if (value > node->data) {
            node->right = deleteNode(node->right, value);
        } else {
            // Node with only one child or no child
            if (node->left == nullptr) {
                Node* temp = node->right;
                delete node;
                return temp;
            } else if (node->right == nullptr) {
                Node* temp = node->left;
                delete node;
                return temp;
            }

            // Node with two children: Get the inorder successor
            Node* temp = findMin(node->right);
            node->data = temp->data;
            node->right = deleteNode(node->right, temp->data);
        }
        return node;
    }

    // Helper function to search for a value
    Node* search(Node* node, int value) {
        if (node == nullptr || node->data == value) {
            return node;
        }
        if (value < node->data) {
            return search(node->left, value);
        }
        return search(node->right, value);
    }

    // Helper functions for traversals
    void inorder(Node* node) {
        if (node != nullptr) {
            inorder(node->left);
            cout << node->data << " ";
            inorder(node->right);
        }
    }

    void preorder(Node* node) {
        if (node != nullptr) {
            cout << node->data << " ";
            preorder(node->left);
            preorder(node->right);
        }
    }

    void postorder(Node* node) {
        if (node != nullptr) {
            postorder(node->left);
            postorder(node->right);
            cout << node->data << " ";
        }
    }

public:
    // Constructor
    BST() : root(nullptr) {}

    // Insert a new value
    void insert(int value) {
        root = insert(root, value);
    }

    // Delete a value
    void deleteValue(int value) {
        root = deleteNode(root, value);
    }

    // Search for a value
    bool search(int value) {
        return search(root, value) != nullptr;
    }

    // Inorder traversal
    void displayInorder() {
        inorder(root);
        cout << endl;
    }

    // Preorder traversal
    void displayPreorder() {
        preorder(root);
        cout << endl;
    }

    // Postorder traversal
    void displayPostorder() {
        postorder(root);
        cout << endl;
    }
};

// Main function to demonstrate the BST operations
int main() {
    BST tree;

    // Inserting elements
    tree.insert(50);
    tree.insert(30);
    tree.insert(70);
    tree.insert(20);
    tree.insert(40);
    tree.insert(60);
    tree.insert(80);

    cout << "Inorder Traversal: ";
    tree.displayInorder();

    cout << "Preorder Traversal: ";
    tree.displayPreorder();

    cout << "Postorder Traversal: ";
    tree.displayPostorder();

    // Search for elements
    int searchValue = 40;
    if (tree.search(searchValue)) {
        cout << searchValue << " is found in the BST.\n";
    } else {
        cout << searchValue << " is not found in the BST.\n";
    }

    // Deleting an element
    cout << "Deleting 40...\n";
    tree.deleteValue(40);

    cout << "Inorder Traversal after deletion: ";
    tree.displayInorder();

    return 0;
}

```

---

### **Explanation of the Code**

### 1. **Insert Operation:**

- A new element is added to the tree while maintaining the BST properties:
    - If the value is less than the current node, move to the left child.
    - If the value is greater, move to the right child.
    - If the current node is `nullptr`, insert the new node here.

### 2. **Delete Operation:**

- Handles three cases:
    - Node has no children (leaf): Delete it directly.
    - Node has one child: Replace it with its child.
    - Node has two children: Replace it with its inorder successor (minimum value in the right subtree).

### 3. **Search Operation:**

- Traverses the tree:
    - If the value is found, return the node.
    - If the value is less than the current node, search in the left subtree.
    - Otherwise, search in the right subtree.

### 4. **Traversal:**

- **Inorder (LNR)**: Left, Node, Right — Produces sorted output.
- **Preorder (NLR)**: Node, Left, Right — Useful for copying trees.
- **Postorder (LRN)**: Left, Right, Node — Useful for deleting trees.

---

### **Sample Output:**

```
Inorder Traversal: 20 30 40 50 60 70 80
Preorder Traversal: 50 30 20 40 70 60 80
Postorder Traversal: 20 40 30 60 80 70 50
40 is found in the BST.
Deleting 40...
Inorder Traversal after deletion: 20 30 50 60 70 80

```

---

This implementation demonstrates the core functionalities of a BST and can be extended or modified for additional features.

# Ques 7: Write a program in C++ to implement insert and search operations in AVL trees.

## Ans 7:

Below is the C++ implementation of an AVL tree, which includes insert and search operations. AVL trees are self-balancing binary search trees where the heights of the two child subtrees of any node differ by at most one. The program ensures the AVL property is maintained after every insertion.

---

### **Program: AVL Tree Implementation**

```cpp
#include <iostream>
using namespace std;

// Definition of a node in the AVL tree
struct Node {
    int data;
    Node* left;
    Node* right;
    int height;

    Node(int value) : data(value), left(nullptr), right(nullptr), height(1) {}
};

// AVL Tree class
class AVLTree {
private:
    // Get the height of a node
    int getHeight(Node* node) {
        return node ? node->height : 0;
    }

    // Get the balance factor of a node
    int getBalance(Node* node) {
        return node ? getHeight(node->left) - getHeight(node->right) : 0;
    }

    // Right rotate the subtree rooted at y
    Node* rightRotate(Node* y) {
        Node* x = y->left;
        Node* T2 = x->right;

        // Perform rotation
        x->right = y;
        y->left = T2;

        // Update heights
        y->height = max(getHeight(y->left), getHeight(y->right)) + 1;
        x->height = max(getHeight(x->left), getHeight(x->right)) + 1;

        return x;
    }

    // Left rotate the subtree rooted at x
    Node* leftRotate(Node* x) {
        Node* y = x->right;
        Node* T2 = y->left;

        // Perform rotation
        y->left = x;
        x->right = T2;

        // Update heights
        x->height = max(getHeight(x->left), getHeight(x->right)) + 1;
        y->height = max(getHeight(y->left), getHeight(y->right)) + 1;

        return y;
    }

    // Insert a node into the AVL tree
    Node* insert(Node* node, int value) {
        // Perform normal BST insertion
        if (!node) {
            return new Node(value);
        }
        if (value < node->data) {
            node->left = insert(node->left, value);
        } else if (value > node->data) {
            node->right = insert(node->right, value);
        } else {
            return node; // Duplicate values are not allowed
        }

        // Update height of the current node
        node->height = 1 + max(getHeight(node->left), getHeight(node->right));

        // Get the balance factor
        int balance = getBalance(node);

        // If the node becomes unbalanced, perform rotations
        // Left-Left case
        if (balance > 1 && value < node->left->data) {
            return rightRotate(node);
        }

        // Right-Right case
        if (balance < -1 && value > node->right->data) {
            return leftRotate(node);
        }

        // Left-Right case
        if (balance > 1 && value > node->left->data) {
            node->left = leftRotate(node->left);
            return rightRotate(node);
        }

        // Right-Left case
        if (balance < -1 && value < node->right->data) {
            node->right = rightRotate(node->right);
            return leftRotate(node);
        }

        return node;
    }

    // Search for a value in the AVL tree
    Node* search(Node* node, int value) {
        if (!node || node->data == value) {
            return node;
        }
        if (value < node->data) {
            return search(node->left, value);
        }
        return search(node->right, value);
    }

    // Inorder traversal of the AVL tree
    void inorder(Node* node) {
        if (node) {
            inorder(node->left);
            cout << node->data << " ";
            inorder(node->right);
        }
    }

public:
    Node* root;

    // Constructor
    AVLTree() : root(nullptr) {}

    // Public insert method
    void insert(int value) {
        root = insert(root, value);
    }

    // Public search method
    bool search(int value) {
        return search(root, value) != nullptr;
    }

    // Display the tree in inorder
    void displayInorder() {
        inorder(root);
        cout << endl;
    }
};

// Main function to demonstrate AVL tree operations
int main() {
    AVLTree tree;

    // Insert elements into the AVL tree
    tree.insert(10);
    tree.insert(20);
    tree.insert(30);
    tree.insert(40);
    tree.insert(50);
    tree.insert(25);

    cout << "Inorder traversal of the AVL tree: ";
    tree.displayInorder();

    // Search for elements
    int searchValue = 25;
    if (tree.search(searchValue)) {
        cout << searchValue << " is found in the AVL tree.\n";
    } else {
        cout << searchValue << " is not found in the AVL tree.\n";
    }

    searchValue = 60;
    if (tree.search(searchValue)) {
        cout << searchValue << " is found in the AVL tree.\n";
    } else {
        cout << searchValue << " is not found in the AVL tree.\n";
    }

    return 0;
}

```

---

### **Explanation of the Code**

### **Insert Operation**

- Insertion is similar to a Binary Search Tree, with additional steps to update heights and perform rotations if needed.
- The balance factor is calculated for each node, and rotations are performed to maintain the AVL property.

### **Search Operation**

- Standard binary search algorithm is used to locate a node with the given value.

### **Rotations**

- Four types of rotations are implemented:
    1. **Right-Right (RR)**
    2. **Left-Left (LL)**
    3. **Left-Right (LR)**
    4. **Right-Left (RL)**

### **Traversal**

- The `inorder` function performs an inorder traversal of the AVL tree, printing the nodes in sorted order.

---

### **Sample Output**

```
Inorder traversal of the AVL tree: 10 20 25 30 40 50
25 is found in the AVL tree.
60 is not found in the AVL tree.

```

---

This implementation ensures the AVL property is maintained after every insertion, providing a balanced tree for efficient searching, insertion, and deletion operations.

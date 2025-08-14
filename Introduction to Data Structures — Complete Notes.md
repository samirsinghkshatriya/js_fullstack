
# 🧠📚 Unit 1: Introduction to Data Structures — Complete Notes

> Designed for clear understanding with simple real‑life analogies and small, runnable C++ examples.

---

## Table of Contents
1. [Introduction to Data Structures and Algorithms](#introduction-to-data-structures-and-algorithms)
2. [Data Types](#data-types)
   - [Primitive Data Types](#primitive-data-types)
   - [Non-Primitive Data Types](#non-primitive-data-types)
3. [Performance Analysis and Measurement](#performance-analysis-and-measurement)
4. [Types of Data Structures](#types-of-data-structures)
   - [Linear Data Structures](#linear-data-structures)
   - [Non-Linear Data Structures](#non-linear-data-structures)
5. [Strings](#strings)
   - [Introduction to Strings](#introduction-to-strings)
   - [Operations on Strings](#operations-on-strings-concatenation-comparison-substring-etc)
6. [Arrays](#arrays)
   - [Introduction to Arrays](#introduction-to-arrays)
   - [Linear Arrays and Their Representation](#linear-arrays-and-their-representation)
7. [Pointers](#pointers-introduction-and-representation)
8. [Records (Structures)](#records-structure-and-representation)
9. [Recursion](#recursion-concept-and-examples)
   - [Tower of Hanoi](#tower-of-hanoi-problem)

---

## Introduction to Data Structures and Algorithms

**Definition**  
- A **data structure (DS)** is a way to organize and store data so that it can be used efficiently.  
- An **algorithm** is a finite sequence of steps that transforms input to output to solve a problem.

**Why learn it?**  
Efficient DS + good algorithms = faster programs that use less memory. They’re essential for scalable software, interviews, and competitive programming.

**Real‑life analogy**  
A **bookshelf** (DS) organizes books; a **search strategy** (algorithm) tells you _how_ to find a specific book quickly.

**Example (C++): Find maximum in an array, step by step**

```cpp
#include <bits/stdc++.h>
using namespace std;

int findMax(const vector<int>& a) {
    // Step 1: assume the first element is the max (initialization)
    int mx = a[0];
    // Step 2: scan each element once (linear scan)
    for (int x : a) {
        // Step 3: update if a larger element is found (comparison + assignment)
        if (x > mx) mx = x;
    }
    // Step 4: return the result
    return mx;
}

int main() {
    vector<int> a = {4, 7, 2, 9, 5};
    cout << "Max = " << findMax(a) << "\n";
}
```

**What’s used & why?**  
- `vector<int>`: simple linear collection.  
- **Loop**: to visit each element exactly once.  
- **Comparison**: to maintain the current best (max).

**Advantages**  
- Simple, easy to write.  
- Works for any numeric array.

**Limitations**  
- Linear time `O(n)`; for huge data, more specialized structures (e.g., heaps) can be used for repeated max queries.

---

## Data Types

### Primitive Data Types

**Definition**  
Basic built‑in types provided by the language: `int`, `char`, `float`/`double`, `bool`.

**Why learn it?**  
They determine memory use and valid operations; choosing the right type avoids overflow/precision bugs.

**Real‑life analogy**  
Think of different **container sizes**: a tiny vial (bool) vs. a bottle (int) vs. a tank (double).

**Example (C++)**

```cpp
#include <bits/stdc++.h>
using namespace std;
int main() {
    int age = 21;
    char grade = 'A';
    double pi = 3.14159;
    bool passed = true;
    cout << age << " " << grade << " " << pi << " " << passed << "\n";
}
```

**Advantages**  
- Fast, direct hardware support.  
- Predictable memory footprint.

**Limitations**  
- Limited range/precision (e.g., `int` overflow, `double` rounding).

---

### Non-Primitive Data Types

**Definition**  
Types built from primitives: arrays, strings, structs/classes, pointers, and user‑defined containers (e.g., `vector`, `list`).

**Why learn it?**  
They model real‑world data and enable complex algorithms.

**Real‑life analogy**  
Combining Lego blocks (primitives) to build cars/houses (non‑primitives).

**Example (C++)**

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Student { int id; string name; double cgpa; };

int main() {
    vector<int> marks = {80, 90, 70};
    string college = "ABC Institute";
    Student s{1, "Riya", 8.7};
    cout << college << " : " << s.name << " -> " << marks[1] << "\n";
}
```

**Advantages**  
- Expressive, closer to problem domain.  
- Reusable and modular.

**Limitations**  
- More memory/overhead if misused.  
- Complexity can increase bugs if not well‑designed.

---

## Performance Analysis and Measurement

**Definition**  
Evaluating how **time** and **space** scale with input size `n` (Big‑O, Big‑Θ, Big‑Ω).

**Why learn it?**  
To pick the right DS/algorithm under constraints (latency, memory, throughput).

**Real‑life analogy**  
Choosing a route in traffic: **shortest path** vs **fastest path** at rush hour.

**Example: Summation vs. Binary Search**

```cpp
#include <bits/stdc++.h>
using namespace std;

// O(n) time, O(1) space
long long sumArray(const vector<int>& a) {
    long long s = 0;
    for (int x : a) s += x;
    return s;
}

// O(log n) time binary search on a sorted array
int binarySearch(const vector<int>& a, int key) {
    int L = 0, R = (int)a.size()-1;
    while (L <= R) {
        int mid = L + (R - L) / 2;
        if (a[mid] == key) return mid;
        else if (a[mid] < key) L = mid + 1;
        else R = mid - 1;
    }
    return -1;
}

int main() {
    vector<int> a(8); iota(a.begin(), a.end(), 1); // [1..8]
    cout << "Sum = " << sumArray(a) << "\n";
    cout << "Find 6 at index " << binarySearch(a, 6) << "\n";
}
```

**What’s used & why?**  
- **Linear scan** for sum: unavoidable if you must read all elements.  
- **Binary search**: requires sorted data; halves the search space each step.

**Advantages**  
- Big‑O abstracts away machine details; easy to compare algorithms.

**Limitations**  
- Hides constants; cache/IO effects matter in practice.  
- Worst‑case vs average‑case differences.

---

## Types of Data Structures

### Linear Data Structures

**Definition**  
Elements are arranged **sequentially**; each has a unique predecessor/successor (except ends). Examples: arrays, linked lists, stacks, queues.

**Why learn it?**  
Great for ordered processing and simple traversals.

**Real‑life analogy**  
A **queue at a ticket counter** (FIFO) or a **stack of plates** (LIFO).

**Example (Stack via `vector`)**

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Stack {
    vector<int> s;
    void push(int x){ s.push_back(x);}      // add to top
    void pop(){ if(!s.empty()) s.pop_back();}
    int top(){ return s.back(); }
    bool empty(){ return s.empty(); }
};

int main(){
    Stack st; st.push(10); st.push(20); st.push(30);
    cout << st.top() << "\n"; // 30
    st.pop();
    cout << st.top() << "\n"; // 20
}
```

**Advantages**  
- Simple, fast operations (e.g., stack push/pop O(1)).

**Limitations**  
- Not efficient for arbitrary middle insertions (array) or random access (linked list).

---

### Non-Linear Data Structures

**Definition**  
Elements are organized in **hierarchical** or **network** form; not strictly sequential. Examples: trees, heaps, graphs, tries.

**Why learn it?**  
They enable faster queries/updates and model relationships (e.g., maps, dependencies).

**Real‑life analogy**  
**Organization chart** (tree), **city map** (graph).

**Example (Mini Tree: parent → children)**

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node{
    int val;
    vector<Node*> child;
    Node(int v): val(v) {}
};

int main(){
    Node* root = new Node(1);
    root->child.push_back(new Node(2));
    root->child.push_back(new Node(3));
    cout << "Root="<<root->val<<", children="<<root->child.size()<<"\n";
    // (Proper deletion omitted for brevity)
}
```

**Advantages**  
- Fast lookups/updates (e.g., BST average O(log n)).  
- Naturally model hierarchies and networks.

**Limitations**  
- Implementation complexity (balancing, memory mgmt).  
- Traversals require recursion/stack/queue logic.

---

## Strings

### Introduction to Strings

**Definition**  
A **string** is a sequence of characters terminated by `'\0'` in C or managed by `std::string` in C++.

**Why learn it?**  
Text processing (names, messages, file paths) is everywhere.

**Real‑life analogy**  
Beads on a thread—each character is a bead.

**Example (C++)**

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s = "Hello";
    cout << s << " length=" << s.size() << "\n";
}
```

**Advantages**  
- High‑level operations (concat, find, substr).

**Limitations**  
- Unicode/encoding pitfalls; costly copies if not careful.

---

### Operations on Strings (concatenation, comparison, substring, etc.)

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    string a = "Hello", b = "World";

    string c = a + " " + b;        // concatenation
    bool eq = (a == b);            // comparison
    string sub = c.substr(0, 5);   // substring "Hello"
    size_t pos = c.find("World");  // search

    cout << c << "\n" << eq << "\n" << sub << "\n" << pos << "\n";
}
```

**Step‑by‑step**  
- `a + " " + b`: creates a new string; O(|a|+|b|).  
- `==`: lexicographic comparison.  
- `substr(start,len)`: copies a portion.  
- `find`: returns index or `npos`.

**Advantages**  
- Easy APIs for common tasks.

**Limitations**  
- Operations may allocate/copy; watch performance for large texts.

---

## Arrays

### Introduction to Arrays

**Definition**  
A contiguous block of elements of the **same type**, accessible by index. In C++, prefer `vector<T>` for safety.

**Why learn it?**  
Fast random access and compact memory layout.

**Real‑life analogy**  
Numbered lockers in a row—locker number is the index.

**Example (C++)**

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    vector<int> a = {10,20,30,40,50};
    cout << a[0] << " " << a.back() << " size=" << a.size() << "\n";
}
```

**Advantages**  
- O(1) index access; cache‑friendly.

**Limitations**  
- Fixed size (raw arrays); insert/delete in middle is O(n).

---

### Linear Arrays and Their Representation

**Memory representation**  
`base_address + index * element_size` (row‑major for 1‑D).

**Insert at position (with shift) — step by step**

```cpp
#include <bits/stdc++.h>
using namespace std;

void insertAt(vector<int>& a, int pos, int val){
    // pos: 0..a.size()
    a.push_back(0);                // 1) grow size by 1
    for(int i = (int)a.size()-1; i > pos; --i) // 2) shift right
        a[i] = a[i-1];
    a[pos] = val;                  // 3) place new value
}

int main(){
    vector<int> a = {1,2,4,5};
    insertAt(a, 2, 3);
    for(int x: a) cout << x << " "; // 1 2 3 4 5
}
```

**Advantages**  
- Simple logic; contiguous memory.

**Limitations**  
- Insertion/deletion O(n) due to shifting.

---

## Pointers (Introduction and Representation)

**Definition**  
A **pointer** stores a **memory address** of another variable.

**Why learn it?**  
Foundation for dynamic memory, arrays, strings, and data structures like linked lists/trees.

**Real‑life analogy**  
A **house address** that points to the house; the address is not the house.

**Example (C++)**

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    int x = 42;
    int* p = &x;        // p holds address of x
    cout << *p << "\n"; // dereference -> value 42
    *p = 50;            // modify x via pointer
    cout << x << "\n";  // 50
}
```

**Representation**  
- `&x` gives the address, `*p` accesses the value at that address.

**Advantages**  
- Direct memory manipulation; dynamic structures.

**Limitations**  
- Dangling/NULL pointers, memory leaks, undefined behavior if misused.

---

## Records (Structure and Representation)

**Definition**  
A **record/struct** groups **heterogeneous** fields under one name.

**Why learn it?**  
Models real entities (Student, Book, Employee) cleanly.

**Real‑life analogy**  
A form with fields: Name, Age, ID—filled for each person.

**Example (C++)**

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Student{ int id; string name; double cgpa; };

int main(){
    Student s{101, "Aman", 8.9};
    cout << s.id << " " << s.name << " " << s.cgpa << "\n";
}
```

**Representation**  
Memory is laid out field‑by‑field with possible padding for alignment.

**Advantages**  
- Readable code; encapsulates related data.

**Limitations**  
- Manual invariants without classes/methods; padding may waste bytes.

---

## Recursion (Concept and Examples)

**Definition**  
A function that **calls itself** with a smaller input until a **base case** stops further calls.

**Why learn it?**  
Simplifies problems with self‑similar structure (divide & conquer, trees, DFS).

**Real‑life analogy**  
Nested **matryoshka dolls**—each doll contains a smaller one until the smallest.

**Example: Factorial**

```cpp
#include <bits/stdc++.h>
using namespace std;
long long fact(int n){
    if(n==0) return 1;        // base case
    return 1LL*n*fact(n-1);   // recursive step
}
int main(){ cout << fact(5) << "\n"; }
```

**Step‑by‑step (n=3)**  
- `fact(3)` → `3 * fact(2)`  
- `fact(2)` → `2 * fact(1)`  
- `fact(1)` → `1 * fact(0)`  
- `fact(0)` → `1` (stop) → multiply back: `1*1*2*3 = 6`

**Advantages**  
- Elegant, mirrors mathematical definitions; concise tree/graph algorithms.

**Limitations**  
- Function call overhead; risk of stack overflow; sometimes iterative is faster.

---

## Tower of Hanoi Problem

**Definition**  
Move `n` disks from **source** to **target** using an **auxiliary** peg, moving one disk at a time and never placing a larger disk on a smaller one.

**Why learn it?**  
Classic example of recursion and exponential time growth.

**Real‑life analogy**  
Rearranging a stack of trays using a side table with the “no‑larger‑on‑smaller” rule.

**Code (C++)**

```cpp
#include <bits/stdc++.h>
using namespace std;

void hanoi(int n, char from, char to, char aux){
    if(n==1){ cout << "Move 1 from " << from << " to " << to << "\n"; return; }
    hanoi(n-1, from, aux, to);
    cout << "Move " << n << " from " << from << " to " << to << "\n";
    hanoi(n-1, aux, to, from);
}

int main(){ hanoi(3,'A','C','B'); }
```

**Step‑by‑step (n=3)**  
1. Move 2 disks A→B using C.  
2. Move disk 3 A→C.  
3. Move 2 disks B→C using A.

**Advantages**  
- Demonstrates recursion and problem decomposition.

**Limitations**  
- Exponential moves (`2^n - 1`); quickly infeasible for large `n`.

---

> Tip: Compile with `g++ -std=c++17 file.cpp && ./a.out` to run examples.

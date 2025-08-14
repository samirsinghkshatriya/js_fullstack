# 🧾 Unit 1 — Code-Only Snippets (C++ with Comments)

## 1) Introduction to Data Structures and Algorithms — Find Max in Array
```cpp
// Topic: Introduction to Data Structures and Algorithms
// What: Linear scan to find maximum in an array
// Why: Demonstrates a simple algorithm working on a basic data structure (array)
// How: Keep current max and update while traversing once (O(n))

#include <bits/stdc++.h>
using namespace std;

int findMax(const vector<int>& a){
    int mx = a[0];                 // current best
    for(int x : a) if(x > mx) mx = x; // compare/update
    return mx;
}

int main(){
    vector<int> a = {4,7,2,9,5};
    cout << "Max=" << findMax(a) << "\n";
}
```
---

## 2) Data Types — Primitive
```cpp
// Topic: Data Types -> Primitive (int, char, double, bool)
// What: Store and print primitive values
// Why: Foundation types affect memory, range, precision

#include <bits/stdc++.h>
using namespace std;
int main(){
    int age = 21;           // integer number
    char grade = 'A';       // single character
    double pi = 3.14159;    // floating-point
    bool passed = true;     // boolean
    cout << age << " " << grade << " " << pi << " " << passed << "\n";
}
```
---

## 3) Data Types — Non-Primitive (array/vector, string, struct)
```cpp
// Topic: Data Types -> Non-Primitive (vector, string, struct)
// What: Combine primitives into expressive, real-world models
// Why: Build complex records/collections

#include <bits/stdc++.h>
using namespace std;

struct Student{ int id; string name; double cgpa; };

int main(){
    vector<int> marks = {80, 90, 70};      // dynamic array
    string college = "ABC Institute";      // text data
    Student s{1, "Riya", 8.7};             // heterogeneous record
    cout << college << " : " << s.name << " -> " << marks[1] << "\n";
}
```
---

## 4) Performance Analysis and Measurement — O(n) vs O(log n)
```cpp
// Topic: Performance Analysis and Measurement
// What: Show O(n) summation and O(log n) binary search
// Why: Compare time complexity behaviors on same data

#include <bits/stdc++.h>
using namespace std;

// O(n) time, O(1) extra space
long long sumArray(const vector<int>& a){
    long long s = 0;
    for(int x : a) s += x;     // visit every element once
    return s;
}

// O(log n) time on sorted array
int binarySearch(const vector<int>& a, int key){
    int L = 0, R = (int)a.size()-1;
    while(L <= R){
        int mid = L + (R - L)/2;       // avoid overflow
        if(a[mid] == key) return mid;  // found
        else if(a[mid] < key) L = mid + 1; // search right half
        else R = mid - 1;              // search left half
    }
    return -1; // not found
}

int main(){
    vector<int> a(8); iota(a.begin(), a.end(), 1); // 1..8 (sorted)
    cout << "Sum=" << sumArray(a) << "\n";
    cout << "Index of 6=" << binarySearch(a,6) << "\n";
}
```
---

## 5) Types of Data Structures — Linear (Stack)
```cpp
// Topic: Types of DS -> Linear DS (Stack using vector)
// What: LIFO push/pop/top
// Why: Fast O(1) operations at one end; models function-call stack

#include <bits/stdc++.h>
using namespace std;

struct Stack{
    vector<int> s;
    void push(int x){ s.push_back(x); }    // push at end
    void pop(){ if(!s.empty()) s.pop_back(); }
    int top(){ return s.back(); }          // read top
    bool empty(){ return s.empty(); }
};

int main(){
    Stack st; st.push(10); st.push(20); st.push(30);
    cout << st.top() << "\n"; // 30
    st.pop();
    cout << st.top() << "\n"; // 20
}
```
---

## 6) Types of Data Structures — Non-Linear (Tree Node + Simple Build)
```cpp
// Topic: Types of DS -> Non-Linear DS (Tree)
// What: Minimal tree node with children
// Why: Represent hierarchical relationships

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
    cout << "Root=" << root->val << ", children=" << root->child.size() << "\n";
    // (Production code should delete nodes to avoid leaks.)
}
```
---

## 7) Strings — Basics and Common Operations
```cpp
// Topic: Strings -> Intro & Operations (concatenation, comparison, substring, find)
// What: Build, join, compare, slice, and search strings
// Why: Text processing is ubiquitous

#include <bits/stdc++.h>
using namespace std;
int main(){
    string a = "Hello", b = "World";
    string c = a + " " + b;         // concatenation
    bool eq = (a == b);             // lexicographic equality
    string sub = c.substr(0, 5);    // "Hello"
    size_t pos = c.find("World");   // index of "World" or npos
    cout << c << "\n" << eq << "\n" << sub << "\n" << pos << "\n";
}
```
---

## 8) Arrays — Indexing and Traversal
```cpp
// Topic: Arrays -> Introduction
// What: Random access and iteration
// Why: Contiguous storage gives O(1) index access

#include <bits/stdc++.h>
using namespace std;
int main(){
    vector<int> a = {10,20,30,40,50};
    cout << a[0] << " " << a.back() << " size=" << a.size() << "\n";
    long long sum = 0;
    for(int x: a) sum += x;         // linear traversal
    cout << "Sum=" << sum << "\n";
}
```
---

## 9) Linear Arrays and Their Representation — Insert by Shifting
```cpp
// Topic: Arrays -> Linear Arrays and Representation
// What: Insert at position by shifting elements right
// Why: Demonstrates contiguous memory consequences (O(n) shift)

#include <bits/stdc++.h>
using namespace std;

void insertAt(vector<int>& a, int pos, int val){
    a.push_back(0);                           // grow size by 1
    for(int i = (int)a.size()-1; i > pos; --i) // shift elements right
        a[i] = a[i-1];
    a[pos] = val;                             // write new value
}

int main(){
    vector<int> a = {1,2,4,5};
    insertAt(a, 2, 3);                        // insert 3 at index 2
    for(int x: a) cout << x << " ";           // 1 2 3 4 5
}
```
---

## 10) Pointers — Address and Dereference
```cpp
// Topic: Pointers -> Introduction and Representation
// What: Store address, access/modify value via pointer
// Why: Foundation for dynamic memory and complex DS

#include <bits/stdc++.h>
using namespace std;
int main(){
    int x = 42;
    int* p = &x;          // p holds address of x
    cout << *p << "\n";   // dereference -> value
    *p = 50;              // modify x using pointer
    cout << x << "\n";    // 50
}
```
---

## 11) Records (Structures) — Heterogeneous Grouping
```cpp
// Topic: Records -> Structure and Representation
// What: Group related fields of different types
// Why: Model real-world entities cleanly

#include <bits/stdc++.h>
using namespace std;

struct Student{ int id; string name; double cgpa; };

int main(){
    Student s{101, "Aman", 8.9};
    cout << s.id << " " << s.name << " " << s.cgpa << "\n";
}
```
---

## 12) Recursion — Factorial
```cpp
// Topic: Recursion -> Concept and Examples
// What: Recursive factorial with base case
// Why: Illustrates self-calls and stopping condition

#include <bits/stdc++.h>
using namespace std;

long long fact(int n){
    if(n==0) return 1;        // base case
    return 1LL*n*fact(n-1);   // recursive step
}

int main(){
    cout << fact(5) << "\n";  // 120
}
```
---

## 13) Tower of Hanoi — Recursive Solution
```cpp
// Topic: Recursion -> Tower of Hanoi Problem
// What: Move n disks from 'from' to 'to' using 'aux'
// Why: Classic recursion with exponential steps (2^n - 1)

#include <bits/stdc++.h>
using namespace std;

void hanoi(int n, char from, char to, char aux){
    if(n==1){ 
        cout << "Move 1 from " << from << " to " << to << "\n"; 
        return; 
    }
    hanoi(n-1, from, aux, to);                   // move n-1 to aux
    cout << "Move " << n << " from " << from << " to " << to << "\n";
    hanoi(n-1, aux, to, from);                   // move n-1 to target
}

int main(){ 
    hanoi(3,'A','C','B');                        // sample run
}
```

# Stacks 
Stack is a data structure to store data and follows the property of LIFO (Last In First Out).

Following operations can be performed on the stack data structure:

-   push -> to insert -> s.push();
-   pop -> to delete -> s.pop();
-   top -> to view the topmost/last value in the stack -> s.top();

---

## Stack Implementation
Stack Implementation using class can be done in two ways:
- Array
- Linked List

## Stack Implementation Using Class

Basic flow of the stack using array

    class Stack {
     
    // properties
     
    public: 
    int *arr; 
    int top; 
    int size; 
    
    //behaviour - constructor
     
    Stack(int size) { 
    this -> size = size; 
    arr = new int[size]; 
    top = -1; 
    } 
    
    void push(int element){ 
    
    } 
    
    void pop(){
    
     } 
     
     int peek(){ 
     
     } 
     
     bool isEmpty(){ 
     
     } 
     };


## Question Links

### Implementing Two Stacks: 
(https://www.naukri.com/code360/problems/two-stacks_983634)

Code:

#include <bits/stdc++.h> 
class TwoStack {

    int *arr;
    int top1;
    int top2;
    int size;

public:

    // Initialize TwoStack.
    TwoStack(int s) {
        this->size = s;
        top1 = -1;
        top2 = s;
        arr = new int[s];
    }

    // Destructor to clean up allocated memory
    ~TwoStack() {
        delete[] arr;
    }
    
    // Push in stack 1.
    void push1(int num) {
        if (top2 - top1 > 1) {  // Corrected the condition
            top1++;
            arr[top1] = num;
        }
    }

    // Push in stack 2.
    void push2(int num) {
        if (top2 - top1 > 1) {  // Corrected the condition
            top2--;
            arr[top2] = num;
        }
    }
    
    // Pop from stack 1 and return popped element.
    int pop1() {
        if (top1 >= 0) {
            int ans = arr[top1];
            top1--;
            return ans;
        } else {
            return -1;
        }
    }

    // Pop from stack 2 and return popped element.
    int pop2() {
        if (top2 < size) {
            int ans = arr[top2];
            top2++;
            return ans;
        } else {
            return -1;
        }
    }
};


## Implementing Queue using Two Stacks 
(https://leetcode.com/problems/implement-queue-using-stacks/description/)

Create two stacks s1 and s2.

Code follows the basic flow of three steps:

- s1 -> s2
- x -> s1
- s2 -> s1

### Time Complexity - O(n)

class MyQueue {
public:
     stack<int> s1, s2;
    
    void push(int x) {

        while(s1.size()){
            s2.push(s1.top());
            s1.pop();
        }

        s1.push(x);

        while(s2.size()){
            s1.push(s2.top());
            s2.pop();
        }
        
    }
    
    int pop() {

    int popp = s1.top();
    s1.pop();
    return popp;
    
        
    }
    
    int peek() {
    int popp = s1.top();
    return popp;
    
        
    }
    
    bool empty() {
    if(s1.empty() && s2.empty()){
        return true;
    }

    else return false;
        
    }
};


### Time Complexity - O(1)

class MyQueue {
public:
    stack<int> s1, s2;

    void push(int x) {
        s1.push(x);
    }
    
    int pop() {
        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }
        int top = s2.top();
        s2.pop();
        return top;
    }
    
    int peek() {
        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }
        return s2.top();
    }
    
    bool empty() {
        return s1.empty() && s2.empty();
    }
};


## Valid Parenthesis  
(https://leetcode.com/problems/valid-parentheses/)

#include <stack>
#include <string>

class Solution {
public:
    bool isValid(std::string s) {
        std::stack<char> st;
        int n = s.size();

        for (int i = 0; i < n; i++) {
            if (s[i] == '(' || s[i] == '[' || s[i] == '{') {
                st.push(s[i]);
            } else {
                if (st.empty()) return false;

                char ch = st.top();
                st.pop();

                if ((s[i] == ')' && ch != '(') || 
                    (s[i] == '}' && ch != '{') || 
                    (s[i] == ']' && ch != '[')) {
                    return false;
                }

             
            }
        }

        return st.empty();
    }
};


### LRU Cache

Code::

class LRUCache {
public:
    list<int> dll; 
    map<int, pair<list<int>::iterator, int>> cache; 
    int capacity;
    
    LRUCache(int capacity) {
        this->capacity = capacity;
    }
    
    void makeMostRecentlyUsed(int key) {
        dll.erase(cache[key].first);
        dll.push_front(key);
        cache[key].first = dll.begin();
    }
    
    int get(int key) {
        if(!cache.count(key))
            return -1;
        
        makeMostRecentlyUsed(key);
        return cache[key].second;
    }
    
    void put(int key, int value) {
        if(cache.count(key)) {
            cache[key].second = value;
            makeMostRecentlyUsed(key);
        } else {
            dll.push_front(key);
            cache[key] = {dll.begin(), value};
            capacity--;
        }
        
        if(capacity < 0) {
            cache.erase(dll.back());
            dll.pop_back();
            capacity++;
        }
    }
};


### Minimum Stack

Code:

#include <stack>
#include <limits>

class MinStack {
public:
    std::stack<int> st;
    std::stack<int> minStack;

    MinStack() {
    }
    
    void push(int val) {
        st.push(val);

        if (minStack.empty() || val <= minStack.top()) {
            minStack.push(val);
        }
    }
    
    void pop() {
        if (st.empty()) return;

        int topElem = st.top();
        st.pop();

        if (topElem == minStack.top()) {
            minStack.pop();
        }
    }
    
    int top() {
        if (st.empty()) return -1; 
        return st.top();
    }
    
    int getMin() {
        if (minStack.empty()) return -1; 
        return minStack.top();
    }
};



Alternate Solution:

class MinStack {
public:

int minEle;

stack<int> st;


    MinStack() {
        
    }
    
    void push(int val) {
        if(st.size() == 0){
            st.push(val);
            minEle = val;
        }

        else {
            if(val >= minEle){
                st.push(val);
            }

            else if(val < minEle){
                st.push(2 * val - minEle);
                minEle = val;
            }
        }
        
    }
    
    void pop() {

        if(st.size() == 0)
        return;

        else {
            if(st.top() > minEle){
                st.pop();
            }

            else if(st.top() <= minEle){
                minEle = 2 * minEle - st.top();
                st.pop();
            }
        }
        
    }
    
    int top() {

        int topp = st.top();
        return topp;
        
    }
    
    int getMin() {

        if(st.size() == 0){
            return minEle;
        }

        else return minEle;


        
    }
};










---
layout: post
title: CS162 - 3A
parent: Introduction to Computer Science II
---

{% include toc.md %}

## Problem

1. Construct a whole list
2. Display the list
3. Delete the whole list
4. Insert a new Node to ther beginning of the list
{% capture code %}
{% highlight cpp linenos %}
void insertAtBeginning(Node* pHead, int x);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
5. Insert a new Node ``x`` after the $1^{st}$ Node ``k`` (By saying Node ``x``, it means the Node with the value of x).  
*Notes:* if there is no ``k``, don't insert.
{% capture code %}
{% highlight cpp linenos %}
void insertAfterK(Node* pHead, int x, int k);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Student's code

{% capture code %}
{% highlight cpp linenos %}
#include <iostream>

using namespace std;

struct Node{
    int data;
    Node* pNext;
};

void inputLL(Node*& pHead);
void displayLL(Node* cur);
void deleteLL(Node*& pHead);
void insertAtBeginning(Node*& pHead, int x);
void insertAfterK(Node* pHead, int x, int k);

int main(){
    Node* pHead = nullptr;
    
    inputLL(pHead);
    int x;
    cout << "data: ";
    cin >> x;
    insertAtBeginning(pHead, x);
    displayLL(pHead);
    
    cout << "data: ";
    cin >> x;
    cout << "value to insert after: ";
    int k;
    cin >> k;
    insertAfterK(pHead, x, k);
    displayLL(pHead);
    
    deleteLL(pHead);
    displayLL(pHead);
}

void inputLL(Node*& pHead) {    
    int x;
    cout << "Please input the number: ";
    cin>>x;
    while(x != 0)
    {
        if(pHead == nullptr) {
            pHead = new Node;
            cur = pHead;
        }
        else {
            cur->pNext = new Node;
            cur = cur->pNext;
        }
        
        int x;
        cout << "Please input the number: ";
        cin>>x;
        cur->data = x;
        cur->pNext = nullptr;
    }
}

void displayLL(Node* cur) {
    for (; cur != nullptr; cur = cur->pNext)
    {
        cout << cur->data << endl;
    }
}

void deleteLL(Node*& pHead) {
    while(pHead != nullptr)
    {
        Node* next = pHead->pNext;
        delete pHead;
        pHead = next;
    }
}

void insertAtBeginning(Node*& pHead, int x) {
    Node* newNode = new Node;
    newNode->data = x;
    newNode->pNext = pHead;
    pHead = newNode;
}

void insertAfterK(Node* pHead, int x, int k) {
    while(pHead != nullptr && pHead->data != k) {
        pHead = pHead->pNext;
    }
    if(pHead == nullptr) {
        return;
    }
    Node* newNode = new Node;
    newNode->data = x;
    newNode->pNext = pHead->pNext;
    pHead->pNext = newNode;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Teacher's Notes

- The order of ``line 80`` and ``line 81`` is very important.
- If you run ``pHead`` in the function ``void insertAfterK()`` which if passed by value, it will not change the value of the actual ``pHead``. Thus it's safe to be iterating through the linked list.
- The ``if`` statement at ``line 88`` means there're no Node ``k`` in the linked list.


### Visualization

{% capture code %}
{% highlight cpp linenos %}
void insertAtBeginning(Node*& pHead, int x);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
![](https://i.imgur.com/3fzY18l.gif)

{% capture code %}
{% highlight cpp linenos %}
void insertAfterK(Node* pHead, int x, int k);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
![](https://i.imgur.com/KKiSXL9.gif)


## Additional sub-problem:

6. Insert Node ``x`` before Node ``k``.

### Student's code

{% capture code %}
{% highlight cpp linenos %}
void insertBeforeK(Node*& pHead, int x, int k);

void insertBeforeK(Node*& pHead, int x, int k) {
    Node* cur = pHead;
    while(cur != nullptr && cur->pNext->data != k) {
        cur = cur->pNext;
    }
    
    if(cur == nullptr) {
        return;
    }
    
    Node* newNode = new Node;
    newNode->data = x;
    newNode->pNext = cur->pNext;
    cur->pNext = newNode;
    
    if(cur == pHead) {
        insertAtBeginning(pHead, x);
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Teacher's code


{% capture code %}
{% highlight cpp linenos %}
void insertBeforeK(Node*& pHead, int x, int k) {
    Node* cur = pHead;
    
    if(!cur) return;
    if(cur->data == k) {
        insertAtBeginning(pHead, x);
        return;
    }
    
    if(cur && cur->pNext && cur->data == k) {
        insertAtBeginning(pHead, x);
        return;
    }
    while(cur && cur->pNext && cur->pNext->data != k) {
        cur = cur->pNext;
    }
    
    if(!cur->pNext) return;
    
    Node* newNode = new Node;
    newNode->data = x;
    newNode->pNext = cur->pNext;
    cur->pNext = newNode;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

*Notes:*
- Make sure that everytime you use a pointer, you have to make sure that the pointer is valid (not a nullptr)
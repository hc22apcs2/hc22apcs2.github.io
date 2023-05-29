---
layout: post
title: CS162 - 6A
parent: Introduction to Computer Science II
grand_parent: Semester II
--- 

*Proofread by Huỳnh Hà Phương Linh*

{% include toc.md %}

## Stack
We have the following pseudo-code:
{% capture code %}
{% highlight cpp linenos %}
void A(...);
void B(...);
void C(...);

int main() {
    int t = 5;
    A(...);
}

void A(...) {
    int t = 7;
    B(...);
}

void B(...) {
    int t(10);
    C(...);
}

void C(...) {
    int t(20);
    ...
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

Compiler does not copy the content of the function `C()` and put it into the implementation of `B()` (similarly to what happens to `B()` and `A()`, `A()` and `main()`). Instead, the compiler will use a `Stack` structure.

Stack has 4 methods:

- `push(...)`: Add new element to the top of a stack.
- `pop()`: Return and remove the topmost element of the stack.
- `isEmpty()`: Return true if the stack is empty.
- `top/peek()`: Return the topmost element of the stack without removing it.

{% capture code %}
{% highlight cpp linenos %}
void push(Node* &pStack, int x);
int pop(Node* &pStack);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

Stack obeys the `Last In First Out` rule (`LIFO`), which means the last data being pushed in will be the last data being poped out.

We can implement the `Stack` based on the `array` data structure but it is not flexible (in size). Using `SLL` will do.

### Implementation

#### Student's code

{% capture code %}
{% highlight cpp linenos %}
void push(Node* &pStack, int x) {
    Node* newNode = new Node;
    newNode->data = x;
    newNode->pNext = pStack;
    pStack = new Node;
}

int pop(Node* &pStack) {
    if(pStack) {
        Node* tmp = pStack;
        int x = tmp->data;
        pStack = pStack->pNext;
        delete tmp;
        return x;
    }
    return -1;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Discussion

#### Why `-1` at `line 16`? Can it be any other integer value?

Yes, and `data` can be any type of data too which is kind of a problem. To solve it, we can wrap the data into a node before pushing or popping it. This way we wouldn't be bothered by the data type (and the returning value).

{% capture code %}
{% highlight cpp linenos %}
void push(Node* &pStack, Node* pNew);
Node* pop(Node* &pStack);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
People also solve the problem by returning the value with a referenced argument of the function.

{% capture code %}
{% highlight cpp linenos %}
bool pop(Node* &pStack, int &val);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

The latter solution is good, find out the reason at home! In the class's scope we'll only use the former one.

### Data abstraction

We can encapsulate the functions into the data structure itself. This is called data abstraction.

{% capture code %}
{% highlight cpp linenos %}
struct MyStack {
    //data member(s)
    Node* pHead = nullptr;
    
    //member functions
    void push(Node* pNew);
    Node* pop();
};
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}


#### Implementation

{% capture code %}
{% highlight cpp linenos %}
void MyStack::push(Node* pNew) {
    pNew->pNext = pHead;
    pHead = pNew;
}

Node* MyStack::pop() {
    if(!pHead) return pHead;
    Node* tmp = pHead;
    pHead = pHead->pNext;
    return tmp;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Usage

{% capture code %}
{% highlight cpp linenos %}
int main() {
    Node pStack = nullptr;
    Node* tmp = new Node;
    tmp->data = 5;
    tmp->pNext = nullptr;
    
    MyStack pS;
    pS.push(tmp);
    
    return 0;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

We can invoke the stack's function using charater dot `'.'`.

## Queue

`Queue` is similar to `Stack` but it follows `First In First Out` (`FIFO`) rule.

Queue has 2 methods:
- `enqueue(...)`: Add new element to the end of the queue.
- `dequeue()`: Return and remove the first element of the queue.

### Implementation

{% capture code %}
{% highlight cpp linenos %}
struct MyQueue {
    Node* pHead = nullptr;
    Node* pTail = nullptr;
    
    void enqueue(Node* pNew);
    Node* dequeue();
};

void MyQueue::enqueue(Node* pNew) {
    if(!pHead) {
        pHead = pNew;
        pTail = pNew;
        pHead->pNext = nullptr;
    } else {
        pTail->pNext = pNew;
        pTail = pTail->pNext;
    }
}

Node* MyQueue::dequeue() {
    if(!pHead) return nullptr;
    Node* tmp = pHead;
    pHead = pHead->pNext;
    if(!pHead) pTail = nullptr;
    return tmp;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
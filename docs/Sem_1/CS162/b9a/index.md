---
layout: post
title: CS162 - 9A - Review
parent: Introduction to Computer Science II
grand_parent: Semester I
--- 

{% include toc.md %}

## Sections

### Pointer

- [CS161 - 1B](https://hc22apcs2.github.io/docs/CS162/b1/)

### Dynamically allocated array

- [CS162 - 1B/#array-allocation](https://hc22apcs2.github.io/docs/CS162/b1/#array-allocation)

### Linked List
1. Singly Linked List
- [CS162 - 2B/#build-linked-list](https://hc22apcs2.github.io/docs/CS162/b2b/#now-its-time-to-build-a-simple-linked-list)
- [CS162 - 3A](https://hc22apcs2.github.io/docs/CS162/b3a/#additional-sub-problem)
- [CS162 - 3B](https://hc22apcs2.github.io/docs/CS162/b3b/)

2. Ordered Linked List
- [CS162 - 4A/#singly-ordered-linked-list](https://hc22apcs2.github.io/docs/CS162/b4a/#introduction---singly-ordered-linked-list)

3. Doubly Linked List
- [CS162 - 4A/#double-linked-list](https://hc22apcs2.github.io/docs/CS162/b4a/#double-linked-list)
- [CS162 - 4B](https://hc22apcs2.github.io/docs/CS162/b4b/)

4. Circular Linked List
- [CS162 - 5A](https://hc22apcs2.github.io/docs/CS162/b5a/)
- [CS162 - 5B](https://hc22apcs2.github.io/docs/CS162/b5b/)
- [CS162 - 5B (Bonus)](https://hc22apcs2.github.io/docs/CS162/b5b-bonus/)

#### Linked List operations:
{:.no_toc}
- Create the list
- Display the list
- Remove the whole list
- Search an element in the list
- Insert a new item into the list
    - beginning
    - after `x`
    - before `x`
    - ...
- Remove a node from the list



|               |              Create               |              Display              |            Remove all             |              Search               |              Insert               |         Remove some nodes         |
| ------------- |:---------------------------------:|:---------------------------------:|:---------------------------------:|:---------------------------------:|:---------------------------------:|:---------------------------------:|
| `Singly LL`   | [code](https://ideone.com/DAnHcV) | [code](https://ideone.com/xLBVeD) | [code](https://ideone.com/89SReN) |               code                | [code](https://ideone.com/xwFzC5) | [code](https://ideone.com/VH1qiJ) |
| `Ordered LL`  |               code                | [code](https://ideone.com/xLBVeD) | [code](https://ideone.com/89SReN) |               code                | [code](https://ideone.com/1VitMx) | [code](https://ideone.com/VH1qiJ) |
| `Doubly LL`   |               code                |               code                | [code](https://ideone.com/fWDFRc) |               code                | [code](https://ideone.com/5ruPUt) | [code](https://ideone.com/HVcHCM) |
| `Circular LL` |               code                |               code                |               code                | [code](https://ideone.com/YSHeuK) |               code                | [code](https://ideone.com/TTDQON) |


### Data abstraction
- Data members
- Member functions

$\Rightarrow$ Struct

### Stack (LIFO)

- [CS162 - 6A/#stack](https://hc22apcs2.github.io/docs/CS162/b6a/#stack)

2 operations:
- push
- pop

If implementation based on `SLL`:
- `push` at the ***beginning*** of `SLL`.
- `pop` at the ***beginning*** of `SLL`.

#### Implementation
{:.no_toc}
{% capture code %}{% highlight cpp linenos %}
struct MyStack {
    Node* pHead = nullptr;
    
    void push(Node* pNew);
    Node* pop();
};

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
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

Full code (runnable): [here](https://ideone.com/PwPmtQ)

### Queue (FIFO)

- [CS162 - 6A/#queue](https://hc22apcs2.github.io/docs/CS162/b6a/#queue)

2 operations:
- enqueue
- dequeue

If implementation based on `SLL`:
- `dequeue` at the ***beginning*** of `SLL` 
- `enqueue` at the ***end*** of `SLL`.

#### Implementation
{:.no_toc}

{% capture code %}{% highlight cpp linenos %}
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
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

Full code (runable): [here](https://ideone.com/EEtT3g)

### Recursion

- [CS162 - 7B](https://hc22apcs2.github.io/docs/CS162/b7b/)
- [CS162 - 8A](https://hc22apcs2.github.io/docs/CS162/b8a/)
- [Types of recursion](https://www.geeksforgeeks.org/types-of-recursions/)

### Binary file

- [CS162 - 8B](https://hc22apcs2.github.io/docs/CS162/b8b/)

## Revision problems

Given $N$ integer numbers: $x_0, x_1, \dots, x_{N-1}$ and an integer $X$, you are asked to implement a program to place basic arithmetic operators in between the $N$ numbers so that we achieve the following equation:

$$x_0 \ \fbox{ } \ x_1 \ \fbox{ } \ x_2 \ \fbox{ } \ \dots \ \fbox{ } \ x_{N-1}=X$$

### Hint
{:.no_toc}

Ta có $N-1$ vị trí cần điền $4$ các phép toán cơ bản vào phương trình, vì thế ta có thể sinh tứ phân trong $O(4^N)$.

Vì phép $*$ và phép $/$ có thứ tự ưu tiên cao hơn phép $+$ và phép $-$, khi tính giá trị của vế trái của phương trình đề bài, ta có thể làm như sau:

Xét 2 phép toán đầu tiên trong dãy giá trị, ta sẽ có các trường hợp sau:

- Toán tử đầu tiên là $*$ hoặc $/$ thì ta tính giá trị của toán tử đó và thế vào vị trí tương ứng
- Toán tử đầu tiên là $+$ hoặc $-$ thì ta sẽ xết tới toán tử thứ 2:
    - Nếu toán tử thứ 2 cũng là $+$ hoặc $-$ thì ta sẽ tính giá trị của toán tử đầu tiên rồi thế vào vị trí tương ứng.
    - Nếu toán tử thứ 2 là $*$ hoặc $/$ thì ta sẽ tính giá trị của toán tử thứ 2 và thế vào vị trí tương ứng.
    
Vì ta phải tính giá trị của 1 toán tử và thay thế 2 tham số của toán tử đó thành 1 tham số duy nhất, ta có thể phải xóa 2 tham số của toán tử và thay bằng kết quả của toán tử. Để xử lý vấn đề này ta có thể đảo thứ tự của toàn bộ các số $x_i$ thành $x_{N-1}, x_{N-2}, \dots, x_0$ thì ta có thể xử lý các phép toán từ trên xuống.
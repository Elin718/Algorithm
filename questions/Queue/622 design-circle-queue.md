## 题目地址
https://leetcode-cn.com/problems/design-circular-queue/

## 题目描述
```
Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Your implementation should support following operations:

MyCircularQueue(k): Constructor, set the size of the queue to be k.
Front: Get the front item from the queue. If the queue is empty, return -1.
Rear: Get the last item from the queue. If the queue is empty, return -1.
enQueue(value): Insert an element into the circular queue. Return true if the operation is successful.
deQueue(): Delete an element from the circular queue. Return true if the operation is successful.
isEmpty(): Checks whether the circular queue is empty or not.
isFull(): Checks whether the circular queue is full or not.

```   


## 思路
### 需要控制rear==head可能会出现的情况
### 1.队列为空
### 2.队列满了
###   队列满了，删除一个节点会怎样？
### 3.判断队列满了的条件

``


``



## 自己出现的问题

- Rear() 中，index<1的时候，capacity和size有啥区别？




## 代码
### 运行时间：40ms

C++ Code：
```C++
class MyCircularQueue {
private:
    int head;
    int rear;
    int capacity;
    int size;
    int *arr;
    
    
public:
    /** Initialize your data structure here. Set the size of the queue to be k. */
    MyCircularQueue(int k) {
        head=0;
        rear=0;
        capacity=k;
        size=0;
        arr=new int[k];
        
    }
    
    /** Insert an element into the circular queue. Return true if the operation is successful. */
    bool enQueue(int value) {
        if(isFull()){
            return false;
        }
        arr[rear]=value;
        
        ++rear;
        if(rear==capacity){
            rear=0;
        }
        ++size;
        return true;
    }
    
    /** Delete an element from the circular queue. Return true if the operation is successful. */
    bool deQueue() {
        if(isEmpty()){
            return false;
        }
        ++head;
        if(head==capacity){
            head=0;
        }
        --size;
        return true;
    }
    
    /** Get the front item from the queue. */
    int Front() {
        if(isEmpty()){
            return -1;
        }
        return arr[head];
    }
    
    /** Get the last item from the queue. */
    int Rear() {
        if(isEmpty()){
            return -1;
        }
        int index=rear-1;
        if(index<0){
            index=capacity-1;
        }
        return arr[index];
    }
    
    /** Checks whether the circular queue is empty or not. */
    bool isEmpty() {
        
        return size==0;
        
    }
    
    /** Checks whether the circular queue is full or not. */
    bool isFull() {
       
        return size==capacity;
    }
};

```

## 题目地址
https://leetcode-cn.com/problems/design-linked-list/

## 题目描述
```
Design your implementation of the linked list. You can choose to use the singly linked list or the doubly linked list. A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node. If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement these functions in your linked list class:

*get(index) : Get the value of the index-th node in the linked list. If the index is invalid, return -1.
*addAtHead(val) : Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
*addAtTail(val) : Append a node of value val to the last element of the linked list.
*addAtIndex(index, val) : Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
*deleteAtIndex(index) : Delete the index-th node in the linked list, if the index is valid.


```   


## 思路
### 只会出现三个节点：头节点、中间节点、尾节点
``
无论是插入、删除、还是获取数据，都只有这三种情况。

``



## 自己出现的问题

- 拿到参数的第一件事，应该是检查参数的有效性
- 遍历的目的是什么？每次for循环中i的值和index的关系很重要。



## 代码
### 运行时间：40ms

C++ Code：
```C++
#include <iostream>
#include <vector>
#include <cstdlib>
#include <string>
#include <stdexcept>
#include <map>
#include <regex>
#include <sstream>
using namespace std;
#include "test2.hpp"
typedef struct Node{

int val;
Node *next;
Node(int a) : val(a),next(NULL){}

};

class MyLinkedList {
private:
Node *head=nullptr;//头结点
Node *tail=nullptr;//尾节点
int time=0;
int size=0;


public:
/** Initialize your data structure here. */
MyLinkedList() {

}

/** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
int get(int index) {

//先验证数据有有效性
//        分三种情况：取头，中间、尾节点
//
if(index>=0 && index<size){
if(index==0){
return head->val;
}else if (index==size-1){
return tail->val;
}else{
//遍历的目的是为了得到index的node
int j=1;
Node *node=head;
for(;j<index+1;j++){
node=node->next;
}
if(!node ||j>index+2) return -1;
int result=node->val;
return result;

}
}

return -1;

}

/** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
void addAtHead(int val) {
Node *node= new Node(val);
node->next=head;
head=node;
size++;
if (size==1) {
tail=head;
}
}

/** Append a node of value val to the last element of the linked list. */
void addAtTail(int val) {
Node *node= new Node(val);
if(!tail && !head){
head=node;
}else if(!head && tail){
cout<<"bug，head为不存在，tail存在"<<endl;
}else if(head && !tail){
cout<<"bug，head为存在，tail不存在"<<endl;
}else{
tail->next=node;
}
tail=node;
size++;
}


/** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
void addAtIndex(int index, int val) {
//思路：
//首先检验index是否有效
//只有三种插入情况，插入表头、表中、表尾
//new一个val值的节点
//再插入
if(index>=0 && index<=size){
Node *insNode=new Node(val);
if(index==0){//插入表头是什么条件
insNode->next=head;
head=insNode;
if(size==0){
tail=insNode;
}
size++;
}else if(index==size){//插入表尾是什么条件
addAtTail(val);
}else{//插入表中是什么条件
Node *node=head;
//遍历的目的是得到index前一个node
for(int j=1;j<index;j++){
node=node->next;
}
insNode->next=node->next;
node->next=insNode;
size++;
}

}
}

/** Delete the index-th node in the linked list, if the index is valid. */

void deleteAtIndex(int index) {
//        先验证index有效性
//三种情况，删头结点不需要遍历，直接改变head的值;删中间节点需要i遍历，不需要改变链表head或者tail的值；
//        删尾节点，需要先遍历再改变尾节点的值

if(index>=0 && index<size){
Node *node=head;
if(index==0){
head=head->next;
}else{
int j=1;
//遍历的目的是为了得到目标index上一个Node
while (node && j<index) {
node=node->next;
j++;
}
if(!node){
cout<<"node is null"<<endl;
}
if(!node->next){
cout<<"node->next is null"<<endl;
}
if(index==size-1){
node->next=nullptr;
tail=node;
}else{
node->next=node->next->next;
}
}
size--;
}
}


};


```

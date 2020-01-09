## 题目地址
https://leetcode-cn.com/problems/linked-list-cycle/

## 题目描述
```
Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

 

```   


## 思路
### 龟兔赛跑，兔子总能追上乌龟的  我在A分支上改了

``
无论是插入、删除、还是获取数据，都只有这三种情况。

``



## 自己出现的问题

- 怎么设定乌龟的速度？怎么设定兔子的速度？
- 临界值



## 代码
### 运行时间：8ms

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
/**
* Definition for singly-linked list.
* struct ListNode {
*     int val;
*     ListNode *next;
*     ListNode(int x) : val(x), next(NULL) {}
* };
*/
class Solution {
public:
bool hasCycle(ListNode *head) {
//双指针
//一个是快指针，一个是慢指针
//         快指针每次index+2，慢指针每次index+1
if(!head || !head->next){
return false;
}
ListNode *slow=head;
ListNode *fast=head->next;
while(slow!=fast){
if(!slow->next || !fast->next || !fast->next->next){
return false;
}
slow=slow->next;
fast=fast->next->next;

}
return true;



}
};


```

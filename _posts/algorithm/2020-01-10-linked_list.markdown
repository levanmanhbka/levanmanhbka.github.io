---
layout: post
title:  "Algorithm - Linked List"
date:   2020-01-01 21:03:36 +0530
tags: "algorithm linked list"
---

Linked list là bài số 2 trong loạt bài ôn lại thuật toán của mình, nó là nền tảng cho hàng loạt các cấu trúc dữ liệu như hashing, tree, tree-e, graph cùng với các thuật toán sau này. Linked List là mở rộng của mảng có đặc điểm: Số lượng phần tử không bị giới hạn, thêm và loại bỏ một phần tử là O(1), kiếm một phần tử là O(n). Các bài dưới đây là những bài mình đã thực hành trên trang [https://leetcode.com](https://leetcode.com/).

### 1. Convert binary number in a linked list to integer
```c++
/**
 * Date: 2019/01/01
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    int getDecimalValue(ListNode* head) {
        int value = 0;
        ListNode* node = head;
        while(node)
        {
            value = (value <<1) + node->val;
            node = node->next;
        }
        return value;
    }
};
```
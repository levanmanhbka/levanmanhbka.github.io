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

### 2. Find middle of the linked list
```c++
/*
 * Date: 2019/01/01
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* oneStep = head;
        ListNode* twoStep = head->next;
        while(twoStep != NULL)
        {
            twoStep = twoStep->next;
            if(twoStep == NULL)
            {
                return oneStep->next;
            }
            else
            {
                twoStep = twoStep->next;
                oneStep = oneStep->next;
            }
        }
        return oneStep;
    }
};
```

### 3. Delete node in linked list
```c++
/*
 * Date: 2019/01/01
 * Bài này mình thấy họ chỉ đưa ra cho mình node
 * không đưa ra giá trị của node cần xóa làm mình ban đầu loay hoay
 */
class Solution {
public:
    void deleteNode(ListNode* node) {
        ListNode* dNode = node->next;
        node->val = node->next->val;
        node->next = node->next->next;
        delete dNode;
    }
};
```
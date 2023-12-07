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
```

### 2. Find middle of the linked list
```c++
/*
 * Date: 2019/01/01
 */
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
```

### 3. Delete node in linked list
```c++
/*
 * Date: 2019/01/01
 * Bài này mình thấy họ chỉ đưa ra cho mình node
 * không đưa ra giá trị của node cần xóa làm mình ban đầu loay hoay
 */
void deleteNode(ListNode* node) {
    ListNode* dNode = node->next;
    node->val = node->next->val;
    node->next = node->next->next;
    delete dNode;
}
```

### 4. Determine if linked list is palindrome
```c++
/*
 * Date: 2019/01/02
 * [1, 0, 1] -> true
 * [1, 1] -> true
 * [1, 2, 3, 3, 2, 1] -> true
 */
bool isPalindrome(ListNode* head) {
    if(head == NULL)
        return true;
    ListNode* point = head;
    stack<int> mstack;
    
    while(point != NULL)
    {
        mstack.push(point->val);
        point = point->next;
    }
    
    point = head;
    while(point != NULL)
    {
        if(point->val != mstack.top())
            return false;
        mstack.pop();
        point = point->next;
    }
    
    return mstack.empty();
}
```

### 5. Remove zero sum consecutive nodes from linked list
Đây là một bài khá hay và mình đã tham khảo một lời giải sau đó code lại. Ý tưởng chính có một con trỏ pre luôn trỏ tới node sau cùng và chắc chắn không bị xóa. Vậy thời điểm ban đầu pre trỏ vào đâu ?
Ở thời điểm ban đầu mọi node đều có thể bị xóa nên chỉ còn cách tạo một node dummy và cho node này trỏ vào đầu linked list, đây chính là vị trí xuất phát của con trỏ pre
![link-list-remove-consecutive-elements.png!](/assets/images/algorithm/link-list-remove-consecutive-elements.png)
```c++
/*
 * Date: 2020/01/09
 */
 ListNode* removeZeroSumSublists(ListNode* head) {
        
    ListNode dummy = ListNode(0);
    dummy.next = head;
    ListNode* pre = &dummy;
    ListNode* p = head;

    while (p)
    {
        int sum = p->val;
        if (sum == 0)
        {
            pre->next = p->next;
            p = p->next;
            continue;
        }

        bool erase = false;
        ListNode * q = p->next;

        while (q)
        {
            sum += q->val;

            if (sum == 0)
            {
                erase = true;
                break;
            }
            q = q->next;
        }

        if (erase)
        {
            p = q->next;
            pre->next = q->next;
        }
        else
        {
            p = p->next;
            pre = pre->next;
        }
    }
    return dummy.next;
}
```

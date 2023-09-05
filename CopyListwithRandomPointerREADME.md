# leet-day53

# Copy Linked List with Random Pointers

## Problem Description

You are given a linked list where each node contains an additional random pointer, which can point to any node in the list, or it can be `null`. The task is to create a deep copy of the linked list, ensuring that the copied list represents the same state as the original list. Additionally, none of the pointers in the new list should point to nodes in the original list.

The linked list is represented as a list of nodes. Each node is represented as a pair `[val, random_index]`, where `val` is an integer representing `Node.val`, and `random_index` is the index of the node to which the `random` pointer points, or it's `null` if it doesn't point to any node.

## Example

### Input
```
head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

### Output
```
[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

## Constraints

- The number of nodes in the list is in the range `[0, 1000]`.
- The `val` of each node is in the range `[-104, 104]`.
- The `random` pointer is either `null` or points to some node in the linked list.

## Approach

We can solve this problem using a hash map (or dictionary) to keep track of the mapping between the original nodes and their corresponding new nodes. The algorithm can be divided into the following steps:

1. Initialize an empty hash map (`map<Node*, Node*> m`) to store the mapping between original and copied nodes.

2. Iterate through the original linked list to create new nodes. For each node `p` in the original list, create a new node with the same `val`, and add the mapping `m[p] = new Node(p->val)`.

3. Iterate through the original list again to set the `next` and `random` pointers for the new nodes. For each node `p` in the original list:
   - Set `m[p]->next` to `m[p->next]` (to connect the copied nodes in the `next` direction).
   - Set `m[p]->random` to `m[p->random]` (to copy the random pointers).

4. Return the head of the copied linked list, which is `m[head]`.

## Complexity Analysis

- Time complexity: O(N), where N is the number of nodes in the linked list. We perform two passes through the list.
- Space complexity: O(N), where N is the number of nodes in the linked list, as we use additional space to store the mapping between original and copied nodes.

---

### Code

Here is the C++ code that implements the above approach:

class Solution {
public:
    Node* copyRandomList(Node* head) {
        map<Node*, Node*> m;
        Node *p = head;
        while (p) {
            m[p] = new Node(p->val);
            p = p->next;
        }
        p = head;
        while (p) {
            m[p]->next = m[p->next];
            m[p]->random = m[p->random];
            p = p->next;
        }
        return m[head];
    }
};
```

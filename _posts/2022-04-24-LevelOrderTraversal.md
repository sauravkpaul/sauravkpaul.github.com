---
layout: post
title:  102. Binary Tree Level Order Traversal
categories: [BinaryTree, Queues]
---

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).
[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/).

## Solution using Queues

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> Q;
        if (!root) {
            return ans;
        }
        Q.push(root);
        int level = 0;
        while (!Q.empty()) {
            ans.push_back(vector<int> ());
            int size = Q.size();
            for(int i = 0 ; i < size; i++) {
                TreeNode* node = Q.front(); Q.pop();
                ans[level].push_back(node->val);
                if(node->left)
                    Q.push(node->left);
                if(node->right)
                    Q.push(node->right);
            }
            level++;
        }
        return ans;
    }
};
```

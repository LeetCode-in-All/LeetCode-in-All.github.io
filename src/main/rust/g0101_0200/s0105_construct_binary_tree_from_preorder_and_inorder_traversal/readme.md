[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 105\. Construct Binary Tree from Preorder and Inorder Traversal

Medium

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]

**Output:** [3,9,20,null,null,15,7]

**Example 2:**

**Input:** preorder = [-1], inorder = [-1]

**Output:** [-1]

**Constraints:**

*   `1 <= preorder.length <= 3000`
*   `inorder.length == preorder.length`
*   `-3000 <= preorder[i], inorder[i] <= 3000`
*   `preorder` and `inorder` consist of **unique** values.
*   Each value of `inorder` also appears in `preorder`.
*   `preorder` is **guaranteed** to be the preorder traversal of the tree.
*   `inorder` is **guaranteed** to be the inorder traversal of the tree.

## Solution

```rust
// Definition for a binary tree node.
// pub struct TreeNode {
//   pub val: i32,
//   pub left: Option<Rc<RefCell<TreeNode>>>,
//   pub right: Option<Rc<RefCell<TreeNode>>>,
// }
// 
// impl TreeNode {
//   #[inline]
//   pub fn new(val: i32) -> Self {
//     TreeNode {
//       val,
//       left: None,
//       right: None
//     }
//   }
// }
use std::collections::HashMap;
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
	pub fn build_tree(preorder: Vec<i32>, inorder: Vec<i32>) -> Option<Rc<RefCell<TreeNode>>> {
		let mut map = HashMap::new(); // Creating map
		let n = inorder.len(); 
		for i in 0..n {
			map.insert(inorder[i], i); // storing index of inorder value for later purpose
		}
		return Self::f(0, n-1, 0, n-1, &preorder, &inorder, &map);  
	}
	fn f(pre_st:usize,pre_en:usize,in_st:usize,in_en:usize,preorder:&Vec<i32>,
		inorder:&Vec<i32>,map:&HashMap<i32,usize>)->Option<Rc<RefCell<TreeNode>>> {
			if pre_st > pre_en || in_st > in_en {return None;} // if there is no node to make return none
			let root = Rc::new(RefCell::new(TreeNode{ val : preorder[pre_st], left : None, right : None}));
			let ind = map.get(&root.borrow().val); // using the map to get the index of root in inorder vector
			let len = ind.unwrap() - in_st; // lenght of left subtree
			root.borrow_mut().left = Self::f(pre_st+1,pre_st+len,in_st,ind.unwrap()-1,preorder,inorder,map);
			root.borrow_mut().right = Self::f(pre_st+len+1,pre_en,ind.unwrap()+1,in_en,preorder,inorder,map);
			return Some(root);
	}
}
```
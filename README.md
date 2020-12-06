# Binary Search Tree

Binary Search Tree in Swift.

A Binary Search Tree (BST) is a Binary Tree with the following restrictions: 

* All the values in nodes to the left subtree of the root must be less than the roots' value.
* All the values in nodes to the right subtree of the root must be greater than the roots' value. 

```swift 
/*
 Valid Binary Search Tree
        10
       /  \
     7     13
   /  \   /  \
  5    9 11   16
  
 Invalid Binary Search Tree
        4
      /   \
     13     1
   /  \   /  \
  2    9 5    3
*/
```

> Insertion, search and deletion on a Binary Search Tree is logorithmic `O(log n)` making it a very efficient data structure. 

## Objectives 

* To be able to **insert** a new node into a Binary Search Tree. 
* To be able to **search** for a given node in a Binary Search Tree. 
* To be able to **delete** a given value from a Binary Search Tree. 

[Link to completed Binary Search Tree](https://repl.it/@alexpaul/BinarySearchTree#main.swift)

## 1. Binary Tree Node 

```swift 
class BinaryTreeNode {
  var value: Int
  var leftChild: BinaryTreeNode?
  var rightChild: BinaryTreeNode?
  init(_ value: Int) {
    self.value = value
  }
}
```

## 2. Insert

![insertion in a BST](https://user-images.githubusercontent.com/1819208/100107840-17f65d00-2e38-11eb-86d9-9b1739a8905c.PNG)

#### Algorithm to insert values into a Binary Search Tree. 

1. If the tree is empty the new node becomes the root. 
2. If the value is less than the root and the root does not have a left child, insert the new node at the left child. 
3. If the root does have a left child, keep doing the above steps recursively until there is no left child, then insert new node. 
4. If the value is greater than the root and the root does not have a right child, insert the new node at the right child. 
5. If the root does have a right child, keep doing the above steps recursively until there is no right child, then insert new node. 


```swift 
func insert(_ root: BinaryTreeNode?, _ value: Int) -> BinaryTreeNode? {
  // 1. - create the new node
  let newNode = BinaryTreeNode(value)
  
  // 2. - if the tree is empty, newNode becomes the root
  guard let root = root else {
    return newNode
  }
  
  // 3. - if value is less than root's value go left
  if value < root.value {
    if root.leftChild == nil {
      root.leftChild = newNode
      return root
    } else {
      insert(root.leftChild, value)
    }
  }
  
  // 4. - if value is greater than root's value go right
  if value > root.value {
    if root.rightChild == nil {
      root.rightChild = newNode
      return root
    } else {
      insert(root.rightChild, value)
    }
  }
  
  return root
}
```

## 3. Traverse

```swift 
func inOrderTraversal(_ root: BinaryTreeNode?) {
  guard let root = root else { return }
  inOrderTraversal(root.leftChild)
  print(root.value, terminator: " ") // "\n" => " "
  inOrderTraversal(root.rightChild)
}

let rootNode = insert(nil, 10)
insert(rootNode, 13)
insert(rootNode, 7)
insert(rootNode, 5)
insert(rootNode, 11)
insert(rootNode, 9)
insert(rootNode, 16)

/*
        10
       /  \
     7     13
   /  \   /  \
  5    9 11   16
*/

inOrderTraversal(rootNode) // 5 7 9 10 11 13 16
```

## 4. Search 

![search sketch](https://user-images.githubusercontent.com/1819208/99878738-6fe15980-2bd5-11eb-9980-372f9ff77293.jpg)

#### Algorithm to search for a value in a Binary Search Tree. 

* If the root value equals to the search value, return true. 
* If the value is less than the root value, search left subtree recursively. 
* If the value is greater than the root value, search the right subtree recursively. 

```swift 
func search(_ root: BinaryTreeNode?, _ value: Int) -> Bool {
  // 1. check if the tree is empty
  guard let root = root else {
    return false
  }
  
  // 2. if the value equal to the root, return true
  if root.value == value {
    return true
  }
  
  // 3. navigate to the left subtree if the value is
  //    less than the root's value
  if value < root.value { // traverse left recursively
    return search(root.leftChild, value)
  }
  
  // 4. navigate to the right subtree if the value is greater than the
  //    root's value
  if value > root.value { // traverse right recursively
    return search(root.rightChild, value)
  }
  
  // 5. value does not exist in the tree
  return false
}

/*
        10
       /  \
     7     13
   /  \   /  \
  5    9 11   16
*/

search(rootNode, 7) // true 
```

## 5. Minimum value in a Binary Search Tree 

To find the minimum value in a Binary Search Tree the left subtree is visited recursively until the last leaf. This leaf node holds the minimum value by the nature of a Binary Search Tree. 

```swift 
func minValue(_ root: BinaryTreeNode?) -> Int {
  guard let root = root else { return 0 }
  if let leftChild = root.leftChild {
    return minValue(leftChild)
  }
  return root.value
}
```

#### Challenge: Write a function to find the maximum value in a Binary Search Tree? 

## 6. Delete 

![Deleing from a BST](https://user-images.githubusercontent.com/1819208/100540554-fb796c80-320b-11eb-8cf1-25942c87a5b1.jpg)

#### Algorithm to delete a node from a Binary Search Tree. 

* If the node is a leaf, simple delete that node. 
* If the node has one child, copy the child's value to the node then delete the child. 
* If the node has two children, first copy the value of its the in-order successor of the node to be deleted (the in-order successor as in the sketch above of the 10 node will be 11), then delete the the in-order successor. 

```swift 
func delete(_ root: BinaryTreeNode?, _ value: Int) -> BinaryTreeNode? {
  // 1.
  // tree is empty return nil
  guard let root = root else { return nil }
  
  // 2.
  // value is less than root, delete and assign leftChild its new value
  if value < root.value {
    root.leftChild = delete(root.leftChild, value) // e.g returns nil to 7 node if deleting 5
  }
  
  // 3.
  // value is greater than root, delete and assign rightChild's its new value
  else if value > root.value {
    root.rightChild = delete(root.rightChild, value)
  }
  
  // 4.
  // value is equal to the roots value
  else {
    // 5.
    // one child
    if root.leftChild == nil {
      return root.rightChild
    } else if root.rightChild == nil {
      return root.leftChild
    }
    
    // 6.
    // two children
    // we use a helper function to get the in-order successor e.g if deleting 10 the in-order successor would be 11
    // we first copy the in-order succsssor to the root
    // then we delete the value we copied from the right subtree 
    root.value = minValue(root.rightChild)
    root.rightChild = delete(root.rightChild, root.value)
  }
  
  return root
}

/*
        10
       /  \
     7     13
   /  \   /  \
  5    9 11   16
*/


delete(rootNode, 5)
inOrderTraversal(rootNode) // 7 9 10 11 13 16
print()

delete(rootNode, 7)
inOrderTraversal(rootNode) // 9 10 11 13 16
print()

delete(rootNode, 10)
inOrderTraversal(rootNode) // 9 11 13 16

```

```swift 
func minValue(_ root: BinaryTreeNode?) -> Int {
  guard let root = root else { return 0 }
  if let leftChild = root.leftChild {
    return minValue(leftChild)
  }
  return root.value
}
```

## 7. Convert an array to a Binary Search Tree 

![array to BST sketch](https://user-images.githubusercontent.com/1819208/101278698-50c4f900-378b-11eb-9575-9103d15de003.jpg)

```swift 
func convertToBST(_ arr: [Int], _ low: Int, _ high: Int, _ root: BinaryTreeNode?) -> BinaryTreeNode? {
  // 1. - base case when we have one node 
  if low > high { 
    return root
  }
  // 2. - calculate the middle index
  let midIndex = (low + high) / 2 
  
  // 3. - create the new root from the middle index
  let root = BinaryTreeNode(arr[midIndex])
  
  // 4. - recursively perform conversion on the left subtree 
  root.left = convertToBST(arr, low, midIndex - 1, root.left)
  
  // 5. - recursively perform conversion on the right subtree
  root.right = convertToBST(arr, midIndex + 1, high, root.right)
  
  // 6. - return the converted BST 
  return root
}

let arr = [3, 10, 7, 5, 1].sorted() 
let bst = convertToBST(arr, 0, arr.count - 1, nil)
inOrderTraversal(bst) // 1 3 5 7 10
```

#### Challenge: convert a degenerate BST or a non-balanced BST to a balanced Binary Search Tree

```swift 
             89                                  20 
            /                                 /     \
           66                               12      66
          /                                /  \    /   \
         34                               5   17  34   89   height = 3
        /
       20                  => 
      /
     17
    /
   12
  /
 5  height = 7
```

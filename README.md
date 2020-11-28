# Binary Search Tree

Binary Search Tree in Swift.

A Binary Search Tree (BST) is a Binary Tree with the following restrictions: 

* All the values in nodes to the root's left subtree must be less than the root's value. 
* All the values in nodes to the root's right subtree must be greater than the root's value. 

## Objectives 

* To be able to insert a new node into a Binary Search Tree. 
* To be able to search for a given node in a Binary Search Tree. 
* To be able to delete a given value from a Binary Search Tree. 

## Binary Tree Node 

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

## Insert

![insertion in a BST](https://user-images.githubusercontent.com/1819208/100107840-17f65d00-2e38-11eb-86d9-9b1739a8905c.PNG)

Algorithm to insert values into a Binary Search Tree. 

1. If the tree is empty the new node becomes the root. 
2. If the value is less than the root and the root does not have a left child, insert the new node at the left child. 
3. If the root does have a left child, keep doing the above steps recursively until there is no left child, then insert new node. 
4. If the value is greater than the root and the root does not have a right child, insert the new node at the right child. 
5. If the root does have a right child, keep doing the above steps recursively until there is no right child, then insert new node. 


```swift 
func insert(_ treeNode: BinaryTreeNode?, _ value: Int) -> BinaryTreeNode? {
  // 1. - create the new node
  let newNode = BinaryTreeNode(value)
  
  // 2. - if the tree is empty, newNode becomes the root
  guard let treeNode = treeNode else {
    return newNode
  }
  
  // 3. - if value is less than root's value go left
  if value < treeNode.value {
    if treeNode.leftChild == nil {
      treeNode.leftChild = newNode
      return treeNode
    } else {
      insert(treeNode.leftChild, value)
    }
  }
  
  // 4. - if value is greater than root's value go right
  if value > treeNode.value {
    if treeNode.rightChild == nil {
      treeNode.rightChild = newNode
      return treeNode
    } else {
      insert(treeNode.rightChild, value)
    }
  }
  
  return treeNode
}
```

## Traverse

```swift 
func inOrderTraversal(_ treeNode: BinaryTreeNode?) {
  guard let treeNode = treeNode else { return }
  if let leftChild = treeNode.leftChild {
    inOrderTraversal(leftChild)
  }
  print(treeNode.value, terminator: " ") // "\n" => " "
  if let rightChild = treeNode.rightChild {
    inOrderTraversal(rightChild)
  }
}

let treeNode = insert(nil, 10)
insert(treeNode, 13)
insert(treeNode, 7)
insert(treeNode, 5)
insert(treeNode, 11)
insert(treeNode, 9)
insert(treeNode, 16)

/*
        10
       /  \
     7     13
   /  \   /  \
  5    9 11   16
*/

inOrderTraversal(treeNode) // 5 7 9 10 11 13 16
```

## Search 

![](https://user-images.githubusercontent.com/1819208/99878738-6fe15980-2bd5-11eb-9980-372f9ff77293.jpg)

Algorithm to insert values into a Binary Search Tree. 

* If the root value equals to the search value, return true. 
* If the value is less than the root value, search left subtree recursively. 
* If the value is greater than the root value, search the right subtree recursively. 

```swift 
func search(_ treeNode: BinaryTreeNode?, _ value: Int) -> Bool {
  // 1. check if the tree is empty
  guard let treeNode = treeNode else {
    return false
  }
  
  // 2. if the value equal to the root, return true
  if treeNode.value == value {
    return true
  }
  
  // 3. navigate to the left subtree if the value is
  //    less than the root's value
  if value < treeNode.value { // traverse left recursively
    return search(treeNode.leftChild, value)
  }
  
  // 4. navigate to the right subtree if the value is greater than the
  //    root's value
  if value > treeNode.value { // traverse right recursively
    return search(treeNode.rightChild, value)
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

search(treeNode, 7) // true 
```

## Minimum value in a Binary Search Tree 

```swift 
func minValue(_ treeNode: BinaryTreeNode?) -> Int {
  if treeNode == nil {
    return 0
  }
  if treeNode?.leftChild != nil {
    return minValue(treeNode?.leftChild)
  }
  return treeNode!.value
}
```

## Delete 

![Deleing from a BST](https://user-images.githubusercontent.com/1819208/100452792-d6f48780-3087-11eb-9651-642539fdffb7.jpg)

```swift 
func delete(_ treeNode: BinaryTreeNode?, _ value: Int) -> BinaryTreeNode? {
  // 1.
  // tree is empty return nil
  guard let treeNode = treeNode else { return nil }
  
  // 2.
  // value is less than root, delete and assign leftChild its new value
  if value < treeNode.value {
    treeNode.leftChild = delete(treeNode.leftChild, value) // e.g returns nil to 7 node if deleting 5
  }
  
  // 3.
  // value is greater than root, delete and assign rightChild's its new value
  else if value > treeNode.value {
    treeNode.rightChild = delete(treeNode.rightChild, value)
  }
  
  // 4.
  // value is equal to the roots value
  else {
    // 5.
    // one child
    if treeNode.leftChild == nil {
      return treeNode.rightChild
    } else if treeNode.rightChild == nil {
      return treeNode.leftChild
    }
    
    // 6.
    // two children
    // we use a helper function to get the in-order successor e.g if deleting 10 the in-order successor would be 11
    // we first copy the in-order succsssor to the root
    // then we delete the value we copied from the right subtree 
    treeNode.value = minValue(treeNode.rightChild)
    treeNode.rightChild = delete(treeNode.rightChild, treeNode.value)
  }
  
  return treeNode
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
func minValue(_ treeNode: BinaryTreeNode?) -> Int {
  if treeNode == nil {
    return 0
  }
  if treeNode?.leftChild != nil {
    return minValue(treeNode?.leftChild)
  }
  return treeNode!.value
}
```

## Resources 

1. [GeeksForGeeks - Delete a node from a BST](https://www.geeksforgeeks.org/binary-search-tree-set-2-delete/)
2. [GeeksForGeeks - Sorted Array to Balanced BST](https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/?ref=lbp)

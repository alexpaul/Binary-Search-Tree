# Binary Search Tree

Binary Search Tree in Swift.

A Binary Search Tree (BST) is a Binary Tree with the following restrictions: 

* All the values in nodes to the root's left subtree must be less than the root's value. 
* All the values in nodes to the root's right subtree must be greater than the root's value. 

## Types of Trees 

```swift 
        
          12
         /  \
        10  15
        
        
          12
         /  \
        10  15
        
        
          12
         /  \
        10  15
```

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

![insertion in a BST](https://user-images.githubusercontent.com/1819208/99795727-47386180-2afa-11eb-9e6c-a809d0645c62.jpg)

Algorithm to insert values into a Binary Search Tree. 

1. If the tree is empty the new node becomes the root. 
2. If the value is less than the root and the root does not have a left child, insert the new node at the left child. 
3. If the root does have a left child, keep doing the above steps recursively until there is no left child, then insert new node. 
4. If the value is greater than the root and the root does not have a right child, insert the new node at the right child. 
5. If the root does have a right child, keep doing the above steps recursively until there is no right child, then insert new node. 


```swift 
func insert(_ rootNode: BinaryTreeNode?, _ value: Int) -> BinaryTreeNode? {
  let newNode = BinaryTreeNode(value)
  guard let _ = rootNode else {
    return newNode
  }
  
  if value < rootNode!.value {
    if rootNode?.leftChild == nil {
      rootNode?.leftChild = newNode
      return rootNode
    } else {
      insert(rootNode?.leftChild, value)
    }
  }
  
  if value > rootNode!.value {
    if rootNode?.rightChild == nil {
      rootNode?.rightChild = newNode
      return rootNode
    } else {
      insert(rootNode?.rightChild, value)
    }
  }
  
  return rootNode
}
```

## Traverse

```swift 
func inOrderTraversal(_ rootNode: BinaryTreeNode?) {
  guard let _ = rootNode else { return }
  if let leftChild = rootNode?.leftChild {
    inOrderTraversal(leftChild)
  }
  print(rootNode!.value, terminator: " ")
  if let rightChild = rootNode?.rightChild {
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
  guard let _ = treeNode else {
    return false
  }
  if treeNode!.value == value {
    return true
  }
  if value > treeNode!.value {
    return search(treeNode?.rightChild, value)
  } else if value < treeNode!.value {
    return search(treeNode?.leftChild, value)
  }
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

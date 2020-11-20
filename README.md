# Binary-Search-Tree

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
class BinaryTreeNode<T> {
  var value: T
  var leftChild: BinaryTreeNode?
  var rightChild: BinaryTreeNode?
  init(_ value: T) {
    self.value = value
  }
}
```

## Insert

![insertion in a BST](https://user-images.githubusercontent.com/1819208/99793072-135b3d00-2af6-11eb-9e41-bbc429a892c7.jpg)

Algorithm to insert values into a Binary Search Tree. 

* In the tree is empty the new value becomes the root. 
* 

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

inOrderTraversal(treeNode) // 5 7 9 10 11 13 16
```

## Search 

```swift 
```

## Delete 

```swift 
```

## Height

```swift 
```

## Balanced 

```swift 
```

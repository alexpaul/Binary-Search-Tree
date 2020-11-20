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
    rootNode?.leftChild = newNode
  }
  
  if value > rootNode!.value {
    rootNode?.rightChild = newNode
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
  print(rootNode!.value)
  if let rightChild = rootNode?.rightChild {
    inOrderTraversal(rightChild)
  }
}

let treeNode = insert(nil, 12)
insert(treeNode, 10)
insert(treeNode, 15)

inOrderTraversal(treeNode) // 10 12 15
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

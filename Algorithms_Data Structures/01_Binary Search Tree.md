## Binary Search Tree

![binary_search_tree](https://miro.medium.com/max/1400/1*tUBYCHi32Zj0B2UCw0qmlA.png);

- A tree data structure is a way to hold data that when visualized, looks like a tree
  - All *data points* in the tree are called *nodes*
  - Top node is the *root*
  - Nodes with branches leading to other nodes are referred to as the *parent* nodes
  - *Leaf* nodes are nodes at the end of the tree that have *no children*

- Binary tree can only have *up to two branches* for every node
  - Binary search trees are *ordered*
  - Each *left subtree* is less than or equal to the parent node
  - Each *right subtree* is greater than or equal to the parent node

- Using the binary search principle, average operations are able to skip about half of the tree
  - Each lookup, insertion or deletion takes time proportional to the logarithm of the number of items stored in the tree
    - Better than the linear time required to find items by key in an unsorted array
    - Slower than the corresponding operations on the hash table

- *Minimum* is always on the bottom left side of the tree

- *Maximum* is always on the bottom right side of the tree

```js
// Node class represents each node in the tree with 3 data properties
//  data: data we are actually trying to store
//  left/right: left/right nodes of the parent node
class Node {
  constructor(data, left = null, right = null) {
    this.data = data;
    this.left = left;
    this.right = right;
  }
}

// Binary Search Tree class
class BST {
  constructor () {
    this.root = null; // creates the top (root) node
  }

  // to add to the tree
  add(data) {
    const node = this.root; // references to the root node

    // if the first node (i.e. root) => null
    //  set root node to the new data that was just put in
    if (node === null) {
      this.root = new Node(data); // this.root in the constructor becomes the value of data
      return; // tree is created with one node
    } else { // if not the first node
      //  use resursive function searchTree
      const searchTree = function (node) { // function expression
        if (data < node.data) { // input data less than data in node object => goes to left node
          if (node.left === null) { // if left node is null => sets the left node
            node.left = new Node(data);
            return;
          } else if (node.left !== null) { // if left node exists, run searchTree again
            return searchTree(node.left); // recursive nature until new left node is created
          }
        } else if (data > node.data) { // input data greater than data in node object => goes to right node
          if (node.right === null) { // if right node is null => sets the right node
            node.right = new Node(data);
            return;
          } else if (node.right !== null) { // if right node exists, run searchTree again
            return searchTree(node.right); // recursive nature until new right node is created
          }
        } else {
          return null;
        }
      };

      return searchTree(node); // runs searchTree function in else statement
    }
  }

  // finds the minimum value in the tree
  findMin() {
    let current = this.root; // set the current as the whole tree
    
    // runs as long as there is a left node
    while (current.left !== null) {
      current = current.left;
    }
    
    // current becomes the node in the bottom left side of the tree
    // current.data is that node
    return current.data;
  }

  // finds the maximum value in the tree
  findMax() {
    let current = this.root;

    while (current.right !== null) {
      current = current.right;
    }

    return current.data;
  }

  // finds a value in the tree
  find(data) {
    let current = this.root;

    // runs as long as current.data does not match the input data
    while (current.data !== data) {
      if (data < current.data) {
        current = current.left;
      } else {
        current = current.right;
      }

      if (current === null) {
        return null;
      }
    }

    return current;
  }

  // checks whether a value is present in the tree
  isPresent(data) {
    let current = this.root;

    while(current) {
      if (data === current.data) {
        return true;
      }

      if (data < current.data) {
        current = current.left;
      } else {
        current = current.right;
      }
    }

    return false;
  }

  // removes a value from the tree
  remove(data) {
    const removeNode = function(node, data) {
      // check for empty tree
      if (node === null) {
        return null;
      }

      // 
      if (data === node.data) {
        // node has no children
        if (node.left === null && node.right === null) {
          return null;
        }

        // node has no left child
        if (node.left === null) {
          return node.right;
        }

        // node has no right child
        if (node.right === null) {
          return node.left;
        }

        // node has two children
        // from the node being removed
        //  go to the right node
        //  then all the way down to the most left sub node
        let tempNode = node.right

        // runs until there is no left node and sets the last left node as tempNode
        while (tempNode.left !== null) {
          tempNode = tempNode.left;
        }

        node.data = tempNode.data
        node.right = removeNode(node.right, tempNode.data); // recursive nature
        
        return node;
      } else if (data < node.data) {
        node.left = removeNode(node.left, data);
        
        return node;
      } else {
        node.right = removeNode(node.right, data);

        return node;
      }
    }

    this.root = removeNode(this.root, data);
  }
}
```
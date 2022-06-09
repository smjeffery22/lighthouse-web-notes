# STACKS

- Stacks are *Last In, First Out (LIFO)* type of service
  - Last item that was put in the stack would be the first one to be taken off the stack
  - Ex. Browser's back button
    - Visit a new website  => stack.push()
    - Pressing back button => stack.pop()

## Functions in Stack

- **Push:** placing data onto a stack
- **Pop:** removing the top element of a stack
- **Peek:** displaying the top element of a stack
- **Length:** determining how many elements are on a stack

- In JS, array object already has all the functions to use it as a stack
  - Can use array as a stack

## Palindrome

```js
const letters = []; // this is our stack
const word = 'racecar';
let rword = '';

// put letters of word into stack
for (let i = 0; i < word.length; i++) {
  letters.push(word[i]);
}

// pop off the stack in reverse order
for (var i =0; i < word.length; i++) {
  rword += letters.pop();
}

if (rword === word) {
  console.log(`${word} is a palindrome!`);
} else {
  console.log(`${word} is not a palindrome!`);
}
```

## Implementing Stack in JS

```js
// creates a stack
const Stack = function () {
  this.count = 0; // keeps track of how many items there are in the stack
  this.storage = {};

  // adds a value onto the end of the stack
  this.push = function (value) {
    this.storage[this.count] = value; // add the value at index 'this.count'
    this.count++; // increment count by 1 to show that there is another item in the stack
  }

  // removes and returns the value at the end of the stack
  this.pop = function () {
    if (this.count === 0) return undefined; // nothing in the stack

    this.count--; // because count is 1 greater than the last index in stack

    const result = this.storage[this.count]; // last item in the stack
    delete this.storage[this.count]; // delete the last item

    return result;
  }

  // returns the size of the stack
  this.size = function () {
    return this.count;
  }

  // returns the value at the end of the stack
  this.peek = function () {
    return this.storage[this.count - 1];
  }
}

myStack.push(2);
myStack.push(4);
myStack.push(6);
myStack.push(8);
console.log(myStack.showStack()); // { '0': 2, '1': 4, '2': 6, '3': 8 }
console.log('removed:', myStack.pop()); // 8
console.log(myStack.showStack()); // { '0': 2, '1': 4, '2': 6 }
console.log('size:', myStack.size()); // 3
console.log('last element:', myStack.peek()); // 6
```

## Sets

- Set data structure is kind of like an array
  - No duplicate items
  - Values are not in any particular order
  - Ex. to check for the presence of an item 

```js
function mySet () {
  // collection will hold the set
  const collection = [];

  // checks for the presence of an element and return true/false
  this.has = function (element) {
    return (collection.indexOf(element) !== -1); // if element not in collection, left side returns -1
  };

  // returns all the values in the set
  this.values = function () {
    return collection;
  };

  // adds an element to the set
  this.add = function (element) {
    // uses the 'has' method defined above
    // if element doesn't exist in collection, push in the element
    if (!this.has(element)) {
      collection.push(element);
      return true;
    }
    return false;
  };

  // removes an element from a set
  this.remove = function (element) {
    if (this.has(element)) {
      index = collection.indexOf(element); // finds the index of the element
      collection.splice(index, 1); // remove the element from the collection
      return true;
    }
    return false;
  };

  // returns the size of the collection
  this.size = function () {
    return collection.length;
  };

  /*
   * all the methods above are included in ES6 implementation of the set
   *  except 'remove' is 'delete'
   *  'size' is a property, not a method so it can be called without ()
   */

  /* below are not included in ES6 set */

  // returns the union of two sets without duplicates
  this.union = function (otherSet) {
    const unionSet = new mySet();
    const firstSet = this.values();
    const secondSet = otherSet.values();

    firstSet.forEach(function (e) {
      unionSet.add(e); // adds all the values from the firstSet into unionSet
    });
    secondSet.forEach(function (e) {
      unionSet.add(e); // adds all the values from the secondSet, but does not add the duplicates
    });

    return unionSet;
  }

  // returns the intersection of two sets as a new set
  this.intersection = function (otherSet) {
    const intersectionSet = new mySet();
    const firstSet = this.values();

    firstSet.forEach(function (e) {
      // if the other set has the element, add the element
      if (otherSet.has(e)) {
        intersectionSet.add(e);
      }
    });

    return intersectionSet;
  }

  // returns the difference of the two sets as a new set
  this.difference = function (otherSet) {
    const differenceSet = new mySet();
    const firstSet = this.values();

    firstSet.forEach(function (e) {
    // if the other set does not have the element, add the element
      if (!otherSet.has(e)) {
        differenceSet.add(e);
      }
    });

    return differenceSet;
  }

  // tests if the set is a subset of a different set
  this.subset = function (otherSet) {
    const firstSet = this.values();

    // checks if all the elements pass the test case
    //  are all the elements in the firstSet also in the otherSet
    return firstSet.every(function(value) {
      return otherSet.has(value);
    })
  }
}
```

## Queues

- Queue data structure is a way to hold the data, similar to stack
  - Stack is FILO
  - Queue is *First In, First Out (FIFO)*
    - In checkout lane => first person in line is the first one out
    - Print queue => first to print gets theirs printed first

```js
function Queue () {
  const collection = [];

  this.print = function () {
    console.log(collection);
  };

  // adds an element at the end of the array
  this.enqueue = function (element) {
    collection.push(element);
  };

  // removes an element from the beginning of the array
  this.dequeue = function () {
    return collection.shift();
  };

  // prints the first item in queue
  this.front = function () {
    return collection[0];
  };

  this.size = function () {
    return collection.length;
  };

  this.isEmpty = function () {
    return (collection.length === 0);
  };
}
```

```js
// elements with priority are sent to the beginning of the queue
function PriorityQueue() {
  const collection = [];

  this.printCollection = function () {
    console.log(collection);
  };

  this.enqueue = function (element) {
    if (this.isEmpty()) {
      collection.push(element); // push the element if the collection is empty
    } else {
      let added = false;

      for (let i = 0; i < collection.length; i++) {
        // checks the priority
        // if the priority of the element is less than the collection element's priority
        //  add the element to the collection at that index
        // if same priority, add the element following the previous same priority element
        if (element[1] < collection[i][1]) {
          collection.splice(i, 0, element);
          added = true;
          break;
        }
      }

      // if the element has not been added, add it to the collection
      if (!added) {
        collection.push(element);
      }
    }
  }

  this.dequeue = function () {
    const value = collection.shift();
    return value[0]; // return the item without the priority number
  };

  this.front = function () {
    return collection[0];
  };

  this.size = function () {
    return collection.length;
  };

  this.isEmpty = function () {
    return (collection.length === 0);
  }
}

const pq = new PriorityQueue();

console.log(pq);
console.log(pq.printCollection());

pq.enqueue(['Beau Carnes', 2]);
pq.enqueue(['Quincy Larson', 3]);
pq.enqueue(['Ewa Mitulska', 1]);
console.log(pq.printCollection());
console.log(pq.dequeue());
console.log(pq.printCollection());
console.log(pq.front());
pq.enqueue(['Jeffery Park', 2]);
console.log(pq.printCollection());
```
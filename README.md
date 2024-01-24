# UOP_COMP53

# 1. Introduction to Data Structures and Algorithm
## 1.1 Data Structure
A data structure is a way of organizing, stroring, and performing operations on data. Operations performed on a data structure include accessing or updating stored data, searching for specific data, inserting new data, and removing data.
![](./basicDataStructures.png) 

- A linked list stores an ordered list of items. The links in each node define the order in which items are stored.
- A binary tree node can have no children, a single left or right child, or both a left and right child.
- The data stored in a list node can be a record with multiple subitems. Ex: A linked list storing employee data might use a record containing the employee's name, title, and salary. Also, the list node itself can be implemented as a record, having subitems for the data and the pointer to the next node.
- Array elements are stored in sequential locations, so can be easily accessed using an index.

### Choosing data structures
The selection of data structures used in a program depends on both the type of data being stored and the operations the program may need to perform on that data. Choosing the best data structure often requires determining which data structure provides a good balance given expected uses.

For example, a program requires insertion of a new data, a linked list may be a better choice than an array
Inserting an item at a specific location in an array requires making room for the item by shifting higher-indexed items. Once the higher index items have been shifted, the new item can be inserted at the desired index.
To insert new item in a linked list, a list node for the new item is first created. Item B's next pointer is assigned to point to item C. Item A's next pointer is updated to point to item B. No shifting of other items was required.

## 1.2 Introduction to algorithim
### Algorithm
An algorithm describes a sequence of steps to solve a computational problem or perform a calculation. An algorithm can be described in English, pseudocode, a programming language, hardware, etc. A computational problem specifies an input, a question about the input that can be answered using a computer, and the desired output.

### Practical applications of algorithms
Computational problems can be found in numerous domains, including e-commerce, internet technologies, biology, manufacturing, transportation, etc. Algorithms have been developed for numerous computational problems within these domains.
![](./commonAlgorithms.png)

### Efficient algorithms and hard problems
Computer scientists and programmers typically focus on using and designing efficient algorithms to solve problems. Algorithm efficiency is most commonly measured by the algorithm runtime, and an efficient algorithm is one whose runtime increases no more than polynomially with respect to the input size. However, some problems exist for which an efficient algorithm is unknown.

NP-complete problems are a set of problems for which no known efficient algorithm exists. NP-complete problems have the following characteristics:

No efficient algorithm has been found to solve an NP-complete problem.
No one has proven that an efficient algorithm to solve an NP-complete problem is impossible.
If an efficient algorithm exists for one NP-complete problem, then all NP-complete problems can be solved efficiently.
By knowing a problem is NP-complete, instead of trying to find an efficient algorithm to solve the problem, a programmer can focus on finding an algorithm to efficiently find a good, but non-optimal, solution.

## 1.3 Relation between data structures and algorithms

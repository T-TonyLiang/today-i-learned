# CS 240E: Data Structures and Data Management
Instructor: Prabhakar Ragde

Persistent Data Structure:
  - Access to all past versions
  - A purely functional approach guarantees persistence
  - Sometimes mutation can be used to improve efficiency
  - The array implementation of the mutable Sequence ADT is efficient
    - All operations are constant time
  - But for our list-based implementation, the index operation takes time O(min{i,n})
    - Can we do better?

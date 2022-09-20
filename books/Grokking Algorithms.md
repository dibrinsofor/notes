# Grokking Algorithms: An illustrated guide for programmers and other curious people

>Context is everything with algorithms. Knowing whether to use BFS or Djikstra's Algorithms is determined by context (the presence of weighted edges) just like choosing to run in a straight line as opposed to in a zig-zag is dependent on context (whether you are being shot at or running into the arms of a loved one). 

>Big O measures the space and time complexity of an algorithm as its input size grows (aka the most optimal solution per context).

<details>
<summary>Chapter 1 Introduction to Algorithms</summary>

If you had to search through a sorted input (or lookup a word in a dictionary) there are a couple techniques you could employ. You could certainly:
- start from the first word in the book and skim through till you find your desired word. Now this is great if you have to lookup "aardvark" or some other "A" word but imagine if you have to lookup a word that starts with "Z" this technique would be very slow `0(n)`
- a more optimal solution would be to adopt Binary Search -- start from the middle of the dictionary and keep splitting halves as you move left or right till you find your word. This technique requires you to scan through fewer words and still arrive at the desired word. This approach is much faster `0(logn)`

> Binary search does not work with unsorted inputs. So if you had to find the 49 from this lot [1, 47, 2, 49, 3, 51, 4] you'd have to adopt some other technique. See where and how it shines though, [1, 2, 3, 4, 47, 49, 51] we could go directly to the middle of the set (4) and we ask ourselves "is the number we're looking for bigger or smaller than 4?" if it's bigger we go straight to right and repeat the process asking ourselves "is this our desired out put or is this number higher or lower?". In this case we acc only need to look at two numbers to get our output (4, 49). Compare that to the other approach where we would need to look through (1, 2, 3, 4, 47, 49)
</details>

<details>
<summary>Chapter 2 Selection Sort</summary>

> Inspired by Adit's style, I attempted a ton of sketches while reading this book. I hope I include them in this summary.

Arrays vs Linked Lists
Arrays is a Data Structure that takes up a contiguous bit of memory to store same type data. Because of their fixed nature deleting and adding to an Array is somewhat expensive `0(n)` as all of that data has to be copied and put in another array that can fit it all. However, reading data from an array happens in constant time `0(1)` as we can make some computations and determine the exact address where this info is in memory. ***Most PLs implement Arrays Dynamically now sha***

Linked Lists can have data scattered all around memory but each node has to have a pointer to where the next bit of data is store in memory. Because of it's loose nature deletions and additions can happen in `0(1)` time as you really just need to modify the pointers. Reading data or searching through a Linked list on the other hand can take some time `0(n)` as you have to physically go though every node in the list.

> Both Data structures allow you to store multiple elements

Selection Sort
If we had to sort items in a shopping list by their attached prices how would we do it? We'd probably need to go through the list pick the most expensive item and take note of it for our new list and keep doing this till we've touched every item from the original list. This technique is commonly known as selection sort, it has a big 0 notation of `0(n^2)` and can get very slow as our input size grows.

</details>

<details>
<summary>Chapter 3 Recursion</summary>

What happens when you're hungry? You look for food you want to eat and you keep looking till you've satisfied that hunger. Recursive algorithms work the exact same way. Recursive functions have a base case and a recursive case that keeps executing until the base case is met. Because of this nature the time complexity of these algorithms is `0(n)` because the function is called recursively n times before reaching a terminating base case, See example.
```python
def countdown(i):
    print(i)
    # this is our base case
    if i <= 0:
        return
    # this is our recursive case 
    else:
        countdown(i-1)
```

>Identifying a good base case is key for DSA problems. Always try to break problems down into the smallest, clearest unit.

Understanding how the OS call stacks work is also key to understanding recursion. All function calls go into the call stack and wont compute until the base case is met. The state of partially complete calls are saved.

>A stack will typically have two methods pop(removes items from top of stack) and push(adds items to the stack). 

TODO: 
- [ ] what is tail recursion?
- [X] learn how OS implement call stacks
</details>

<details>
<summary>Chapter 4 Quicksort</summary>

Quicksort is an in-place D&C algorithm meaning you have to break your problem into its smallest unit and solve that tiny unit. For Quicksort, you pick a pivot and compare each successive element against that pivot if it's bigger move it to the right sublist, else move it to the left sublist and then combine everything. It runs at about `0(logn)` on average but can reach `0(n^2)` at the worst case -- when your input is already sorted. [Here's an ELI5 explanation](https://www.reddit.com/r/explainlikeimfive/comments/lb7w1/comment/c2r9isp/?utm_source=share&utm_medium=web2x&context=3)

>It is much faster than selection sort

>Try to always explain your LC solutions in inductive proofs. build from bottom up.

Big 0 of common algorithms in comparison

| Algorithm      | Big 0 notation |
| :---        |    ----:   |
| Binary Search  | `0(logn)` |
| Simple Search | `0(n)` |
|Quick Sort|`0(nlogn)`|
|Merge Sort|`0(nlogn)`|
|Selection Sort|`0(n^2)`|
|Travelling Salesman|`0(n!)`|

#### Merge Sort vs. Quicksort
- Quick sort has a smaller **constant than Merge sort.
- Hits average case way more often
- Is faster in practice

>when you say 0(n) there's usually a hidden constant beside the n that usually does not matter but is really prevalent when comparing Merge Sort and Quick Sort.

TODO:
- [ ] implement the travelling salesman algo in Go with concurrency

</details>

<details>
<summary>Chapter 5 Hash Tables</summary>

>hashmaps, dictionaries, associative arrays are all other names for this.

Hashmaps are a k-v data store that use hash functions to find an appropriate index in an array to store data. Hashmaps allow for quick lookups.

>They combine best and worst parts of arrays and linked lists.

Hash functions map strings to numbers. They must be:
- must be consistent. if I want to hash `"Dibri's favourite Phrase"` the hash function must always return the same number
- is aware of the array size
- maps different strings to different indexes

|Function|Hash Tables|Hash Tables (Worst Case)|Arrays|Linked Lists|
|:---| :---:|:---: |:---: |---:|
|Search | `0(1)`|`0(n)`|`0(1)`|`0(n)`|
|Insert |`0(1)`|`0(n)`|`0(n)`|`0(1)`|
|Delete |`0(1)`|`0(n)`|`0(n)`|`0(1)`|

Collisions can happen, i.e different strings can get mapped to the same index and to fix this we can extend that array index point to an alt node (intro. a frankenstein array-linked list). Other things that can help prevent collisions are a low `load factor` and a good hash function (that distributes values in the array evenly).

>load factors help to resizing as the array grows, they calculate how much space is left in the array by comparing number of items in the array with number of slots available. You should be aiming for a number under 0.7.

#### Applications of Hash Tables
- Lookups (DNS Resolution, Phone Books)
- Caches
- Prevent Duplicates
</details>

<details>
<summary>Chapter 6 Breadth-First Search</summary>

BFS is great for finding the shortest paths between two things. It is considered an `0(V+E)` operation. 
<!-- if you dey try reach the court at BCON, there are a bunch of routes you can take but applying BFS will return the route with the few paths or checkpoints. -->

BFS can help:
- find the shortest path from node A to node B
- Discover whether a path exists between A & B, i.e searching for someone in your friend group who has a ball

To tackle the friend example you would start by listing all your immediate friends with balls (`Difu, Kosi, Dagogo`) and once you ask someone if they have it then `fin` else get all their friends who may have balls and add them to your list and repeat the process till you've got a ball. This is how BFS works.

> tl;dr - queues help the algorithm remember what node to search next.

Queues are a FIFO (First In, First Out) Data structure used to implement BFS. Because of how queues work, they are the perfect data structure to use when we do not care about revisiting nodes, they can be used to avoid recursion. The queue keeps track of the locations remaining to be searched as opposed to needing a potentially large amount of processor stack space for a recursive solution.

> When working with BFS problems consider modelling your problem in form of a graph before applying the PFS. 

A graph is a data type used to model a set of connections. It is made up by a bunch of Nodes connected by Edges (or arcs). Graphs can be directed or indirected. indirected graphs just means the relationship between nodes goes both ways.

A tree is a graph where no edges point back. It flows in one direction from the root node.

</details>

<details>
<summary>Chapter 7 Dijkstra’s Algorithm</summary>

BFS is great for finding the path with fewer segments (or edges) but once these edges get weighted, it's a different ball game. BFS won't account for the weights. 

> A graph with weights is called a weighted graph. A graph without weights is called an unweighted graph.

Dijkstra's algorithm is a more appropriate when looking for the most optimal path, it takes note of the weights to perform an `0(ElogV)` operation. Dijkstra's algo, however, only works with DAGs (directed acyclic graphs). 

Also, once a problem involves -ve weights or some logic that will result in -ve weights Dijkstra's algo will not work. A more appropriate algo would be Bellman Ford Algorithm which works with negative weights and runs at `0(V*E)`.

> Because Dijkstra's goal is to find the optimal path (not just any path), it, by definition, cannot work with negative weights, since it cannot find the optimal path.
</details>

<details open>
<summary>Chapter 8 Greedy Algorithms</summary>
</details>
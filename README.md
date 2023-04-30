Download Link: https://assignmentchef.com/product/solved-cs251-project-07-finish-earlier-project-or-minqueue-v2
<br>
Since this is the last week of classes, there are 3 options for project #07.  Your options are defined by the following pseudo-code:

There will be 4 sets of submissions available on Gradescope, one for each option.  After the due date, you *must* also submit an online google form to inform us of what we should grade.  If you do not submit this form before Monday, 12/9 @ 12noon, we will assume you have nothing to submit for project #07.  Link to google form:  <a href="https://bit.ly/cs251-project07">http://bit.ly/cs251</a><a href="https://bit.ly/cs251-project07">–</a><a href="https://bit.ly/cs251-project07">project07</a> .

<h1>minqueue v2</h1>

Dijkstra’s algorithm requires a priority queue that returns the next vertex to process, based on the vertex with the shortest distance from the starting vertex.  In project #06, a <strong>minqueue&lt;TKey, TValue&gt;</strong> class was defined in “minqueue.h” to provide this functionality.  The implementation was easy to understand, but inefficient.

Your assignment is to provide an O(lgN) implementation based on a <strong>min-heap</strong> data structure.  As discussed in class (days 39 and 40), this is a tree-based data structure implemented using an array.  However, our <strong>minqueue</strong> needs to extend the traditional min-heap to allow O(1) or O(lgN) lookup of keys — as required by Dijkstra’s algorithm.  Recall that Dijkstra’s algorithm, when it finds a shorter path, needs to update an existing (key, value) pair in the queue, and reorder the queue appropriately.

Here is the design of the <strong>minqueue&lt;TKey, TValue&gt;</strong> class that you must implement.  You must implement this design as given, you cannot the function names, parameters, or return values.  The comments provide a summary of each function:




/*minqueue.h*/




//

// Min queue that stores (key, value) pairs using a min-heap

// implementation.  When pop is called, the key from the  // (key, value) pair with the smallest value is returned; if

// two pairs have the same value, the smaller key is returned.

// Push and pop have O(lgN) time complexity.

//

// &lt;&lt; YOUR NAME &gt;&gt;

//

// Original author: Prof. Joe Hummel

// U. of Illinois, Chicago

// CS 251: Fall 2019

// Project #07

//




#pragma once




#include &lt;iostream&gt;

#include &lt;vector&gt;

#include &lt;exception&gt;

#include &lt;stdexcept&gt;




using namespace std;




template&lt;typename TKey, typename TValue&gt; class minqueue

{ private: public:

//

// default constructor:

//

// Queue has a max capacity for efficient implementation.

// This max capacity must be specified at queue creation.

//

minqueue(int capacity)

{     //     // TODO:

//

}




//

// fill constructor:

//

// This allows for the efficient O(N) construction of

// a queue with an initial set of keys, all with the same

// initial value.  The max capacity of the queue is

// set to the # of keys provided for initialization;   // it is assumed the keys are in ascending order.

//

minqueue(vector&lt;TKey&gt; keys, TValue initialValue)

{     //     // TODO:

//

}







//

// destructor:   //

virtual ~minqueue()

{     //     // TODO:

//

}




//   // empty:

//

// Returns true if empty, false if not.

//   bool empty()

{




}







//

// push:

//

// Inserts the given (key, value) pair into the queue such that

// pop always returns the pair with the minimum value.  If the

// key is *already* in the queue, it’s value is updated to the

// given value and the queue reordered.  If the key is not in   // the queue, the (key, value) pairs is added and the queue   // reordered.

//

// NOTE: if two keys have the same value, i.e. (key1, value) and

// (key2, value), then those pairs are ordered into ascending value   // by their key.

//

void pushinorder(TKey key, TValue value)

{

//     // TODO:

//




//

// we need to insert a new (key, value) pair but the queue is full:

//

//if (…)

//{

//  throw runtime_error(“minqueue::pushinorder: queue full”);

//}

//

}







//

// front:

//

// Returns the key at the front of the queue; does *not* pop the

// (key, value) pair.  Throws a logic_error exception if the queue   // is empty.

//

TKey minfront()

{

if (empty())

{

throw logic_error(“minqueue::minfront: queue empty”);

}




//     // TODO:

//

}




//   // pop:

//

// Pops and discards the (key, value) pair at the front of the queue.   // Throws a logic_error exception if the queue is empty.

//

void minpop()

{

if (empty())

{

throw logic_error(“minqueue::minpop: queue empty”);

}




//

// TODO:

//

}




};




<h1>Implementation details</h1>

Your implementation will need 2 data structures.  The 1<sup>st</sup> is an array to store the min-heap tree, and this should be an array of (key, value) pairs.  Keep in mind the minqueue is ordered by <strong>value</strong>; if two pairs have the same value, then order by <strong>key</strong>.




The 2<sup>nd</sup> data structure enables O(1) or O(lgN) lookup to see if a key is already in the minqueue, and if so, where it is.  You cannot search the array since it’s not ordered by key — linear search would be the only option, and that’s too slow.  The choice of the 2<sup>nd</sup> data structure is up to you, but it needs to enable O(1) or O(lgN) lookup of a key’s position.




The algorithms for push and pop are well-known.  These are discussed in zybooks, and here’s another reference I also find helpful:




Pop:  <a href="http://www.algolist.net/Data_structures/Binary_heap/Remove_minimum">http://www.algolist.net/Data_structures/Binary_heap/Remove_minimum</a>

Push:  <a href="http://www.algolist.net/Data_structures/Binary_heap/Insertion">http://www.algolist.net/Data_structures/Binary_heap/Insertion</a> <strong> </strong>




As elements are pushed, popped and swapped, don’t forget to update data structure #2.  Note that our version of “push” needs to be more sophisticated than a traditional min-heap since the key may already be in the queue.  In this case, the recommended approach is to <strong>delete</strong> the existing (key, value) pair, and then do a traditional <strong>push</strong> of a new (key, value) pair.  Here’s the pseudo-code for deleting a (key, value) pair from *any* position in minqueue.  This is different than <strong>pop</strong>, which only deletes the first element:




<strong>delete(key, value): </strong>

<ol>

 <li>Let p = position of (key, value) pair in array</li>

 <li>If p denotes the last position in the queue, reduce # of elements by 1 and return;</li>

 <li>Move last pair into position p</li>

 <li>Reduce # of elements by 1</li>

 <li>Let (K, V) be the pair at position p. Does K have a parent?  If so, compare values and see if (K, V)</li>

</ol>

should sift upward… If sift occurs, update p to new position and repeat this step.

<ol start="6">

 <li>Let (K, V) be the pair at position p. Does K have children?  One child or two?  If just one child, compare values and sift downward if necessary.  If two children, compare against the smaller of the two children, and sift download if necessary; if the children have the same value and a sift download should occur, swap with the child with the smaller key.  If sift occurs, update p to new position and repeat this step.</li>

 <li></li>

</ol>




For initial testing, I would recommend using project #06 — your implementation should be compatible with the minqueue used in project #06.  A Codio project is provided with the initial “minqueue.h” file; see “<strong>cs251project07-minqueue-v2</strong>”.  If you prefer to work outside of Codio, the “minqueue.h” file is also available on the course web page under “Projects”, “<a href="https://www.dropbox.com/sh/cwil0m0rnxpn5jj/AACGY8Ojhhh01fcg6YRQBQRsa?dl=0">project07</a><a href="https://www.dropbox.com/sh/cwil0m0rnxpn5jj/AACGY8Ojhhh01fcg6YRQBQRsa?dl=0">–</a><a href="https://www.dropbox.com/sh/cwil0m0rnxpn5jj/AACGY8Ojhhh01fcg6YRQBQRsa?dl=0">files</a><a href="https://www.dropbox.com/sh/cwil0m0rnxpn5jj/AACGY8Ojhhh01fcg6YRQBQRsa?dl=0">”</a>.




<h1>Requirements</h1>

<ol>

 <li>Follow minqueue.h design as given.</li>

 <li>Push, pop and front must be O(lgN) in time.</li>

 <li>Data structure #1 must be an array of (key, value) pairs.</li>

 <li>Data structure #2 must enable O(1) or O(lgN) lookup of key’s position in data structure #1.</li>

</ol>



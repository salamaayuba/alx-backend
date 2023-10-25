Cache replacement policies

Article
Talk
Read
Edit
View history

Tools
From Wikipedia, the free encyclopedia
This article is about general cache algorithms. For detailed algorithms specific to paging, see page replacement algorithm. For detailed algorithms specific to the cache between a CPU and RAM, see CPU cache.
Not to be confused with cache placement policies.
In computing, cache replacement policies (also known as cache replacement algorithms or cache algorithms) are optimizing instructions or algorithms which a computer program or hardware-maintained structure can utilize to manage a cache of information. Caching improves performance by keeping recent or often-used data items in memory locations which are faster, or computationally cheaper to access, than normal memory stores. When the cache is full, the algorithm must choose which items to discard to make room for new data.

Overview
The average memory reference time is[1]

�
=
�
×
�
�
+
�
ℎ
+
�
{\displaystyle T=m\times T_{m}+T_{h}+E}
where

�
m = miss ratio = 1 - (hit ratio)
�
�
T_{m} = time to make main-memory access when there is a miss (or, with a multi-level cache, average memory reference time for the next-lower cache)
�
ℎ
T_{h}= latency: time to reference the cache (should be the same for hits and misses)
�
E = secondary effects, such as queuing effects in multiprocessor systems
A cache has two primary figures of merit: latency and hit ratio. A number of secondary factors also affect cache performance.[1]

The hit ratio of a cache describes how often a searched-for item is found. More-efficient replacement policies track more usage information to improve the hit rate for a given cache size. The latency of a cache describes how long after requesting a desired item the cache can return that item when there is a hit. Faster replacement strategies typically track of less usage information—or, with a direct-mapped cache, no information—to reduce the time required to update the information. Each replacement strategy is a compromise between hit rate and latency.

Hit-rate measurements are typically performed on benchmark applications, and the hit ratio varies by application. Video and audio streaming applications often have a hit ratio near zero, because each bit of data in the stream is read once (a compulsory miss), used, and then never read or written again. Many cache algorithms (particularly LRU) allow streaming data to fill the cache, pushing out information which will soon be used again (cache pollution).[2] Other factors may be size, length of time to obtain, and expiration. Depending on cache size, no further caching algorithm to discard items may be needed. Algorithms also maintain cache coherence when several caches are used for the same data, such as multiple database servers updating a shared data file.

Policies
Bélády's algorithm
The most efficient caching algorithm would be to discard information which would not be needed for the longest time; this is known as Bélády's optimal algorithm, optimal replacement policy, or the clairvoyant algorithm. Since it is generally impossible to predict how far in the future information will be needed, this is unfeasible in practice. The practical minimum can be calculated after experimentation, and the effectiveness of a chosen cache algorithm can be compared.

Chart of Belady's algorithm
When a page fault occurs, a set of pages is in memory. In the example, the sequence of 5, 0, 1 is accessed by Frame 1, Frame 2, and Frame 3 respectively. When 2 is accessed, it replaces value 5 (which is in frame 1, predicting that value 5 will not be accessed in the near future. Because a general-purpose operating system cannot predict when 5 will be accessed, Bélády's algorithm cannot be implemented there.

Random replacement (RR)
Random replacement selects an item and discards it to make space when necessary. This algorithm does not require keeping any access history. It has been used in ARM processors due to its simplicity,[3] and it allows efficient stochastic simulation.[4]

Simple queue-based policies
First in first out (FIFO)
With this algorithm, the cache behaves like a FIFO queue; it evicts blocks in the order in which they were added, regardless of how often or how many times they were accessed before.

Last in first out (LIFO) or First in last out (FILO)
The cache behaves like a stack, and unlike a FIFO queue. The cache evicts the block added most recently first, regardless of how often or how many times it was accessed before.

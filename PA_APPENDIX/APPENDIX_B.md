#List of Problems and Algorithms
#一些著名问题与算法

If you’re having hull problems, I feel bad for you, son; I’ve got 99 problems, but a breach ain’t one.

—Anonymous1

如果你的船裂了个缺口，我只能同情你了；我有99个问题，但不包括这个。

——匿名

This appendix does not list every problem and algorithm mentioned in the book, because some algorithms are only discussed to illustrate a principle and some problems serve only as examples for certain algorithms. The most important problems and algorithms, however, are sketched out here, with some references to the main text. If you’re unable to find what you’re looking for by consulting this appendix, take a look in the index.

In most descriptions in this appendix, n refers to the problem size (such as the number of elements in a sequence). For the special case of graphs, though, n refers to the number of nodes, and m refers to the number of edges.


这篇附录并不会列举本书中提到的所有问题与算法，因为有一些算法仅仅是为了试图说明某个原理，而有一些问题仅仅是为了某个算法而创造的。然而，作为索引，这里会列举本书中最重要的那些问题预算法。如果你查阅了这篇附录，并没有找到你所需要的那个问题或者算法，那么请查阅目录。

在本附录大多数描述中，n表示问题规模，例如一个序列中的元素数量。而在图论问题中，n表示节点的数量，m表示边的数量。

##Problems

##问题

__Cliques and independent sets.__ A clique is a graph where there is an edge between every pair of nodes. The main problem of interest here is finding a clique in a larger graph (that is, identifying a clique as a subgraph). An independent set in a graph is a set of nodes where no pair is connected by an edge. In other words, finding an independent set is equivalent to taking the complement of the edge set and finding a clique. Finding a k-clique (a clique of k nodes) or finding the largest clique in a graph (the max- clique problem) is NP-hard. (For more information, see Chapter 11.)

__完全图（Cliques）与独立集__完全图是每对顶点之间都有一条边的图。主要的有趣的问题在于，怎样在一幅更大的图中，找到一个完全图（也就是说，在这幅比较大的图中，找到一个子图，该子图是一个完全图）。独立集是一幅图中互相没有边相连的点。换句话说，找到一个独立集，等价于将图中每两点之间的连接关系倒转后，找到该图的完全子图。找到一个k-完全图（有含有K个节点的完全图），或者找到一幅图中的最大完全图（最大完全图问题），是NP难问题（更多内容请查阅第11章）。

__Closest pair.__ Given a set of points in the Euclidean plane, find the two points that are closest to each other. This can be solved in loglinear time using the divide-and-conquer strategy (see Chapter 6).

__最接近的数对__在欧几里得平面上给出一些点，找到其中最接近的两个点。它可以在对数限行时间内，使用分解-解决算法解决（见第6章）。

__Compression and optimal decision trees.__ A Huffman tree is a tree whose leaves have weights (frequencies), and the sum of their weights multiplied by their depth is as small as possible. This makes such trees useful for constructing compression codes and as decision trees when a probability distribution is known for the outcomes. Huffman trees can be built using Huffman’s algorithm, described in Chapter 7 (Listing 7-1).

__压缩与最佳决策树__霍夫曼树是叶子节点有权重的树。权重与节点深度的乘积和越小越好。这样的树对于构建压缩编码非常有效，而权重可能是节点已知的概率分布。霍夫曼树可以使用第七章描述的霍夫曼算法来构建（清单7-1）。

__Connected and strongly connected components.__ An undirected graph is connected if there is a path from every node to every other. A directed graph is connected if its underlying undirected graph is connected. A connected component is a maximal subgraph that is connected. Connected components can be found using traversal algorithms such as DFS (Listing 5-5) or BFS (Listing 5-9), for example. If there is a (directed) path from every node to every other in a directed graph, it is called strongly connected. A strongly connected component (SCC) is a maximal subgraph that is strongly connected. SCCs can be found using Kosaraju’s algorithm (Listing 5-10).

__连通与强连通分量。__如果一个无向图的每个节点都可以找到通向其他任意节点的路径，那么我们把这幅图称为连通图。一个有向图底层的无向图如果是连通的，那么这个有向图也是一个连通图。连通分量是一幅图中的极大连通子图。连通分量可以使用遍历算法来获得，如DFS（清单5-5）或者BFS（清单5-9）。如果在一个有向图中，每个节点到其他任何一个节点，都可以找到一条有向路径，那么这个图被称为强连通图。强连通组件（SCC）是一幅连通图中的极大强连通子图。SCC可以使用Kosaraju算法找到（清单5-10）。

__Convex hulls__. A convex hull is the minimum convex region containing a set of points in the Euclidean plane. Convex hulls can be found in loglinear time using the divide-and-conquer strategy (see Chapter 6).

__凸包。__在欧几里得平面，凸包是最小的包含所有点的凸多边形区域。使用分解-解决算法，凸包可以在对数线性时间内解决（见第六章）。

__Finding the minimum/maximum/median.__ Finding the minimum and maximum of a sequence can be found in linear time by a simple scan. Repeatedly finding and extracting the maximum or minimum in constant time, given linear-time preparation, can be done using a binary heap. It is also possible to find the kth smallest element of a sequence (the median for k = n/2) in linear (or expected linear) time, using the select or randomized select. (For more information, see Chapter 6).

__寻找最小值/最大值/中位数。__通过一次遍历，我们就可以找到序列的最小值与最大值。通过使用二叉堆，以及线性的准备时间，那么在常数时间里，我们就可以反复提取最大值和最小了。通过随机选择算法，我们也可能在线性时间（或者预期在线性时间）内，找到序列的第k小的元素。（更多信息请参考第六章）。

__Flow and cut problems.__ How many units of flow can be pushed through a network with flow capacities on the edges? That is the max-flow problem. An equivalent problem is finding the set of edge capacities that most constrain the flow; this is the min-cut problem. There are several versions of these problems. For example, you could add costs to the edges, and find the cheapest of the maximum flows. You could add lower bound on each edge and look for a feasible flow. You could even add separate supplies and demands in each node. These problems are dealt with in detail in Chapter 10.

__流量和切割问题。__在一幅图中，如果每条边上标注了流量，那么网络的总流量应该是多少？这就是最大流量问题。等价的问题是，找到一组边，能够最大化地限制流量。这是最小切割问题。类似的问题有数个版本。例如，在边上标注过路费，然后寻找最省钱的路径。或者，在每条边上标注最小流量，然后寻找可行路径。甚至可以在节点上标注通过该节点的消耗或是要求。第十章讨论了这一系列问题。

__Graph coloring.__ Try to color the nodes of a graph so that no neighbors share a color. Now try to do this with a given number of colors, or even to find the lowest such number (the chromatic number of the graph). This is an NP-hard problem in general. If, however, you’re asked to see if a graph is two-colorable (or bipartite), the problem can be solved in linear time using simple traversal. The problem of finding a clique cover is equivalent to finding an independent set cover, which is an identical problem to graph coloring. (See Chapter 11 for more on graph coloring.)

__图着色问题。__首先，尝试将一幅图中的点着色，使得每一对直接连接的节点的颜色都不同。然后，尝试使用指定种类的颜色，甚至尝试用最少的颜色来为图着色。基本上，这是一个NP难问题。然而，判断一幅图是否可以只用两种颜色着色（或者说，这个图是否是个二分图），那么这个问题可以在线性时间内单次遍历解决。寻找覆盖等价于寻找一个独立的集合覆盖，这个问题非常类似于图着色问题。（关于图着色问题，更多信息请参见第十一章。）

__Hamilton cycles/paths and TSP ... and Euler tours.__ Several path and subgraph problems can be solved efficiently. If, however, you want to visit every node exactly once, you’re in trouble. Any problem involving this constraint is NP-hard, including finding a Hamilton cycle (visit every node once and return), a Hamilton path (visit every node once, without returning), or a shortest tour of a complete graph (the Traveling Salesman/Salesrep problem). The problems are NP-hard both for the directed and undirected case (see Chapter 11). The related problem of visiting every edge exactly once, though— finding a so-called Euler tour—is solvable in polynomial time (see Chapter 5). The TSP problem is NP- hard even for special cases such as using Euclidean distances in the plane, but it can be efficiently approximated to within a factor of 1.5 for this case, and for any other metric distance. Approximating the TSP problem in general, though, is NP-hard. (See Chapter 11 for more information.)

__哈密顿回路/路径，TSP，和欧拉路径__在路径问题和子图问题中，有几个问题有高效的解决方式。然而，并不一定存在一种方法，可以访问所有的节点，并且每个节点只访问一次。任何有这种限制的问题都被称为NP难问题，包括寻找哈密顿回路（从某个节点出发，仅访问每个节点一次并且回到出发节点），哈密顿路径（从某个节点出发，访问每个节点一次，并且不需要回到出发节点），以及寻找完全图的最短路径（旅行商问题）。对于有向图和无向图，这些问题都是NP难问题。然而，一个相关的问题：寻找欧拉路径（从某个节点出发，仅访问每条边一次，不需要回到出发节点）则可以在多项式时间内得到解决（见第五章）。甚至对于比较特殊的例子，TSP问题仍然是NP难问题，例如在平面上使用欧几里得距离，但对于这个例子，我们可以将因子规约于1.5，并且可以使用其他矩阵距离。然而，大多数类似的TSP问题，是NP难的。（更多信息，请参见第十一章。）

__Longest increasing subsequence.__ Find the longest subsequence of a given sequence whose elements are in increasing order. This can be solved in loglinear time using dynamic programming (see Chapter 8).

__最长的升序子序列__寻找给定的序列中长度最长的序列，这个序列为升序。这个问题可以使用动态编程（第8章），从而在对数线性时间内解决。

__Matching.__ There are many matching problems, all of which involve linking some object to others. The problems discussed in this book are bipartite matching and min-cost bipartite matching (Chapter 10) and the stable marriage problem (Chapter 7). Bipartite matching (or maximum bipartite matching) involves finding the greatest subset of edges in a bipartite graph so that no two edges in the subset share a node. The min-cost version does the same, but minimizes the sum of edge costs over this subset. The stable marriage problem is a bit different; there, all men and women have preference rankings of the members of the opposite sex. A stable set of marriages is characterized by the fact that you can’t find a pair that would rather have each other than their current mates.

__匹配。__匹配问题有很多，而最典型的问题就是对象互相指向的问题。本书中所讨论的指向问题是二分匹配问题及花费最少的二分匹配问题（第10章）。例如，在一个二分图中寻找边的最大子集，使得这个子集中没有两条边的任意两个端点重合。这个问题的另一个版本是，将边上标注权，从而寻找使得权最大的，且符合此条件的子集。稳定婚姻问题与此稍有不同。每个人都对所有的异性打分，然后通过为他们分配配偶，使得任意两个异性都不会宁愿抛弃他们被指定的配偶而在一起。

Minimum spanning trees. A spanning tree is a subgraph whose edges form a tree over all the nodes of the original graph. A minimum spanning tree is one that minimizes the sum of edge costs. Minimum spanning trees can be found using Kruskal’s algorithm (Listing 7-4) or Prim’s algorithm (Listing 7-5), for example. Because the number of edges is fixed, a maximum spanning tree can be found by simply negating the edge weights.

__最小生成树__。生成树是一个图的子图，这个子图要包含原图所有的节点，并且是一棵树。最小生成树是在边上有权的情况下，权最小的生成树。寻找最小生成树可以使用克鲁斯卡算法（清单7-4）或者Prim算法（清单7-5）。例如，由于边的数量是固定的，最大生成树可以通过取消边的权来找到。

Partitioning and bin packing. Partitioning involves dividing a set of numbers into two sets with equal sums, while the bin packing problem involves packing a set of numbers into a set of “bins” so that the sum in each bin is below a certain limit and so that the number of bins is as small as possible. Both problems are NP-hard. (See Chapter 11.)

__Partitioning and bin packing.__分割问题与装箱问题。分割问题是指，将一个数的集合一分为二，使得两个子集的和相等。而装箱问题是指，将一个集合中的数放入若干个“箱子”，使得每个箱子内数的和不超过某个值，而使得箱子的个数尽可能小。这两个问题都是NP难问题（见第11章）。

SAT, Circuit-SAT, k-CNF-SAT. These are all varieties of the satisfaction problem (SAT), which asks you to determine whether a given logical (Boolean) formula can ever be true, if you’re allowed to set the variables to whatever truth values you want. The circuit-SAT problem simply uses logical circuits rather than formulas, and k-CNF-SAT involves formulas in conjunctive normal form, where each clause consists of k literals. The latter can be solved in polynomial time for k = 2. The other problems, as well as k-CNF-SAT for k > 2, are NP-complete. (See Chapter 11.)

__SAT，Circuit-SAT，和k-CNF-SAT。__这些都是满足性问题。这类问题【还是不要乱翻了……】

__Searching.__ This is a very common and extremely important problem. You have a key and want to find an associated value. This is, for example, how variables work in dynamic languages such as Python. It’s also how you find almost anything on the Internet these days. Two important solutions are hash tables (see Chapter 2) and binary search or search trees (see Chapter 6). Given a probability distribution for the objects in the data set, optimal search trees can be constructed using dynamic programming (see Chapter 8).

__查询。__这是一个非常普遍而又非常重要的问题：通过某个键查询到对应的值。这就是动态语言（例如Python）的变量运作方式。在当今互联网世界，这几乎也是寻找任何信息的方式。大致上，我们有两种解决方式：使用哈希表（见第二章）或者使用二分查找（即搜索树，见第六章）。而如果数据集中的元素有概率分布的话，使用动态语言也可以为其创建最佳搜索树以优化查询。

__Sequence comparison.__ You may want to compare two sequences to know how similar (or dissimilar) they are. One way of doing this is to find the longest subsequence the two have in common (longest common subsequence) or to find the minimum number of basic edit operations to go from one sequence to the other (so-called edit distance, or Levenshtein distance). These two problems are more or less equivalent; see Chapter 8 for more information.

__序列比较。__比较两个序列，以得出它们相同的元素或不同的元素。解决此类问题的方法之一是寻找两个序列中的最长畅通子序列，或者寻找从一个序列变换到另一个序列所需的最少基本操作数（即Levenshtein distance算法）。这两个问题是等价的。更多信息详见第八章。

__Sequence modification.__ Inserting an element into the middle of a linked list is cheap (constant time), but finding a given location is costly (linear time); for an array, the opposite is true (constant lookup, linear insert, because all later elements must be shifted). Appending can be done cheaply for both structures, though (see the black box sidebar on list in Chapter 2).

__序列变换。__向一个链表中插入元素的时间复杂度是非常小的（常数时间），但寻找指定位置的元素的时间复杂度很大（线性时间）。而对于数组而言，则刚好相反（寻找时间为常数，而插入时间为线性，因为元素插入位置之后的所有元素都需要移动）。但是向两者末端插入元素的时间都非常小（见第二章的某个黑盒子）。

__Set and vertex covers.__ A vertex cover is a set of vertices that cover (that is, are adjacent to) all the edges of the graph. A set cover is a generalization of this idea, where the nodes are replaced with subsets, and you want to cover the entire set. The problem lies in constraining or minimizing the number of nodes/subsets. Both problems are NP-hard (see Chapter 11).

__集合与顶点覆盖。__顶点覆盖集是指能够覆盖图中所有的边的顶点集合（即每条边至少有一个顶点在顶点覆盖集中）。如果将这个概念中的顶点换为子集，则可以引申出集合覆盖的概念。这个问题的重点在于限制或最小化顶点与子集的数量。这两个问题都是NP难问题（见第十一章）。

__Shortest paths.__ This problem involves finding the shortest path from one node to another, from one node to all the others (or vice versa), or from all nodes to all others. The one-to-one, one-to-all, and all- to-one cases are solved the same way, normally using BFS for unweighted graphs, DAG shortest path for DAGs, Dijkstra’s algorithm for nonnegative edge weights, and Bellman–Ford in the general case. To speed up things in practice (although without affecting the worst-case running time), one can also use bidirectional Dijkstra, or the A* algorithm. For the all pairs shortest paths problem, the algorithms of choice are probably Floyd–Warshall or (for sparse graphs) Johnson’s algorithm. If the edges are nonnegative, Johnson’s algorithm is (asymptotically) equivalent to running Dijkstra’s algorithm from every node (which may be more effective). (For more information on shortest path algorithms, see Chapters 5 and 9.) Note that the longest path problem (for general graphs) can be used to find Hamilton paths, which means that it is NP-hard. This, in fact, means that the shortest path problem is also NP-hard in the general case. If we disallow negative cycles in the graph, however, our polynomial algorithms will work.

__最短路径问题。__这一系列问题包括：1.寻找从某个节点到另一个节点的最短路径。2.寻找从某个节点到所有其他节点节点（或相反）的最短路径和。3.寻找从每个节点到所有其他节点的最短路径和的和【别闹】。前两者可以使用同一种方法解决，一般如果是未加权图的话使用BFS算法，DAG图的话使用DAG最短路径算法，权重非负的话使用Dijkstra算法，一般情况使用Bellman–Ford算法。在实践中，为了加快运算速度（虽然无法提升最坏情况的运行时间），可以使用双向Dijkstra算法，即A*算法。而对于第三种问题，可选的算法有Floyd–Warshall算法，或者Johnson算法（对于稀疏图而言）。如果边的权非负，Johnson算法是（渐进）等价于对每个点使用Dijkstra算法（后者更为高效）。关于最短路径算法的更多信息，见第五章和第九章。注意，最长路径问题（对一般图）课被用于寻找哈密尔顿路径，也就是说，这是个NP难问题。事实上，这意味着，对于一般情况，最短路径问题也是NP难的。然而，如果我们删去图中的负环，我们的算法即可在多项式时间内解决问题。

__Sorting and element uniqueness.__ Sorting is an important operation and an essential subroutine for several other algorithms. In Python, you would normally sort by using the list.sort method or the sorted function, both of which use a highly efficient implementation of the timsort algorithm. Other algorithms include insertion sort, selection sort, and gnome sort (all of which have a quadratic running time), as well as heapsort, mergesort, and quicksort (which are loglinear, although this holds only in the average case for quicksort). For the info on the quadratic sorting algorithms, see Chapter 5; for the loglinear (divide-and-conquer) algorithms, see Chapter 6. Deciding whether a set of real numbers contains duplicates cannot (in the worst case) be solved with a running time better than loglinear. By reduction, neither can sorting.
The halting problem. Determine whether a given algorithm will terminate with a given input. The problem is undecidable (that is, unsolvable) in the general case (see Chapter 11).

__排序问题与元素重复性问题。__排序是非常重要的操作，也是一些其他算法的第一步。在Python中，一般使用list.sort方法或者sorted函数即可完成排序，两者都使用了时间排序算法的高效实现。其他算法包括插入排序法，选择排序法及gnome排序法，这些算法的运行时间都是二次的。除此之外，还有堆排序，合并排序与快速排序法，他们的平均情况的运行时间是对数线性的。对于那些运行时间为二次的排序算法，可以参考第五章。对于对数线性（使用分解-合并）算法，可以参考第六章。判断一个集合中的实数是否含有重复值的问题，在最坏情况下运行时间至少为对数线性的。【后面的没怎么看懂】

__The knapsack problem and integer programming.__ The knapsack problem involves choosing a valuable subset of a set of items, under certain constraints. In the (bounded) fractional case, you have a certain amount of some substances, each of which has a unit value (value per unit of weight). You also have a knapsack that can carry a certain maximum weight. The (greedy) solution is to take as much as you can of each substance, starting with the one with the highest unit value. For the integral knapsack problem, you can only take entire items—fractions aren’t allowed. Each item has a weight and a value. For the bounded case (also known as 0-1 knapsack) you have a limited number of objects of each type. (Another perspective would be that you have a fixed set of objects that you either take or not.) In the unbounded case, you can take as many as you want from each of a set of object types (still respecting your carrying capacity, of course). A special case known as the subset sum problem involves selecting a subset of a set of numbers so that the subset has a given sum. These problems are all NP-hard (see Chapter 11), but admit pseudopolynomial solutions based on dynamic programming (see Chapter 8). The fractional knapsack case, as explained, can even be solved in polynomial time using a greedy strategy (see Chapter 7). Integer programming is, in some ways, a generalization of the knapsack problem (and is therefore obviously NP-hard). It is simply linear programming where the variables are constrained to be integers.

__背包问题和整数规划。__背包问题是在某种限制下，在一个集合中取出一个满足某种数量条件的子集的问题。在数量不限的情况下，你拥有几种物品，这些物品各有不同的重量，不同物品单位重量的价值不尽相同。同时，你有一个背包可以放置这些物品，但是有一个重量上限。（贪心的）解决方式是，从价值最高的物品开始，尽可能多的放置物品。而对于整数背包问题，你要把一种物品整个放进去，而不能仅放入这个物品的几分之几。每种物品都有重量和价值，对于有限制的情况（也被称为0-1背包问题），每种物品都有一定的数量。（另一种同类型的问题是，你有一些固定的物品集合，你可以拿或者不拿这些集合，但不能把一个集合分开）。在物品数量不限的情况下，你可以想取多少物品就取多少物品（当然，也要考虑背包容量）。子集和问题是一个特例。它描述了这样一个问题：如何从一个数的集合中取出一个子集，使得子集中元素的和为一个指定的数。这些问题都是NP难问题（见第十一章），但使用动态编程的话，可以在伪多项式时间内得到解（见第八章）。而背包问题，甚至可以通过贪心算法，在多项式时间内解决（见第七章）。整数规划在一定程度上是一般化的背包问题（所以很明显是NP难问题）。它只是变量为整数的线性规划问题。

__Topological sorting.__ Order the nodes of a DAG so that all the edges point in the same direction. If the edges represent dependencies, a topological sorting represents an ordering that respects the dependencies. This problem can be solved by a form of reference counting (see Chapter 4) or by using DFS (see Chapter 5).

__拓扑排序。__将DAG图中的节点按照某种规则排序，使得所有的彼岸指向同样的方向。假设边代表了依赖关系，那么拓扑排序就代表了按照这种依赖关系，为节点制定顺序。使用参考计数（第四章）或者DFS（第五章）可以解决这个问题。

__Traversal.__ The problem here is to visit all the objects in some connected structure, usually represented as nodes in a graph or tree. The idea can be either to visit every node or to visit only those needed to solve some problem. The latter strategy of ignoring parts of the graph or tree is called pruning and is used (for example) in search trees and in the branch and bound strategy. For a lot on traversal, see Chapter 5.

__遍历。__这里的问题是，如何在一个连通的结构中，访问所有的对象。通常这个问题被表述为如何遍历图或者树中的节点。问题可能要求你访问每个节点，或者仅仅是其中需要的节点。后者，即忽略图或者树的一部分的策略，被称为修剪，用于注入搜索树和分支定界策略中。更多信息请参考第五章。
# Title: Lexis: An Optimization Framework for Discovering the Hierarchical Structure of Sequential Data

# Author: Siyari, Dilkina, Dovrolis (2016)

#### General Content:
Propose algorithm that constructs an optimized hierarchical representation of a given set of target strings, the Lexis-DAG. The DAG displays how to derive each target string through the concatenation of intermediate substrings by minimizing the total number of such concatenations or DAG edges.


#### Keypoints:

* Problem is related to the SGP which is NP hard. The authors also prove this for the Lexis optimization problem and propose a greedy algorithm which efficiently constructs the DAG.

* Problem of construction is a synthetic design problem: construction of min cost DAG which shows how to produce a given set  of targets from a given alphabet in hierarchical manner, through the construction of intermediate substrings that are re-used in at least two higher-level strings.
  * Cost of DAG <-> related to concatenation work that corresponding hierarchy would require.

* Optimized DAG can be thought of as a plausible hypothesis for the unknown process that created given targets as long as we have reasons to believe that the process cares to minimize the same cost function that the DAG optimization considers.

* 2 cost functions (turn out to be algorithmically identical):
  * Min total number of concatenations
  * Min number of DAG edges
  * Which one to use is application specific - Lexis is NP hard for both

* Intermediate nodes/core: minimal set of DAG nodes that can cover a given fraction of s-to-t paths. Represents the most central substrings in corresponding

* Lexis-DAG - $D(V,A)$ with 3 conditions:
  1. $v \in V$ represents string $S(v)$, $V_S$ sources, $V_T$ targets, $V_M$ intermediate nodes. $V = V_S \cup V_M \cup V_T$
  2. Each node in $V_M \cup V_T$ represents a string that is the concatenation of substrings, $d_{in}(v)$: # incoming edges for v, $d_{out}(v): # outgoing edges for v
  3. Lexis-DAG should only include intermediate nodes with 2 outgoing edges - re-used in at least two concatenation operations

* Lexis Optimization Problem: Construct min-cost Lexis DAG for given alphabet S and targets T for given cost function:

$$\min_{(E, V_M)} C(D) s.t. D=(V, E) \text{ is Lexis-DAG for S and T}$$

* No explicit min of nodes in $V_M$ - but implicit through cost functions
  * Edge costs: $\mathcal{E}(D) = \sum_{v \in V} d_{in}(v) = |E|$
  * Concatenation costs: $C(D) = \sum_{v\in V\setminus V_s} (d_{in} -1) = |E| - V\setminus V_s$
  * Both problems are NP-hard

* G-Lexis idea: Search for substring $\xi$ that will lead to max cost reduction, when added as new intermediate node. Algo starts from trivial Lexis-DAG with no intermediate nodes and edges from the source nodes representing alphabet symbols to each occurance in target

* $I(v)$: Sequence of nodes appearing in incoming edges of v
  * $\leftrightarrow$ sequence of nodes whose string concatenation results in string $S(v)$ represented by v
  * $\leftrightarrow$ strings of alphabet of Lexis-DAG
  * Look for repeated substring $\xi \in I_{T \cup M} = \{I(v | v) \in V_T \cup V_M\}$ that can be used to construct new intermediate node
  * Can construct new intermediate nodes for $\xi$, create incoming edges based in symbols in $\xi$ and replace incoming edges to each of the non-overlapping repeated occurances of $\xi$ with a single outgoing edge from the new node.

Algorithm:

1. Init $V \leftarrow V_T \cup V_S$ and E, constructing each target in T from characters in S. $V_M \leftarrow \emptyset$.
2. Repeat:
  * $I_{T \cup M} \leftarrow \{I(v | v) \in V_T \cup V_M\}$
  * Select $\xi$ with max $(R_{T \cup M, \xi} -1)(|\xi| - 1)=0$, where $R_{T \cup M, \xi}$ is number of repeats $\xi$ in $I_{T \cup M}$.
  * if $(R_{T \cup M, \xi}-1)(|\xi| - 1) = 0$, break. Terminate when there are no more substrings with length at least 2 and which are repeated at least twice.
  * $V \leftarrow V \cup \{\sigma_{\xi}\}$ where $\sigma_{\xi}$ is new intermediate node and update E accordingly.

* Substring that max saved cost is a max repeat: substrings of length at least 2, whose extensionto right or left would reduce its occurences in the given set of strings
  * Suffix tree over set of input strings captures all right-max repeats which are superset of all mac repeats. To pick the one with max saved cost we need the count of non-overlapping occurences of these substrings - minimal augmented suffix tree
  * Here: implementation using regular suffix tree - Iterate over all occurances of selected substring, skipping overlapping occurances
    * $O(L) \text{ vs } O(L \log L)$ where L is total length of target strings
    * Overall runtime: $O(L^2)$ since max # iterations is $O(L)$ (each iteration reduces number of edges/concats which at start is $O(L)$)

* After construction: rank constructed intermediate nodes in terms of significance or centrality
  * Dependency chain: the higher the number of s-to-t paths traversing an intermediate node v (path centrality), the more important v is in terms of number of dependency chains it participates in.
  * Core of Lexis-DAG: Set of intermediate nodes that represent, as a whole the most important substrings in that Lexis-DAG
    * Should include nodes of high path centrality
    * Almost all s-to-t dependency chains of Lexis-DAG should traverse at least one of the core nodes

* Data compression: Looks for regularities that can be used to compress the data - patterns often useful as such regularities

* Minimum Description Principle: Compression scheme that results in smallest size for joint representation of both dictionary and encoding of data using that dictionary


#### Questions:

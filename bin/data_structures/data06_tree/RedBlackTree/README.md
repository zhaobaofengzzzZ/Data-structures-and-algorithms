## 红黑树 (Red-Black Tree )

红黑树:平衡二叉树，广泛用在C++的STL中。map和set都是用红黑树实现的。

是一种自平衡二叉查找树，是在计算机科学中用到的一种数据结构，典型的用途是实现关联数组。
它是在1972年由Rudolf Bayer发明的，当时被称为平衡二叉B树（symmetric binary B-trees）。
后来，在1978年被 Leo J. Guibas 和 Robert Sedgewick 修改为如今的“红黑树”。

红黑树和AVL树类似，都是在进行插入和删除操作时通过特定操作保持二叉查找树的平衡，从而获得较高的查找性能。
它虽然是复杂的，但它的最坏情况运行时间也是非常良好的，并且在实践中是高效的： 它可以在O(log n)时间内做查找，插入和删除，这里的n是树中元素的数目。

###  数据结构

它的统计性能要好于平衡二叉树(有些书籍根据作者姓名，Adelson-Velskii和Landis，将其称为AVL-树)，
因此，红黑树在很多地方都有应用。
在C++ STL中，很多部分(包括set, multiset, map, multimap)
应用了红黑树的变体(SGI STL中的红黑树有一些变化，这些修改提供了更好的性能，以及对set操作的支持)。
其他平衡树还有：AVL，SBT，伸展树，TREAP 等等。

###  树的旋转

当我们在对红黑树进行插入和删除等操作时，对树做了修改，那么可能会违背红黑树的性质。
为了保持红黑树的性质，我们可以通过对树进行旋转，即修改树中某些结点的颜色及指针结构，
以达到对红黑树进行插入、删除结点等操作时，红黑树依然能保持它特有的性质（五点性质）。

###  性质
红黑树是每个节点都带有颜色属性的二叉查找树，颜色或红色或黑色。
在二叉查找树强制一般要求以外，对于任何有效的红黑树我们增加了如下的额外要求:

性质1. 节点是红色或黑色。
性质2. 根节点是黑色。
性质3 每个叶节点（NIL节点，空节点）是黑色的。
性质4 每个红色节点的两个子节点都是黑色。(从每个叶子到根的所有路径上不能有两个连续的红色节点)
性质5. 从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。

这些约束强制了红黑树的关键性质: 从根到叶子的最长的可能路径不多于最短的可能路径的两倍长。
结果是这个树大致上是平衡的。
因为操作比如插入、删除和查找某个值的最坏情况时间都要求与树的高度成比例，这个在高度上的理论上限允许红黑树在最坏情况下都是高效的，而不同于普通的二叉查找树。
要知道为什么这些特性确保了这个结果，注意到性质4导致了路径不能有两个毗连的红色节点就足够了。
最短的可能路径都是黑色节点，最长的可能路径有交替的红色和黑色节点。因为根据性质5所有最长的路径都有相同数目的黑色节点，这就表明了没有路径能多于任何其他路径的两倍长。
在很多树数据结构的表示中，一个节点有可能只有一个子节点，而叶子节点不包含数据。
用这种范例表示红黑树是可能的，但是这会改变一些属性并使算法复杂。为此，本文中我们使用 "nil 叶子" 或"空(null)叶子"，如上图所示，它不包含数据而只充当树在此结束的指示。
这些节点在绘图中经常被省略，导致了这些树好象同上述原则相矛盾，而实际上不是这样。与此有关的结论是所有节点都有两个子节点，尽管其中的一个或两个可能是空叶子。

图论中知名度比较高的算法应该就是 [Dijkstra 最短路径算法](https://labuladong.github.io/algo/2/19/43/)， [环检测和拓扑排序](https://labuladong.github.io/algo/2/19/36/)， [二分图判定算法](https://labuladong.github.io/algo/2/19/37/) 以及今天要讲的最小生成树（Minimum Spanning Tree）算法了。

最小生成树算法主要有 Prim 算法（普里姆算法）和 Kruskal 算法（克鲁斯卡尔算法）两种，这两种算法虽然都运用了贪心思想，但从实现上来说差异还是蛮大的。

本文先来讲比较简单易懂的 Kruskal 算法，然后在下一篇文章 [Prim 算法模板](https://labuladong.github.io/algo/2/19/41/) 中聊 Prim 算法。

什么是最小生成树？

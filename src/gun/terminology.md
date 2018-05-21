#  术语

Gun 对于图形理论和网状网络有其自己的解释。在这里我们看到这些术语所表述的确切含义。

### Node

图形化的对象。它仅仅包含原始数据（只有指针和其他 node）。也可以被理解为图形理论中的顶点(vertex)

### Pseudo-merge/Union

两个对象的巧妙合并。并不像 `Object.assign`, 它使用 HAM 解决冲突来确保对象更新或合并。

### Pseudo-node/Key Node

Gun 中用来添加2进制索引的一种特殊的 node 形式(在`.key()`中)。它提供一组唯一 ID 来模拟合并一个完整的 node.

### Soul

Gun 中的每个 node 都拥有的全宇宙唯一的 ID(在元数据中用`#`表示)。

### Graph

存储唯一 nodes 的对象。

### Peer

网状网络的单一设备。通常扮演服务器和客户端的角色。

### Mesh

能够回应相联 peer 请求的协同网络(如果请求中收到了数据，会再发一个请求回去)。是网状网络（在網路節點間透過動態路由的方式來進行資料與控制指令的傳送）的概念。

### Partition

当一组 peers 不能相互交流时(比如服务器间丢失链接)，单个的 peer 还是会继续服务客户端。

### Universe

应用中每个 peer 间， Node 和 Graph 的数量总和。


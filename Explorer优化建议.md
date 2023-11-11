1. 降低RPC请求频次

    ```
    1. 目前有两次按step读取block的操作，可以合并成一次step读block操作；
    2. 获取latest块高，可以180秒一次，不用实时；
    ```

![image-20230912171529625](/Users/geeker/Library/Application Support/typora-user-images/image-20230912171529625.png)

结论：在step=5的前提下，经过上述优化后，一轮step可以优化掉5秒时间，约为step的值；



2. 数据库批量更新

    ```
    1. 一个Step的block和交易，一次写原子操作(block表和transaction表)
    ```



3. 引入Redis，降低对数据库的查询依赖



4. 微服务拆分

    ```
    架构层的事情；所有的服务都压到一台服务器上，会形成硬件资源竞争，本身也会降低性能；
    1. 数据同步；
    2. 数据整理；
    3. 后台任务；
    
    P.S 将网络密集型和CPU/memory密集型区分部署
    ```
    



5. 数据请求

    ```
    1. rpc请求node节点获取block的时候，要不停的重试失败的块请求，不要跳过失败请求留给后续的sync模块，这样会增加逻辑复杂度；微服务要stay simple， stay foolish;
    ```

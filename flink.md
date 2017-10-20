1. Flink 是 Apache 旗下的一个开源项目，是一个分布式的 *流式数据* 和 *批量数据* 处理的 *平台*。它的核心是一个流式数据处理的引擎，然后在其上，构建了批量数据处理的功能和接口。Flink 运行于 jvm 之上，提供了 scala 和 java 的 api.
2. 流式数据处理和传统的批量数据处理或数据库的区别：
    1. 和批量数据处理的区别
        * 数据处理的实时性
        * 数据量是无限的
        * 数据没有持久性的存储，只会在一定范围内缓存数据；流式数据处理是增量计算，批量数据处理是全量计算
    2. 和数据库的区别
        * 数据处理多为聚合（aggregate）性的，例如数据统计之类的操作
        * 不提供传统数据库 ACID 的特性（非事务型）
        * 可以简单理解为对数据进行实时的统计分析（类似 OLAP）
3. Flink 进行流数据处理所用到的组件：
    * 在概念上分为 **stream** 和  **transformation**
        * stream 代表着数据
        * transformation 代表着对数据的处理
    * 在程序实现上，以上两个概念分别对应着　**stream** 和　**operator** 两种对象
        * operators 以一定的先后顺序组织起来，表达了数据处理的逻辑； streams 流入一个 operator，经过处理后，流出并进入下一个 operator
        * 一个 operator 可以有多个 input streams 和 output streams
        * 常见的 operator 有：map, filter, keyBy, window 等等
        * Flink 的数据处理程序包括了 streams 和 operators，这样一个完整的数据处理过程，在 Flink 中称为 **streaming dataflow**
        * 每一个 dataflow 都包含了两类特殊的 operator
            - source: 是数据的输入来源，一个 dataflow 可以有 1 或 多 个 source
            - sink: 是数据处理结果的输出目的地，一个 dataflow 可以有 1 或 多 个 sink
            - 其它类型的 operators 在 Flink 中也统称为 Transformation Operators
        * Flink dataflow 的示例图： ![Flink Dataflow](https://ci.apache.org/projects/flink/flink-docs-release-1.3/fig/program_dataflow.svg)
4. 平台组件
    * TaskManager
        - 执行对数据的处理，执行中的数据处理也称为 **Flink Job**
        - 分布式，同一个数据处理工作，可以分解为多个任务，运行在不同的 TaskManagers 上面
    * JobManager
        - 调度、协调各个分布式数据处理任务
        - 非分布式，当 Flink Cluster 里面存在多个 JobManagers 时，只会有一个 leader 在工作，其它都是备份机(standby)
    * Flink Application Program
        - Dataflow Graph Builder: 构建数据处理的过程，Flink 应用程序的主要任务就是实现一个 builder
        - Client: 把构建好的 Dataflow Graph 发送给 JobManager，然后由 JobManager 去调度执行
    * Operation Tools
        - CLI: 命令行工具 bin/flink，可以提交打包成 jar 文件的 Flink 程序，可以控制 jobs 的执行等等
        - Web Server
            * Dashboard: 通过网页，提供 Flink Cluster 的各种信息，可以对 jobs 进行一些控制
            * Monitoring REST API: 用 REST API 的形式，提供 Flink Cluster 的各种信息，可以对 jobs 进行大部分控制操作
5. Flink 应用程序概述
    1. Flink 应用程序的基本结构
        1. 获取（构造）一个 *execution environment* 实例
        2. 指定 source operators
        3. 指定 Transformation Operators
        4. 指定 sink operators
        5. 把应用程序，通过 *execution environment* 实例，提交到 jobmanager
    2. Flink 应用程序的部署方式
        * 应用程序自主部署: 应用程序在运行过程中，把数据处理任务提交到 jobmanager
            * 同步阻塞式
            * 异步非阻塞式（detached mode）
        * 外部部署应用程序: 通过 Operation Tools，把打包的 jar 文件提交到 jobmanager
            * 同步阻塞式: CLI run
            * 异步非阻塞式（detached mode）: CLI run in detached mode，REST API

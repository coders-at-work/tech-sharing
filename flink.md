1. Flink 是 Apache 旗下的一个开源项目，是一个分布式的 **流式数据** 和 **批量数据** 处理的 **平台**。它的核心是一个流式数据处理的引擎，然后在其上，构建了批量数据处理的功能和接口。Flink 运行于 jvm 之上，提供了 scala 和 java 的 api.
2. 流式数据处理和传统的批量数据处理的区别：
    * 数据处理多为聚合（aggregate）性的，例如数据统计之类的操作
    * 数据处理的实时性
    * 数据没有永久性的存储，只会在一定范围内缓存数据
    * 可以简单理解为对数据进行实时的统计分析
3. Flink 进行流数据处理所用到的组件：
    * 在概念上分为 **stream** 和  **transformation**
        * stream 代表着数据
        * transformation 代表着对数据的处理
    * 在程序实现上，以上两个概念分别对应着　**stream** 和　**operator** 两种对象
        * operators 以一定的先后顺序组织起来，表达了数据处理的逻辑； streams 流入一个 operator，经过处理后，流出并进入下一个 operator
        * input streams 和 output streams 的数量关系是 M:N 的
        * 常见的 operator 有：map, filter, keyBy, window 等等
        * Flink 的数据处理程序包括了 stream 和 operator，这样一个完整的数据处理过程，在 Flink 中称为 **streaming dataflow**
        * 每一个 dataflow 都包含了两类特殊的 operator
            1. source: 是数据的输入来源，一个 dataflow 可以有 1 或 多 个 source
            2. sink: 是数据处理结果的输出目的地，一个 dataflow 可以有 1 或 多 个 sink
            3. 其它类型的 operators 在 Flink 中也统称为 Transformation Operators
        * Flink dataflow 的示例图： ![Flink Dataflow](https://ci.apache.org/projects/flink/flink-docs-release-1.3/fig/program_dataflow.svg)
4. 平台组件
    * TaskManager
    * JobManager
    * Flink Application Program
        * Client
        * Job Graph Builder
    * Operation Tools

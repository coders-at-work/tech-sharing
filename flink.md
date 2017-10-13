1. Flink 是 Apache 旗下的一个开源项目，是一个分布式的 *流式数据* 和 *批量数据* 处理的 *平台*。它的核心是一个流式数据处理的引擎，然后在其上，构建了批量数据处理的功能和接口。Flink 运行于 jvm 之上，提供了 scala 和 java 的 api.
2. 流式数据处理和传统的批量数据处理的区别：
    * 数据处理多为聚合（aggregate）性的，例如数据统计之类的操作
    * 数据处理的实时性
    * 数据没有永久性的存储，只会在一定范围内缓存数据
    * 可以简单理解为对数据进行实时的统计分析
3. 平台组件
    * TaskManager
    * JobManager
    * Flink Application Program
        * Client
        * Job Graph Builder
    * Operation Tools
4. 利用 Flink 进行流数据处理要用到的组件：
    * 概念上分为 stream 和  transformation
        * stream 代表着数据
        * transformation 代表着对数据的处理
    * 在程序实现上，对应着　stream 和　operator 两种对象

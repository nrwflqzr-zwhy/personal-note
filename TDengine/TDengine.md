# 产品简介

TDengine 是一款开源、高性能、云原生的[时序数据库](https://tdengine.com/tsdb/)，且针对物联网、车联网、工业互联网、金融、IT 运维等场景进行了优化。TDengine 的代码，包括集群功能，都在 GNU AGPL v3.0 下开源。除核心的时序数据库功能外，TDengine 还提供[缓存](https://docs.taosdata.com/develop/cache/)、[数据订阅](https://docs.taosdata.com/develop/tmq/)、[流式计算](https://docs.taosdata.com/develop/stream/)等其它功能以降低系统复杂度及研发和运维成本。

本章节介绍 TDengine 的主要功能、竞争优势、适用场景、与其他数据库的对比测试等等，让大家对 TDengine 有个整体的了解。

## 主要功能

TDengine 的主要功能如下：

1. 写入数据，支持

   - [SQL 写入](https://docs.taosdata.com/develop/insert-data/sql-writing/)

   - 无模式（Schemaless）写入

     ，支持多种标准写入协议

     - [InfluxDB Line 协议](https://docs.taosdata.com/develop/insert-data/influxdb-line/)
     - [OpenTSDB Telnet 协议](https://docs.taosdata.com/develop/insert-data/opentsdb-telnet/)
     - [OpenTSDB JSON 协议](https://docs.taosdata.com/develop/insert-data/opentsdb-json/)

   - 与多种第三方工具的无缝集成，它们都可以仅通过配置而无需任何代码即可将数据写入 TDengine

     - [Telegraf](https://docs.taosdata.com/third-party/telegraf/)
     - [Prometheus](https://docs.taosdata.com/third-party/prometheus/)
     - [StatsD](https://docs.taosdata.com/third-party/statsd/)
     - [collectd](https://docs.taosdata.com/third-party/collectd/)
     - [Icinga2](https://docs.taosdata.com/third-party/icinga2/)
     - [TCollector](https://docs.taosdata.com/third-party/tcollector/)
     - [EMQX](https://docs.taosdata.com/third-party/emq-broker/)
     - [HiveMQ](https://docs.taosdata.com/third-party/hive-mq-broker/)

2. 查询数据，支持

   - [标准 SQL](https://docs.taosdata.com/taos-sql/)，含嵌套查询
   - [时序数据特色函数](https://docs.taosdata.com/taos-sql/function/#time-series-extensions)
   - [时序数据特色查询](https://docs.taosdata.com/taos-sql/distinguished/)，例如降采样、插值、累加和、时间加权平均、状态窗口、会话窗口等
   - [用户自定义函数（UDF）](https://docs.taosdata.com/taos-sql/udf/)

3. [缓存](https://docs.taosdata.com/develop/cache/)，将每张表的最后一条记录缓存起来，这样无需 Redis 就能对时序数据进行高效处理

4. [流式计算（Stream Processing）](https://docs.taosdata.com/develop/stream/)，TDengine 不仅支持连续查询，还支持事件驱动的流式计算，这样在处理时序数据时就无需 Flink 或 Spark 这样流式计算组件

5. [数据订阅](https://docs.taosdata.com/develop/tmq/)，应用程序可以订阅一张表或一组表的数据，提供与 Kafka 相同的 API，而且可以指定过滤条件

6. 可视化

   - 支持与 [Grafana](https://docs.taosdata.com/third-party/grafana/) 的无缝集成
   - 支持与 Google Data Studio 的无缝集成

7. 集群

   - [集群部署](https://docs.taosdata.com/deployment/)，可以通过增加节点进行水平扩展以提升处理能力
   - 可以通过 [Kubernetes 部署 TDengine](https://docs.taosdata.com/deployment/k8s/)
   - 通过多副本提供高可用能力

8. 管理

   - [监控](https://docs.taosdata.com/operation/monitor/)运行中的 TDengine 实例
   - 多种[数据导入](https://docs.taosdata.com/operation/import/)方式
   - 多种[数据导出](https://docs.taosdata.com/operation/export/)方式

9. 工具

   - 提供[交互式命令行程序（CLI）](https://docs.taosdata.com/reference/taos-shell/)，便于管理集群，检查系统状态，做即席查询
   - 提供压力测试工具 [taosBenchmark](https://docs.taosdata.com/reference/taosbenchmark/)，用于测试 TDengine 的性能

10. 编程

    - 提供各种语言的[连接器（Connector）](https://docs.taosdata.com/connector/): 如 [C/C++](https://docs.taosdata.com/connector/cpp/)、[Java](https://docs.taosdata.com/connector/java/)、[Go](https://docs.taosdata.com/connector/go/)、[Node.js](https://docs.taosdata.com/connector/node/)、[Rust](https://docs.taosdata.com/connector/rust/)、[Python](https://docs.taosdata.com/connector/python/)、[C#](https://docs.taosdata.com/connector/csharp/) 等
    - 支持 [REST 接口](https://docs.taosdata.com/connector/rest-api/)

更多细节功能，请阅读整个文档。

## 竞争优势

由于 TDengine 充分利用了[时序数据特点](https://www.taosdata.com/blog/2019/07/09/105.html)，比如结构化、无需事务、很少删除或更新、写多读少等等，因此与其他时序数据库相比，TDengine 有以下特点：

- **[高性能](https://www.taosdata.com/tdengine/fast)**：TDengine 是唯一一个解决了时序数据存储的高基数难题的时序数据库，支持上亿数据采集点，并在数据插入、查询和数据压缩上远胜其它时序数据库。
- **[极简时序数据平台](https://www.taosdata.com/tdengine/simplified_solution_for_time-series_data_processing)**：TDengine 内建缓存、流式计算和数据订阅等功能，为时序数据的处理提供了极简的解决方案，从而大幅降低了业务系统的设计复杂度和运维成本。
- **[云原生](https://www.taosdata.com/tdengine/cloud_native_time-series_database)**：通过原生的分布式设计、数据分片和分区、存算分离、RAFT 协议、Kubernetes 部署和完整的可观测性，TDengine 是一款云原生时序数据库并且能够部署在公有云、私有云和混合云上。
- **[简单易用](https://www.taosdata.com/tdengine/ease_of_use)**：对系统管理员来说，TDengine 大幅降低了管理和维护的代价。对开发者来说， TDengine 提供了简单的接口、极简的解决方案和与第三方工具的无缝集成。对数据分析专家来说，TDengine 提供了便捷的数据访问能力。
- **[分析能力](https://www.taosdata.com/tdengine/easy_data_analytics)**：通过超级表、存储计算分离、分区分片、预计算和其它技术，TDengine 能够高效地浏览、格式化和访问数据。
- **[核心开源](https://www.taosdata.com/tdengine/open_source_time-series_database)**：TDengine 的核心代码包括集群功能全部在开源协议下公开。全球超过 140k 个运行实例，GitHub Star 20k，且拥有一个活跃的开发者社区。

采用 TDengine，可将典型的物联网、车联网、工业互联网大数据平台的总拥有成本大幅降低。表现在几个方面：

1. 由于其超强性能，它能将系统所需的计算资源和存储资源大幅降低
2. 因为支持 SQL，能与众多第三方软件无缝集成，学习迁移成本大幅下降
3. 因为是一款极简的时序数据平台，系统复杂度、研发和运营成本大幅降低

## 技术生态

在整个时序大数据平台中，TDengine 扮演的角色如下：

![TDengine Database 技术生态图](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/eco_system-e7df30b8384261a015b003f4125b9ddf.webp)

<center>图 1. TDengine 技术生态图</center>

上图中，左侧是各种数据采集或消息队列，包括 OPC-UA、MQTT、Telegraf、也包括 Kafka，他们的数据将被源源不断的写入到 TDengine。右侧则是可视化、BI  工具、组态软件、应用程序。下侧则是 TDengine 自身提供的命令行程序（CLI）以及可视化管理工具。

## 典型适用场景

作为一个高性能、分布式、支持 SQL 的时序数据库（Database），TDengine 的典型适用场景包括但不限于 IoT、工业互联网、车联网、IT  运维、能源、金融证券等领域。需要指出的是，TDengine  是针对时序数据场景设计的专用数据库和专用大数据处理工具，因其充分利用了时序大数据的特点，它无法用来处理网络爬虫、微博、微信、电商、ERP、CRM 等通用型数据。下面本文将对适用场景做更多详细的分析。

### 数据源特点和需求

从数据源角度，设计人员可以从下面几个角度分析 TDengine 在目标应用系统里面的适用性。

| 数据源特点和需求             | 不适用 | 可能适用 | 非常适用 | 简单说明                                                     |
| ---------------------------- | ------ | -------- | -------- | ------------------------------------------------------------ |
| 总体数据量巨大               |        |          | √        | TDengine 在容量方面提供出色的水平扩展功能，并且具备匹配高压缩的存储结构，达到业界最优的存储效率。 |
| 数据输入速度偶尔或者持续巨大 |        |          | √        | TDengine 的性能大大超过同类产品，可以在同样的硬件环境下持续处理大量的输入数据，并且提供很容易在用户环境里面运行的性能评估工具。 |
| 数据源数目巨大               |        |          | √        | TDengine 设计中包含专门针对大量数据源的优化，包括数据的写入和查询，尤其适合高效处理海量（千万或者更多量级）的数据源。 |

### 系统架构要求

| 系统架构要求           | 不适用 | 可能适用 | 非常适用 | 简单说明                                                     |
| ---------------------- | ------ | -------- | -------- | ------------------------------------------------------------ |
| 要求简单可靠的系统架构 |        |          | √        | TDengine 的系统架构非常简单可靠，自带消息队列，缓存，流式计算，监控等功能，无需集成额外的第三方产品。 |
| 要求容错和高可靠       |        |          | √        | TDengine 的集群功能，自动提供容错灾备等高可靠功能。          |
| 标准化规范             |        |          | √        | TDengine 使用标准的 SQL 语言提供主要功能，遵守标准化规范。   |

### 系统功能需求

| 系统功能需求               | 不适用 | 可能适用 | 非常适用 | 简单说明                                                     |
| -------------------------- | ------ | -------- | -------- | ------------------------------------------------------------ |
| 要求完整的内置数据处理算法 |        | √        |          | TDengine 实现了通用的数据处理算法，但是还没有做到妥善处理各行各业的所有需求，因此特殊类型的处理需求还需要在应用层面解决。 |
| 需要大量的交叉查询处理     |        | √        |          | 这种类型的处理更多应该用关系型数据库处理，或者应该考虑 TDengine 和关系型数据库配合实现系统功能。 |

### 系统性能需求

| 系统性能需求           | 不适用 | 可能适用 | 非常适用 | 简单说明                                                     |
| ---------------------- | ------ | -------- | -------- | ------------------------------------------------------------ |
| 要求较大的总体处理能力 |        |          | √        | TDengine 的集群功能可以轻松地让多服务器配合达成处理能力的提升。 |
| 要求高速处理数据       |        |          | √        | TDengine 专门为 IoT 优化的存储和数据处理设计，一般可以让系统得到超出同类产品多倍数的处理速度提升。 |
| 要求快速处理小粒度数据 |        |          | √        | 这方面 TDengine 性能可以完全对标关系型和 NoSQL 型数据处理系统。 |

### 系统维护需求

| 系统维护需求           | 不适用 | 可能适用 | 非常适用 | 简单说明                                                     |
| ---------------------- | ------ | -------- | -------- | ------------------------------------------------------------ |
| 要求系统可靠运行       |        |          | √        | TDengine 的系统架构非常稳定可靠，日常维护也简单便捷，对维护人员的要求简洁明了，最大程度上杜绝人为错误和事故。 |
| 要求运维学习成本可控   |        |          | √        | 同上。                                                       |
| 要求市场有大量人才储备 | √      |          |          | TDengine 作为新一代产品，目前人才市场里面有经验的人员还有限。但是学习成本低，我们作为厂家也提供运维的培训和辅助服务。 |

## 与其他数据库的对比测试

- [用 InfluxDB 开源的性能测试工具对比 InfluxDB 和 TDengine](https://www.taosdata.com/blog/2020/01/13/1105.html)
- [TDengine 与 OpenTSDB 对比测试](https://www.taosdata.com/blog/2019/08/21/621.html)
- [TDengine 与 Cassandra 对比测试](https://www.taosdata.com/blog/2019/08/14/573.html)
- [TDengine VS InfluxDB ，写入性能大 PK ！](https://www.taosdata.com/2021/11/05/3248.html)
- [TDengine 和 InfluxDB 查询性能对比测试报告](https://www.taosdata.com/2022/02/22/5969.html)
- [TDengine 与 InfluxDB、OpenTSDB、Cassandra、MySQL、ClickHouse 等数据库的对比测试报告](https://www.taosdata.com/downloads/TDengine_Testing_Report_cn.pdf)



# 数据模型和基本概念

为了便于解释基本概念，便于撰写示例程序，整个 TDengine  文档以智能电表作为典型时序数据场景。假设每个智能电表采集电流、电压、相位三个量，有多个智能电表，每个电表有位置 Location 和分组  Group ID 的静态属性. 其采集的数据类似如下的表格：

| Device ID | Timestamp     | Collected Metrics | Tags     |         |                         |      |
| --------- | ------------- | ----------------- | -------- | ------- | ----------------------- | ---- |
| current   | voltage       | phase             | location | groupid |                         |      |
| d1001     | 1538548685000 | 10.3              | 219      | 0.31    | California.SanFrancisco | 2    |
| d1002     | 1538548684000 | 10.2              | 220      | 0.23    | California.SanFrancisco | 3    |
| d1003     | 1538548686500 | 11.5              | 221      | 0.35    | California.LosAngeles   | 3    |
| d1004     | 1538548685500 | 13.4              | 223      | 0.29    | California.LosAngeles   | 2    |
| d1001     | 1538548695000 | 12.6              | 218      | 0.33    | California.SanFrancisco | 2    |
| d1004     | 1538548696600 | 11.8              | 221      | 0.28    | California.LosAngeles   | 2    |
| d1002     | 1538548696650 | 10.3              | 218      | 0.25    | California.SanFrancisco | 3    |
| d1001     | 1538548696800 | 12.3              | 221      | 0.31    | California.SanFrancisco | 2    |

表 1. 智能电表数据示例

每一条记录都有设备 ID、时间戳、采集的物理量（如上表中的 `current`、`voltage` 和 `phase`）以及每个设备相关的静态标签（`location` 和 `groupid`）。每个设备是受外界的触发，或按照设定的周期采集数据。采集的数据点是时序的，是一个数据流。

## 采集量（Metric）

采集量是指传感器、设备或其他类型采集点采集的物理量，比如电流、电压、温度、压力、GPS 位置等，是随时间变化的，数据类型可以是整型、浮点型、布尔型，也可是字符串。随着时间的推移，存储的采集量的数据量越来越大。智能电表示例中的电流、电压、相位就是采集量。

## 标签（Label/Tag）

标签是指传感器、设备或其他类型采集点的静态属性，不是随时间变化的，比如设备型号、颜色、设备的所在地等，数据类型可以是任何类型。虽然是静态的，但 TDengine 容许用户修改、删除或增加标签值。与采集量不一样的是，随时间的推移，存储的标签的数据量不会有什么变化。智能电表示例中的 `location` 与 `groupid` 就是标签。

## 数据采集点（Data Collection Point）

数据采集点是指按照预设时间周期或受事件触发采集物理量的硬件或软件。一个数据采集点可以采集一个或多个采集量，**但这些采集量都是同一时刻采集的，具有相同的时间戳**。对于复杂的设备，往往有多个数据采集点，每个数据采集点采集的周期都可能不一样，而且完全独立，不同步。比如对于一台汽车，有数据采集点专门采集 GPS 位置，有数据采集点专门采集发动机状态，有数据采集点专门采集车内的环境，这样一台汽车就有三个数据采集点。智能电表示例中的  d1001、d1002、d1003、d1004 等就是数据采集点。

## 表（Table）

因为采集量一般是结构化数据，同时为降低学习门槛，TDengine 采用传统的关系型数据库模型管理数据。用户需要先创建库，然后创建表，之后才能插入或查询数据。

为充分利用其数据的时序性和其他数据特点，TDengine 采取**一个数据采集点一张表**的策略，要求对每个数据采集点单独建表（比如有一千万个智能电表，就需创建一千万张表，上述表格中的 d1001，d1002，d1003，d1004 都需单独建表），用来存储这个数据采集点所采集的时序数据。这种设计有几大优点：

1. 由于不同数据采集点产生数据的过程完全独立，每个数据采集点的数据源是唯一的，一张表也就只有一个写入者，这样就**可采用无锁方式**来写，写入速度就能大幅提升。
2. 对于一个数据采集点而言，其产生的数据是按照时间排序的，因此写的操作可用追加的方式实现，进一步大幅提高数据写入速度。
3. 一个数据采集点的数据是以块为单位连续存储的。如果读取一个时间段的数据，它能大幅减少随机读取操作，成数量级的提升读取和查询速度。
4. 一个数据块内部，采用列式存储，**对于不同数据类型，采用不同压缩算法**，而且由于一个数据采集点的采集量的变化是缓慢的，压缩率更高。

如果采用传统的方式，将多个数据采集点的数据写入一张表，由于网络延时不可控，不同数据采集点的数据到达服务器的时序是无法保证的，写入操作是要有锁保护的，而且一个数据采集点的数据是难以保证连续存储在一起的。**采用一个数据采集点一张表的方式，能最大程度的保证单个数据采集点的插入和查询的性能是最优的。**

==**TDengine 建议用数据采集点的名字（如上表中的 d1001）来做表名**==。每个数据采集点可能同时采集多个采集量（如上表中的 `current`、`voltage` 和 `phase`），**每个采集量对应一张表中的一列**，数据类型可以是整型、浮点型、字符串等。除此之外，==**表的第一列必须是时间戳**==，即数据类型为 Timestamp。对采集量，TDengine 将自动按照时间戳建立索引，但对采集量本身不建任何索引。数据用列式存储方式保存。

对于复杂的设备，比如汽车，它有多个数据采集点，那么就需要为一辆汽车建立多张表。

## 超级表（STable）

由于一个数据采集点一张表，导致表的数量巨增，难以管理，而且应用经常需要做采集点之间的聚合操作，聚合的操作也变得复杂起来。为解决这个问题，TDengine 引入超级表（Super Table，简称为 STable）的概念。

**超级表是指某一特定类型的数据采集点的集合**。同一类型的数据采集点，其表的结构是完全一样的，但每个表（数据采集点）的静态属性（标签）是不一样的。描述一个超级表（某一特定类型的数据采集点的集合），除需要定义采集量的表结构之外，还需要定义其标签的 Schema，标签的数据类型可以是整数、浮点数、字符串、JSON，标签可以有多个，可以事后增加、删除或修改。**如果整个系统有 N  个不同类型的数据采集点，就需要建立 N 个超级表。**超级表的数量与数据采集点的类型一一对应

在 TDengine 的设计里，**表用来代表一个具体的数据采集点，超级表用来代表一组相同类型的数据采集点集合**。智能电表示例中，我们可以创建一个超级表 `meters`.

## 子表（Subtable）

当为某个具体数据采集点创建表时，用户可以使用超级表的定义做模板，同时指定该具体采集点（表）的具体标签值来创建该表。**通过超级表创建的表称之为子表**。正常的表与子表的差异在于：

1. 子表就是表，因此所有正常表的 SQL 操作都可以在子表上执行。
2. 子表在正常表的基础上有扩展，它是**带有静态标签**的，而且这些标签可以事后增加、删除、修改，而正常的表没有。
3. 子表一定属于一张超级表，但普通表不属于任何超级表
4. 普通表无法转为子表，子表也无法转为普通表。

超级表与基于超级表建立的子表之间的关系表现在：

1. 一张超级表包含有多张子表，这些子表具有相同的采集量 Schema，但带有不同的标签值。
2. 不能通过子表调整数据或标签的模式，**对于超级表的数据模式修改立即对所有的子表生效。**
3. 超级表只定义一个模板，自身不存储任何数据或标签信息。因此，不能向一个超级表写入数据，只能将数据写入子表中。

查询既可以在表上进行，也可以在超级表上进行。**针对超级表的查询，TDengine  将把所有子表中的数据视为一个整体数据集进行处理，**会先把满足标签过滤条件的表从超级表中找出来，然后再扫描这些表的时序数据，进行聚合操作，这样需要扫描的数据集会大幅减少，从而显著提高查询的性能。本质上，TDengine 通过对超级表查询的支持，实现了多个同类数据采集点的高效聚合。

TDengine 系统建议给一个数据采集点建表，需要通过超级表建表，而不是建普通表。在智能电表的示例中，我们可以通过超级表 `meters` 创建子表 d1001、d1002、d1003、d1004 等。

为了更好地理解采集量、标签、超级与子表的关系，可以参考下面关于智能电表数据模型的示意图。

![智能电表数据模型示意图](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/supertable-f2896ade8b7eeb2694f5c23efb6ed9cc.webp)

<center>图 1. 智能电表数据模型示意图</center>

## 库（Database）

库是指一组表的集合。TDengine  容许一个运行实例有多个库，而且**每个库可以配置不同的存储策略**。不同类型的数据采集点往往具有不同的数据特征，包括**数据采集频率的高低，数据保留时间的长短，副本的数目，数据块的大小，是否允许更新数据**等等。为了在各种场景下 TDengine 都能最大效率的工作，TDengine 建议将不同数据特征的超级表创建在不同的库里。

一个库里，可以有一到多个超级表，但一个超级表只属于一个库。一个超级表所拥有的子表全部存在一个库里。

## FQDN & Endpoint

FQDN（Fully Qualified Domain Name，完全限定域名）是 Internet 上特定计算机或主机的完整域名。FQDN  由两部分组成:主机名和域名。例如，假设邮件服务器的 FQDN 可能是 mail.tdengine.com。主机名是 mail，主机位于域名  tdengine.com 中。DNS（Domain Name System），负责将 FQDN 翻译成 IP，是互联网应用的寻址方式。对于没有  DNS 的系统，可以通过配置 hosts 文件来解决。

TDengine 集群的每个节点是由 Endpoint  来唯一标识的，Endpoint 是由 FQDN 外加 Port 组成，比如 h1.tdengine.com:6030。这样当 IP  发生变化的时候，我们依然可以使用 FQDN 来动态找到节点，不需要更改集群的任何配置。而且采用 FQDN，便于内网和外网对同一个集群的统一访问。

TDengine 不建议采用直接的 IP 地址访问集群，不利于管理。不了解 FQDN 概念，请看博文[《一篇文章说清楚 TDengine 的 FQDN》](https://www.taosdata.com/blog/2020/09/11/1824.html)。



# 通过 Docker 快速体验 TDengine

本节首先介绍如何通过 Docker 快速体验 TDengine，然后介绍如何在 Docker 环境下体验 TDengine 的写入和查询功能。如果你不熟悉 Docker，请使用[安装包的方式快速体验](https://docs.taosdata.com/get-started/package/)。如果您希望为 TDengine 贡献代码或对内部技术实现感兴趣，请参考 [TDengine GitHub 主页](https://github.com/taosdata/TDengine)下载源码构建和安装。

## 启动 TDengine

如果已经安装了 Docker，首先拉取最新的 TDengine 容器镜像：

```shell
docker pull tdengine/tdengine:latest
```

或者指定版本的容器镜像：

```shell
docker pull tdengine/tdengine:3.0.1.4
```

然后只需执行下面的命令：

```shell
docker run -d -p 6030:6030 -p 6041:6041 -p 6043-6049:6043-6049 -p 6043-6049:6043-6049/udp tdengine/tdengine
```

注意：TDengine 3.0 服务端仅使用 6030 TCP 端口。6041 为 taosAdapter 所使用提供 REST 服务端口。6043-6049 为 taosAdapter 提供第三方应用接入所使用端口，可根据需要选择是否打开。

确定该容器已经启动并且在正常运行。

```shell
docker ps
```

进入该容器并执行 `bash`

```shell
docker exec -it <container name> bash
```

然后就可以执行相关的 Linux 命令操作和访问 TDengine。

注：Docker 工具自身的下载和使用请参考 [Docker 官网文档](https://docs.docker.com/get-docker/)。

## 运行 TDengine CLI

进入容器，执行 `taos`：

```text
$ taos

taos>
```

## 使用 taosBenchmark 体验写入速度

可以使用 TDengine 的自带工具 taosBenchmark 快速体验 TDengine 的写入速度。

启动 TDengine 的服务，在终端执行 `taosBenchmark`（曾命名为 `taosdemo`）：

```bash
$ taosBenchmark
```

该命令将在数据库 `test` 下面自动创建一张超级表 `meters`，该超级表下有 1 万张表，表名为 `d0` 到 `d9999`，每张表有 1 万条记录，每条记录有 `ts`、`current`、`voltage`、`phase` 四个字段，时间戳从 2017-07-14 10:40:00 000 到 2017-07-14 10:40:09 999，每张表带有标签 `location` 和 `groupId`，groupId 被设置为 1 到 10，location 被设置为 `California.Campbell`、`California.Cupertino`、`California.LosAngeles`、`California.MountainView`、`California.PaloAlto`、`California.SanDiego`、`California.SanFrancisco`、`California.SanJose`、`California.SantaClara` 或者 `California.Sunnyvale`。

这条命令很快完成 1 亿条记录的插入。具体时间取决于硬件性能，即使在一台普通的 PC 服务器往往也仅需十几秒。

taosBenchmark 命令本身带有很多选项，配置表的数目、记录条数等等，您可以设置不同参数进行体验，请执行 `taosBenchmark --help` 详细列出。taosBenchmark 详细使用方法请参照[如何使用 taosBenchmark 对 TDengine 进行性能测试](https://www.taosdata.com/2021/10/09/3111.html)和 [taosBenchmark 参考手册](https://docs.taosdata.com/reference/taosbenchmark/)。

## 使用 TDengine CLI 体验查询速度

使用上述 `taosBenchmark` 插入数据后，可以在 TDengine CLI（taos）输入查询命令，体验查询速度。

查询超级表 `meters` 下的记录总条数：

```sql
SELECT COUNT(*) FROM test.meters;
```

查询 1 亿条记录的平均值、最大值、最小值等：

```sql
SELECT AVG(current), MAX(voltage), MIN(phase) FROM test.meters;
```

查询 location = "California.SanFrancisco" 的记录总条数：

```sql
SELECT COUNT(*) FROM test.meters WHERE location = "California.SanFrancisco";
```

查询 groupId = 10 的所有记录的平均值、最大值、最小值等：

```sql
SELECT AVG(current), MAX(voltage), MIN(phase) FROM test.meters WHERE groupId = 10;
```

对表 `d10` 按 10 每秒进行平均值、最大值和最小值聚合统计：

```sql
SELECT FIRST(ts), AVG(current), MAX(voltage), MIN(phase) FROM test.d10 INTERVAL(10s);
```

在上面的查询中，你选择的是区间内的第一个时间戳（ts），另一种选择方式是 `\_wstart`，它将给出时间窗口的开始。关于窗口查询的更多信息，参见[特色查询](https://docs.taosdata.com/taos-sql/distinguished/)。

## 其它

更多关于在 Docker 环境下使用 TDengine 的细节，请参考 [在 Docker 下使用 TDengine](https://docs.taosdata.com/reference/docker/)。使用安装包立即开始

# 使用安装包立即开始

您可以[用 Docker 立即体验](https://docs.taosdata.com/get-started/docker/) TDengine。如果您希望对 TDengine 贡献代码或对内部实现感兴趣，请参考我们的 [TDengine GitHub 主页](https://github.com/taosdata/TDengine) 下载源码构建和安装.

TDengine 完整的软件包包括服务端（taosd）、应用驱动（taosc）、用于与第三方系统对接并提供 RESTful 接口的  taosAdapter、命令行程序（CLI，taos）和一些工具软件。目前 TDinsight 仅在 Linux 系统上安装和运行，后续将支持  Windows、macOS 等系统。TDengine 除了提供多种语言的连接器之外，还通过 [taosAdapter](https://docs.taosdata.com/reference/taosadapter/) 提供 [RESTful 接口](https://docs.taosdata.com/connector/rest-api/)。

为方便使用，标准的服务端安装包包含了 taosd、taosAdapter、taosc、taos、taosdump、taosBenchmark、TDinsight  安装脚本和示例代码；如果您只需要用到服务端程序和客户端连接的 C/C++ 语言支持，也可以仅下载 Lite 版本的安装包。

在  Linux 系统上，TDengine 社区版提供 Deb 和 RPM 格式安装包，用户可以根据自己的运行环境选择合适的安装包。其中 Deb 支持 Debian/Ubuntu 及其衍生系统，RPM 支持 CentOS/RHEL/SUSE 及其衍生系统。同时我们也为企业用户提供 tar.gz 格式安装包，也支持通过 `apt-get` 工具从线上进行安装。需要注意的是，RPM 和 Deb 包不含 `taosdump` 和 TDinsight 安装脚本，这些工具需要通过安装 taosTools 包获得。TDengine 也提供 Windows x64 平台和 macOS x64/m1 平台的安装包。

## 安装

- Deb 安装
- RPM 安装
- tar.gz 安装
- apt-get
- Windows 安装
- macOS 安装

1. 从列表中下载获得 Deb 安装包；
   - [TDengine-server-3.0.4.1-Linux-x64.deb (45.4 M)](https://docs.taosdata.com/get-started/package/#!)
   - [taosTools-2.5.0-Linux-x64-comp3.deb (0.3 M)](https://docs.taosdata.com/get-started/package/#!)
2. 进入到安装包所在目录，执行如下的安装命令：

> 请将 `<version>` 替换为下载的安装包版本

```bash
sudo dpkg -i TDengine-server-<version>-Linux-x64.deb
```



##### info

下载其他组件、最新 Beta 版及之前版本的安装包，请点击[发布历史页面](https://docs.taosdata.com/releases/tdengine/)。



##### note

当安装第一个节点时，出现 `Enter FQDN:` 提示的时候，不需要输入任何内容。只有当安装第二个或以后更多的节点时，才需要输入已有集群中任何一个可用节点的 FQDN，支持该新节点加入集群。当然也可以不输入，而是在新节点启动前，配置到新节点的配置文件中。

## 启动

- Linux 系统
- Windows 系统
- macOS 系统

安装后，请使用 `systemctl` 命令来启动 TDengine 的服务进程。

```bash
systemctl start taosd
```

检查服务是否正常工作：

```bash
systemctl status taosd
```

如果服务进程处于活动状态，则 status 指令会显示如下的相关信息：

```text
Active: active (running)
```

如果后台服务进程处于停止状态，则 status 指令会显示如下的相关信息：

```text
Active: inactive (dead)
```

如果 TDengine 服务正常工作，那么您可以通过 TDengine 的命令行程序 `taos` 来访问并体验 TDengine。

如下 `systemctl` 命令可以帮助你管理 TDengine 服务：

- 启动服务进程：`systemctl start taosd`
- 停止服务进程：`systemctl stop taosd`
- 重启服务进程：`systemctl restart taosd`
- 查看服务状态：`systemctl status taosd`

##### info

- `systemctl` 命令需要 *root* 权限来运行，如果您非 *root* 用户，请在命令前添加 `sudo`。
- `systemctl stop taosd` 指令在执行后并不会马上停止 TDengine 服务，而是会等待系统中必要的落盘工作正常完成。在数据量很大的情况下，这可能会消耗较长时间。
- 如果系统中不支持 `systemd`，也可以用**手动运行 `/usr/local/taos/bin/taosd`** 方式启动 TDengine 服务。

**TDengine 命令行（CLI）**

为便于检查 TDengine 的状态，执行数据库（Database）的各种即席（Ad Hoc）查询，TDengine 提供一命令行应用程序（以下简称为 TDengine CLI）taos。要进入 TDengine 命令行，您只要在终端执行 `taos` 即可。

```bash
taos
```

如果连接服务成功，将会打印出欢迎消息和版本信息。如果失败，则会打印错误消息出来（请参考 [FAQ](https://docs.taosdata.com/train-faq/faq/) 来解决终端连接服务端失败的问题）。TDengine CLI 的提示符号如下：

```cmd
taos>
```

在 TDengine CLI 中，用户可以通过 SQL 命令来创建/删除数据库、表等，并进行数据库（Database）插入查询操作。在终端中运行的 SQL 语句需要以分号（;）结束来运行。示例：

```sql
CREATE DATABASE demo;
USE demo;
CREATE TABLE t (ts TIMESTAMP, speed INT);
INSERT INTO t VALUES ('2019-07-15 00:00:00', 10);
INSERT INTO t VALUES ('2019-07-15 01:00:00', 20);
SELECT * FROM t;

           ts            |    speed    |
========================================
 2019-07-15 00:00:00.000 |          10 |
 2019-07-15 01:00:00.000 |          20 |

Query OK, 2 row(s) in set (0.003128s)
```

除执行 SQL 语句外，系统管理员还可以从 TDengine CLI 进行检查系统运行状态、添加删除用户账号等操作。TDengine CLI 连同应用驱动也可以独立安装在机器上运行，更多细节请参考 [TDengine 命令行](https://docs.taosdata.com/reference/taos-shell/)。

## 使用 taosBenchmark 体验写入速度

可以使用 TDengine 的自带工具 taosBenchmark 快速体验 TDengine 的写入速度。

启动 TDengine 服务，然后在终端执行 `taosBenchmark`（曾命名为 `taosdemo`）：

```bash
$ taosBenchmark
```

该命令将在数据库 `test` 下面自动创建一张超级表 `meters`，该超级表下有 1 万张表，表名为 `d0` 到 `d9999`，每张表有 1 万条记录，每条记录有 `ts`、`current`、`voltage`、`phase` 四个字段，时间戳从 2017-07-14 10:40:00 000 到 2017-07-14 10:40:09 999，每张表带有标签 `location` 和 `groupId`，groupId 被设置为 1 到 10，location 被设置为 `California.Campbell`、`California.Cupertino`、`California.LosAngeles`、`California.MountainView`、`California.PaloAlto`、`California.SanDiego`、`California.SanFrancisco`、`California.SanJose`、`California.SantaClara` 或者 `California.Sunnyvale`。

这条命令很快完成 1 亿条记录的插入。具体时间取决于硬件性能，即使在一台普通的 PC 服务器往往也仅需十几秒。

taosBenchmark 命令本身带有很多选项，配置表的数目、记录条数等等，您可以设置不同参数进行体验，请执行 `taosBenchmark --help` 详细列出。taosBenchmark 详细使用方法请参照[如何使用 taosBenchmark 对 TDengine 进行性能测试](https://www.taosdata.com/2021/10/09/3111.html)和 [taosBenchmark 参考手册](https://docs.taosdata.com/reference/taosbenchmark/)。

## 使用 TDengine CLI 体验查询速度

使用上述 `taosBenchmark` 插入数据后，可以在 TDengine CLI（taos）输入查询命令，体验查询速度。

查询超级表 `meters` 下的记录总条数：

```sql
SELECT COUNT(*) FROM test.meters;
```

查询 1 亿条记录的平均值、最大值、最小值等：

```sql
SELECT AVG(current), MAX(voltage), MIN(phase) FROM test.meters;
```

查询 location = "California.SanFrancisco" 的记录总条数：

```sql
SELECT COUNT(*) FROM test.meters WHERE location = "California.SanFrancisco";
```

查询 groupId = 10 的所有记录的平均值、最大值、最小值等：

```sql
SELECT AVG(current), MAX(voltage), MIN(phase) FROM test.meters WHERE groupId = 10;
```

对表 `d10` 按 10 每秒进行平均值、最大值和最小值聚合统计：

```sql
SELECT FIRST(ts), AVG(current), MAX(voltage), MIN(phase) FROM test.d10 INTERVAL(10s);
```

在上面的查询中，你选择的是区间内的第一个时间戳（ts），另一种选择方式是 `\_wstart`，它将给出时间窗口的开始。关于窗口查询的更多信息，参见[特色查询](https://docs.taosdata.com/taos-sql/distinguished/)。



# 开发指南

开发一个应用，如果你准备采用 TDengine 作为时序数据处理的工具，那么有如下几个事情要做：

1. 确定应用到 TDengine 的连接方式。无论你使用何种编程语言，你总是可以使用 REST 接口, 但也可以使用每种编程语言独有的连接器进行方便的连接。
2. 根据自己的应用场景，确定数据模型。根据数据特征，决定建立一个还是多个库；分清静态标签、采集量，建立正确的超级表，建立子表。
3. 决定插入数据的方式。TDengine 支持使用标准的 SQL 写入，但同时也支持 Schemaless 模式写入，这样不用手工建表，可以将数据直接写入。
4. 根据业务要求，看需要撰写哪些 SQL 查询语句。
5. 如果你要基于时序数据做轻量级的实时统计分析，包括各种监测看板，那么建议你采用 TDengine 3.0 的流式计算功能，而不用额外部署 Spark, Flink 等复杂的流式计算系统。
6. 如果你的应用有模块需要消费插入的数据，希望有新的数据插入时，就能获取通知，那么建议你采用 TDengine 提供的数据订阅功能，而无需专门部署 Kafka 或其他消息队列软件。
7. 在很多场景下（如车辆管理），应用需要获取每个数据采集点的最新状态，那么建议你采用 TDengine 的 Cache 功能，而不用单独部署 Redis 等缓存软件。
8. 如果你发现 TDengine 的函数无法满足你的要求，那么你可以使用用户自定义函数（UDF）来解决问题。

本部分内容就是按照上述顺序组织的。为便于理解，TDengine 为每个功能和每个支持的编程语言都提供了示例代码。如果你希望深入了解 SQL 的使用，需要查看[SQL 手册](https://docs.taosdata.com/taos-sql/)。如果想更深入地了解各连接器的使用，请阅读[连接器参考指南](https://docs.taosdata.com/connector/)。如果还希望想将 TDengine 与第三方系统集成起来，比如 Grafana, 请参考[第三方工具](https://docs.taosdata.com/third-party/)。

## 建立连接

TDengine  提供了丰富的应用程序开发接口，为了便于用户快速开发自己的应用，TDengine 支持了多种编程语言的连接器，其中官方连接器包括支持  C/C++、Java、Python、Go、Node.js、C#、Rust、Lua（社区贡献）和 PHP  （社区贡献）的连接器。这些连接器支持使用原生接口（taosc）和 REST 接口（部分语言暂不支持）连接 TDengine  集群。社区开发者也贡献了多个非官方连接器，例如 ADO.NET 连接器、Lua 连接器和 PHP 连接器。

### 连接器建立连接的方式

连接器建立连接的方式，TDengine 提供两种:

1. 通过 taosAdapter 组件提供的 REST API 建立与 taosd 的连接，这种连接方式下文中简称“REST 连接”
2. 通过客户端驱动程序 taosc 直接与服务端程序 taosd 建立连接，这种连接方式下文中简称“原生连接”。

无论使用何种方式建立连接，连接器都提供了相同或相似的 API 操作数据库，都可以执行 SQL 语句，只是初始化连接的方式稍有不同，用户在使用上不会感到什么差别。

关键不同点在于：

1. 使用 REST 连接，用户无需安装客户端驱动程序 taosc，具有跨平台易用的优势，但性能要下降 30% 左右。
2. 使用原生连接可以体验 TDengine 的全部功能，如[参数绑定接口](https://docs.taosdata.com/connector/cpp/#参数绑定-api)、[订阅](https://docs.taosdata.com/connector/cpp/#订阅和消费-api)等等。

### 安装客户端驱动 taosc

如果选择原生连接，而且应用程序不在 TDengine 同一台服务器上运行，你需要先安装客户端驱动，否则可以跳过此一步。为避免客户端驱动和服务端不兼容，请使用一致的版本。

#### 安装步骤

- Linux
- Windows
- macOS

1. 下载客户端安装包

   - [TDengine-client-3.0.4.1-Linux-x64.tar.gz (34.6 M)](https://docs.taosdata.com/develop/connect/#!)
   - [TDengine-client-3.0.4.1-Linux-arm64.tar.gz (10.4 M)](https://docs.taosdata.com/develop/connect/#!)
   - [TDengine-client-3.0.4.1-Linux-x64-Lite.tar.gz (6.4 M)](https://docs.taosdata.com/develop/connect/#!)

    [所有下载](https://docs.taosdata.com/releases/tdengine/)

2. 解压缩软件包

   将软件包放置在当前用户可读写的任意目录下，然后执行下面的命令：`tar -xzvf TDengine-client-VERSION.tar.gz` 其中 VERSION 需要替换为实际版本的字符串。

3. 执行安装脚本

   解压软件包之后，会在解压目录下看到以下文件(目录)：

   -  *install_client.sh*：安装脚本，用于应用驱动程序
   -  *package.tar.gz*：应用驱动安装包
   -  *driver*：TDengine 应用驱动 driver
   - *examples*: 各种编程语言的示例程序(c/C#/go/JDBC/MATLAB/python/R) 运行 install_client.sh 进行安装。

4. 配置 taos.cfg

   编辑 `taos.cfg` 文件（默认路径/etc/taos/taos.cfg），将 `firstEP` 修改为 TDengine 服务器的 End Point，例如：`h1.tdengine.com:6030`

##### tip

1. 如本机没有部署 TDengine 服务，仅安装了应用驱动，则 `taos.cfg` 中仅需配置 `firstEP`，无需在本机配置 `FQDN`。
2. 为防止与服务器端连接时出现“Unable to resolve FQDN”错误，建议确认本机的 `/etc/hosts` 文件已经配置了服务器正确的 FQDN 值，或配置好了 DNS 服务。

#### 安装验证

以上安装和配置完成后，并确认 TDengine 服务已经正常启动运行，此时可以执行安装包里带有的 TDengine 命令行程序 taos 进行登录。

- Linux
- Windows
- macOS

在 Linux shell 下直接执行 `taos` 连接到 TDengine 服务，进入到 TDengine CLI 界面，示例如下：

```text
$ taos

taos> show databases;
              name              |
=================================
 information_schema             |
 performance_schema             |
 db                             |
Query OK, 3 rows in database (0.019154s)

taos>
```

### 安装连接器



如果使用 Maven 管理项目，只需在 pom.xml 中加入以下依赖。

```xml
<dependency>
  <groupId>com.taosdata.jdbc</groupId>
  <artifactId>taos-jdbcdriver</artifactId>
  <version>3.0.0</version>
</dependency>
```

### 建立连接

在执行这一步之前，请确保有一个正在运行的，且可以访问到的 TDengine，而且服务端的 FQDN 配置正确。以下示例代码，都假设 TDengine 安装在本机，且 FQDN（默认  localhost） 和 serverPort（默认 6030） 都使用默认配置。

原生连接

```java
package com.taos.example;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Properties;

import com.taosdata.jdbc.TSDBDriver;

public class JNIConnectExample {
    public static void main(String[] args) throws SQLException {
        String jdbcUrl = "jdbc:TAOS://localhost:6030?user=root&password=taosdata";
        Properties connProps = new Properties();
        connProps.setProperty(TSDBDriver.PROPERTY_KEY_CHARSET, "UTF-8");
        connProps.setProperty(TSDBDriver.PROPERTY_KEY_LOCALE, "en_US.UTF-8");
        connProps.setProperty(TSDBDriver.PROPERTY_KEY_TIME_ZONE, "UTC-8");
        Connection conn = DriverManager.getConnection(jdbcUrl, connProps);
        System.out.println("Connected");
        conn.close();
    }
}

// use
// String jdbcUrl = "jdbc:TAOS://localhost:6030/dbName?user=root&password=taosdata";
// if you want to connect a specified database named "dbName".
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/java/src/main/java/com/taos/example/JNIConnectExample.java)

REST 连接

```java
    public static void main(String[] args) throws SQLException {
        String jdbcUrl = "jdbc:TAOS-RS://localhost:6041?user=root&password=taosdata";
        Connection conn = DriverManager.getConnection(jdbcUrl);
        System.out.println("Connected");
        conn.close();
    }
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/java/src/main/java/com/taos/example/RESTConnectExample.java)

使用 REST 连接时，如果查询数据量比较大，还可开启批量拉取功能。

开启批量拉取功能

```java
    public static void main(String[] args) throws SQLException {
        String jdbcUrl = "jdbc:TAOS-RS://localhost:6041?user=root&password=taosdata";
        Properties connProps = new Properties();
        connProps.setProperty(TSDBDriver.PROPERTY_KEY_BATCH_LOAD, "true");
        Connection conn = DriverManager.getConnection(jdbcUrl, connProps);
        System.out.println("Connected");
        conn.close();
    }
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/java/src/main/java/com/taos/example/WSConnectExample.java)

更多连接参数配置，参考[Java 连接器](https://docs.taosdata.com/connector/java/)

##### tip

如果建立连接失败，大部分情况下是 FQDN 或防火墙的配置不正确，详细的排查方法请看[《常见问题及反馈》](https://docs.taosdata.com/train-faq/faq)中的“遇到错误 Unable to establish connection, 我怎么办？”

## TDengine 数据建模

TDengine 采用类关系型数据模型，需要建库、建表。因此对于一个具体的应用场景，需要考虑**库、超级表和普通表**的设计。本节不讨论细致的语法规则，只介绍概念。

关于数据建模请参考[视频教程](https://www.taosdata.com/blog/2020/11/11/1945.html)。

### 创建库

不同类型的数据采集点往往具有不同的数据特征，包括数据采集频率的高低，数据保留时间的长短，副本的数目，数据块的大小，是否允许更新数据等等。为了在各种场景下 TDengine 都能以最大效率工作，TDengine  建议将不同数据特征的表创建在不同的库里，因为每个库可以配置不同的存储策略。创建一个库时，除 SQL  标准的选项外，还可以指定保留时长、副本数、缓存大小、时间精度、文件块里最大最小记录条数、是否压缩、一个数据文件覆盖的天数等多种参数。比如：

```sql
CREATE DATABASE power KEEP 365 DURATION 10 BUFFER 16 WAL_LEVEL 1;
```

上述语句将创建一个名为 power 的库，这个库的数据将保留 365 天（超过 365 天将被自动删除），每 10 天一个数据文件，每个 VNode 的写入内存池的大小为 16 MB，对该数据库入会写 WAL 但不执行 FSYNC。详细的语法及参数请见 [数据库管理](https://docs.taosdata.com/taos-sql/database/) 章节。

创建库之后，需要使用 SQL 命令 `USE` 将当前库切换过来，例如：

```sql
USE power;
```

将当前连接里操作的库换为 power，否则对具体表操作前，需要使用“库名.表名”来指定库的名字。

##### note

- 任何一张表或超级表必须属于某个库，在创建表之前，必须先创建库。
- 创建并插入记录、查询历史记录的时候，均需要指定**时间戳**。

### 创建超级表

一个物联网系统，往往存在多种类型的设备，比如对于电网，存在智能电表、变压器、母线、开关等等。为便于多表之间的聚合，使用 TDengine, 需要对每个类型的数据采集点创建一个超级表。以 [表 1](https://docs.taosdata.com/concept/) 中的智能电表为例，可以使用如下的 SQL 命令创建超级表： 

```sql
CREATE STABLE meters (ts timestamp, current float, voltage int, phase float) TAGS (location binary(64), groupId int);
```

与创建普通表一样，创建超级表时，需要提供表名（示例中为 meters），表结构 Schema，即数据列的定义。**第一列必须为时间戳**（示例中为 ts），其他列为采集的物理量（示例中为 current,  voltage, phase），数据类型可以为整型、浮点型、字符串等。除此之外，还需要提供标签的 Schema （示例中为 location,  groupId），标签的数据类型可以为整型、浮点型、字符串等。采集点的静态属性往往可以作为标签*（这个标签是针对于表的）*，比如采集点的地理位置、设备型号、设备组  ID、管理员 ID 等等。**标签的 Schema 可以事后增加、删除、修改**。具体定义以及细节请见 [TDengine SQL 的超级表管理](https://docs.taosdata.com/taos-sql/stable/) 章节。

**每一种类型的数据采集点需要建立一个超级表**，因此一个物联网系统，往往会有多个超级表。对于电网，我们就需要对智能电表、变压器、母线、开关等都建立一个超级表。在物联网中，一个设备就可能有多个数据采集点（比如一台风力发电的风机，有的采集点采集电流、电压等电参数，有的采集点采集温度、湿度、风向等环境参数），这个时候，对这一类型的设备，需要建立多张超级表。

一张超级表**最多容许 4096 列**，如果一个采集点采集的物理量个数超过 4096，需要建多张超级表来处理。*（这里对我们影响不大）*，一个系统可以有多个 Database，一个 Database 里可以有一到多个超级表。

### 创建表

TDengine 对每个数据采集点需要独立建表。与标准的关系型数据库一样，一张表有表名，Schema，但除此之外，还可以带有一到多个标签。创建时，需要使用超级表做模板，同时指定标签的具体值。以 [表 1](https://docs.taosdata.com/concept/) 中的智能电表为例，可以使用如下的 SQL 命令建表：

```sql
CREATE TABLE d1001 USING meters TAGS ("California.SanFrancisco", 2); #子表需要指定TAGS的值（这也是多个子表中的区分之一）
```

其中 d1001 是表名，meters 是超级表的表名，后面紧跟标签 Location 的具体标签值为  "California.SanFrancisco"，标签 groupId 的具体标签值为  2。虽然在创建表时，需要指定标签值，但可以事后修改。详细细则请见 [TDengine SQL 的表管理](https://docs.taosdata.com/taos-sql/table/) 章节。

TDengine 建议将**数据采集点的全局唯一 ID** 作为表名（比如设备序列号）。但对于有的场景，并没有唯一的 ID，可以将多个 ID 组合成一个唯一的 ID。**不建议将具有唯一性的 ID 作为标签值。**

#### 自动建表

在某些特殊场景中，用户在写数据时并不确定某个数据采集点的表是否存在，此时可在写入数据时使用自动建表语法来创建不存在的表，若该表已存在则不会建立新表且后面的 USING 语句被忽略。比如：

```sql
INSERT INTO d1001 USING meters TAGS ("California.SanFrancisco", 2) VALUES (NOW, 10.2, 219, 0.32);
```

上述 SQL 语句将记录`(NOW, 10.2, 219, 0.32)`插入表 d1001。如果表 d1001 还未创建，则使用超级表 meters 做模板自动创建，同时打上标签值 `"California.SanFrancisco", 2`。

关于自动建表的详细语法请参见 [插入记录时自动建表](https://docs.taosdata.com/taos-sql/insert/#插入记录时自动建表) 章节。

### 多列模型 vs 单列模型

TDengine  支持多列模型，只要物理量是一个数据采集点同时采集的（时间戳一致），这些量就可以作为不同列放在一张超级表里。但还有一种极限的设计，单列模型，每个采集的物理量都单独建表，因此每种类型的物理量都单独建立一超级表。比如电流、电压、相位，就建三张超级表。

TDengine 建议尽可能采用多列模型，因为插入效率以及存储效率更高。但对于有些场景，一个采集点的采集量的种类经常变化，这个时候，如果采用多列模型，就需要频繁修改超级表的结构定义，让应用变的复杂，这个时候，采用单列模型会显得更简单。



## SQL 写入

### SQL 写入简介

应用通过连接器执行 INSERT 语句来插入数据，用户还可以通过 TDengine CLI，手动输入 INSERT 语句插入数据。

#### 一次写入一条

下面这条 INSERT 就将一条记录写入到表 d1001 中：

```sql
INSERT INTO d1001 VALUES (ts1, 10.3, 219, 0.31);
```

这里的`ts1`为Unix时间戳(Unix timestamp)，允许插入的最老记录的时间戳，是相对于当前服务器时间，减去配置的 KEEP 值。时间戳详情规则参考 [TDengine SQL数据写入 关于时间戳一节](https://docs.taosdata.com/taos-sql/insert/)

### 一次写入多条

TDengine 支持一次写入多条记录，比如下面这条命令就将两条记录写入到表 d1001 中：（两条记录上不需要 “,” ）

```sql
INSERT INTO d1001 VALUES (ts1, 10.2, 220, 0.23) (ts2, 10.3, 218, 0.25); 
```

这里的`ts1`和`ts2`为Unix时间戳(Unix timestamp)，允许插入的最老记录的时间戳，是相对于当前服务器时间，减去配置的 KEEP 值。时间戳详情规则参考 [TDengine SQL数据写入 关于时间戳一节](https://docs.taosdata.com/taos-sql/insert/)

### 一次写入多表

TDengine 也支持一次向多个表写入数据，比如下面这条命令就向 d1001 写入两条记录，向 d1002 写入一条记录：

```sql
INSERT INTO d1001 VALUES (ts1, 10.3, 219, 0.31) (ts2, 12.6, 218, 0.33) d1002 VALUES (ts3, 12.3, 221, 0.31);
```

这里的`ts1`、`ts2`和`ts3`为Unix时间戳(Unix timestamp)，允许插入的最老记录的时间戳，是相对于当前服务器时间，减去配置的 KEEP 值。时间戳详情规则参考 [TDengine SQL数据写入 关于时间戳一节](https://docs.taosdata.com/taos-sql/insert/)

详细的 SQL INSERT 语法规则参考 [TDengine SQL 的数据写入](https://docs.taosdata.com/taos-sql/insert/)。

##### info

- 要提高写入效率，需要批量写入。一般来说一批写入的记录条数越多，插入效率就越高。但**一条记录不能超过 48KB**，一条 SQL 语句总长度不能超过 **1MB**。（大约20条）
- TDengine  支持多线程同时写入，要进一步提高写入速度，一个客户端需要打开多个同时写。但线程数达到一定数量后，无法再提高，甚至还会下降，因为线程频繁切换，会带来额外开销，合适的线程数量与服务端的处理能力，服务端的具体配置，数据库的参数，数据定义的 Schema，写入数据的 Batch Size  等很多因素相关。一般来说，服务端和客户端处理能力越强，所能支持的并发写入的线程可以越多；数据库配置时的 **vgroups**  参数值越多（但仍然要在服务端的处理能力以内）则所能支持的并发写入越多；数据定义的 Schema 越简单，所能支持的并发写入越多。

##### warning

- 对同一张表，如果**新插入记录的时间戳已经存在，则指定了新值的列会用新值覆盖旧值**，而没有指定新值的列则不受影响。
- 写入的数据的时间戳必须大于当前时间减去数据库配置参数 KEEP 的时间。如果 KEEP 配置为 3650 天，那么无法写入比 3650 天还早的数据。写入数据的时间戳也不能大于当前时间加配置参数  DURATION。如果 DURATION 为 2，那么**无法写入比当前时间还晚 2 天的数据**。

### 示例程序

#### 普通 SQL 写入

```c
// compile with
// gcc -o insert_example insert_example.c -ltaos
#include <stdio.h>
#include <stdlib.h>
#include "taos.h"


/**
 * @brief execute sql and print affected rows.
 * 
 * @param taos 
 * @param sql 
 */
void executeSQL(TAOS *taos, const char *sql) {
  TAOS_RES *res = taos_query(taos, sql);  //TAOS_RES是什么类型
  int       code = taos_errno(res);
  if (code != 0) {
    printf("Error code: %d; Message: %s\n", code, taos_errstr(res));
    taos_free_result(res);
    taos_close(taos);
    exit(EXIT_FAILURE);
  }
  int affectedRows = taos_affected_rows(res); //返回影响的行数
  printf("affected rows %d\n", affectedRows);
  taos_free_result(res);
}



int main() {
   TAOS *taos = taos_connect("localhost", "root", "taosdata", NULL, 6030);  //ip、账号、密码、数据库、端口号 返回为空表示失败
  if (taos == NULL) { 
    printf("failed to connect to server\n");
    exit(EXIT_FAILURE);
  }
  executeSQL(taos, "CREATE DATABASE power");
  executeSQL(taos, "USE power");
  executeSQL(taos, "CREATE STABLE meters (ts TIMESTAMP, current FLOAT, voltage INT, phase FLOAT) TAGS (location BINARY(64), groupId INT)");
  executeSQL(taos, "INSERT INTO d1001 USING meters TAGS('California.SanFrancisco', 2) VALUES ('2018-10-03 14:38:05.000', 10.30000, 219, 0.31000) ('2018-10-03 14:38:15.000', 12.60000, 218, 0.33000) ('2018-10-03 14:38:16.800', 12.30000, 221, 0.31000)"
                "d1002 USING meters TAGS('California.SanFrancisco', 3) VALUES ('2018-10-03 14:38:16.650', 10.30000, 218, 0.25000)"
                "d1003 USING meters TAGS('California.LosAngeles', 2) VALUES ('2018-10-03 14:38:05.500', 11.80000, 221, 0.28000) ('2018-10-03 14:38:16.600', 13.40000, 223, 0.29000)"
                "d1004 USING meters TAGS('California.LosAngeles', 3) VALUES ('2018-10-03 14:38:05.000', 10.80000, 223, 0.29000) ('2018-10-03 14:38:06.500', 11.50000, 221, 0.35000)"); //这里的语法怎么做到的？
  taos_close(taos);
  taos_cleanup(); //清理运行环境，应用退出前调用
}

// output:
// affected rows 0
// affected rows 0
// affected rows 0
// affected rows 8
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/c/insert_example.c)

##### note

1. 无论 RESTful 方式建立连接还是本地驱动方式建立连接，以上示例代码都能正常工作。
2. 唯一需要注意的是：由于 RESTful 接口无状态， 不能使用 `USE db;` 语句来切换数据库, 所以在上面示例中使用了`dbName.tbName`指定表名。

### 参数绑定写入

TDengine 也提供了支持参数绑定的 Prepare API，与 MySQL 类似，这些 API 目前也仅支持用问号 `?` 来代表待绑定的参数。在通过参数绑定接口写入数据时，就避免了 SQL 语法解析的资源消耗，从而在绝大多数情况下显著提升写入性能。

需要注意的是，只有使用原生连接的连接器，才能使用参数绑定功能。

一次绑定一行

```c
// compile with
// gcc -o stmt_example stmt_example.c -ltaos
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "taos.h"

/**
 * @brief execute sql only.
 * 
 * @param taos 
 * @param sql 
 */
void executeSQL(TAOS *taos, const char *sql) {
  TAOS_RES *res = taos_query(taos, sql);
  int       code = taos_errno(res);
  if (code != 0) {
    printf("%s\n", taos_errstr(res));
    taos_free_result(res);
    taos_close(taos);
    exit(EXIT_FAILURE);
  }
  taos_free_result(res);
}

/**
 * @brief check return status and exit program when error occur.
 * 
 * @param stmt 
 * @param code 
 * @param msg 
 */
void checkErrorCode(TAOS_STMT *stmt, int code, const char* msg) {
  if (code != 0) {
    printf("%s. error: %s\n", msg, taos_stmt_errstr(stmt)); // 用于在其他 STMT API 返回错误（返回错误码或空指针）时获取错误信息。
    taos_stmt_close(stmt); //释放所有资源
    exit(EXIT_FAILURE);
  }
}

typedef struct {
  int64_t ts;
  float current;
  int voltage;
  float phase;
} Row;

/**
 * @brief insert data using stmt API
 * 
 * @param taos 
 */
void insertData(TAOS *taos) {
  // init
  TAOS_STMT *stmt = taos_stmt_init(taos); //创建参数绑定对象
  // prepare
  const char *sql = "INSERT INTO ? USING meters TAGS(?, ?) VALUES(?, ?, ?, ?)";
  int code = taos_stmt_prepare(stmt, sql, 0); //解析insert语句
  checkErrorCode(stmt, code, "failed to execute taos_stmt_prepare");
  // bind table name and tags
  TAOS_BIND tags[2];
  /**
  typedef struct TAOS_BIND {
  	int            buffer_type;
  	void *         buffer;
  	uintptr_t      buffer_length;  // not in use
  	uintptr_t *    length;
  	int *          is_null;
  	int            is_unsigned;    // not in use
  	int *          error;          // not in use
	} TAOS_BIND;
  */
  char* location = "California.SanFrancisco";
  int groupId = 2;
  tags[0].buffer_type = TSDB_DATA_TYPE_BINARY;
  tags[0].buffer_length = strlen(location);
  tags[0].length = &tags[0].buffer_length;
  tags[0].buffer = location;
  tags[0].is_null = NULL;
  
  tags[1].buffer_type = TSDB_DATA_TYPE_INT;
  tags[1].buffer_length = sizeof(int);
  tags[1].length = &tags[1].buffer_length;
  tags[1].buffer = &groupId;
  tags[1].is_null = NULL;
//"INSERT INTO ? USING meters TAGS(?, ?) VALUES(?, ?, ?, ?)"
  code = taos_stmt_set_tbname_tags(stmt, "d1001", tags); //设置表名和tags
  checkErrorCode(stmt, code, "failed to execute taos_stmt_set_tbname_tags");

  // insert two rows
  Row rows[2] = {
    {1648432611249, 10.3, 219, 0.31},
    {1648432611749, 12.6, 218, 0.33},
  };

  TAOS_BIND values[4];
  values[0].buffer_type = TSDB_DATA_TYPE_TIMESTAMP;
  values[0].buffer_length = sizeof(int64_t);
  values[0].length = &values[0].buffer_length;
  values[0].is_null = NULL;

  values[1].buffer_type = TSDB_DATA_TYPE_FLOAT;
  values[1].buffer_length = sizeof(float);
  values[1].length = &values[1].buffer_length;
  values[1].is_null = NULL;

  values[2].buffer_type = TSDB_DATA_TYPE_INT;
  values[2].buffer_length = sizeof(int);
  values[2].length = &values[2].buffer_length;
  values[2].is_null = NULL;

  values[3].buffer_type = TSDB_DATA_TYPE_FLOAT;
  values[3].buffer_length = sizeof(float);
  values[3].length = &values[3].buffer_length;
  values[3].is_null = NULL;

  for (int i = 0; i < 2; ++i) {
    values[0].buffer = &rows[i].ts;
    values[1].buffer = &rows[i].current;
    values[2].buffer = &rows[i].voltage;
    values[3].buffer = &rows[i].phase;
    code = taos_stmt_bind_param(stmt, values); // 绑定参数 （这种方式的好处能够单独处理表名和TAGS，避免重复操作）
      // taos_stmt_bind_param_batch() 也可以直接以多行的方式设置VALUES值，并直接加入batch
    checkErrorCode(stmt, code, "failed to execute taos_stmt_bind_param");
    code = taos_stmt_add_batch(stmt); // 将当前绑定的参数加入批处理，多加入一些数据，能够提高效率
    checkErrorCode(stmt, code, "failed to execute taos_stmt_add_batch");
  }
  // execute
  code = taos_stmt_execute(stmt);
  checkErrorCode(stmt, code, "failed to execute taos_stmt_execute");
  int affectedRows = taos_stmt_affected_rows(stmt);
  printf("successfully inserted %d rows\n", affectedRows);
  // close
  taos_stmt_close(stmt);
}

int main() {
  TAOS *taos = taos_connect("localhost", "root", "taosdata", NULL, 6030);
  if (taos == NULL) {
    printf("failed to connect to server\n");
    exit(EXIT_FAILURE);
  }
  executeSQL(taos, "CREATE DATABASE power");
  executeSQL(taos, "USE power");
  executeSQL(taos, "CREATE STABLE meters (ts TIMESTAMP, current FLOAT, voltage INT, phase FLOAT) TAGS (location BINARY(64), groupId INT)");
  insertData(taos);
  taos_close(taos);
  taos_cleanup();
}


// output:
// successfully inserted 2 rows
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/c/stmt_example.c)

一次绑定多行

```c
// compile with
// gcc -o multi_bind_example multi_bind_example.c -ltaos
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "taos.h"

/**
 * @brief execute sql only and ignore result set
 *
 * @param taos
 * @param sql
 */
void executeSQL(TAOS *taos, const char *sql) {
  TAOS_RES *res = taos_query(taos, sql);
  int       code = taos_errno(res);
  if (code != 0) {
    printf("%s\n", taos_errstr(res));
    taos_free_result(res);
    taos_close(taos);
    exit(EXIT_FAILURE);
  }
  taos_free_result(res);
}

/**
 * @brief exit program when error occur.
 *
 * @param stmt
 * @param code
 * @param msg
 */
void checkErrorCode(TAOS_STMT *stmt, int code, const char *msg) {
  if (code != 0) {
    printf("%s. error: %s\n", msg, taos_stmt_errstr(stmt));
    taos_stmt_close(stmt);
    exit(EXIT_FAILURE);
  }
}

/**
 * @brief insert data using stmt API
 *
 * @param taos
 */
void insertData(TAOS *taos) {
  // init
  TAOS_STMT *stmt = taos_stmt_init(taos);
  // prepare
  const char *sql = "INSERT INTO ? USING meters TAGS(?, ?) values(?, ?, ?, ?)";
  int         code = taos_stmt_prepare(stmt, sql, 0);
  checkErrorCode(stmt, code, "failed to execute taos_stmt_prepare");
  // bind table name and tags
  TAOS_BIND tags[2];
  char     *location = "California.SanFrancisco";
  int       groupId = 2;
  tags[0].buffer_type = TSDB_DATA_TYPE_BINARY;
  tags[0].buffer_length = strlen(location);
  tags[0].length = &tags[0].buffer_length;
  tags[0].buffer = location;
  tags[0].is_null = NULL;

  tags[1].buffer_type = TSDB_DATA_TYPE_INT;
  tags[1].buffer_length = sizeof(int);
  tags[1].length = &tags[1].buffer_length;
  tags[1].buffer = &groupId;
  tags[1].is_null = NULL;

  code = taos_stmt_set_tbname_tags(stmt, "d1001", tags);
  checkErrorCode(stmt, code, "failed to execute taos_stmt_set_tbname_tags");

  // insert two rows with multi binds
  TAOS_MULTI_BIND params[4];
  // values to bind
  int64_t ts[] = {1648432611249, 1648432611749};
  float   current[] = {10.3, 12.6};
  int     voltage[] = {219, 218};
  float   phase[] = {0.31, 0.33};
  // is_null array
  char is_null[2] = {0};
  // length array
  int32_t int64Len[2] = {sizeof(int64_t)};
  int32_t floatLen[2] = {sizeof(float)};
  int32_t intLen[2] = {sizeof(int)};

  params[0].buffer_type = TSDB_DATA_TYPE_TIMESTAMP;
  params[0].buffer_length = sizeof(int64_t);
  params[0].buffer = ts;
  params[0].length = int64Len;
  params[0].is_null = is_null;
  params[0].num = 2;

  params[1].buffer_type = TSDB_DATA_TYPE_FLOAT;
  params[1].buffer_length = sizeof(float);
  params[1].buffer = current;
  params[1].length = floatLen;
  params[1].is_null = is_null;
  params[1].num = 2;

  params[2].buffer_type = TSDB_DATA_TYPE_INT;
  params[2].buffer_length = sizeof(int);
  params[2].buffer = voltage;
  params[2].length = intLen;
  params[2].is_null = is_null;
  params[2].num = 2;

  params[3].buffer_type = TSDB_DATA_TYPE_FLOAT;
  params[3].buffer_length = sizeof(float);
  params[3].buffer = phase;
  params[3].length = floatLen;
  params[3].is_null = is_null;
  params[3].num = 2;

  code = taos_stmt_bind_param_batch(stmt, params); // bind batch
  checkErrorCode(stmt, code, "failed to execute taos_stmt_bind_param_batch");
  code = taos_stmt_add_batch(stmt);  // add batch
  checkErrorCode(stmt, code, "failed to execute taos_stmt_add_batch");
  // execute
  code = taos_stmt_execute(stmt);
  checkErrorCode(stmt, code, "failed to execute taos_stmt_execute");
  int affectedRows = taos_stmt_affected_rows(stmt);
  printf("successfully inserted %d rows\n", affectedRows);
  // close
  taos_stmt_close(stmt);
}

int main() {
  TAOS *taos = taos_connect("localhost", "root", "taosdata", NULL, 6030);
  if (taos == NULL) {
    printf("failed to connect to server\n");
    exit(EXIT_FAILURE);
  }
  executeSQL(taos, "DROP DATABASE IF EXISTS power");
  executeSQL(taos, "CREATE DATABASE power");
  executeSQL(taos, "USE power");
  executeSQL(taos,
             "CREATE STABLE meters (ts TIMESTAMP, current FLOAT, voltage INT, phase FLOAT) TAGS (location BINARY(64), "
             "groupId INT)");
  insertData(taos);
  taos_close(taos);
  taos_cleanup();
}

// output:
// successfully inserted 2 rows
```



## 高效写入

本节介绍如何高效地向 TDengine 写入数据。

### 高效写入原理

#### 客户端程序的角度

从客户端程序的角度来说，高效写入数据要考虑以下几个因素：

1. **单次写入的数据量**。一般来讲，每批次写入的数据量越大越高效（但超过一定阈值其优势会消失）。使用 SQL 写入 TDengine 时，尽量在一条 SQL 中拼接更多数据。目前，TDengine 支持的一条 SQL 的最大长度为  **1,048,576（1MB）**个字符
2. **并发连接数**。一般来讲，同时写入数据的并发连接数越多写入越高效（但超过一定阈值反而会下降，取决于服务端处理能力）
3. 数据在不同表（或子表）之间的分布，即要**写入数据的相邻性**。一般来说，每批次只向同一张表（或子表）写入数据比向多张表（或子表）写入数据要更高效
4. 写入方式。一般来讲：
   - **参数绑定写入比 SQL 写入更高效**。因参数绑定方式**避免了 SQL 解析**。（但增加了 C 接口的调用次数，对于连接器也有性能损耗）
   - SQL 写入不自动建表比自动建表更高效。因自动建表要频繁检查表是否存在
   - SQL 写入比无模式写入更高效。因无模式写入会自动建表且支持动态更改表结构

客户端程序要充分且恰当地利用以上几个因素。在单次写入中尽量只向同一张表（或子表）写入数据，每批次写入的数据量经过测试和调优设定为一个最适合当前系统处理能力的数值，并发写入的连接数同样经过测试和调优后设定为一个最适合当前系统处理能力的数值，以实现在当前系统中的最佳写入速度。

#### 数据源的角度

**客户端程序通常需要从数据源读数据再写入 TDengine。从数据源角度来说，以下几种情况需要在读线程和写线程之间增加队列：**

1. **有多个数据源，单个数据源生成数据的速度远小于单线程写入的速度，但数据量整体比较大。此时队列的作用是把多个数据源的数据汇聚到一起，增加单次写入的数据量。**
2. **单个数据源生成数据的速度远大于单线程写入的速度。此时队列的作用是增加写入的并发度。**
3. **单张表的数据分散在多个数据源。此时队列的作用是将同一张表的数据提前汇聚到一起，提高写入时数据的相邻性。**

可能后期优化的方面在这里

如果写应用的数据源是 Kafka, 写应用本身即 Kafka 的消费者，则可利用 Kafka 的特性实现高效写入。比如：

1. 将同一张表的数据写到同一个 Topic 的同一个 Partition，增加数据的相邻性
2. 通过订阅多个 Topic 实现数据汇聚
3. 通过增加 Consumer 线程数增加写入的并发度
4. 通过增加每次 Fetch 的最大数据量来增加单次写入的最大数据量

#### 服务器配置的角度

从服务端配置的角度，要根据系统中磁盘的数量，磁盘的 I/O 能力，以及处理器能力在创建数据库时设置适当的 vgroups 数量以充分发挥系统性能。如果 vgroups  过少，则系统性能无法发挥；如果 vgroups 过多，会造成无谓的资源竞争。常规推荐 **vgroups 数量为 CPU 核数的 2  倍**，但仍然要结合具体的系统资源配置进行调优。

更多调优参数，请参考 [数据库管理](https://docs.taosdata.com/taos-sql/database/) 和 [服务端配置](https://docs.taosdata.com/reference/config/)。

### 高效写入示例

#### 场景设计

下面的示例程序展示了如何高效写入数据，场景设计如下：

- TDengine 客户端程序从其它数据源不断读入数据，在示例程序中采用生成模拟数据的方式来模拟读取数据源
- 单个连接向 TDengine 写入的速度无法与读数据的速度相匹配，因此客户端程序启动多个线程，每个线程都建立了与 TDengine 的连接，每个线程都有一个独占的固定大小的消息队列
- 客户端程序将接收到的数据根据所属的**表名（或子表名）HASH 到不同的线程**，即写入该线程所对应的消息队列，以此**确保属于某个表（或子表）的数据一定会被一个固定的线程处理**（这样可能效率高一些？）
- 各个子线程在将所关联的消息队列中的数据读空后或者读取数据量达到一个预定的阈值后将该批数据写入 TDengine，并继续处理后面接收到的数据

![TDengine 高效写入示例场景的线程模型](data:image/webp;base64,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)

#### 示例代码

这一部分是针对以上场景的示例代码。对于其它场景高效写入原理相同，不过代码需要适当修改。

本示例代码假设源数据属于同一张超级表（meters）的不同子表。程序在开始写入数据之前已经在 test 库创建了这个超级表。对于子表，将根据收到的数据，由应用程序自动创建。如果实际场景是多个超级表，只需修改写任务自动建表的代码。

| 类名             | 功能说明                                                     |
| ---------------- | ------------------------------------------------------------ |
| FastWriteExample | 主程序                                                       |
| ReadTask         | 从模拟源中读取数据，将表名经过 Hash 后得到 Queue 的 Index，写入对应的 Queue |
| WriteTask        | 从 Queue 中获取数据，组成一个 **Batch**，写入 TDengine       |
| MockDataSource   | 模拟生成一定数量 meters 子表的数据                           |
| SQLWriter        | WriteTask 依赖这个类完成 SQL 拼接、自动建表、 SQL 写入、SQL 长度检查 |
| StmtWriter       | 实现参数绑定方式批量写入（暂未完成）                         |
| DataBaseMonitor  | 统计写入速度，并每隔 10 秒把当前写入速度打印到控制台         |

#### FastWriteExample

主程序负责：

1.  创建消息队列
2.  启动写线程
3.  启动读线程
4.  每隔 10 秒统计一次写入速度

主程序默认暴露了 4 个参数，每次启动程序都可调节，用于测试和调优：

1.  读线程个数。默认为 1。
2.  写线程个数。默认为 3。
3.  模拟生成的总表数。默认为 1,000。将会平分给各个读线程。如果总表数较大，建表需要花费较长，开始统计的写入速度可能较慢。
4.  每批最多写入记录数量。默认为 3,000。

队列容量（taskQueueCapacity）也是与性能有关的参数，可通过修改程序调节。一般来讲，队列容量越大，入队被阻塞的概率越小，队列的吞吐量越大，但是内存占用也会越大。示例程序默认值已经设置地足够大。

```java
package com.taos.example.highvolume;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;


public class FastWriteExample {
    final static Logger logger = LoggerFactory.getLogger(FastWriteExample.class);

    final static int taskQueueCapacity = 1000000; //任务队列容量
    final static List<BlockingQueue<String>> taskQueues = new ArrayList<>();
    final static List<ReadTask> readTasks = new ArrayList<>();
    final static List<WriteTask> writeTasks = new ArrayList<>();
    final static DataBaseMonitor databaseMonitor = new DataBaseMonitor();

    public static void stopAll() {
        logger.info("shutting down");
        readTasks.forEach(task -> task.stop());
        writeTasks.forEach(task -> task.stop());
        databaseMonitor.close();
    }

    public static void main(String[] args) throws InterruptedException, SQLException {
        int readTaskCount = args.length > 0 ? Integer.parseInt(args[0]) : 1; //读线程个数
        int writeTaskCount = args.length > 1 ? Integer.parseInt(args[1]) : 3; //写线程个数
        int tableCount = args.length > 2 ? Integer.parseInt(args[2]) : 1000; //模拟生成的总表数
        int maxBatchSize = args.length > 3 ? Integer.parseInt(args[3]) : 3000; //每批最多写入记录数量

        logger.info("readTaskCount={}, writeTaskCount={} tableCount={} maxBatchSize={}",
                readTaskCount, writeTaskCount, tableCount, maxBatchSize);

        databaseMonitor.init().prepareDatabase();

        // Create task queues, whiting tasks and start writing threads.
        for (int i = 0; i < writeTaskCount; ++i) {
            BlockingQueue<String> queue = new ArrayBlockingQueue<>(taskQueueCapacity); //基于数组的阻塞队列
            taskQueues.add(queue);
            WriteTask task = new WriteTask(queue, maxBatchSize);
            Thread t = new Thread(task); //继承了Runnable
            t.setName("WriteThread-" + i);  
            t.start();
        } // 跑起来 writeTaskCount 给写线程

        // create reading tasks and start reading threads
        int tableCountPerTask = tableCount / readTaskCount; 
        for (int i = 0; i < readTaskCount; ++i) {
            ReadTask task = new ReadTask(i, taskQueues, tableCountPerTask);
            Thread t = new Thread(task);
            t.setName("ReadThread-" + i);
            t.start();
        } // 跑起来 ReadTaskCount 给写线程

        Runtime.getRuntime().addShutdownHook(new Thread(FastWriteExample::stopAll));

        long lastCount = 0;
        while (true) {
            Thread.sleep(10000);
            long numberOfTable = databaseMonitor.getTableCount();
            long count = databaseMonitor.count();
            logger.info("numberOfTable={} count={} speed={}", numberOfTable, count, (count - lastCount) / 10);
            lastCount = count;
        }
    }
}
```

####  ReadTask

读任务负责从数据源读数据。每个读任务都关联了一个模拟数据源。每个模拟数据源可生成一点数量表的数据。不同的模拟数据源生成不同表的数据。

读任务采用阻塞的方式写消息队列。也就是说，一旦队列满了，写操作就会阻塞。

```java
package com.taos.example.highvolume;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.Iterator;
import java.util.List;
import java.util.concurrent.BlockingQueue;

class ReadTask implements Runnable {
    private final static Logger logger = LoggerFactory.getLogger(ReadTask.class);
    private final int taskId;
    private final List<BlockingQueue<String>> taskQueues;
    private final int queueCount;
    private final int tableCount;
    private boolean active = true;

    public ReadTask(int readTaskId, List<BlockingQueue<String>> queues, int tableCount) {
        this.taskId = readTaskId;
        this.taskQueues = queues;
        this.queueCount = queues.size();
        this.tableCount = tableCount;
    }

    /**
     * Assign data received to different queues.
     * Here we use the suffix number in table name.
     * You are expected to define your own rule in practice.
     *
     * @param line record received
     * @return which queue to use
     */
    public int getQueueId(String line) {
        String tbName = line.substring(0, line.indexOf(',')); // For example: tb1_101
        String suffixNumber = tbName.split("_")[1];
        return Integer.parseInt(suffixNumber) % this.queueCount;
    }

    @Override
    public void run() {
        logger.info("started");
        Iterator<String> it = new MockDataSource("tb" + this.taskId, tableCount);
        try {
            while (it.hasNext() && active) {
                String line = it.next();
                int queueId = getQueueId(line);
                taskQueues.get(queueId).put(line);
            }
        } catch (Exception e) {
            logger.error("Read Task Error", e);
        }
    }

    public void stop() {
        logger.info("stop");
        this.active = false;
    }
}
```

####  WriteTask

```java
package com.taos.example.highvolume;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.concurrent.BlockingQueue;

class WriteTask implements Runnable {
    private final static Logger logger = LoggerFactory.getLogger(WriteTask.class);
    private final int maxBatchSize;

    // the queue from which this writing task get raw data.
    private final BlockingQueue<String> queue;

    // A flag indicate whether to continue.
    private boolean active = true;

    public WriteTask(BlockingQueue<String> taskQueue, int maxBatchSize) {
        this.queue = taskQueue;
        this.maxBatchSize = maxBatchSize;
    }

    @Override
    public void run() {
        logger.info("started");
        String line = null; // data getting from the queue just now.
        SQLWriter writer = new SQLWriter(maxBatchSize);
        try {
            writer.init();
            while (active) {
                line = queue.poll();
                if (line != null) {
                    // parse raw data and buffer the data.
                    writer.processLine(line);
                } else if (writer.hasBufferedValues()) {
                    // write data immediately if no more data in the queue
                    writer.flush();
                } else {
                    // sleep a while to avoid high CPU usage if no more data in the queue and no buffered records, .
                    Thread.sleep(100);
                }
            }
            if (writer.hasBufferedValues()) {
                writer.flush();
            }
        } catch (Exception e) {
            String msg = String.format("line=%s, bufferedCount=%s", line, writer.getBufferedCount());
            logger.error(msg, e);
        } finally {
            writer.close();
        }
    }

    public void stop() {
        logger.info("stop");
        this.active = false;
    }
}
```

## 查询数据

### 主要查询功能

TDengine 采用 SQL 作为查询语言。应用程序可以通过 REST API 或连接器发送 SQL 语句，用户还可以通过 TDengine 命令行工具  taos 手动执行 SQL 即席查询（Ad-Hoc Query）。TDengine 支持如下查询功能：

- 单列、多列数据查询
- 标签和数值的多种过滤条件：>, <, =, <>, like 等
- 聚合结果的分组（Group by）、排序（Order by）、约束输出（Limit/Offset）
- 时间窗口（Interval）、会话窗口（Session）和状态窗口（State_window）等窗口切分聚合查询
- 数值列及聚合结果的四则运算
- 时间戳对齐的连接查询（Join Query: 隐式连接）操作
- 多种聚合/计算函数: count, max, min, avg, sum, twa, stddev, leastsquares, top, bottom,  first, last, percentile, apercentile, last_row, spread, diff 等

例如：在命令行工具 taos 中，从表 d1001 中查询出 voltage > 215 的记录，按时间降序排列，仅仅输出 2 条。

```sql
taos> select * from d1001 where voltage > 215 order by ts desc limit 2;
           ts            |       current        |   voltage   |        phase         |
======================================================================================
 2018-10-03 14:38:16.800 |             12.30000 |         221 |              0.31000 |
 2018-10-03 14:38:15.000 |             12.60000 |         218 |              0.33000 |
Query OK, 2 row(s) in set (0.001100s)
```

为满足物联网场景的需求，TDengine 支持几个特殊的函数，比如 twa(时间加权平均)，spread (最大值与最小值的差)，last_row(最后一条记录)等，更多与物联网场景相关的函数将添加进来。

具体的查询语法请看 [TDengine SQL 的数据查询](https://docs.taosdata.com/taos-sql/select/) 章节。

### 多表聚合查询

物联网场景中，往往同一个类型的数据采集点有多个。TDengine 采用超级表(STable)的概念来描述某一个类型的数据采集点，一张普通的表来描述一个具体的数据采集点。同时 TDengine  使用标签来描述数据采集点的静态属性，一个具体的数据采集点有具体的标签值。通过指定标签的过滤条件，TDengine  提供了一高效的方法将超级表(某一类型的数据采集点)所属的子表进行聚合查询。对普通表的聚合函数以及绝大部分操作都适用于超级表，语法完全一样。

#### 示例一

在 TDengine CLI，查找加利福尼亚州所有智能电表采集的电压平均值，并按照 location 分组。

```text
taos> SELECT AVG(voltage), location FROM meters GROUP BY location;
       avg(voltage)        |                             location                             |
===============================================================================================
             219.200000000 | California.SanFrancisco                                          |
             221.666666667 | California.LosAngeles                                            |
Query OK, 2 rows in database (0.005995s)
```

#### 示例二

在 TDengine CLI, 查找 groupId 为 2 的所有智能电表的记录条数，电流的最大值。

```text
taos> SELECT count(*), max(current) FROM meters where groupId = 2;
     cunt(*)  |    max(current)  |
==================================
            5 |             13.4 |
Query OK, 1 row(s) in set (0.002136s)
```

在 [TDengine SQL 的数据查询](https://docs.taosdata.com/taos-sql/select/) 一章，查询类操作都会注明是否支持超级表。

### 降采样查询、插值

物联网场景里，经常需要通过降采样（down sampling）将采集的数据按时间段进行聚合。TDengine 提供了一个简便的关键词 interval 让按照时间窗口的查询操作变得极为简单。比如，将智能电表 d1001 采集的电流值每 10 秒钟求和

```text
taos> SELECT _wstart, sum(current) FROM d1001 INTERVAL(10s);
         _wstart         |       sum(current)        |
======================================================
 2018-10-03 14:38:00.000 |              10.300000191 |
 2018-10-03 14:38:10.000 |              24.900000572 |
Query OK, 2 rows in database (0.003139s)
```

降采样操作也适用于超级表，比如：将加利福尼亚州所有智能电表采集的电流值每秒钟求和

```text
taos> SELECT _wstart, SUM(current) FROM meters where location like "California%" INTERVAL(1s);
         _wstart         |       sum(current)        |
======================================================
 2018-10-03 14:38:04.000 |              10.199999809 |
 2018-10-03 14:38:05.000 |              23.699999809 |
 2018-10-03 14:38:06.000 |              11.500000000 |
 2018-10-03 14:38:15.000 |              12.600000381 |
 2018-10-03 14:38:16.000 |              34.400000572 |
Query OK, 5 rows in database (0.007413s)
```

降采样操作也支持时间偏移，比如：将所有智能电表采集的电流值每秒钟求和，但要求每个时间窗口从 500 毫秒开始

```text
taos> SELECT _wstart, SUM(current) FROM meters INTERVAL(1s, 500a);
         _wstart         |       sum(current)        |
======================================================
 2018-10-03 14:38:03.500 |              10.199999809 |
 2018-10-03 14:38:04.500 |              10.300000191 |
 2018-10-03 14:38:05.500 |              13.399999619 |
 2018-10-03 14:38:06.500 |              11.500000000 |
 2018-10-03 14:38:14.500 |              12.600000381 |
 2018-10-03 14:38:16.500 |              34.400000572 |
Query OK, 6 rows in database (0.005515s)
```

物联网场景里，每个数据采集点采集数据的时间是难同步的，但很多分析算法(比如 FFT)需要把采集的数据严格按照时间等间隔的对齐，在很多系统里，需要应用自己写程序来处理，但使用 TDengine 的降采样操作就轻松解决。

如果一个时间间隔里，没有采集的数据，TDengine 还提供插值计算的功能。

语法规则细节请见 [TDengine SQL 的按时间窗口切分聚合](https://docs.taosdata.com/taos-sql/distinguished/) 章节。

### 示例代码

#### 查询数据

在 [SQL 写入](https://docs.taosdata.com/develop/insert-data/sql-writing/) 一章，我们创建了 power 数据库，并向 meters 表写入了一些数据，以下示例代码展示如何查询这个表的数据。

```c
// compile with:
// gcc -o query_example query_example.c -ltaos
#include <inttypes.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <taos.h>

typedef uint16_t VarDataLenT;

#define TSDB_NCHAR_SIZE sizeof(int32_t)
#define VARSTR_HEADER_SIZE sizeof(VarDataLenT)

#define GET_FLOAT_VAL(x) (*(float *)(x))
#define GET_DOUBLE_VAL(x) (*(double *)(x))

#define varDataLen(v) ((VarDataLenT *)(v))[0]

int printRow(char *str, TAOS_ROW row, TAOS_FIELD *fields, int numFields) {
  int  len = 0;
  char split = ' ';

  for (int i = 0; i < numFields; ++i) { //对每列属性
    if (i > 0) {
      str[len++] = split; //属性之间加入空格
    }
    //sprintf的作用是将后面的格式化串加入到str中

    if (row[i] == NULL) {
      len += sprintf(str + len, "%s", "NULL");
      continue;
    }

    switch (fields[i].type) {
      case TSDB_DATA_TYPE_TINYINT:
        len += sprintf(str + len, "%d", *((int8_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_UTINYINT:
        len += sprintf(str + len, "%u", *((uint8_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_SMALLINT:
        len += sprintf(str + len, "%d", *((int16_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_USMALLINT:
        len += sprintf(str + len, "%u", *((uint16_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_INT:
        len += sprintf(str + len, "%d", *((int32_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_UINT:
        len += sprintf(str + len, "%u", *((uint32_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_BIGINT:
        len += sprintf(str + len, "%" PRId64, *((int64_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_UBIGINT:
        len += sprintf(str + len, "%" PRIu64, *((uint64_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_FLOAT: {
        float fv = 0;
        fv = GET_FLOAT_VAL(row[i]);
        len += sprintf(str + len, "%f", fv);
      } break;

      case TSDB_DATA_TYPE_DOUBLE: {
        double dv = 0;
        dv = GET_DOUBLE_VAL(row[i]);
        len += sprintf(str + len, "%lf", dv);
      } break;

      case TSDB_DATA_TYPE_BINARY:
      case TSDB_DATA_TYPE_NCHAR: {
        int32_t charLen = varDataLen((char *)row[i] - VARSTR_HEADER_SIZE);
        memcpy(str + len, row[i], charLen);
        len += charLen;
      } break;

      case TSDB_DATA_TYPE_TIMESTAMP:
        len += sprintf(str + len, "%" PRId64, *((int64_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_BOOL:
        len += sprintf(str + len, "%d", *((int8_t *)row[i]));
      default:
        break;
    }
  }

  return len;
}

/**
 * @brief print column name and values of each row
 *
 * @param res
 * @return int
 */
static int printResult(TAOS_RES *res) {
  int         numFields = taos_num_fields(res); //获取查询结果中的列数 taos_field_count(TAOS_RES*) 具有同样的功能	
  TAOS_FIELD *fields = taos_fetch_fields(res); //获取查询结果集每列数据的属性（列的名称、列的数据类型、列的长度），与 taos_num_fields() 配合使用，可用来解析 taos_fetch_row() 返回的一个元组(一行)的数据。 TAOS_FIELD 的结构如下：
    /*
    typedef struct taosField {
 		 char     name[65];  // column name
  		 uint8_t  type;      // data type
  		 int16_t  bytes;     // length, in bytes
	} TAOS_FIELD;
    
    */
  char        header[256] = {0}; 
  int len = 0;
  for (int i = 0; i < numFields; ++i) {
    len += sprintf(header + len, "%s ", fields[i].name);  //将列名放入到header中
  }
  puts(header); //输出一个字符串并换行

  TAOS_ROW row = NULL;
  while ((row = taos_fetch_row(res))) { //taos_fetch_row 按行获取查询结果中的数据
    char temp[256] = {0};
    printRow(temp, row, fields, numFields);
    puts(temp);
  }
}

int main() {
  TAOS *taos = taos_connect("localhost", "root", "taosdata", "power", 6030);
  if (taos == NULL) {
    puts("failed to connect to server");
    exit(EXIT_FAILURE);
  }
  TAOS_RES *res = taos_query(taos, "SELECT * FROM meters LIMIT 2");
  if (taos_errno(res) != 0) {
    printf("failed to execute taos_query. error: %s\n", taos_errstr(res));
    exit(EXIT_FAILURE);
  }
  printResult(res);
  taos_free_result(res);
  taos_close(taos);
  taos_cleanup();
}

// output:
// ts current voltage phase location groupid 
// 1648432611249 10.300000 219 0.310000 California.SanFrancisco 2
// 1648432611749 12.600000 218 0.330000 California.SanFrancisco 2
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/c/query_example.c)

##### note

1. 无论是使用 REST 连接还是原生连接的连接器，以上示例代码都能正常工作。
2. 唯一需要注意的是：由于 REST 接口无状态， 不能使用 `use db` 语句来切换数据库。

#### 异步查询

除同步查询 API 之外，TDengine 还提供性能更高的异步调用 API 处理数据插入、查询操作。在软硬件环境相同的情况下，异步 API  处理数据插入的速度比同步 API 快 2-4 倍。异步 API  采用非阻塞式的调用方式，在系统真正完成某个具体数据库操作前，立即返回。调用的线程可以去处理其他工作，从而可以提升整个应用的性能。异步 API  在网络延迟严重的情况下，优点尤为突出。

需要注意的是，只有使用原生连接的连接器，才能使用异步查询功能。

```c
/**
 * @brief call back function of taos_fetch_row_a
 *
 * @param param : the third parameter you passed to taos_fetch_row_a
 * @param res : pointer of TAOS_RES
 * @param numOfRow : number of rows fetched in this batch. will be 0 if there is no more data.
 * @return void*
 */
void *fetch_row_callback(void *param, TAOS_RES *res, int numOfRow) {
  printf("numOfRow = %d \n", numOfRow);
  int         numFields = taos_num_fields(res);
  TAOS_FIELD *fields = taos_fetch_fields(res);
  TAOS       *_taos = (TAOS *)param;
  if (numOfRow > 0) {
    for (int i = 0; i < numOfRow; ++i) {
      TAOS_ROW row = taos_fetch_row(res);
      char     temp[256] = {0};
      printRow(temp, row, fields, numFields);
      puts(temp);
    }
    taos_fetch_rows_a(res, fetch_row_callback, _taos);
  } else {
    printf("no more data, close the connection.\n");
    taos_free_result(res);
    taos_close(_taos);
    taos_cleanup();
  }
}

/**
 * @brief callback function of taos_query_a
 *
 * @param param: the fourth parameter you passed to taos_query_a 传递给taos_query_a的第四个参数
 * @param res : the result set
 * @param code : status code
 * @return void*
 */
void *select_callback(void *param, TAOS_RES *res, int code) {
  printf("query callback ...\n");
  TAOS *_taos = (TAOS *)param;
  if (code == 0 && res) {
    printHeader(res);
    taos_fetch_rows_a(res, fetch_row_callback, _taos);
  } else {
    printf("failed to execute taos_query. error: %s\n", taos_errstr(res));
    taos_free_result(res);
    taos_close(_taos);
    taos_cleanup();
    exit(EXIT_FAILURE);
  }
}

int main() {
  TAOS *taos = taos_connect("localhost", "root", "taosdata", "power", 6030);
  if (taos == NULL) {
    puts("failed to connect to server");
    exit(EXIT_FAILURE);
  }
  // param one is the connection returned by taos_connect.
  // param two is the SQL to execute.
  // param three is the callback function.
  // param four can be any pointer. It will be passed to your callback function as the first parameter. we use taos
  // here, because we want to close it after getting data.
  taos_query_a(taos, "SELECT * FROM meters", select_callback, taos); //异步执行sql语句，select_callback用于指定回调函数，第二个参数是查询返回的结果集
  sleep(1);
}

// output:
// query callback ...
// ts current voltage phase location groupid
// numOfRow = 8
// 1538548685500 11.800000 221 0.280000 california.losangeles 2
// 1538548696600 13.400000 223 0.290000 california.losangeles 2
// 1538548685000 10.800000 223 0.290000 california.losangeles 3
// 1538548686500 11.500000 221 0.350000 california.losangeles 3
// 1538548685000 10.300000 219 0.310000 california.sanfrancisco 2
// 1538548695000 12.600000 218 0.330000 california.sanfrancisco 2
// 1538548696800 12.300000 221 0.310000 california.sanfrancisco 2
// 1538548696650 10.300000 218 0.250000 california.sanfrancisco 3
// numOfRow = 0
// no more data, close the connection.
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/c/async_query_example.c)

## 流式计算

(在数据插入过程中，进行相应的计算并存储结果)

在时序数据的处理中，经常要对原始数据进行清洗、预处理，再使用时序数据库进行长久的储存。在传统的时序数据解决方案中，常常需要部署 Kafka、Flink 等流处理系统。而流处理系统的复杂性，带来了高昂的开发与运维成本。

TDengine 3.0 的流式计算引擎提供了实时处理写入的数据流的能力，使用 SQL  定义实时流变换，当数据被写入流的源表后，数据会被以定义的方式自动处理，并根据定义的触发模式向目的表推送结果。它提供了替代复杂流处理系统的轻量级解决方案，并能够在高吞吐的数据写入的情况下，提供毫秒级的计算结果延迟。

流式计算可以包含数据过滤，标量函数计算（含UDF），以及窗口聚合（支持滑动窗口、会话窗口与状态窗口），可以以超级表、子表、普通表为源表，写入到目的超级表。在创建流时，目的超级表将被自动创建，随后新插入的数据会被流定义的方式处理并写入其中，通过 partition by 子句，可以以表名或标签划分 partition，不同的 partition 将写入到目的超级表的不同子表。

TDengine 的流式计算能够支持分布在多个 vnode 中的超级表聚合；还能够处理乱序数据的写入：它提供了 watermark 机制以度量容忍数据乱序的程度，并提供了 ignore expired 配置项以决定乱序数据的处理策略——丢弃或者重新计算。

详见 [流式计算](https://docs.taosdata.com/taos-sql/stream/)

### 流式计算的创建

```sql
CREATE STREAM [IF NOT EXISTS] stream_name [stream_options] INTO stb_name AS subquery
stream_options: {
 TRIGGER    [AT_ONCE | WINDOW_CLOSE | MAX_DELAY time]
 WATERMARK   time
 IGNORE EXPIRED [0 | 1]
}
```

详细的语法规则参考 [流式计算](https://docs.taosdata.com/taos-sql/stream/)

#### 示例一

企业电表的数据经常都是成百上千亿条的，那么想要将这些分散、凌乱的数据清洗或转换都需要比较长的时间，很难做到高效性和实时性，以下例子中，通过流计算可以将电表电压大于 220V 的数据清洗掉，然后以 5 秒为窗口整合并计算出每个窗口中电流的最大值，最后将结果输出到指定的数据表中。

##### 创建 DB 和原始数据表

首先准备数据，完成建库、建一张超级表和多张子表操作

```sql
DROP DATABASE IF EXISTS power;
CREATE DATABASE power;
USE power;

CREATE STABLE meters (ts timestamp, current float, voltage int, phase float) TAGS (location binary(64), groupId int);

CREATE TABLE d1001 USING meters TAGS ("California.SanFrancisco", 2);
CREATE TABLE d1002 USING meters TAGS ("California.SanFrancisco", 3);
CREATE TABLE d1003 USING meters TAGS ("California.LosAngeles", 2);
CREATE TABLE d1004 USING meters TAGS ("California.LosAngeles", 3);
```

##### 创建流

```sql
create stream current_stream trigger at_once into current_stream_output_stb as select _wstart as wstart, _wend as wend, max(current) as max_current from meters where voltage <= 220 interval (5s);
```

##### 写入数据

```sql
insert into d1001 values("2018-10-03 14:38:05.000", 10.30000, 219, 0.31000);
insert into d1001 values("2018-10-03 14:38:15.000", 12.60000, 218, 0.33000);
insert into d1001 values("2018-10-03 14:38:16.800", 12.30000, 221, 0.31000);
insert into d1002 values("2018-10-03 14:38:16.650", 10.30000, 218, 0.25000);
insert into d1003 values("2018-10-03 14:38:05.500", 11.80000, 221, 0.28000);
insert into d1003 values("2018-10-03 14:38:16.600", 13.40000, 223, 0.29000);
insert into d1004 values("2018-10-03 14:38:05.000", 10.80000, 223, 0.29000);
insert into d1004 values("2018-10-03 14:38:06.500", 11.50000, 221, 0.35000);
```

##### 查询以观察结果

```sql
taos> select wstart, wend, max_current from current_stream_output_stb;
          wstart         |          wend           |     max_current      |
===========================================================================
 2018-10-03 14:38:05.000 | 2018-10-03 14:38:10.000 |             10.30000 |
 2018-10-03 14:38:15.000 | 2018-10-03 14:38:20.000 |             12.60000 |
Query OK, 2 rows in database (0.018762s)
```

#### 示例二

依然以示例一中的数据为基础，我们已经采集到了每个智能电表的电流和电压数据，现在需要求出有功功率和无功功率，并将地域和电表名以符号 "." 拼接，然后以电表名称分组输出到新的数据表中。

##### 创建 DB 和原始数据表

参考示例一 [创建 DB 和原始数据表](https://docs.taosdata.com/develop/stream/#创建-db-和原始数据表)

##### 创建流

```sql
create stream power_stream trigger at_once into power_stream_output_stb as select ts, concat_ws(".", location, tbname) as meter_location, current*voltage*cos(phase) as active_power, current*voltage*sin(phase) as reactive_power from meters partition by tbname;
```

##### 写入数据

参考示例一 [写入数据](https://docs.taosdata.com/develop/stream/#写入数据)

##### 查询以观察结果

```sql
taos> select ts, meter_location, active_power, reactive_power from power_stream_output_stb;
           ts            |         meter_location         |       active_power        |      reactive_power       |
===================================================================================================================
 2018-10-03 14:38:05.000 | California.LosAngeles.d1004    |            2307.834596289 |             688.687331847 |
 2018-10-03 14:38:06.500 | California.LosAngeles.d1004    |            2387.415754896 |             871.474763418 |
 2018-10-03 14:38:05.500 | California.LosAngeles.d1003    |            2506.240411679 |             720.680274962 |
 2018-10-03 14:38:16.600 | California.LosAngeles.d1003    |            2863.424274422 |             854.482390839 |
 2018-10-03 14:38:05.000 | California.SanFrancisco.d1001  |            2148.178871730 |             688.120784090 |
 2018-10-03 14:38:15.000 | California.SanFrancisco.d1001  |            2598.589176205 |             890.081451418 |
 2018-10-03 14:38:16.800 | California.SanFrancisco.d1001  |            2588.728381186 |             829.240910475 |
 2018-10-03 14:38:16.650 | California.SanFrancisco.d1002  |            2175.595991997 |             555.520860397 |
Query OK, 8 rows in database (0.014753s)
```

## 数据订阅

为了帮助应用实时获取写入 TDengine  的数据，或者以事件到达顺序处理数据，TDengine 提供了类似消息队列产品的数据订阅、消费接口。这样在很多场景下，采用 TDengine  的时序数据处理系统不再需要集成消息队列产品，比如 kafka, 从而简化系统设计的复杂度，降低运营维护成本。

与 kafka 一样，你需要定义 *topic*, 但 TDengine 的 *topic* 是基于一个已经存在的超级表、子表或普通表的查询条件，即一个 `SELECT` 语句。你可以使用 SQL 对标签、表名、列、表达式等条件进行过滤，以及对数据进行标量函数与 UDF  计算（不包括数据聚合）。与其他消息队列软件相比，这是 TDengine  数据订阅功能的最大的优势，它提供了更大的灵活性，数据的颗粒度可以由应用随时调整，而且数据的过滤与预处理交给  TDengine，而不是应用完成，有效的减少传输的数据量与应用的复杂度。

消费者订阅 *topic*  后，可以实时获得最新的数据。多个消费者可以组成一个消费者组 (consumer group),  一个消费者组里的多个消费者共享消费进度，便于多线程、分布式地消费数据，提高消费速度。但不同消费者组中的消费者即使消费同一个 topic,  并不共享消费进度。一个消费者可以订阅多个 topic。如果订阅的是超级表，数据可能会分布在多个不同的 vnode 上，也就是多个 shard  上，这样一个消费组里有多个消费者可以提高消费效率。TDengine 的消息队列提供了消息的 ACK 机制，在宕机、重启等复杂环境下确保 at  least once 消费。

为了实现上述功能，**TDengine 会为 WAL (Write-Ahead-Log)  文件自动创建索引以支持快速随机访问**，并提供了灵活可配置的文件切换与保留机制：用户可以按需指定 WAL 文件保留的时间以及大小（详见 create database 语句）。通过以上方式将 WAL 改造成了一个保留事件到达顺序的、可持久化的存储引擎（但由于 TSDB 具有远比 WAL  更高的压缩率，我们不推荐保留太长时间，一般来说，不超过几天）。 对于以 topic 形式创建的查询，TDengine 将对接 WAL 而不是  TSDB 作为其存储引擎。在消费时，TDengine 根据当前消费进度从 WAL  直接读取数据，并使用统一的查询引擎实现过滤、变换等操作，将数据推送给消费者。

本文档不对消息队列本身的基础知识做介绍，如果需要了解，请自行搜索。

注意：默认是从wal消费数据，如果wal被删除，消费到的数据会不全，此时可以将参数 experimental.snapshot.enable  设置为true，从tsdb获取全部数据，但是这样的话就不能保证数据的消费顺序。所以建议根据自己的消费情况合理的设置wal的保留策略，保证可以从wal里订阅到全部数据。

### 主要数据结构和 API

不同语言下， TMQ 订阅相关的 API 及数据结构如下：

```c
typedef struct tmq_t      tmq_t;
typedef struct tmq_conf_t tmq_conf_t;
typedef struct tmq_list_t tmq_list_t;

typedef void(tmq_commit_cb(tmq_t *, int32_t code, void *param));

DLL_EXPORT tmq_list_t *tmq_list_new();
DLL_EXPORT int32_t     tmq_list_append(tmq_list_t *, const char *);
DLL_EXPORT void        tmq_list_destroy(tmq_list_t *);
DLL_EXPORT tmq_t *tmq_consumer_new(tmq_conf_t *conf, char *errstr, int32_t errstrLen);
DLL_EXPORT const char *tmq_err2str(int32_t code);

DLL_EXPORT int32_t   tmq_subscribe(tmq_t *tmq, const tmq_list_t *topic_list);
DLL_EXPORT int32_t   tmq_unsubscribe(tmq_t *tmq);
DLL_EXPORT TAOS_RES *tmq_consumer_poll(tmq_t *tmq, int64_t timeout);
DLL_EXPORT int32_t   tmq_consumer_close(tmq_t *tmq);
DLL_EXPORT int32_t   tmq_commit_sync(tmq_t *tmq, const TAOS_RES *msg);
DLL_EXPORT void      tmq_commit_async(tmq_t *tmq, const TAOS_RES *msg, tmq_commit_cb *cb, void *param);

enum tmq_conf_res_t {
  TMQ_CONF_UNKNOWN = -2,
  TMQ_CONF_INVALID = -1,
  TMQ_CONF_OK = 0,
};
typedef enum tmq_conf_res_t tmq_conf_res_t;

DLL_EXPORT tmq_conf_t    *tmq_conf_new();
DLL_EXPORT tmq_conf_res_t tmq_conf_set(tmq_conf_t *conf, const char *key, const char *value);
DLL_EXPORT void           tmq_conf_destroy(tmq_conf_t *conf);
DLL_EXPORT void           tmq_conf_set_auto_commit_cb(tmq_conf_t *conf, tmq_commit_cb *cb, void *param);
```

这些 API 的文档请见 [C/C++ Connector](https://docs.taosdata.com/connector/cpp/)，下面介绍一下它们的具体用法（超级表和子表结构请参考“数据建模”一节），完整的示例代码请见下面 C 语言的示例代码。

### 写入数据

首先完成建库、建一张超级表和多张子表操作，然后就可以写入数据了，比如：

```sql
DROP DATABASE IF EXISTS tmqdb;
CREATE DATABASE tmqdb WAL_RETENTION_PERIOD 3600;  # wal保留期
CREATE TABLE tmqdb.stb (ts TIMESTAMP, c1 INT, c2 FLOAT, c3 VARCHAR(16)) TAGS(t1 INT, t3 VARCHAR(16));
CREATE TABLE tmqdb.ctb0 USING tmqdb.stb TAGS(0, "subtable0");
CREATE TABLE tmqdb.ctb1 USING tmqdb.stb TAGS(1, "subtable1");       
INSERT INTO tmqdb.ctb0 VALUES(now, 0, 0, 'a0')(now+1s, 0, 0, 'a00');
INSERT INTO tmqdb.ctb1 VALUES(now, 1, 1, 'a1')(now+1s, 11, 11, 'a11');
```

### 创建 *topic*

TDengine 使用 SQL 创建一个 topic：

```sql
CREATE TOPIC topic_name AS SELECT ts, c1, c2, c3 FROM tmqdb.stb WHERE c1 > 1;
```

### **TMQ 支持多种订阅类型**

#### 列订阅

语法：

```sql
CREATE TOPIC topic_name as subquery
```

通过 `SELECT` 语句订阅（包括 `SELECT *`，或 `SELECT ts, c1` 等指定列订阅，可以带条件过滤、标量函数计算，但不支持聚合函数、不支持时间窗口聚合）。需要注意的是：

- 该类型 TOPIC 一旦创建则订阅数据的结构确定。
- 被订阅或用于计算的列或标签不可被删除（`ALTER table DROP`）、修改（`ALTER table MODIFY`）。
- 若发生表结构变更，新增的列不出现在结果中。

#### 超级表订阅

语法：

```sql
CREATE TOPIC topic_name AS STABLE stb_name
```

与 `SELECT * from stbName` 订阅的区别是：

- 不会限制用户的表结构变更。
- 返回的是非结构化的数据：返回数据的结构会随之超级表的表结构变化而变化。
- 用户对于要处理的每一个数据块都可能有不同的表结构。
- 返回数据不包含标签。

#### 数据库订阅

语法：

```sql
CREATE TOPIC topic_name AS DATABASE db_name;
```

通过该语句可创建一个包含数据库所有表数据的订阅

### 创建消费者 *consumer*

消费者需要通过一系列配置选项创建，基础配置项如下表所示：

| 参数名称                       | 类型    | 参数说明                                                     | 备注                                                         |
| ------------------------------ | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `td.connect.ip`                | string  | 用于创建连接，同 `taos_connect`                              | 仅用于建立原生连接                                           |
| `td.connect.user`              | string  | 用于创建连接，同 `taos_connect`                              | 仅用于建立原生连接                                           |
| `td.connect.pass`              | string  | 用于创建连接，同 `taos_connect`                              | 仅用于建立原生连接                                           |
| `td.connect.port`              | integer | 用于创建连接，同 `taos_connect`                              | 仅用于建立原生连接                                           |
| `group.id`                     | string  | 消费组 ID，同一消费组共享消费进度                            | **必填项**。最大长度：192。                                  |
| `client.id`                    | string  | 客户端 ID                                                    | 最大长度：192。                                              |
| `auto.offset.reset`            | enum    | 消费组订阅的初始位置                                         | `earliest`: default;从头开始订阅;  `latest`: 仅从最新数据开始订阅;  `none`: 没有提交的 offset 无法订阅 |
| `enable.auto.commit`           | boolean | 是否启用消费位点自动提交，true: 自动提交，客户端应用无需commit；false：客户端应用需要自行commit | 默认值为 true                                                |
| `auto.commit.interval.ms`      | integer | 消费记录自动提交消费位点时间间隔，单位为毫秒                 | 默认值为 5000                                                |
| `experimental.snapshot.enable` | boolean | 是否允许从 TSDB 消费数据。当其关闭时，只能消费依据 WAL 保留策略仍然在WAL中的数据；当其打开时，除WAL中的数据以外，也能够消费已经从WAL中删除但落盘到TSDB中的数据 | 实验功能，默认关闭                                           |
| `msg.with.table.name`          | boolean | 是否允许从消息中解析表名, 不适用于列订阅（列订阅时可将 tbname 作为列写入 subquery 语句） | 默认关闭                                                     |

对于不同编程语言，其设置方式如下：

```c
/* 根据需要，设置消费组 (group.id)、自动提交 (enable.auto.commit)、
   自动提交时间间隔 (auto.commit.interval.ms)、用户名 (td.connect.user)、密码 (td.connect.pass) 等参数 */
tmq_conf_t* conf = tmq_conf_new();
tmq_conf_set(conf, "enable.auto.commit", "true");
tmq_conf_set(conf, "auto.commit.interval.ms", "1000");
tmq_conf_set(conf, "group.id", "cgrpName");
tmq_conf_set(conf, "td.connect.user", "root");
tmq_conf_set(conf, "td.connect.pass", "taosdata");
tmq_conf_set(conf, "auto.offset.reset", "earliest");
tmq_conf_set(conf, "experimental.snapshot.enable", "true");
tmq_conf_set(conf, "msg.with.table.name", "true");
tmq_conf_set_auto_commit_cb(conf, tmq_commit_cb_print, NULL);

tmq_t* tmq = tmq_consumer_new(conf, NULL, 0);
tmq_conf_destroy(conf);
```

上述配置中包括 consumer group ID，如果多个 consumer 指定的 consumer group ID 一样，则自动形成一个 consumer group，共享消费进度。

### 订阅 *topics*

一个 consumer 支持同时订阅多个 topic。

```c
// 创建订阅 topics 列表
tmq_list_t* topicList = tmq_list_new();
tmq_list_append(topicList, "topicName");
// 启动订阅
tmq_subscribe(tmq, topicList);
tmq_list_destroy(topicList);
```

### 消费

以下代码展示了不同语言下如何对 TMQ 消息进行消费。

```c
// 消费数据
while (running) {
  TAOS_RES* msg = tmq_consumer_poll(tmq, timeOut);
  msg_process(msg);
}  
```

这里是一个 **while** 循环，每调用一次 tmq_consumer_poll()，获取一个消息，该消息与普通查询返回的结果集完全相同，可以使用相同的解析 API 完成消息内容的解析。

### 结束消费

消费结束后，应当取消订阅。

```c
/* 取消订阅 */
tmq_unsubscribe(tmq);  //与tmq_subscribe对应

/* 关闭消费者对象 */
tmq_consumer_close(tmq);
```

### 删除 *topic*

如果不再需要订阅数据，可以删除 topic，需要注意：**只有当前未在订阅中的 TOPIC 才能被删除。**

```sql
/* 删除 topic */
DROP TOPIC topic_name;
```

### 状态查看

1、*topics*：查询已经创建的 topic

```sql
SHOW TOPICS;
```

2、consumers：查询 consumer 的状态及其订阅的 topic

```sql
SHOW CONSUMERS;
```

3、subscriptions：查询 consumer 与 vgroup 之间的分配关系

```sql
SHOW SUBSCRIPTIONS;
```

### 示例代码

以下是各语言的完整示例代码。

```c
/*
 * Copyright (c) 2019 TAOS Data, Inc. <jhtao@taosdata.com>
 *
 * This program is free software: you can use, redistribute, and/or modify
 * it under the terms of the GNU Affero General Public License, version 3
 * or later ("AGPL"), as published by the Free Software Foundation.
 *
 * This program is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.
 *
 * You should have received a copy of the GNU Affero General Public License
 * along with this program. If not, see <http://www.gnu.org/licenses/>.
 */

#include <assert.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include "taos.h"

static int  running = 1;
static char dbName[64] = "tmqdb";
static char stbName[64] = "stb";
static char topicName[64] = "topicname";

static int32_t msg_process(TAOS_RES* msg) {
  char    buf[1024];
  int32_t rows = 0;

  const char* topicName = tmq_get_topic_name(msg);
  const char* dbName = tmq_get_db_name(msg);
  int32_t     vgroupId = tmq_get_vgroup_id(msg);

  printf("topic: %s\n", topicName);
  printf("db: %s\n", dbName);
  printf("vgroup id: %d\n", vgroupId);

  while (1) {
    TAOS_ROW row = taos_fetch_row(msg);
    if (row == NULL) break;

    TAOS_FIELD* fields = taos_fetch_fields(msg);
    int32_t     numOfFields = taos_field_count(msg);
    int32_t*    length = taos_fetch_lengths(msg);
    int32_t     precision = taos_result_precision(msg);
    rows++;
    taos_print_row(buf, row, fields, numOfFields);
    printf("row content: %s\n", buf);
  }

  return rows;
}

static int32_t init_env() {
  TAOS* pConn = taos_connect("localhost", "root", "taosdata", NULL, 0);
  if (pConn == NULL) {
    return -1;
  }

  TAOS_RES* pRes;
  // drop database if exists
  printf("create database\n");
  pRes = taos_query(pConn, "drop database if exists tmqdb");
  if (taos_errno(pRes) != 0) {
    printf("error in drop tmqdb, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  // create database
  pRes = taos_query(pConn, "create database tmqdb wal_retention_period 3600"); //wal_retention_period 设置为 3600
  if (taos_errno(pRes) != 0) {
    printf("error in create tmqdb, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  // create super table
  printf("create super table\n");
  pRes = taos_query(
      pConn, "create table tmqdb.stb (ts timestamp, c1 int, c2 float, c3 varchar(16)) tags(t1 int, t3 varchar(16))");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table stb, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);  //每次执行后都要free掉结果

  // create sub tables
  printf("create sub tables\n");
  pRes = taos_query(pConn, "create table tmqdb.ctb0 using tmqdb.stb tags(0, 'subtable0')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb0, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create table tmqdb.ctb1 using tmqdb.stb tags(1, 'subtable1')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb1, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create table tmqdb.ctb2 using tmqdb.stb tags(2, 'subtable2')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb2, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create table tmqdb.ctb3 using tmqdb.stb tags(3, 'subtable3')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb3, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  // insert data
  printf("insert data into sub tables\n");
  pRes = taos_query(pConn, "insert into tmqdb.ctb0 values(now, 0, 0, 'a0')(now+1s, 0, 0, 'a00')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "insert into tmqdb.ctb1 values(now, 1, 1, 'a1')(now+1s, 11, 11, 'a11')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "insert into tmqdb.ctb2 values(now, 2, 2, 'a1')(now+1s, 22, 22, 'a22')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "insert into tmqdb.ctb3 values(now, 3, 3, 'a1')(now+1s, 33, 33, 'a33')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  taos_close(pConn);  //关闭连接
  return 0;
}

int32_t create_topic() {
  printf("create topic\n");
  TAOS_RES* pRes; 
  TAOS*     pConn = taos_connect("localhost", "root", "taosdata", NULL, 0);
  if (pConn == NULL) {
    return -1;
  }

  pRes = taos_query(pConn, "use tmqdb");
  if (taos_errno(pRes) != 0) {
    printf("error in use tmqdb, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create topic topicname as select ts, c1, c2, c3, tbname from tmqdb.stb where c1 > 1"); //查询超级表，即在所有的子表中聚合查询
  if (taos_errno(pRes) != 0) {
    printf("failed to create topic topicname, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  taos_close(pConn);
  return 0;
}

void tmq_commit_cb_print(tmq_t* tmq, int32_t code, void* param) {
  printf("tmq_commit_cb_print() code: %d, tmq: %p, param: %p\n", code, tmq, param);
}

tmq_t* build_consumer() {
  tmq_conf_res_t code;
  tmq_conf_t*    conf = tmq_conf_new();

  code = tmq_conf_set(conf, "enable.auto.commit", "true");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  code = tmq_conf_set(conf, "auto.commit.interval.ms", "1000");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  code = tmq_conf_set(conf, "group.id", "cgrpName");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  code = tmq_conf_set(conf, "client.id", "user defined name");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  code = tmq_conf_set(conf, "td.connect.user", "root");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  code = tmq_conf_set(conf, "td.connect.pass", "taosdata");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  code = tmq_conf_set(conf, "auto.offset.reset", "earliest");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  code = tmq_conf_set(conf, "experimental.snapshot.enable", "false");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  tmq_conf_set_auto_commit_cb(conf, tmq_commit_cb_print, NULL);

  tmq_t* tmq = tmq_consumer_new(conf, NULL, 0);
  tmq_conf_destroy(conf);
  return tmq;
}

tmq_list_t* build_topic_list() {
  tmq_list_t* topicList = tmq_list_new();
  int32_t     code = tmq_list_append(topicList, "topicname");
  if (code) {
    return NULL;
  }
  return topicList;
}

void basic_consume_loop(tmq_t* tmq) {
  int32_t totalRows = 0;
  int32_t msgCnt = 0;
  int32_t timeout = 5000;
  while (running) {
    TAOS_RES* tmqmsg = tmq_consumer_poll(tmq, timeout);
    if (tmqmsg) {
      msgCnt++;
      totalRows += msg_process(tmqmsg);
      taos_free_result(tmqmsg);
    } else {
      break;
    }
  }

  fprintf(stderr, "%d msg consumed, include %d rows\n", msgCnt, totalRows);
}

int main(int argc, char* argv[]) {
  int32_t code;

  if (init_env() < 0) {  //创建数据库、超级表、子表并插入数据
    return -1;
  }

  if (create_topic() < 0) {//创建topic
    return -1;
  }

  tmq_t* tmq = build_consumer(); /
  if (NULL == tmq) {
    fprintf(stderr, "%% build_consumer() fail!\n");
    return -1;
  }

  tmq_list_t* topic_list = build_topic_list();
  if (NULL == topic_list) {
    return -1;
  }

  if ((code = tmq_subscribe(tmq, topic_list))) {
    fprintf(stderr, "%% Failed to tmq_subscribe(): %s\n", tmq_err2str(code));
  }
  tmq_list_destroy(topic_list);

  basic_consume_loop(tmq);

  code = tmq_consumer_close(tmq);
  if (code) {
    fprintf(stderr, "%% Failed to close consumer: %s\n", tmq_err2str(code));
  } else {
    fprintf(stderr, "%% Consumer closed\n");
  }

  return 0;
}
```

[查看源码](https://github.com/taosdata/TDengine/blob/3.0/docs/examples/c/tmq_example.c)

## 缓存

为了实现高效的写入和查询，TDengine 充分利用了各种缓存技术，本节将对 TDengine 中对缓存的使用做详细的说明。

### 写缓存

TDengine  采用时间驱动缓存管理策略（First-In-First-Out，FIFO），又称为写驱动的缓存管理机制。这种策略有别于读驱动的数据缓存模式（Least-Recent-Used，LRU），直接将最近写入的数据保存在系统的缓存中。当缓存达到临界值的时候，将最早的数据批量写入磁盘。一般意义上来说，对于物联网数据的使用，用户最为关心最近产生的数据，即当前状态。TDengine 充分利用了这一特性，将最近到达的（当前状态）数据保存在缓存中。

每个 vnode 的写入缓存大小在创建数据库时决定，创建数据库时的两个关键参数 vgroups 和 buffer 分别决定了该数据库中的数据由多少个 vgroup 处理，以及向其中的每个 vnode 分配多少写入缓存。

```sql
create database db0 vgroups 100 buffer 16MB
```

理论上缓存越大越好，但超过一定阈值后再增加缓存对写入性能提升并无帮助，一般情况下使用默认值即可。

### 读缓存

在创建数据库时可以选择是否缓存该数据库中每个子表的最新数据。由参数 cachemodel 设置，分为四种情况：

- none: 不缓存
- last_row: 缓存子表最近一行数据，这将显著改善 last_row 函数的性能
- last_value: 缓存子表每一列最近的非 NULL 值，这将显著改善无特殊影响（比如 WHERE, ORDER BY, GROUP BY, INTERVAL）时的 last 函数的性能
- both: 同时缓存最近的行和列，即等同于上述 cachemodel 值为 last_row 和 last_value 的行为同时生效

### 元数据缓存

为了更高效地处理查询和写入，每个 vnode 都会缓存自己曾经获取到的元数据。元数据缓存由创建数据库时的两个参数 pages 和 pagesize 决定。

```sql
create database db0 pages 128 pagesize 16kb
```

上述语句会为数据库 db0 的每个 vnode 创建 128 个 page，每个 page 16kb 的元数据缓存。

### 文件系统缓存

TDengine 利用 WAL 技术来提供基本的数据可靠性。写入 WAL 本质上是以顺序追加的方式写入磁盘文件。此时文件系统缓存在写入性能中也会扮演关键角色。在创建数据库时可以利用 wal 参数来选择性能优先或者可靠性优先。

- 1: 写 WAL 但不执行 fsync ，新写入 WAL 的数据保存在文件系统缓存中但并未写入磁盘，这种方式性能优先
- 2: 写 WAL 且执行 fsync，新写入 WAL 的数据被立即同步到磁盘上，可靠性更高

### 客户端缓存

为了进一步提升整个系统的处理效率，除了以上提到的服务端缓存技术之外，在 TDengine 的所有客户端都要调用的核心库 libtaos.so （也称为 taosc ）中也充分利用了缓存技术。在 taosc  中会缓存所访问过的各个数据库、超级表以及子表的元数据，集群的拓扑结构等关键元数据。

当有多个客户端同时访问 TDengine  集群，且其中一个客户端对某些元数据进行了修改的情况下，有可能会出现其它客户端所缓存的元数据不同步或失效的情况，此时需要在客户端执行 "reset query cache" 以让整个缓存失效从而强制重新拉取最新的元数据重新建立缓存。



## UDF（用户定义函数）

在有些应用场景中，应用逻辑需要的查询无法直接使用系统内置的函数来表示。利用 UDF(User Defined Function) 功能，TDengine  可以插入用户编写的处理代码并在查询中使用它们，就能够很方便地解决特殊应用场景中的使用需求。 UDF  通常以数据表中的一列数据做为输入，同时支持以嵌套子查询的结果作为输入。

用户可以通过 UDF 实现两类函数：标量函数和聚合函数。标量函数对每行数据输出一个值，如求绝对值 abs，正弦函数 sin，字符串拼接函数 concat 等。聚合函数对多行数据进行输出一个值，如求平均数 avg，最大值 max 等。

TDengine 支持通过 C/Python 语言进行 UDF 定义。接下来结合示例讲解 UDF 的使用方法。

### 用 C 语言实现 UDF

使用 C 语言实现 UDF 时，需要实现规定的接口函数

- 标量函数需要实现标量接口函数 scalarfn 。
- 聚合函数需要实现聚合接口函数 aggfn_start ， aggfn ， aggfn_finish。
- 如果需要初始化，实现 udf_init；如果需要清理工作，实现udf_destroy。

接口函数的名称是 UDF 名称，或者是 UDF 名称和特定后缀（_start, _finish, _init, _destroy)的连接。列表中的scalarfn，aggfn, udf需要替换成udf函数名。

#### 用 C 语言实现标量函数

标量函数实现模板如下

```c
#include "taos.h"
#include "taoserror.h"
#include "taosudf.h"

// initialization function. if no initialization, we can skip definition of it. The initialization function shall be concatenation of the udf name and _init suffix
// @return error number defined in taoserror.h
int32_t scalarfn_init() {
    // initialization.
    return TSDB_CODE_SUCCESS;
}

// scalar function main computation function
// @param inputDataBlock, input data block composed of multiple columns with each column defined by SUdfColumn
// @param resultColumn, output column
// @return error number defined in taoserror.h
int32_t scalarfn(SUdfDataBlock* inputDataBlock, SUdfColumn* resultColumn) {
    // read data from inputDataBlock and process, then output to resultColumn.
    return TSDB_CODE_SUCCESS;
}

// cleanup function. if no cleanup related processing, we can skip definition of it. The destroy function shall be concatenation of the udf name and _destroy suffix.
// @return error number defined in taoserror.h
int32_t scalarfn_destroy() {
    // clean up
    return TSDB_CODE_SUCCESS;
}
```

scalarfn 为函数名的占位符，需要替换成函数名，如bit_and。

#### 用 C 语言实现聚合函数

聚合函数的实现模板如下

```c
#include "taos.h"
#include "taoserror.h"
#include "taosudf.h"

// Initialization function. if no initialization, we can skip definition of it. The initialization function shall be concatenation of the udf name and _init suffix
// @return error number defined in taoserror.h
int32_t aggfn_init() {
    // initialization.
    return TSDB_CODE_SUCCESS;
}

// aggregate start function. The intermediate value or the state(@interBuf) is initialized in this function. The function name shall be concatenation of udf name and _start suffix
// @param interbuf intermediate value to initialize
// @return error number defined in taoserror.h
int32_t aggfn_start(SUdfInterBuf* interBuf) {
    // initialize intermediate value in interBuf
    return TSDB_CODE_SUCCESS;
}

// aggregate reduce function. This function aggregate old state(@interbuf) and one data bock(inputBlock) and output a new state(@newInterBuf).
// @param inputBlock input data block
// @param interBuf old state
// @param newInterBuf new state
// @return error number defined in taoserror.h
int32_t aggfn(SUdfDataBlock* inputBlock, SUdfInterBuf *interBuf, SUdfInterBuf *newInterBuf) {
    // read from inputBlock and interBuf and output to newInterBuf
    return TSDB_CODE_SUCCESS;
}

// aggregate function finish function. This function transforms the intermediate value(@interBuf) into the final output(@result). The function name must be concatenation of aggfn and _finish suffix.
// @interBuf : intermediate value
// @result: final result
// @return error number defined in taoserror.h
int32_t int32_t aggfn_finish(SUdfInterBuf* interBuf, SUdfInterBuf *result) {
    // read data from inputDataBlock and process, then output to result
    return TSDB_CODE_SUCCESS;
}

// cleanup function. if no cleanup related processing, we can skip definition of it. The destroy function shall be concatenation of the udf name and _destroy suffix.
// @return error number defined in taoserror.h
int32_t aggfn_destroy() {
    // clean up
    return TSDB_CODE_SUCCESS;
}
```

aggfn为函数名的占位符，需要修改为自己的函数名，如l2norm。

#### C 语言 UDF 接口函数定义

接口函数的名称是 udf 名称，或者是 udf 名称和特定后缀（_start, _finish, _init, _destroy)的连接。以下描述中函数名称中的 scalarfn，aggfn, udf 需要替换成udf函数名。

接口函数返回值表示是否成功。如果返回值是 TSDB_CODE_SUCCESS，表示操作成功，否则返回的是错误代码。错误代码定义在 taoserror.h，和 taos.h  中的API共享错误码的定义。例如， TSDB_CODE_UDF_INVALID_INPUT  表示输入无效输入。TSDB_CODE_OUT_OF_MEMORY 表示内存不足。

接口函数参数类型见数据结构定义。

##### 标量函数接口

 `int32_t scalarfn(SUdfDataBlock* inputDataBlock, SUdfColumn *resultColumn)` 

 其中 scalarFn 是函数名的占位符。这个函数对数据块进行标量计算，通过设置resultColumn结构体中的变量设置值

参数的具体含义是：

- inputDataBlock: 输入的数据块
- resultColumn: 输出列 

##### 聚合函数接口

```
int32_t aggfn_start(SUdfInterBuf *interBuf)
int32_t aggfn(SUdfDataBlock* inputBlock, SUdfInterBuf *interBuf, SUdfInterBuf *newInterBuf)
int32_t aggfn_finish(SUdfInterBuf* interBuf, SUdfInterBuf *result)
```

其中 aggfn 是函数名的占位符。首先调用aggfn_start生成结果buffer，然后相关的数据会被分为多个行数据块，对每个数据块调用  aggfn 用数据块更新中间结果，最后再调用 aggfn_finish 从中间结果产生最终结果，最终结果只能含 0 或 1 条结果数据。

参数的具体含义是：

- interBuf：中间结果 buffer。
- inputBlock：输入的数据块。
- newInterBuf：新的中间结果buffer。
- result：最终结果。

#### 初始化和销毁接口

```
int32_t udf_init()
int32_t udf_destroy()
```

其中 udf 是函数名的占位符。udf_init 完成初始化工作。 udf_destroy 完成清理工作。如果没有初始化工作，无需定义udf_init函数。如果没有清理工作，无需定义udf_destroy函数。

#### C 语言 UDF 数据结构

```c
typedef struct SUdfColumnMeta {
  int16_t type;
  int32_t bytes;
  uint8_t precision;
  uint8_t scale;
} SUdfColumnMeta;

typedef struct SUdfColumnData {
  int32_t numOfRows;
  int32_t rowsAlloc;
  union {
    struct {
      int32_t nullBitmapLen;
      char   *nullBitmap;
      int32_t dataLen;
      char   *data;
    } fixLenCol;

    struct {
      int32_t varOffsetsLen;
      int32_t   *varOffsets;
      int32_t payloadLen;
      char   *payload;
      int32_t payloadAllocLen;
    } varLenCol;
  };
} SUdfColumnData;

typedef struct SUdfColumn {
  SUdfColumnMeta colMeta;
  bool           hasNull;
  SUdfColumnData colData;
} SUdfColumn;

typedef struct SUdfDataBlock {
  int32_t numOfRows;
  int32_t numOfCols;
  SUdfColumn **udfCols;
} SUdfDataBlock;

typedef struct SUdfInterBuf {
  int32_t bufLen;
  char* buf;
  int8_t numOfResult; //zero or one
} SUdfInterBuf;
```

数据结构说明如下：

- SUdfDataBlock 数据块包含行数 numOfRows 和列数 numCols。udfCols[i] (0 <= i <= numCols-1)表示每一列数据，类型为SUdfColumn*。
- SUdfColumn 包含列的数据类型定义 colMeta 和列的数据 colData。
- SUdfColumnMeta 成员定义同 taos.h 数据类型定义。
- SUdfColumnData 数据可以变长，varLenCol 定义变长数据，fixLenCol 定义定长数据。 
- SUdfInterBuf 定义中间结构 buffer，以及 buffer 中结果个数 numOfResult

为了更好的操作以上数据结构，提供了一些便利函数，定义在 taosudf.h。

#### 编译 C UDF

用户定义函数的 C 语言源代码无法直接被 TDengine 系统使用，而是需要先编译为 动态链接库，之后才能载入 TDengine 系统。

例如，按照上一章节描述的规则准备好了用户定义函数的源代码 bit_and.c，以 Linux 为例可以执行如下指令编译得到动态链接库文件：

```bash
gcc -g -O0 -fPIC -shared bit_and.c -o libbitand.so
```

这样就准备好了动态链接库 libbitand.so 文件，可以供后文创建 UDF 时使用了。为了保证可靠的系统运行，编译器 GCC 推荐使用 7.5 及以上版本。

#### C UDF 示例代码

##### 标量函数示例 [bit_and](https://github.com/taosdata/TDengine/blob/3.0/tests/script/sh/bit_and.c)

bit_add 实现多列的按位与功能。如果只有一列，返回这一列。bit_add 忽略空值。

```c++
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "taosudf.h"

DLL_EXPORT int32_t bit_and_init() { return 0; } //实现初始化

DLL_EXPORT int32_t bit_and_destroy() { return 0; } //实现清理工作

DLL_EXPORT int32_t bit_and(SUdfDataBlock* block, SUdfColumn* resultCol) { //标量函数接口
  if (block->numOfCols < 2) {
    return TSDB_CODE_UDF_INVALID_INPUT;
  }

  for (int32_t i = 0; i < block->numOfCols; ++i) {
    SUdfColumn* col = block->udfCols[i];
    if (!(col->colMeta.type == TSDB_DATA_TYPE_INT)) {
      return TSDB_CODE_UDF_INVALID_INPUT;
    }
  }

  SUdfColumnData* resultData = &resultCol->colData;

  for (int32_t i = 0; i < block->numOfRows; ++i) {
    if (udfColDataIsNull(block->udfCols[0], i)) {
      udfColDataSetNull(resultCol, i);
      continue;
    }
    int32_t result = *(int32_t*)udfColDataGetData(block->udfCols[0], i);
    int     j = 1;
    for (; j < block->numOfCols; ++j) {
      if (udfColDataIsNull(block->udfCols[j], i)) {
        udfColDataSetNull(resultCol, i);
        break;
      }

      char* colData = udfColDataGetData(block->udfCols[j], i);
      result &= *(int32_t*)colData;
    }
    if (j == block->numOfCols) {
      udfColDataSet(resultCol, i, (char*)&result, false);
    }
  }
  resultData->numOfRows = block->numOfRows;

  return TSDB_CODE_SUCCESS;
}
```

##### 聚合函数示例1 返回值为数值类型 [l2norm](https://github.com/taosdata/TDengine/blob/3.0/tests/script/sh/l2norm.c)

l2norm 实现了输入列的所有数据的二阶范数，即对每个数据先平方，再累加求和，最后开方。

```c++
#include <string.h>
#include <stdlib.h>
#include <stdio.h>
#include <math.h>

#include "taosudf.h"

DLL_EXPORT int32_t l2norm_init() {
  return 0;
}

DLL_EXPORT int32_t l2norm_destroy() {
  return 0;
}

DLL_EXPORT int32_t l2norm_start(SUdfInterBuf *buf) {
  *(int64_t*)(buf->buf) = 0;
  buf->bufLen = sizeof(double);
  buf->numOfResult = 1;
  return 0;
}

DLL_EXPORT int32_t l2norm(SUdfDataBlock* block, SUdfInterBuf *interBuf, SUdfInterBuf *newInterBuf) {
  double sumSquares = *(double*)interBuf->buf;
  int8_t numNotNull = 0;
  for (int32_t i = 0; i < block->numOfCols; ++i) {
    SUdfColumn* col = block->udfCols[i];
    if (!(col->colMeta.type == TSDB_DATA_TYPE_INT || 
          col->colMeta.type == TSDB_DATA_TYPE_DOUBLE)) {
      return TSDB_CODE_UDF_INVALID_INPUT;
    }
  }
  for (int32_t i = 0; i < block->numOfCols; ++i) {
    for (int32_t j = 0; j < block->numOfRows; ++j) {
      SUdfColumn* col = block->udfCols[i];
      if (udfColDataIsNull(col, j)) {
        continue;
      }
      switch (col->colMeta.type) {
        case TSDB_DATA_TYPE_INT: {
          char* cell = udfColDataGetData(col, j);
          int32_t num = *(int32_t*)cell;
          sumSquares += (double)num * num;
          break;
        }
        case TSDB_DATA_TYPE_DOUBLE: {
          char* cell = udfColDataGetData(col, j);
          double num = *(double*)cell;
          sumSquares += num * num;
          break;
        }
        default: 
          break;
      }
      ++numNotNull;
    }
  }

  *(double*)(newInterBuf->buf) = sumSquares;
  newInterBuf->bufLen = sizeof(double);
  newInterBuf->numOfResult = 1;
  return 0;
}

DLL_EXPORT int32_t l2norm_finish(SUdfInterBuf* buf, SUdfInterBuf *resultData) {
  double sumSquares = *(double*)(buf->buf);
  *(double*)(resultData->buf) = sqrt(sumSquares);
  resultData->bufLen = sizeof(double);
  resultData->numOfResult = 1;
  return 0;
}
```

### 管理和使用 UDF

在使用 UDF 之前需要先将其加入到 TDengine 系统中。关于如何管理和使用 UDF，请参考[管理和使用 UDF](https://docs.taosdata.com/taos-sql/udf/)

# 连接器

TDengine  提供了丰富的应用程序开发接口，为了便于用户快速开发自己的应用，TDengine 支持了多种编程语言的连接器，其中官方连接器包括支持  C/C++、Java、Python、Go、Node.js、C# 和 Rust 的连接器。这些连接器支持使用原生接口（taosc）和 REST  接口（部分语言暂不支持）连接 TDengine 集群。社区开发者也贡献了多个非官方连接器，例如 ADO.NET 连接器、Lua 连接器和 PHP 连接器。

![TDengine Database connector architecture](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/connector-11ffb2bf63d17d862919ca85a7fd1ff6.webp)

## 支持的平台

目前 TDengine 的原生接口连接器可支持的平台包括：X64/ARM64 等硬件平台，以及 Linux/Win64 等开发环境。对照矩阵如下：

| **CPU**       | **OS**    | **Java** | **Python** | **Go** | **Node.js** | **C#** | **Rust** | C/C++ |
| ------------- | --------- | -------- | ---------- | ------ | ----------- | ------ | -------- | ----- |
| **X86 64bit** | **Linux** | ●        | ●          | ●      | ●           | ●      | ●        | ●     |
| **X86 64bit** | **Win64** | ●        | ●          | ●      | ●           | ●      | ●        | ●     |
| **ARM64**     | **Linux** | ●        | ●          | ●      | ●           | ○      | ○        | ●     |

其中 ● 表示官方测试验证通过，○ 表示非官方测试验证通过，-- 表示未经验证。

使用 REST 连接由于不依赖客户端驱动可以支持更广泛的操作系统。

## 版本支持

TDengine 版本更新往往会增加新的功能特性，列表中的连接器版本为连接器最佳适配版本。

| **TDengine 版本**      | **Java**  | **Python** | **Go**       | **C#**        | **Node.js**     | **Rust** |
| ---------------------- | --------- | ---------- | ------------ | ------------- | --------------- | -------- |
| **3.0.0.0 及以上**     | 3.0.2以上 | 当前版本   | 3.0 分支     | 3.0.0         | 3.0.0           | 当前版本 |
| **2.4.0.14 及以上**    | 2.0.38    | 当前版本   | develop 分支 | 1.0.2 - 1.0.6 | 2.0.10 - 2.0.12 | 当前版本 |
| **2.4.0.4 - 2.4.0.13** | 2.0.37    | 当前版本   | develop 分支 | 1.0.2 - 1.0.6 | 2.0.10 - 2.0.12 | 当前版本 |
| **2.2.x.x**            | 2.0.36    | 当前版本   | master 分支  | n/a           | 2.0.7 - 2.0.9   | 当前版本 |
| **2.0.x.x**            | 2.0.34    | 当前版本   | master 分支  | n/a           | 2.0.1 - 2.0.6   | 当前版本 |

## 功能特性

连接器对 TDengine 功能特性的支持对照如下：

### 使用原生接口（taosc）

| **功能特性**        | **Java** | **Python** | **Go** | **C#** | **Node.js** | **Rust** |
| ------------------- | -------- | ---------- | ------ | ------ | ----------- | -------- |
| **连接管理**        | 支持     | 支持       | 支持   | 支持   | 支持        | 支持     |
| **普通查询**        | 支持     | 支持       | 支持   | 支持   | 支持        | 支持     |
| **参数绑定**        | 支持     | 支持       | 支持   | 支持   | 支持        | 支持     |
| **数据订阅（TMQ）** | 支持     | 支持       | 支持   | 支持   | 支持        | 支持     |
| **Schemaless**      | 支持     | 支持       | 支持   | 支持   | 支持        | 支持     |
| **DataFrame**       | 不支持   | 支持       | 不支持 | 不支持 | 不支持      | 不支持   |

##### info

由于不同编程语言数据库框架规范不同，并不意味着所有 C/C++ 接口都需要对应封装支持。

### 使用 http (REST 或 WebSocket) 接口

| **功能特性**                   | **Java** | **Python** | **Go**   | **C#**   | **Node.js** | **Rust** |
| ------------------------------ | -------- | ---------- | -------- | -------- | ----------- | -------- |
| **连接管理**                   | 支持     | 支持       | 支持     | 支持     | 支持        | 支持     |
| **普通查询**                   | 支持     | 支持       | 支持     | 支持     | 支持        | 支持     |
| **参数绑定**                   | 暂不支持 | 暂不支持   | 支持     | 支持     | 暂不支持    | 支持     |
| **数据订阅（TMQ）**            | 支持     | 支持       | 支持     | 暂不支持 | 暂不支持    | 支持     |
| **Schemaless**                 | 支持     | 暂不支持   | 暂不支持 | 暂不支持 | 暂不支持    | 暂不支持 |
| **批量拉取（基于 WebSocket）** | 支持     | 支持       | 支持     | 支持     | 支持        | 支持     |
| **DataFrame**                  | 不支持   | 支持       | 不支持   | 不支持   | 不支持      | 不支持   |

##### warning

- 无论选用何种编程语言的连接器，2.0 及以上版本的 TDengine 推荐数据库应用的每个线程都建立一个独立的连接，或基于线程建立连接池，以避免连接内的“USE statement”状态量在线程之间相互干扰（但连接的查询和写入操作都是线程安全的）。

## 安装客户端驱动

##### info

只有在没有安装 TDengine 服务端软件的系统上使用原生接口连接器才需要安装客户端驱动。

### 安装步骤

- Linux
- Windows
- MacOS

1. 下载客户端安装包

   - [TDengine-client-3.0.4.1-Linux-x64.tar.gz (34.6 M)](https://docs.taosdata.com/connector/#!)
   - [TDengine-client-3.0.4.1-Linux-arm64.tar.gz (10.4 M)](https://docs.taosdata.com/connector/#!)
   - [TDengine-client-3.0.4.1-Linux-x64-Lite.tar.gz (6.4 M)](https://docs.taosdata.com/connector/#!)

    [所有下载](https://docs.taosdata.com/releases/tdengine/)

2. 解压缩软件包

   将软件包放置在当前用户可读写的任意目录下，然后执行下面的命令：`tar -xzvf TDengine-client-VERSION.tar.gz` 其中 VERSION 需要替换为实际版本的字符串。

3. 执行安装脚本

   解压软件包之后，会在解压目录下看到以下文件(目录)：

   -  *install_client.sh*：安装脚本，用于应用驱动程序
   -  *package.tar.gz*：应用驱动安装包
   -  *driver*：TDengine 应用驱动 driver
   - *examples*: 各种编程语言的示例程序(c/C#/go/JDBC/MATLAB/python/R) 运行 install_client.sh 进行安装。

4. 配置 taos.cfg

   编辑 `taos.cfg` 文件（默认路径/etc/taos/taos.cfg），将 `firstEP` 修改为 TDengine 服务器的 End Point，例如：`h1.tdengine.com:6030`

##### 

##### tip

1. 如本机没有部署 TDengine 服务，仅安装了应用驱动，则 `taos.cfg` 中仅需配置 `firstEP`，无需在本机配置 `FQDN`。
2. 为防止与服务器端连接时出现“Unable to resolve FQDN”错误，建议确认本机的 `/etc/hosts` 文件已经配置了服务器正确的 FQDN 值，或配置好了 DNS 服务。

### 安装验证

以上安装和配置完成后，并确认 TDengine 服务已经正常启动运行，此时可以执行 TDengine CLI 工具进行登录。

- Linux
- Windows
- MacOS

在 Linux shell 下直接执行 `taos` 连接到 TDengine 服务，进入到 TDengine CLI 界面，示例如下：

```text
$ taos

taos> show databases;
              name              |
=================================
 information_schema             |
 performance_schema             |
 db                             |
Query OK, 3 rows in database (0.019154s)

taos>
```

## C/C++ Connector

C/C++ 开发人员可以使用 TDengine  的客户端驱动，即 C/C++连接器 （以下都用 TDengine 客户端驱动表示），开发自己的应用来连接 TDengine  集群完成数据存储、查询以及其他功能。TDengine 客户端驱动的 API 类似于 MySQL 的 C API。应用程序使用时，需要包含  TDengine 头文件 *taos.h*，里面列出了提供的 API 的函数原型；应用程序还要链接到所在平台上对应的动态库。

```c
#include <taos.h>
```

TDengine 服务端或客户端安装后，`taos.h` 位于：

- Linux：`/usr/local/taos/include`
- Windows：`C:\TDengine\include`
- macOS：`/usr/local/include`

TDengine 客户端驱动的动态库位于：

- Linux: `/usr/local/taos/driver/libtaos.so`
- Windows: `C:\TDengine\taos.dll`
- macOS: `/usr/local/lib/libtaos.dylib`

### 支持的平台

请参考[支持的平台列表](https://docs.taosdata.com/connector/#支持的平台)

### 支持的版本

TDengine 客户端驱动的版本号与 TDengine 服务端的版本号是一一对应的强对应关系，建议使用与 TDengine  服务端完全相同的客户端驱动。虽然低版本的客户端驱动在前三段版本号一致（即仅第四段版本号不同）的情况下也能够与高版本的服务端相兼容，但这并非推荐用法。强烈不建议使用高版本的客户端驱动访问低版本的服务端。

### 安装步骤

TDengine 客户端驱动的安装请参考 [安装指南](https://docs.taosdata.com/connector/#安装步骤)

### 建立连接

使用客户端驱动访问 TDengine 集群的基本过程为：建立连接、查询和写入、关闭连接、清除资源。

下面为建立连接的示例代码，其中省略了查询和写入部分，展示了如何建立连接、关闭连接以及清除资源。

```c
  TAOS *taos = taos_connect("localhost:6030", "root", "taosdata", NULL, 0);
  if (taos == NULL) {
    printf("failed to connect to server, reason:%s\n", "null taos" /*taos_errstr(taos)*/);
    exit(1);
  }

  /* put your code here for read and write */

  taos_close(taos);
  taos_cleanup();
```

在上面的示例代码中， `taos_connect()` 建立到客户端程序所在主机的 6030 端口的连接，`taos_close()`关闭当前连接，`taos_cleanup()`清除客户端驱动所申请和使用的资源。

##### note

- 如未特别说明，当 API 的返回值是整数时，*0* 代表成功，其它是代表失败原因的错误码，当返回值是指针时， *NULL* 表示失败。
- 所有的错误码以及对应的原因描述在 `taoserror.h` 文件中。

### 示例程序

本节展示了使用客户端驱动访问 TDengine 集群的常见访问方式的示例代码。

#### 同步查询示例

```c++
/*
 * Copyright (c) 2019 TAOS Data, Inc. <jhtao@taosdata.com>
 *
 * This program is free software: you can use, redistribute, and/or modify
 * it under the terms of the GNU Affero General Public License, version 3
 * or later ("AGPL"), as published by the Free Software Foundation.
 *
 * This program is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.
 *
 * You should have received a copy of the GNU Affero General Public License
 * along with this program. If not, see <http://www.gnu.org/licenses/>.
 */

// TAOS standard API example. The same syntax as MySQL, but only a subset
// to compile: gcc -o demo demo.c -ltaos

#include <inttypes.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "taos.h"  // TAOS header file

static void queryDB(TAOS *taos, char *command) {
  int i;
  TAOS_RES *pSql = NULL;
  int32_t   code = -1;

  for (i = 0; i < 5; i++) {
    if (NULL != pSql) {
      taos_free_result(pSql);
      pSql = NULL;
    }
    
    pSql = taos_query(taos, command);
    code = taos_errno(pSql);
    if (0 == code) {
      break;
    }    
  }

  if (code != 0) {
    fprintf(stderr, "Failed to run %s, reason: %s\n", command, taos_errstr(pSql));
    taos_free_result(pSql);
    taos_close(taos);
    exit(EXIT_FAILURE);
  }

  taos_free_result(pSql);
}

void Test(TAOS *taos, char *qstr, int i);

int main(int argc, char *argv[]) {
  char      qstr[1024];

  // connect to server
  if (argc < 2) {
    printf("please input server-ip \n");
    return 0;
  }

  TAOS *taos = taos_connect(argv[1], "root", "taosdata", NULL, 0);
  if (taos == NULL) {
    printf("failed to connect to server, reason:%s\n", "null taos"/*taos_errstr(taos)*/);
    exit(1);
  }
  for (int i = 0; i < 100; i++) {
    Test(taos, qstr, i);
  }
  taos_close(taos);
  taos_cleanup();
}
void Test(TAOS *taos, char *qstr, int index)  {
  printf("==================test at %d\n================================", index);
  queryDB(taos, "drop database if exists demo");
  queryDB(taos, "create database demo");
  TAOS_RES *result;
  queryDB(taos, "use demo");

  queryDB(taos, "create table m1 (ts timestamp, ti tinyint, si smallint, i int, bi bigint, f float, d double, b binary(10))");
  printf("success to create table\n");

  int i = 0;
  for (i = 0; i < 10; ++i) {
    sprintf(qstr, "insert into m1 values (%" PRId64 ", %d, %d, %d, %d, %f, %lf, '%s')", (uint64_t)(1546300800000 + i * 1000), i, i, i, i*10000000, i*1.0, i*2.0, "hello");
    printf("qstr: %s\n", qstr);
    
    // note: how do you wanna do if taos_query returns non-NULL
    // if (taos_query(taos, qstr)) {
    //   printf("insert row: %i, reason:%s\n", i, taos_errstr(taos));
    // }
    TAOS_RES *result1 = taos_query(taos, qstr);
    if (result1 == NULL || taos_errno(result1) != 0) {
      printf("failed to insert row, reason:%s\n", taos_errstr(result1));    
      taos_free_result(result1);
      exit(1);
    } else {
      printf("insert row: %i\n", i);
    }
    taos_free_result(result1);
  }
  printf("success to insert rows, total %d rows\n", i);

  // query the records
  sprintf(qstr, "SELECT * FROM m1");
  result = taos_query(taos, qstr);
  if (result == NULL || taos_errno(result) != 0) {
    printf("failed to select, reason:%s\n", taos_errstr(result));    
    taos_free_result(result);
    exit(1);
  }

  TAOS_ROW    row;
  int         rows = 0;
  int         num_fields = taos_field_count(result);  //这个应该是获取列数
  TAOS_FIELD *fields = taos_fetch_fields(result); //获取每一列的字段

  printf("num_fields = %d\n", num_fields);
  printf("select * from table, result:\n");
  // fetch the records row by row
  while ((row = taos_fetch_row(result))) {
    char temp[1024] = {0};
    rows++;
    taos_print_row(temp, row, fields, num_fields);
    printf("%s\n", temp);
  }

  taos_free_result(result);
  printf("====demo end====\n\n");
}

int taos_print_row(char *str, TAOS_ROW row, TAOS_FIELD *fields, int num_fields) {
  int32_t len = 0;
  for (int i = 0; i < num_fields; ++i) {
    if (i > 0) {
      str[len++] = ' ';
    }

    if (row[i] == NULL) {
      len += sprintf(str + len, "%s", TSDB_DATA_NULL_STR);
      continue;
    }

    switch (fields[i].type) {
      case TSDB_DATA_TYPE_TINYINT:
        len += sprintf(str + len, "%d", *((int8_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_UTINYINT:
        len += sprintf(str + len, "%u", *((uint8_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_SMALLINT:
        len += sprintf(str + len, "%d", *((int16_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_USMALLINT:
        len += sprintf(str + len, "%u", *((uint16_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_INT:
        len += sprintf(str + len, "%d", *((int32_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_UINT:
        len += sprintf(str + len, "%u", *((uint32_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_BIGINT:
        len += sprintf(str + len, "%" PRId64, *((int64_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_UBIGINT:
        len += sprintf(str + len, "%" PRIu64, *((uint64_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_FLOAT: {
        float fv = 0;
        fv = GET_FLOAT_VAL(row[i]);
        len += sprintf(str + len, "%f", fv);
      } break;

      case TSDB_DATA_TYPE_DOUBLE: {
        double dv = 0;
        dv = GET_DOUBLE_VAL(row[i]);
        len += sprintf(str + len, "%lf", dv);
      } break;

      case TSDB_DATA_TYPE_BINARY:
      case TSDB_DATA_TYPE_NCHAR: {
        int32_t charLen = varDataLen((char *)row[i] - VARSTR_HEADER_SIZE);
        if (fields[i].type == TSDB_DATA_TYPE_BINARY) {
          assert(charLen <= fields[i].bytes && charLen >= 0);
        } else {
          assert(charLen <= fields[i].bytes * TSDB_NCHAR_SIZE && charLen >= 0);
        }

        memcpy(str + len, row[i], charLen);
        len += charLen;
      } break;

      case TSDB_DATA_TYPE_TIMESTAMP:
        len += sprintf(str + len, "%" PRId64, *((int64_t *)row[i]));
        break;

      case TSDB_DATA_TYPE_BOOL:
        len += sprintf(str + len, "%d", *((int8_t *)row[i]));
      default:
        break;
    }
  }
  str[len] = 0;

  return len;
}
```

#### 异步查询示例

```c++
/*
 * Copyright (c) 2019 TAOS Data, Inc. <jhtao@taosdata.com>
 *
 * This program is free software: you can use, redistribute, and/or modify
 * it under the terms of the GNU Affero General Public License, version 3
 * or later ("AGPL"), as published by the Free Software Foundation.
 *
 * This program is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.
 *
 * You should have received a copy of the GNU Affero General Public License
 * along with this program. If not, see <http://www.gnu.org/licenses/>.
 */

// TAOS asynchronous API example
// this example opens multiple tables, insert/retrieve multiple tables
// it is used by TAOS internally for one performance testing
// to compiple: gcc -o asyncdemo asyncdemo.c -ltaos

#include <stdio.h>
#include <stdlib.h>
#include <sys/time.h>
#include <unistd.h>
#include <string.h>
#include <inttypes.h>
#include "taos.h"

int     points = 5;
int     numOfTables = 3;
int     tablesInsertProcessed = 0;
int     tablesSelectProcessed = 0;
int64_t st, et;

typedef struct {
  int       id;
  TAOS     *taos;
  char      name[32];
  time_t    timeStamp;
  int       value;
  int       rowsInserted;
  int       rowsTried;
  int       rowsRetrieved;
} STable;

void taos_insert_call_back(void *param, TAOS_RES *tres, int code);
void taos_select_call_back(void *param, TAOS_RES *tres, int code);
void shellPrintError(TAOS *taos);

static void queryDB(TAOS *taos, char *command) {
  int i;
  TAOS_RES *pSql = NULL;
  int32_t   code = -1;

  for (i = 0; i < 5; i++) {
    if (NULL != pSql) {
      taos_free_result(pSql);
      pSql = NULL;
    }
    
    pSql = taos_query(taos, command);
    code = taos_errno(pSql);
    if (0 == code) {
      break;
    }    
  }

  if (code != 0) {
    fprintf(stderr, "Failed to run %s, reason: %s\n", command, taos_errstr(pSql));
    taos_free_result(pSql);
    taos_close(taos);
    taos_cleanup();
    exit(EXIT_FAILURE);
  }

  taos_free_result(pSql);
}

int main(int argc, char *argv[])
{
  TAOS   *taos;
  struct  timeval systemTime;
  int     i;
  char    sql[1024]  = { 0 };
  char    prefix[20] = { 0 };
  char    db[128]    = { 0 };
  STable *tableList; //自定义的结构

  if (argc != 5) {
    printf("usage: %s server-ip dbname rowsPerTable numOfTables\n", argv[0]);
    exit(0);
  }

  // a simple way to parse input parameters
  if (argc >= 3) strncpy(db, argv[2], sizeof(db) - 1);
  if (argc >= 4) points = atoi(argv[3]); //默认值是5
  if (argc >= 5) numOfTables = atoi(argv[4]);  //默认值是3

  size_t size = sizeof(STable) * (size_t)numOfTables;
  tableList = (STable *)malloc(size);
  memset(tableList, 0, size);

  taos = taos_connect(argv[1], "root", "taosdata", NULL, 0);
  if (taos == NULL)
    shellPrintError(taos);  //打印错误消息

  printf("success to connect to server\n");

  sprintf(sql, "drop database if exists %s", db);
  queryDB(taos, sql); //删除数据库

  sprintf(sql, "create database %s", db);
  queryDB(taos, sql); //创建数据库

  sprintf(sql, "use %s", db);
  queryDB(taos, sql); //使用数据库

  strcpy(prefix, "asytbl_");
  /*
    typedef struct {
      int       id;
      TAOS     *taos;
      char      name[32];
      time_t    timeStamp;
      int       value;
      int       rowsInserted;
      int       rowsTried;
      int       rowsRetrieved;
    } STable;
  */
  for (i = 0; i < numOfTables; ++i) {
    tableList[i].id = i;
    tableList[i].taos = taos;  //多个表指向同一个连接
    sprintf(tableList[i].name, "%s%d", prefix, i);
    sprintf(sql, "create table %s%d (ts timestamp, volume bigint)", prefix, i);
    //sprintf(sql, "create table %s (ts timestamp, volume bigint)", tableList[i].name);
    queryDB(taos, sql);
  }  

  gettimeofday(&systemTime, NULL); //两个指针将获取当前时间和时区信息
  for (i = 0; i < numOfTables; ++i)
    tableList[i].timeStamp = (time_t)(systemTime.tv_sec) * 1000 + systemTime.tv_usec / 1000; //这里拿到了一个假的时间创建表的时间

  printf("success to create tables, press any key to insert\n");
  getchar();

  printf("start to insert...\n");
  gettimeofday(&systemTime, NULL);
  st = systemTime.tv_sec * 1000000 + systemTime.tv_usec;

  tablesInsertProcessed = 0;
  tablesSelectProcessed = 0;

  for (i = 0; i<numOfTables; ++i) {
    // insert records in asynchronous API
    sprintf(sql, "insert into %s values(%ld, 0)", tableList[i].name, 1546300800000 + i);
    taos_query_a(taos, sql, taos_insert_call_back, (void *)(tableList + i));
  }

  printf("once insert finished, presse any key to query\n");
  getchar();

  while(1) {
    if (tablesInsertProcessed < numOfTables) {
       printf("wait for process finished\n");
       sleep(1);
       continue;
    }  

    break;
  }

  printf("start to query...\n");
  gettimeofday(&systemTime, NULL);
  st = systemTime.tv_sec * 1000000 + systemTime.tv_usec;


  for (i = 0; i < numOfTables; ++i) {
    // select records in asynchronous API 
    sprintf(sql, "select * from %s", tableList[i].name);
    taos_query_a(taos, sql, taos_select_call_back, (void *)(tableList + i));
  }

  printf("\nonce finished, press any key to exit\n");
  getchar();

  while(1) {
    if (tablesSelectProcessed < numOfTables) {
       printf("wait for process finished\n");
       sleep(1);
       continue;
    }  

    break;
  }

  for (i = 0; i<numOfTables; ++i)  {
    printf("%s inserted:%d retrieved:%d\n", tableList[i].name, tableList[i].rowsInserted, tableList[i].rowsRetrieved);
  }

  taos_close(taos);
  free(tableList);

  printf("==== async demo end====\n");
  printf("\n");
  return 0;
}

void shellPrintError(TAOS *con)
{
  fprintf(stderr, "TDengine error: %s\n", taos_errstr(con));
  taos_close(con);
  taos_cleanup();
  exit(1);
}

void taos_insert_call_back(void *param, TAOS_RES *tres, int code) //这三个参数分别是taos_query_a的最后一个参数、查询结果、错误代码
{
  STable *pTable = (STable *)param;
  struct  timeval systemTime;
  char    sql[128];

  pTable->rowsTried++;

  if (code < 0)  {
    printf("%s insert failed, code:%d, rows:%d\n", pTable->name, code, pTable->rowsTried);
  }
  else if (code == 0) {
    printf("%s not inserted\n", pTable->name);
  }
  else {
    pTable->rowsInserted++;
  }

  if (pTable->rowsTried < points) {
    // for this demo, insert another record
    sprintf(sql, "insert into %s values(%ld, %d)", pTable->name, 1546300800000+pTable->rowsTried*1000, pTable->rowsTried);
    taos_query_a(pTable->taos, sql, taos_insert_call_back, (void *)pTable);  //应该是插入了points行数据
  }
  else {
    printf("%d rows data are inserted into %s\n", points, pTable->name);
    tablesInsertProcessed++;
    if (tablesInsertProcessed >= numOfTables) {
      gettimeofday(&systemTime, NULL);
      et = systemTime.tv_sec * 1000000 + systemTime.tv_usec;
      printf("%" PRId64 " mseconds to insert %d data points\n", (et - st) / 1000, points*numOfTables);
    }
  }
  
  taos_free_result(tres); //释放查询结果
}

void taos_retrieve_call_back(void *param, TAOS_RES *tres, int numOfRows)
{
  STable   *pTable = (STable *)param;
  struct timeval systemTime;

  if (numOfRows > 0) {

    for (int i = 0; i<numOfRows; ++i) {
      // synchronous API to retrieve a row from batch of records
      /*TAOS_ROW row = */(void)taos_fetch_row(tres);
      // process row
    }

    pTable->rowsRetrieved += numOfRows;

    // retrieve next batch of rows
    taos_fetch_rows_a(tres, taos_retrieve_call_back, pTable);

  }
  else {
    if (numOfRows < 0)
      printf("%s retrieve failed, code:%d\n", pTable->name, numOfRows);

    //taos_free_result(tres);
    printf("%d rows data retrieved from %s\n", pTable->rowsRetrieved, pTable->name);

    tablesSelectProcessed++;
    if (tablesSelectProcessed >= numOfTables) {
      gettimeofday(&systemTime, NULL);
      et = systemTime.tv_sec * 1000000 + systemTime.tv_usec;
      printf("%" PRId64 " mseconds to query %d data rows\n", (et - st) / 1000, points * numOfTables);
    }

    taos_free_result(tres);
  }


}

void taos_select_call_back(void *param, TAOS_RES *tres, int code)
{
  STable *pTable = (STable *)param;

  if (code == 0 && tres) {
    // asynchronous API to fetch a batch of records
    taos_fetch_rows_a(tres, taos_retrieve_call_back, pTable);
  }
  else {
    printf("%s select failed, code:%d\n", pTable->name, code);
    taos_free_result(tres);
    taos_cleanup();
    exit(1);
  }
}
```



#### 参数绑定示例

```c++
// TAOS standard API example. The same syntax as MySQL, but only a subet 
// to compile: gcc -o prepare prepare.c -ltaos

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "taos.h"

void taosMsleep(int mseconds);

int main(int argc, char *argv[])
{
  TAOS     *taos;
  TAOS_RES *result;
  int      code;
  TAOS_STMT *stmt;

  // connect to server
  if (argc < 2) {
    printf("please input server ip \n");
    return 0;
  }

  taos = taos_connect(argv[1], "root", "taosdata", NULL, 0);
  if (taos == NULL) {
    printf("failed to connect to db, reason:%s\n", taos_errstr(taos));
    exit(1);
  }   

  result = taos_query(taos, "drop database demo"); 
  taos_free_result(result);

  result = taos_query(taos, "create database demo");
  code = taos_errno(result);
  if (code != 0) {
    printf("failed to create database, reason:%s\n", taos_errstr(result));
    taos_free_result(result);
    exit(1);
  }
  taos_free_result(result);

  result = taos_query(taos, "use demo");
  taos_free_result(result);

  // create table
  const char* sql = "create table m1 (ts timestamp, b bool, v1 tinyint, v2 smallint, v4 int, v8 bigint, f4 float, f8 double, bin binary(40), blob nchar(10))";
  result = taos_query(taos, sql);
  code = taos_errno(result);
  if (code != 0) {
    printf("failed to create table, reason:%s\n", taos_errstr(result));
    taos_free_result(result);
    exit(1);
  }
  taos_free_result(result);

  // sleep for one second to make sure table is created on data node
  // taosMsleep(1000);

  // insert 10 records
  struct {
      int64_t ts;
      int8_t b;
      int8_t v1;
      int16_t v2;
      int32_t v4;
      int64_t v8;
      float f4;
      double f8;
      char bin[40];
      char blob[80];
  } v = {0};

  int32_t boolLen = sizeof(int8_t);
  int32_t sintLen = sizeof(int16_t);
  int32_t intLen = sizeof(int32_t);
  int32_t bintLen = sizeof(int64_t);
  int32_t floatLen = sizeof(float);
  int32_t doubleLen = sizeof(double);
  int32_t binLen = sizeof(v.bin);
  int32_t ncharLen = 30;

  stmt = taos_stmt_init(taos);
  TAOS_MULTI_BIND params[10];
  params[0].buffer_type = TSDB_DATA_TYPE_TIMESTAMP;
  params[0].buffer_length = sizeof(v.ts);
  params[0].buffer = &v.ts;
  params[0].length = &bintLen;
  params[0].is_null = NULL;
  params[0].num = 1;

  params[1].buffer_type = TSDB_DATA_TYPE_BOOL;
  params[1].buffer_length = sizeof(v.b);
  params[1].buffer = &v.b;
  params[1].length = &boolLen;
  params[1].is_null = NULL;
  params[1].num = 1;

  params[2].buffer_type = TSDB_DATA_TYPE_TINYINT;
  params[2].buffer_length = sizeof(v.v1);
  params[2].buffer = &v.v1;
  params[2].length = &boolLen;
  params[2].is_null = NULL;
  params[2].num = 1;

  params[3].buffer_type = TSDB_DATA_TYPE_SMALLINT;
  params[3].buffer_length = sizeof(v.v2);
  params[3].buffer = &v.v2;
  params[3].length = &sintLen;
  params[3].is_null = NULL;
  params[3].num = 1;

  params[4].buffer_type = TSDB_DATA_TYPE_INT;
  params[4].buffer_length = sizeof(v.v4);
  params[4].buffer = &v.v4;
  params[4].length = &intLen;
  params[4].is_null = NULL;
  params[4].num = 1;

  params[5].buffer_type = TSDB_DATA_TYPE_BIGINT;
  params[5].buffer_length = sizeof(v.v8);
  params[5].buffer = &v.v8;
  params[5].length = &bintLen;
  params[5].is_null = NULL;
  params[5].num = 1;

  params[6].buffer_type = TSDB_DATA_TYPE_FLOAT;
  params[6].buffer_length = sizeof(v.f4);
  params[6].buffer = &v.f4;
  params[6].length = &floatLen;
  params[6].is_null = NULL;
  params[6].num = 1;

  params[7].buffer_type = TSDB_DATA_TYPE_DOUBLE;
  params[7].buffer_length = sizeof(v.f8);
  params[7].buffer = &v.f8;
  params[7].length = &doubleLen;
  params[7].is_null = NULL;
  params[7].num = 1;

  params[8].buffer_type = TSDB_DATA_TYPE_BINARY;
  params[8].buffer_length = sizeof(v.bin);
  params[8].buffer = v.bin;
  params[8].length = &binLen;
  params[8].is_null = NULL;
  params[8].num = 1;

  strcpy(v.blob, "一二三四五六七八九十");
  params[9].buffer_type = TSDB_DATA_TYPE_NCHAR;
  params[9].buffer_length = sizeof(v.blob);
  params[9].buffer = v.blob;
  params[9].length = &ncharLen;
  params[9].is_null = NULL;
  params[9].num = 1;

  char is_null = 1;

  sql = "insert into m1 values(?,?,?,?,?,?,?,?,?,?)";
  code = taos_stmt_prepare(stmt, sql, 0); //填充sql
  if (code != 0){
    printf("failed to execute taos_stmt_prepare. code:0x%x\n", code);
  }
  v.ts = 1591060628000;
  for (int i = 0; i < 10; ++i) {
    v.ts += 1;
    for (int j = 1; j < 10; ++j) {
      params[j].is_null = ((i == j) ? &is_null : 0);
    }
    v.b = (int8_t)i % 2;
    v.v1 = (int8_t)i;
    v.v2 = (int16_t)(i * 2);
    v.v4 = (int32_t)(i * 4);
    v.v8 = (int64_t)(i * 8);
    v.f4 = (float)(i * 40);
    v.f8 = (double)(i * 80);
    for (int j = 0; j < sizeof(v.bin); ++j) {
      v.bin[j] = (char)(i + '0');
    }

    taos_stmt_bind_param(stmt, params); //绑定多个参数
    taos_stmt_add_batch(stmt); // 加入到batch中
  }
  if (taos_stmt_execute(stmt) != 0) { //执行
    printf("failed to execute insert statement.\n");
    exit(1);
  }
  taos_stmt_close(stmt);

  // query the records
  stmt = taos_stmt_init(taos); // 唉 每次都都得释放掉
  taos_stmt_prepare(stmt, "SELECT * FROM m1 WHERE v1 > ? AND v2 < ?", 0); //这里给个0干什么
  v.v1 = 5;
  v.v2 = 15;
  taos_stmt_bind_param(stmt, params + 2);
  if (taos_stmt_execute(stmt) != 0) {
    printf("failed to execute select statement.\n");
    exit(1);
  }

  result = taos_stmt_use_result(stmt);

  TAOS_ROW    row;
  int         rows = 0;
  int         num_fields = taos_num_fields(result);
  TAOS_FIELD *fields = taos_fetch_fields(result);

  // fetch the records row by row
  while ((row = taos_fetch_row(result))) {
    char temp[256] = {0};
    rows++;
    taos_print_row(temp, row, fields, num_fields);
    printf("%s\n", temp);
  }
  if (rows == 2) {
    printf("two rows are fetched as expectation\n");
  } else {
    printf("expect two rows, but %d rows are fetched\n", rows);
  }

  taos_free_result(result);
  taos_stmt_close(stmt);

  return 0;
}
```

#### 无模式写入示例

```c++
#include "taos.h"
#include <stdio.h>
#include <stdlib.h>
#include <sys/time.h>
#include <time.h>
#include <unistd.h>
#include <inttypes.h>
#include <string.h>


int numSuperTables = 8;
int numChildTables = 4;
int numRowsPerChildTable = 2048;

static int64_t getTimeInUs() {
  struct timeval systemTime;
  gettimeofday(&systemTime, NULL);
  return (int64_t)systemTime.tv_sec * 1000000L + (int64_t)systemTime.tv_usec;
}

int main(int argc, char* argv[]) {
  TAOS_RES *result;
  const char* host = "127.0.0.1";
  const char* user = "root";
  const char* passwd = "taosdata";

  taos_options(TSDB_OPTION_TIMEZONE, "GMT-8");
  TAOS* taos = taos_connect(host, user, passwd, "", 0);
  if (taos == NULL) {
    printf("\033[31mfailed to connect to db, reason:%s\033[0m\n", taos_errstr(taos));
    exit(1);
  }

  const char* info = taos_get_server_info(taos);
  printf("server info: %s\n", info);
  info = taos_get_client_info(taos);
  printf("client info: %s\n", info);
  result = taos_query(taos, "drop database if exists db;");
  taos_free_result(result);
  usleep(100000);
  result = taos_query(taos, "create database db precision 'ms';");
  taos_free_result(result);
  usleep(100000);

  (void)taos_select_db(taos, "db");

  time_t ct = time(0);
  int64_t ts = ct * 1000;
  char* lineFormat = "sta%d,t0=true,t1=127i8,t2=32767i16,t3=%di32,t4=9223372036854775807i64,t9=11.12345f32,t10=22.123456789f64,t11=\"binaryTagValue\",t12=L\"ncharTagValue\" c0=true,c1=127i8,c2=32767i16,c3=2147483647i32,c4=9223372036854775807i64,c5=254u8,c6=32770u16,c7=2147483699u32,c8=9223372036854775899u64,c9=11.12345f32,c10=22.123456789f64,c11=\"binaryValue\",c12=L\"ncharValue\" %" PRId64;

  int lineNum = numSuperTables * numChildTables * numRowsPerChildTable;
  char** lines = calloc((size_t)lineNum, sizeof(char*));
  int l = 0;
  for (int i = 0; i < numSuperTables; ++i) {
    for (int j = 0; j < numChildTables; ++j) {
      for (int k = 0; k < numRowsPerChildTable; ++k) {
        char* line = calloc(512, 1);
        snprintf(line, 512, lineFormat, i, j, ts + 10 * l);
        lines[l] = line;
        ++l;
      }
    }
  }

  printf("%s\n", "begin taos_insert_lines");
  int64_t  begin = getTimeInUs();
  TAOS_RES *res = taos_schemaless_insert(taos, lines, lineNum, TSDB_SML_LINE_PROTOCOL, TSDB_SML_TIMESTAMP_MILLI_SECONDS);
  int64_t end = getTimeInUs();
  printf("code: %s. time used: %" PRId64 "\n", taos_errstr(res), end-begin);
  taos_free_result(res);

  return 0;
}
```



#### 订阅和消费示例

```c++
/*
 * Copyright (c) 2019 TAOS Data, Inc. <jhtao@taosdata.com>
 *
 * This program is free software: you can use, redistribute, and/or modify
 * it under the terms of the GNU Affero General Public License, version 3
 * or later ("AGPL"), as published by the Free Software Foundation.
 *
 * This program is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.
 *
 * You should have received a copy of the GNU Affero General Public License
 * along with this program. If not, see <http://www.gnu.org/licenses/>.
 */

#include <assert.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include "taos.h"

static int  running = 1;
const char* topic_name = "topicname";

static int32_t msg_process(TAOS_RES* msg) {
  char    buf[1024];
  int32_t rows = 0;

  const char* topicName = tmq_get_topic_name(msg);
  const char* dbName = tmq_get_db_name(msg);
  int32_t     vgroupId = tmq_get_vgroup_id(msg);

  printf("topic: %s\n", topicName);
  printf("db: %s\n", dbName);
  printf("vgroup id: %d\n", vgroupId);

  while (1) {
    TAOS_ROW row = taos_fetch_row(msg);
    if (row == NULL) break;

    TAOS_FIELD* fields = taos_fetch_fields(msg);
    int32_t     numOfFields = taos_field_count(msg);
    // int32_t*    length = taos_fetch_lengths(msg);
    int32_t precision = taos_result_precision(msg);
    rows++;
    taos_print_row(buf, row, fields, numOfFields);
    printf("precision: %d, row content: %s\n", precision, buf);
  }

  return rows;
}

static int32_t init_env() {
  TAOS* pConn = taos_connect("localhost", "root", "taosdata", NULL, 0);
  if (pConn == NULL) {
    return -1;
  }

  TAOS_RES* pRes;
  // drop database if exists
  printf("create database\n");
  pRes = taos_query(pConn, "drop topic topicname");
  if (taos_errno(pRes) != 0) {
    printf("error in drop topicname, reason:%s\n", taos_errstr(pRes));
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "drop database if exists tmqdb");
  if (taos_errno(pRes) != 0) {
    printf("error in drop tmqdb, reason:%s\n", taos_errstr(pRes));
  }
  taos_free_result(pRes);

  // create database
  pRes = taos_query(pConn, "create database tmqdb precision 'ns'");
  if (taos_errno(pRes) != 0) {
    printf("error in create tmqdb, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  // create super table
  printf("create super table\n");
  pRes = taos_query(
      pConn, "create table tmqdb.stb (ts timestamp, c1 int, c2 float, c3 varchar(16)) tags(t1 int, t3 varchar(16))");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table stb, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  // create sub tables
  printf("create sub tables\n");
  pRes = taos_query(pConn, "create table tmqdb.ctb0 using tmqdb.stb tags(0, 'subtable0')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb0, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create table tmqdb.ctb1 using tmqdb.stb tags(1, 'subtable1')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb1, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create table tmqdb.ctb2 using tmqdb.stb tags(2, 'subtable2')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb2, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create table tmqdb.ctb3 using tmqdb.stb tags(3, 'subtable3')");
  if (taos_errno(pRes) != 0) {
    printf("failed to create super table ctb3, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  // insert data
  printf("insert data into sub tables\n");
  pRes = taos_query(pConn, "insert into tmqdb.ctb0 values(now, 0, 0, 'a0')(now+1s, 0, 0, 'a00')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "insert into tmqdb.ctb1 values(now, 1, 1, 'a1')(now+1s, 11, 11, 'a11')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "insert into tmqdb.ctb2 values(now, 2, 2, 'a1')(now+1s, 22, 22, 'a22')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "insert into tmqdb.ctb3 values(now, 3, 3, 'a1')(now+1s, 33, 33, 'a33')");
  if (taos_errno(pRes) != 0) {
    printf("failed to insert into ctb0, reason:%s\n", taos_errstr(pRes));
    goto END;
  }
  taos_free_result(pRes);
  taos_close(pConn);
  return 0;

END:
  taos_free_result(pRes);
  taos_close(pConn);
  return -1;
}

int32_t create_topic() {
  printf("create topic\n");
  TAOS_RES* pRes;
  TAOS*     pConn = taos_connect("localhost", "root", "taosdata", NULL, 0);
  if (pConn == NULL) {
    return -1;
  }

  pRes = taos_query(pConn, "use tmqdb");
  if (taos_errno(pRes) != 0) {
    printf("error in use tmqdb, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  pRes = taos_query(pConn, "create topic topicname as select ts, c1, c2, c3, tbname from tmqdb.stb where c1 > 1");
  if (taos_errno(pRes) != 0) {
    printf("failed to create topic topicname, reason:%s\n", taos_errstr(pRes));
    return -1;
  }
  taos_free_result(pRes);

  taos_close(pConn);
  return 0;
}

void tmq_commit_cb_print(tmq_t* tmq, int32_t code, void* param) {
  printf("tmq_commit_cb_print() code: %d, tmq: %p, param: %p\n", code, tmq, param);
}

tmq_t* build_consumer() {
  tmq_conf_res_t code;
  tmq_t*         tmq = NULL;

  tmq_conf_t* conf = tmq_conf_new();
  code = tmq_conf_set(conf, "enable.auto.commit", "true");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }
  code = tmq_conf_set(conf, "auto.commit.interval.ms", "1000");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }
  code = tmq_conf_set(conf, "group.id", "cgrpName");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }
  code = tmq_conf_set(conf, "client.id", "user defined name");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }
  code = tmq_conf_set(conf, "td.connect.user", "root");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }
  code = tmq_conf_set(conf, "td.connect.pass", "taosdata");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }
  code = tmq_conf_set(conf, "auto.offset.reset", "earliest");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }
  code = tmq_conf_set(conf, "experimental.snapshot.enable", "false");
  if (TMQ_CONF_OK != code) {
    tmq_conf_destroy(conf);
    return NULL;
  }

  tmq_conf_set_auto_commit_cb(conf, tmq_commit_cb_print, NULL);
  tmq = tmq_consumer_new(conf, NULL, 0);

_end:
  tmq_conf_destroy(conf);
  return tmq;
}

tmq_list_t* build_topic_list() {
  tmq_list_t* topicList = tmq_list_new();
  int32_t     code = tmq_list_append(topicList, topic_name);
  if (code) {
    tmq_list_destroy(topicList);
    return NULL;
  }
  return topicList;
}

void basic_consume_loop(tmq_t* tmq) {
  int32_t totalRows = 0;
  int32_t msgCnt = 0;
  int32_t timeout = 5000;
  while (running) {
    TAOS_RES* tmqmsg = tmq_consumer_poll(tmq, timeout);
    if (tmqmsg) {
      msgCnt++;
      totalRows += msg_process(tmqmsg);
      taos_free_result(tmqmsg);
    } else {
      break;
    }
  }

  fprintf(stderr, "%d msg consumed, include %d rows\n", msgCnt, totalRows);
}

void consume_repeatly(tmq_t* tmq) {
  int32_t               numOfAssignment = 0;
  tmq_topic_assignment* pAssign = NULL;

  int32_t code = tmq_get_topic_assignment(tmq, topic_name, &pAssign, &numOfAssignment);
  if (code != 0) {
    fprintf(stderr, "failed to get assignment, reason:%s", tmq_err2str(code));
  }

  // seek to the earliest offset
  for(int32_t i = 0; i < numOfAssignment; ++i) {
    tmq_topic_assignment* p = &pAssign[i];

    code = tmq_offset_seek(tmq, topic_name, p->vgId, p->begin);
    if (code != 0) {
      fprintf(stderr, "failed to seek to %ld, reason:%s", p->begin, tmq_err2str(code));
    }
  }

  free(pAssign);

  // let's do it again
  basic_consume_loop(tmq);
}

int main(int argc, char* argv[]) {
  int32_t code;

  if (init_env() < 0) {
    return -1;
  }

  if (create_topic() < 0) {
    return -1;
  }

  tmq_t* tmq = build_consumer();
  if (NULL == tmq) {
    fprintf(stderr, "build_consumer() fail!\n");
    return -1;
  }

  tmq_list_t* topic_list = build_topic_list();
  if (NULL == topic_list) {
    return -1;
  }

  if ((code = tmq_subscribe(tmq, topic_list))) {
    fprintf(stderr, "Failed to tmq_subscribe(): %s\n", tmq_err2str(code));
  }

  tmq_list_destroy(topic_list);

  basic_consume_loop(tmq);

  consume_repeatly(tmq);

  code = tmq_consumer_close(tmq);
  if (code) {
    fprintf(stderr, "Failed to close consumer: %s\n", tmq_err2str(code));
  } else {
    fprintf(stderr, "Consumer closed\n");
  }

  return 0;
}
```



##### info

更多示例代码及下载请见 [GitHub](https://github.com/taosdata/TDengine/tree/develop/examples/c)。 也可以在安装目录下的 `examples/c` 路径下找到。 该目录下有 makefile，在 Linux/macOS 环境下，直接执行 make 就可以编译得到执行文件。 **提示：**在 ARM 环境下编译时，请将 makefile 中的 `-msse4.2` 去掉，这个选项只有在 x64/x86 硬件平台上才能支持。

### API 参考

以下分别介绍 TDengine 客户端驱动的基础 API、同步 API、异步 API、订阅 API 和无模式写入 API。

#### 基础 API

基础 API 用于完成创建数据库连接等工作，为其它 API 的执行提供运行时环境。

- `void taos_init()`

  初始化运行环境。如果没有主动调用该 API，那么调用 `taos_connect()` 时驱动将自动调用该 API，故程序一般无需手动调用。

- `void taos_cleanup()`

  清理运行环境，应用退出前应调用。

- `int taos_options(TSDB_OPTION option, const void * arg, ...)`

  设置客户端选项，目前支持区域设置（`TSDB_OPTION_LOCALE`）、字符集设置（`TSDB_OPTION_CHARSET`）、时区设置（`TSDB_OPTION_TIMEZONE`）、配置文件路径设置（`TSDB_OPTION_CONFIGDIR`）。区域设置、字符集、时区默认为操作系统当前设置。

- `char *taos_get_client_info()`

  获取客户端版本信息。

- `TAOS *taos_connect(const char *host, const char *user, const char *pass, const char *db, int port)`

  创建数据库连接，初始化连接上下文。其中需要用户提供的参数包含：

  - host：TDengine 集群中任一节点的 FQDN
  - user：用户名
  - pass：密码
  - db：  数据库名字，如果用户没有提供，也可以正常连接，用户可以通过该连接创建新的数据库，如果用户提供了数据库名字，则说明该数据库用户已经创建好，缺省使用该数据库
  - port：taosd 程序监听的端口

  返回值为空表示失败。应用程序需要保存返回的参数，以便后续使用。

  ##### 

- ##### info

  同一进程可以根据不同的 host/port 连接多个 TDengine 集群

- `char *taos_get_server_info(TAOS *taos)`

  获取服务端版本信息。

- `int taos_select_db(TAOS *taos, const char *db)`

  将当前的缺省数据库设置为 `db`。

- `int taos_get_current_db(TAOS *taos, char *database, int len, int *required)`

  - database，len为用户在外面申请的空间，内部会把当前db赋值到database里。
  - 只要是没有正常把db名赋值到database中（包括截断），返回错误，返回值为-1，然后用户可以通过  taos_errstr(NULL) 来获取错误提示。
  - 如果，database == NULL 或者 len<=0 返回错误，required里保存存储db需要的空间（包含最后的'\0'）
  - 如果，len 小于 存储db需要的空间（包含最后的'\0'），返回错误，database里赋值截断的数据，以'\0'结尾。
  - 如果，len 大于等于 存储db需要的空间（包含最后的'\0'），返回正常0，database里赋值以'\0‘结尾的db名。

- `void taos_close(TAOS *taos)`

  关闭连接，其中`taos`是 `taos_connect()` 返回的句柄。

#### 同步查询 API

本小节介绍 API 均属于同步接口。应用调用后，会阻塞等待响应，直到获得返回结果或错误信息。

- `TAOS_RES* taos_query(TAOS *taos, const char *sql)`

  执行 SQL 语句，可以是 DQL、DML 或 DDL 语句。 其中的 `taos` 参数是通过 `taos_connect()` 获得的句柄。不能通过返回值是否是 `NULL` 来判断执行结果是否失败，而是需要用 `taos_errno()` 函数解析结果集中的错误代码来进行判断。

- `int taos_result_precision(TAOS_RES *res)`

  返回结果集时间戳字段的精度，`0` 代表毫秒，`1` 代表微秒，`2` 代表纳秒。

- `TAOS_ROW taos_fetch_row(TAOS_RES *res)`

  按行获取查询结果集中的数据。

- `int taos_fetch_block(TAOS_RES *res, TAOS_ROW *rows)`

  批量获取查询结果集中的数据，返回值为获取到的数据的行数。

- `int taos_num_fields(TAOS_RES *res)` 和 `int taos_field_count(TAOS_RES *res)`

  这两个 API 等价，用于获取查询结果集中的列数。

- `int* taos_fetch_lengths(TAOS_RES *res)`

  获取结果集中每个字段的长度。返回值是一个数组，其长度为结果集的列数。

- `int taos_affected_rows(TAOS_RES *res)`

  获取被所执行的 SQL 语句影响的行数。

- `TAOS_FIELD *taos_fetch_fields(TAOS_RES *res)`

  获取查询结果集每列数据的属性（列的名称、列的数据类型、列的长度），与 `taos_num_fields()` 配合使用，可用来解析 `taos_fetch_row()` 返回的一个元组(一行)的数据。 `TAOS_FIELD` 的结构如下：

```c
typedef struct taosField {
  char     name[65];  // column name
  uint8_t  type;      // data type
  int16_t  bytes;     // length, in bytes
} TAOS_FIELD;
```

- `void taos_stop_query(TAOS_RES *res)`

  停止当前查询的执行。

- `void taos_free_result(TAOS_RES *res)`

  释放查询结果集以及相关的资源。查询完成后，务必调用该 API 释放资源，否则可能导致应用内存泄露。但也需注意，释放资源后，如果再调用 `taos_consume()` 等获取查询结果的函数，将导致应用崩溃。

- `char *taos_errstr(TAOS_RES *res)`

  获取最近一次 API 调用失败的原因,返回值为字符串标识的错误提示信息。

- `int taos_errno(TAOS_RES *res)`

  获取最近一次 API 调用失败的原因，返回值为错误代码。

##### 

##### note

2.0 及以上版本 TDengine 推荐数据库应用的每个线程都建立一个独立的连接，或基于线程建立连接池。而不推荐在应用中将该连接 (TAOS*) 结构体传递到不同的线程共享使用。基于 TAOS 结构体发出的查询、写入等操作具有多线程安全性，但 “USE statement”  等状态量有可能在线程之间相互干扰。此外，C  语言的连接器可以按照需求动态建立面向数据库的新连接（该过程对用户不可见），同时建议只有在程序最后退出的时候才调用 `taos_close()` 关闭连接。 另一个需要注意的是，在上述同步 API 执行过程中，不能调用类似 pthread_cancel 之类的 API 来强制结束线程，因为涉及一些模块的同步操作，如果强制结束线程有可能造成包括但不限于死锁等异常状况。

#### 异步查询 API

TDengine 还提供性能更高的异步 API 处理数据插入、查询操作。在软硬件环境相同的情况下，异步 API 处理数据插入的速度比同步 API 快 2 ～ 4 倍。异步 API  采用非阻塞式的调用方式，在系统真正完成某个具体数据库操作前，立即返回。调用的线程可以去处理其他工作，从而可以提升整个应用的性能。异步 API  在网络延迟严重的情况下，优势尤为突出。

异步 API  都需要应用提供相应的回调函数，回调函数参数设置如下：前两个参数都是一致的，第三个参数依不同的 API 而定。第一个参数 param  是应用调用异步 API 时提供给系统的，用于回调时，应用能够找回具体操作的上下文，依具体实现而定。第二个参数是 SQL  操作的结果集，如果为空，比如 insert 操作，表示没有记录返回，如果不为空，比如 select 操作，表示有记录返回。

异步 API 对于使用者的要求相对较高，用户可根据具体应用场景选择性使用。下面是两个重要的异步 API：

- `void taos_query_a(TAOS *taos, const char *sql, void (*fp)(void *param, TAOS_RES *, int code), void *param);`

  异步执行 SQL 语句。

  - taos：调用 `taos_connect()` 返回的数据库连接
  - sql：需要执行的 SQL 语句
  - fp：用户定义的回调函数，其第三个参数 `code` 用于指示操作是否成功，`0` 表示成功，负数表示失败（调用 `taos_errstr()` 可获取失败原因）。应用在定义回调函数的时候，主要处理第二个参数 `TAOS_RES *`，该参数是查询返回的结果集
  - param：应用提供一个用于回调的参数

- `void taos_fetch_rows_a(TAOS_RES *res, void (*fp)(void *param, TAOS_RES *, int numOfRows), void *param);`

  批量获取异步查询的结果集，只能与 `taos_query_a()` 配合使用。其中：

  - res：`taos_query_a()` 回调时返回的结果集
  - fp：回调函数。其参数 `param` 是用户可定义的传递给回调函数的参数结构体；`numOfRows` 是获取到的数据的行数（不是整个查询结果集的函数）。 在回调函数中，应用可以通过调用 `taos_fetch_row()` 前向迭代获取批量记录中每一行记录。读完一块内的所有记录后，应用需要在回调函数中继续调用 `taos_fetch_rows_a()` 获取下一批记录进行处理，直到返回的记录数 `numOfRows` 为零（结果返回完成）或记录数为负值（查询出错）。

TDengine 的异步 API 均采用非阻塞调用模式。应用程序可以用多线程同时打开多张表，并可以同时对每张打开的表进行查询或者插入操作。需要指出的是，**客户端应用必须确保对同一张表的操作完全串行化**，即对同一个表的插入或查询操作未完成时（未返回时），不能够执行第二个插入或查询操作。

#### 参数绑定 API

除了直接调用 `taos_query()` 进行查询，TDengine 也提供了支持参数绑定的 Prepare API，风格与 MySQL 类似，目前也仅支持用问号 `?` 来代表待绑定的参数。

从 2.1.1.0 和 2.1.2.0 版本开始，TDengine  大幅改进了参数绑定接口对数据写入（INSERT）场景的支持。这样在通过参数绑定接口写入数据时，就避免了 SQL  语法解析的资源消耗，从而在绝大多数情况下显著提升写入性能。此时的典型操作步骤如下：

1. 调用 `taos_stmt_init()` 创建参数绑定对象；
2. 调用 `taos_stmt_prepare()` 解析 INSERT 语句；
3. 如果 INSERT 语句中预留了表名但没有预留 TAGS，那么调用 `taos_stmt_set_tbname()` 来设置表名；
4. 如果 INSERT 语句中既预留了表名又预留了 TAGS（例如 INSERT 语句采取的是自动建表的方式），那么调用 `taos_stmt_set_tbname_tags()` 来设置表名和 TAGS 的值；
5. 调用 `taos_stmt_bind_param_batch()` 以多行的方式设置 VALUES 的值，或者调用 `taos_stmt_bind_param()` 以单行的方式设置 VALUES 的值；
6. 调用 `taos_stmt_add_batch()` 把当前绑定的参数加入批处理；
7. 可以重复第 3 ～ 6 步，为批处理加入更多的数据行；
8. 调用 `taos_stmt_execute()` 执行已经准备好的批处理指令；
9. 执行完毕，调用 `taos_stmt_close()` 释放所有资源。

说明：如果 `taos_stmt_execute()` 执行成功，假如不需要改变 SQL 语句的话，那么是可以复用 `taos_stmt_prepare()` 的解析结果，直接进行第 3 ～ 6 步绑定新数据的。但如果执行出错，那么并不建议继续在当前的环境上下文下继续工作，而是建议释放资源，然后从 `taos_stmt_init()` 步骤重新开始。

接口相关的具体函数如下（也可以参考 [prepare.c](https://github.com/taosdata/TDengine/blob/develop/examples/c/prepare.c) 文件中使用对应函数的方式）：

- `TAOS_STMT* taos_stmt_init(TAOS *taos)`

  创建一个 TAOS_STMT 对象用于后续调用。

- `int taos_stmt_prepare(TAOS_STMT *stmt, const char *sql, unsigned long length)`

  解析一条 SQL 语句，将解析结果和参数信息绑定到 stmt 上，如果参数 length 大于 0，将使用此参数作为 SQL 语句的长度，如等于 0，将自动判断 SQL 语句的长度。

- `int taos_stmt_bind_param(TAOS_STMT *stmt, TAOS_BIND *bind)`

  不如 `taos_stmt_bind_param_batch()` 效率高，但可以支持非 INSERT 类型的 SQL 语句。 进行参数绑定，bind 指向一个数组（代表所要绑定的一行数据），需保证此数组中的元素数量和顺序与 SQL 语句中的参数完全一致。TAOS_BIND 的使用方法与 MySQL 中的 MYSQL_BIND 类似，具体定义如下：

  ```c
  typedef struct TAOS_BIND {
    int            buffer_type;
    void *         buffer;
    uintptr_t      buffer_length;  // not in use
    uintptr_t *    length;
    int *          is_null;
    int            is_unsigned;    // not in use
    int *          error;          // not in use
  } TAOS_BIND;
  ```

```
int taos_stmt_set_tbname(TAOS_STMT* stmt, const char* name)
```

（2.1.1.0 版本新增，仅支持用于替换 INSERT 语句中的参数值） 当 SQL 语句中的表名使用了 `?` 占位时，可以使用此函数绑定一个具体的表名。

```
int taos_stmt_set_tbname_tags(TAOS_STMT* stmt, const char* name, TAOS_BIND* tags)
```

（2.1.2.0 版本新增，仅支持用于替换 INSERT 语句中的参数值） 当 SQL 语句中的表名和 TAGS 都使用了 `?` 占位时，可以使用此函数绑定具体的表名和具体的 TAGS 取值。最典型的使用场景是使用了自动建表功能的 INSERT 语句（目前版本不支持指定具体的 TAGS 列）。TAGS 参数中的列数量需要与 SQL 语句中要求的 TAGS 数量完全一致。

```
int taos_stmt_bind_param_batch(TAOS_STMT* stmt, TAOS_MULTI_BIND* bind)
```

（2.1.1.0 版本新增，仅支持用于替换 INSERT 语句中的参数值） 以多列的方式传递待绑定的数据，需要保证这里传递的数据列的顺序、列的数量与 SQL 语句中的 VALUES 参数完全一致。TAOS_MULTI_BIND 的具体定义如下：

```c
typedef struct TAOS_MULTI_BIND {
  int          buffer_type;
  void *       buffer;
  uintptr_t    buffer_length;
  uintptr_t *  length;
  char *       is_null;
  int          num;             // the number of columns
} TAOS_MULTI_BIND;
```

- `int taos_stmt_add_batch(TAOS_STMT *stmt)`

  将当前绑定的参数加入批处理中，调用此函数后，可以再次调用 `taos_stmt_bind_param()` 或 `taos_stmt_bind_param_batch()` 绑定新的参数。需要注意，此函数仅支持 INSERT/IMPORT 语句，如果是 SELECT 等其他 SQL 语句，将返回错误。

- `int taos_stmt_execute(TAOS_STMT *stmt)`

  执行准备好的语句。目前，一条语句只能执行一次。

- `TAOS_RES* taos_stmt_use_result(TAOS_STMT *stmt)`

  获取语句的结果集。结果集的使用方式与非参数化调用时一致，使用完成后，应对此结果集调用 `taos_free_result()` 以释放资源。

- `int taos_stmt_close(TAOS_STMT *stmt)`

  执行完毕，释放所有资源。

- `char * taos_stmt_errstr(TAOS_STMT *stmt)`

  （2.1.3.0 版本新增） 用于在其他 STMT API 返回错误（返回错误码或空指针）时获取错误信息。

#### 无模式（schemaless）写入 API

除了使用 SQL 方式或者使用参数绑定 API 写入数据外，还可以使用 Schemaless 的方式完成写入。Schemaless  可以免于预先创建超级表/数据子表的数据结构，而是可以直接写入数据，TDengine  系统会根据写入的数据内容自动创建和维护所需要的表结构。Schemaless 的使用方式详见 [Schemaless 写入](https://docs.taosdata.com/reference/schemaless/) 章节，这里介绍与之配套使用的 C/C++ API。

- `TAOS_RES* taos_schemaless_insert(TAOS* taos, const char* lines[], int numLines, int protocol, int precision)`

  **功能说明** 该接口将行协议的文本数据写入到 TDengine 中。

  **参数说明** taos: 数据库连接，通过 `taos_connect()` 函数建立的数据库连接。 lines：文本数据。满足解析格式要求的无模式文本字符串。 numLines:文本数据的行数，不能为 0 。 protocol: 行协议类型，用于标识文本数据格式。 precision：文本数据中的时间戳精度字符串。

  **返回值** TAOS_RES 结构体，应用可以通过使用 `taos_errstr()` 获得错误信息，也可以使用 `taos_errno()` 获得错误码。 在某些情况下，返回的 TAOS_RES 为 `NULL`，此时仍然可以调用 `taos_errno()` 来安全地获得错误码信息。 返回的 TAOS_RES 需要调用方来负责释放，否则会出现内存泄漏。

  **说明** 协议类型是枚举类型，包含以下三种格式：

  - TSDB_SML_LINE_PROTOCOL：InfluxDB 行协议（Line Protocol)
  - TSDB_SML_TELNET_PROTOCOL: OpenTSDB Telnet 文本行协议
  - TSDB_SML_JSON_PROTOCOL: OpenTSDB Json 协议格式

  时间戳分辨率的定义，定义在 `taos.h` 文件中，具体内容如下：

  - TSDB_SML_TIMESTAMP_NOT_CONFIGURED = 0,
  - TSDB_SML_TIMESTAMP_HOURS,
  - TSDB_SML_TIMESTAMP_MINUTES,
  - TSDB_SML_TIMESTAMP_SECONDS,
  - TSDB_SML_TIMESTAMP_MILLI_SECONDS,
  - TSDB_SML_TIMESTAMP_MICRO_SECONDS,
  - TSDB_SML_TIMESTAMP_NANO_SECONDS

  需要注意的是，时间戳分辨率参数只在协议类型为 `SML_LINE_PROTOCOL` 的时候生效。 对于 OpenTSDB 的文本协议，时间戳的解析遵循其官方解析规则 — 按照时间戳包含的字符的数量来确认时间精度。

  **schemaless 其他相关的接口**

- `TAOS_RES *taos_schemaless_insert_with_reqid(TAOS *taos, char *lines[], int numLines, int protocol, int precision, int64_t reqid)`

- `TAOS_RES *taos_schemaless_insert_raw(TAOS *taos, char *lines, int len, int32_t *totalRows, int protocol, int precision)`

- `TAOS_RES *taos_schemaless_insert_raw_with_reqid(TAOS *taos, char *lines, int  len, int32_t *totalRows, int protocol, int precision, int64_t reqid)`

- `TAOS_RES *taos_schemaless_insert_ttl(TAOS *taos, char *lines[], int numLines, int protocol, int precision, int32_t ttl)`

- `TAOS_RES *taos_schemaless_insert_ttl_with_reqid(TAOS *taos, char *lines[], int  numLines, int protocol, int precision, int32_t ttl, int64_t reqid)`

- `TAOS_RES *taos_schemaless_insert_raw_ttl(TAOS *taos, char *lines, int len,  int32_t *totalRows, int protocol, int precision, int32_t ttl)`

- `TAOS_RES *taos_schemaless_insert_raw_ttl_with_reqid(TAOS *taos, char *lines, int len, int32_t *totalRows, int protocol, int precision, int32_t ttl,  int64_t reqid)`

  **说明**

  - 上面这7个接口是扩展接口，主要用于在schemaless写入时传递ttl、reqid参数，可以根据需要使用。
  - 带_raw的接口通过传递的参数lines指针和长度len来表示数据，为了解决原始接口数据包含'\0'而被截断的问题。totalRows指针返回解析出来的数据行数。
  - 带_ttl的接口可以传递ttl参数来控制建表的ttl到期时间。
  - 带_reqid的接口可以通过传递reqid参数来追踪整个的调用链。





# 部署集群

TDengine  支持集群，提供水平扩展的能力。如果需要获得更高的处理能力，只需要多增加节点即可。TDengine  采用虚拟节点技术，将一个节点虚拟化为多个虚拟节点，以实现负载均衡。同时，TDengine可以将多个节点上的虚拟节点组成虚拟节点组，通过多副本机制，以保证供系统的高可用。TDengine的集群功能完全开源。

本章节主要介绍如何在主机上人工部署集群，以及如何使用 Kubernetes 和 Helm部署集群。

# 集群部署和管理

## 准备工作

### 第零步

规划集群所有物理节点的 FQDN，将规划好的 FQDN 分别添加到每个物理节点的 /etc/hosts；修改每个物理节点的 /etc/hosts，将所有集群物理节点的 IP 与 FQDN 的对应添加好。【如部署了 DNS，请联系网络管理员在 DNS 上做好相关配置】

### 第一步

如果搭建集群的物理节点中，存有之前的测试数据，或者装过其他版本的 TDengine，请先将其删除，并清空所有数据（如果需要保留原有数据，请联系涛思交付团队进行旧版本升级、数据迁移），具体步骤请参考博客[《TDengine 多种安装包的安装和卸载》](https://www.taosdata.com/blog/2019/08/09/566.html)。

##### 

##### note

因为 FQDN 的信息会写进文件，如果之前没有配置或者更改 FQDN，且启动了 TDengine。请一定在确保数据无用或者备份的前提下，清理一下之前的数据（rm -rf /var/lib/taos/*）；

##### 

##### note

客户端所在服务器也需要配置，确保它可以正确解析每个节点的 FQDN 配置，不管是通过 DNS 服务，还是修改 hosts 文件。

### 第二步

确保集群中所有主机在端口 6030-6042 上的 TCP/UDP 协议能够互通。

### 第三步

在所有物理节点安装 TDengine，且版本必须是一致的，但不要启动 taosd。安装时，提示输入是否要加入一个已经存在的 TDengine  集群时，第一个物理节点直接回车创建新集群，后续物理节点则输入该集群任何一个在线的物理节点的 FQDN:端口号（默认 6030）；

### 第四步

检查所有数据节点，以及应用程序所在物理节点的网络设置：

每个物理节点上执行命令 `hostname -f`，查看和确认所有节点的 hostname 是不相同的（应用驱动所在节点无需做此项检查）；

每个物理节点上执行 ping host，其中 host 是其他物理节点的 hostname，看能否 ping 通其它物理节点；如果不能 ping  通，需要检查网络设置，或 /etc/hosts 文件（Windows 系统默认路径为  C:\Windows\system32\drivers\etc\hosts），或 DNS 的配置。如果无法 ping 通，是无法组成集群的；

从应用运行的物理节点，ping taosd 运行的数据节点，如果无法 ping 通，应用是无法连接 taosd 的，请检查应用所在物理节点的 DNS 设置或 hosts 文件；

每个数据节点的 End Point 就是输出的 hostname 外加端口号，比如 h1.taosdata.com:6030。

### 第五步

修改 TDengine 的配置文件（所有节点的文件 /etc/taos/taos.cfg 都需要修改）。假设准备启动的第一个数据节点 End Point 为 h1.taosdata.com:6030，其与集群配置相关参数如下：

```c
// firstEp 是每个数据节点首次启动后连接的第一个数据节点
firstEp               h1.taosdata.com:6030

// 必须配置为本数据节点的 FQDN，如果本机只有一个 hostname，可注释掉本项
fqdn                  h1.taosdata.com

// 配置本数据节点的端口号，缺省是 6030
serverPort            6030
```

一定要修改的参数是 firstEp 和 fqdn。在每个数据节点，firstEp 需全部配置成一样，但 fqdn 一定要配置成其所在数据节点的值。其他参数可不做任何修改，除非你很清楚为什么要修改。

加入到集群中的数据节点 dnode，下表中涉及集群相关的参数必须完全相同，否则不能成功加入到集群中。

| **#** | **配置参数名称** | **含义**                    |
| ----- | ---------------- | --------------------------- |
| 1     | statusInterval   | dnode 向 mnode 报告状态时长 |
| 2     | timezone         | 时区                        |
| 3     | locale           | 系统区位信息及编码格式      |
| 4     | charset          | 字符集编码                  |

## 启动集群

按照《立即开始》里的步骤，启动第一个数据节点，例如 h1.taosdata.com，然后执行 taos，启动 TDengine CLI，在其中执行命令 “SHOW DNODES”，如下所示：

```text
taos> show dnodes;
id | endpoint | vnodes | support_vnodes | status | create_time | note |
============================================================================================================================================
1 | h1.taosdata.com:6030 | 0 | 1024 | ready | 2022-07-16 10:50:42.673 | |
Query OK, 1 rows affected (0.007984s)
```

上述命令里，可以看到刚启动的数据节点的 End Point 是：h1.taos.com:6030，就是这个新集群的 firstEp。

## 添加数据节点

将后续的数据节点添加到现有集群，具体有以下几步：

按照《立即开始》一章的方法在每个物理节点启动 taosd；（注意：每个物理节点都需要在 taos.cfg 文件中将 firstEp 参数配置为新集群首个节点的 End Point——在本例中是 h1.taos.com:6030）

在第一个数据节点，使用 CLI 程序 taos，登录进 TDengine 系统，执行命令：

```sql
CREATE DNODE "h2.taos.com:6030";
```

将新数据节点的 End Point（准备工作中第四步获知的）添加进集群的 EP 列表。“fqdn:port”需要用双引号引起来，否则出错。请注意将示例的“h2.taos.com:6030” 替换为这个新数据节点的 End Point。

然后执行命令

```sql
SHOW DNODES;
```

查看新节点是否被成功加入。如果该被加入的数据节点处于离线状态，请做两个检查：

查看该数据节点的 taosd 是否正常工作，如果没有正常运行，需要先检查为什么? 查看该数据节点 taosd 日志文件 taosdlog.0 里前面几行日志（一般在 /var/log/taos 目录），看日志里输出的该数据节点 fqdn 以及端口号是否为刚添加的 End Point。如果不一致，需要将正确的 End Point 添加进去。 按照上述步骤可以源源不断的将新的数据节点加入到集群。

##### 

##### tip

任何已经加入集群在线的数据节点，都可以作为后续待加入节点的 firstEp。 firstEp 这个参数仅仅在该数据节点首次加入集群时有作用，加入集群后，该数据节点会保存最新的 mnode 的 End Point 列表，不再依赖这个参数。 接下来，配置文件中的 firstEp 参数就主要在客户端连接的时候使用了，例如 TDengine CLI 如果不加参数，会默认连接由 firstEp 指定的节点。 两个没有配置 firstEp 参数的数据节点 dnode 启动后，会独立运行起来。这个时候，无法将其中一个数据节点加入到另外一个数据节点，形成集群。无法将两个独立的集群合并成为新的集群。

## 查看数据节点

启动 TDengine CLI 程序 taos，然后执行：

```sql
SHOW DNODES;
```

它将列出集群中所有的 dnode，每个 dnode 的 ID，end_point（fqdn:port），状态（ready，offline 等），vnode 数目，还未使用的 vnode 数目等信息。在添加或删除一个数据节点后，可以使用该命令查看。

输出如下（具体内容仅供参考，取决于实际的集群配置）

```text
taos> show dnodes;
   id   |            endpoint            | vnodes | support_vnodes |   status   |       create_time       |              note              |
============================================================================================================================================
      1 | trd01:6030                     |    100 |           1024 | ready      | 2022-07-15 16:47:47.726 |                                |
Query OK, 1 rows affected (0.006684s)
```

## 查看虚拟节点组

为充分利用多核技术，并提供横向扩展能力，数据需要分片处理。因此 TDengine 会将一个 DB 的数据切分成多份，存放在多个 vnode 里。这些 vnode 可能分布在多个数据节点 dnode  里，这样就实现了水平扩展。一个 vnode 仅仅属于一个 DB，但一个 DB 可以有多个 vnode。vnode 所在的数据节点是 mnode  根据当前系统资源的情况，自动进行分配的，无需任何人工干预。

启动 CLI 程序 taos，然后执行：

```sql
USE SOME_DATABASE;
SHOW VGROUPS;
```

输出如下（具体内容仅供参考，取决于实际的集群配置）

```text
taos> use db;
Database changed.

taos> show vgroups;
  vgroup_id  |            db_name             |   tables    |  v1_dnode   | v1_status  |  v2_dnode   | v2_status  |  v3_dnode   | v3_status  |    status    |   nfiles    |  file_size  | tsma |
================================================================================================================================================================================================
           2 | db                             |           0 |           1 | leader     |        NULL | NULL       |        NULL | NULL       | NULL         |        NULL |        NULL |    0 |
           3 | db                             |           0 |           1 | leader     |        NULL | NULL       |        NULL | NULL       | NULL         |        NULL |        NULL |    0 |
           4 | db                             |           0 |           1 | leader     |        NULL | NULL       |        NULL | NULL       | NULL         |        NULL |        NULL |    0 |
Query OK, 8 row(s) in set (0.001154s)
```

## 删除数据节点

启动 CLI 程序 taos，执行：

```sql
DROP DNODE "fqdn:port";
```

或者

```sql
DROP DNODE dnodeId;
```

通过 “fqdn:port” 或 dnodeID 来指定一个具体的节点都是可以的。其中 fqdn 是被删除的节点的 FQDN，port 是其对外服务器的端口号；dnodeID 可以通过 SHOW DNODES 获得。

##### 

##### warning

数据节点一旦被 drop 之后，不能重新加入集群。需要将此节点重新部署（清空数据文件夹）。集群在完成 `drop dnode` 操作之前，会将该 dnode 的数据迁移走。 请注意 `drop dnode` 和 停止 taosd 进程是两个不同的概念，不要混淆：因为删除 dnode 之前要执行迁移数据的操作，因此被删除的 dnode 必须保持在线状态。待删除操作结束之后，才能停止 taosd 进程。 一个数据节点被 drop 之后，其他节点都会感知到这个 dnodeID 的删除操作，任何集群中的节点都不会再接收此 dnodeID 的请求。 dnodeID 是集群自动分配的，不得人工指定。它在生成时是递增的，不会重复。

## 常见问题

1、建立集群时使用 CREATE DNODE 增加新节点后，新节点始终显示 offline 状态？

```sql
  1）首先要检查增加的新节点上的 taosd 服务是否已经正常启动
  
  2）如果已经启动，再检查到新节点的网络是否通畅，可以使用 ping fqdn 验证下
  
  3）如果前面两步都没有问题，这一步要检查新节点做为独立集群在运行了，可以使用 taos -h fqdn 连接上后，show dnodes; 命令查看.
    如果显示的列表与你主节点上显示的不一致，说明此节点自己单独成立了一个集群，解决的方法是停止新节点上的服务，然后清空新节点上 
    taos.cfg 中配置的 dataDir 目录下的所有文件，重新启动新节点服务即可解决。
    
```



# 在 Kubernetes 上部署 TDengine 集群

作为面向云原生架构设计的时序数据库，TDengine 支持 Kubernetes 部署。这里介绍如何使用 YAML 文件一步一步从头创建一个 TDengine 集群，并重点介绍 Kubernetes 环境下 TDengine 的常用操作。

## 前置条件

要使用 Kubernetes 部署管理 TDengine 集群，需要做好如下准备工作。

- 本文适用 Kubernetes v1.5 以上版本
- 本文和下一章使用 minikube、kubectl 和 helm 等工具进行安装部署，请提前安装好相应软件
- Kubernetes 已经安装部署并能正常访问使用或更新必要的容器仓库或其他服务

以下配置文件也可以从 [GitHub 仓库](https://github.com/taosdata/TDengine-Operator/tree/3.0/src/tdengine) 下载。

## 配置 Service 服务

创建一个 Service 配置文件：`taosd-service.yaml`，服务名称 `metadata.name` (此处为 "taosd") 将在下一步中使用到。添加 TDengine 所用到的端口：

```yaml
---
apiVersion: v1
kind: Service
metadata:
  name: "taosd"
  labels:
    app: "tdengine"
spec:
  ports:
    - name: tcp6030
      protocol: "TCP"
      port: 6030
    - name: tcp6041
      protocol: "TCP"
      port: 6041
  selector:
    app: "tdengine"
```

## 有状态服务 StatefulSet

根据 Kubernetes 对各类部署的说明，我们将使用 StatefulSet 作为 TDengine 的服务类型。 创建文件 `tdengine.yaml`，其中 replicas 定义集群节点的数量为 3。节点时区为中国（Asia/Shanghai），每个节点分配 10G 标准（standard）存储。你也可以根据实际情况进行相应修改。

```yaml
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: "tdengine"
  labels:
    app: "tdengine"
spec:
  serviceName: "taosd"
  replicas: 3
  updateStrategy:
    type: RollingUpdate
  selector:
    matchLabels:
      app: "tdengine"
  template:
    metadata:
      name: "tdengine"
      labels:
        app: "tdengine"
    spec:
      containers:
        - name: "tdengine"
          image: "tdengine/tdengine:3.0.0.0"
          imagePullPolicy: "IfNotPresent"
          ports:
            - name: tcp6030
              protocol: "TCP"
              containerPort: 6030
            - name: tcp6041
              protocol: "TCP"
              containerPort: 6041
          env:
            # POD_NAME for FQDN config
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            # SERVICE_NAME and NAMESPACE for fqdn resolve
            - name: SERVICE_NAME
              value: "taosd"
            - name: STS_NAME
              value: "tdengine"
            - name: STS_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
            # TZ for timezone settings, we recommend to always set it.
            - name: TZ
              value: "Asia/Shanghai"
            # TAOS_ prefix will configured in taos.cfg, strip prefix and camelCase.
            - name: TAOS_SERVER_PORT
              value: "6030"
            # Must set if you want a cluster.
            - name: TAOS_FIRST_EP
              value: "$(STS_NAME)-0.$(SERVICE_NAME).$(STS_NAMESPACE).svc.cluster.local:$(TAOS_SERVER_PORT)"
            # TAOS_FQND should always be set in k8s env.
            - name: TAOS_FQDN
              value: "$(POD_NAME).$(SERVICE_NAME).$(STS_NAMESPACE).svc.cluster.local"
          volumeMounts:
            - name: taosdata
              mountPath: /var/lib/taos
          readinessProbe:
            exec:
              command:
                - taos-check
            initialDelaySeconds: 5
            timeoutSeconds: 5000
          livenessProbe:
            exec:
              command:
                - taos-check
            initialDelaySeconds: 15
            periodSeconds: 20
  volumeClaimTemplates:
    - metadata:
        name: taosdata
      spec:
        accessModes:
          - "ReadWriteOnce"
        storageClassName: "standard"
        resources:
          requests:
            storage: "10Gi"
```

## 使用 kubectl 命令部署 TDengine 集群

顺序执行以下命令。

```bash
kubectl apply -f taosd-service.yaml
kubectl apply -f tdengine.yaml
```

上面的配置将生成一个三节点的 TDengine 集群，dnode 为自动配置，可以使用 show dnodes 命令查看当前集群的节点：

```bash
kubectl exec -i -t tdengine-0 -- taos -s "show dnodes"
kubectl exec -i -t tdengine-1 -- taos -s "show dnodes"
kubectl exec -i -t tdengine-2 -- taos -s "show dnodes"
```

输出如下：

```text
taos> show dnodes
   id   |            endpoint            | vnodes | support_vnodes |   status   |       create_time       |              note              |
============================================================================================================================================
      1 | tdengine-0.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:14:57.285 |                                |
      2 | tdengine-1.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:15:11.302 |                                |
      3 | tdengine-2.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:15:23.290 |                                |
Query OK, 3 rows in database (0.003655s)
```

## 使能端口转发

利用 kubectl 端口转发功能可以使应用可以访问 Kubernetes 环境运行的 TDengine 集群。

```text
kubectl port-forward tdengine-0 6041:6041 &
```

使用 curl 命令验证 TDengine REST API 使用的 6041 接口。

```text
$ curl -u root:taosdata -d "show databases" 127.0.0.1:6041/rest/sql
Handling connection for 6041
{"code":0,"column_meta":[["name","VARCHAR",64],["create_time","TIMESTAMP",8],["vgroups","SMALLINT",2],["ntables","BIGINT",8],["replica","TINYINT",1],["strict","VARCHAR",4],["duration","VARCHAR",10],["keep","VARCHAR",32],["buffer","INT",4],["pagesize","INT",4],["pages","INT",4],["minrows","INT",4],["maxrows","INT",4],["comp","TINYINT",1],["precision","VARCHAR",2],["status","VARCHAR",10],["retention","VARCHAR",60],["single_stable","BOOL",1],["cachemodel","VARCHAR",11],["cachesize","INT",4],["wal_level","TINYINT",1],["wal_fsync_period","INT",4],["wal_retention_period","INT",4],["wal_retention_size","BIGINT",8],["wal_roll_period","INT",4],["wal_segment_size","BIGINT",8]],"data":[["information_schema",null,null,16,null,null,null,null,null,null,null,null,null,null,null,"ready",null,null,null,null,null,null,null,null,null,null],["performance_schema",null,null,10,null,null,null,null,null,null,null,null,null,null,null,"ready",null,null,null,null,null,null,null,null,null,null]],"rows":2} 
```

## 使用 dashboard 进行图形化管理

 minikube 提供 dashboard 命令支持图形化管理界面。

```text
$ minikube dashboard
* Verifying dashboard health ...
* Launching proxy ...
* Verifying proxy health ...
* Opening http://127.0.0.1:46617/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
http://127.0.0.1:46617/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/
```

对于某些公有云环境，minikube 绑定在 127.0.0.1 IP 地址上无法通过远程访问，需要使用 kubectl proxy 命令将端口映射到 0.0.0.0 IP  地址上，再通过浏览器访问虚拟机公网 IP 和端口以及相同的 dashboard URL 路径即可远程访问 dashboard。

```text
$ kubectl proxy --accept-hosts='^.*$' --address='0.0.0.0'
```

## 集群扩容

TDengine 集群支持自动扩容：

```bash
kubectl scale statefulsets tdengine --replicas=4
```

上面命令行中参数 `--replica=4` 表示要将 TDengine 集群扩容到 4 个节点，执行后首先检查 POD 的状态：

```bash
kubectl get pods -l app=tdengine
```

输出如下：

```text
NAME         READY   STATUS    RESTARTS   AGE
tdengine-0   1/1     Running   0          161m
tdengine-1   1/1     Running   0          161m
tdengine-2   1/1     Running   0          32m
tdengine-3   1/1     Running   0          32m
```

此时 POD 的状态仍然是 Running，TDengine 集群中的 dnode 状态要等 POD 状态为 `ready` 之后才能看到：

```bash
kubectl exec -i -t tdengine-3 -- taos -s "show dnodes"
```

扩容后的四节点 TDengine 集群的 dnode 列表:

```text
taos> show dnodes
   id   |            endpoint            | vnodes | support_vnodes |   status   |       create_time       |              note              |
============================================================================================================================================
      1 | tdengine-0.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:14:57.285 |                                |
      2 | tdengine-1.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:15:11.302 |                                |
      3 | tdengine-2.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:15:23.290 |                                |
      4 | tdengine-3.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:33:16.039 |                                |
Query OK, 4 rows in database (0.008377s)
```

## 集群缩容

由于 TDengine 集群在扩缩容时会对数据进行节点间迁移，使用 kubectl 命令进行缩容需要首先使用 "drop dnodes" 命令，节点删除完成后再进行 Kubernetes 集群缩容。

注意：由于 Kubernetes Statefulset 中 Pod 的只能按创建顺序逆序移除，所以 TDengine drop dnode 也需要按照创建顺序逆序移除，否则会导致 Pod 处于错误状态。

```text
$ kubectl exec -i -t tdengine-0 -- taos -s "drop dnode 4"
$ kubectl exec -it tdengine-0 -- taos -s "show dnodes"

taos> show dnodes
   id   |            endpoint            | vnodes | support_vnodes |   status   |       create_time       |              note              |
============================================================================================================================================
      1 | tdengine-0.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:14:57.285 |                                |
      2 | tdengine-1.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:15:11.302 |                                |
      3 | tdengine-2.taosd.default.sv... |      0 |            256 | ready      | 2022-08-10 13:15:23.290 |                                |
Query OK, 3 rows in database (0.004861s)
```

确认移除成功后（使用 kubectl exec -i -t tdengine-0 -- taos -s "show dnodes" 查看和确认 dnode 列表），使用 kubectl 命令移除 POD：

```text
kubectl scale statefulsets tdengine --replicas=3
```

最后一个 POD 将会被删除。使用命令 kubectl get pods -l app=tdengine 查看POD状态：

```text
$ kubectl get pods -l app=tdengine
NAME READY STATUS RESTARTS AGE
tdengine-0 1/1 Running 0 4m7s
tdengine-1 1/1 Running 0 3m55s
tdengine-2 1/1 Running 0 2m28s
```

POD删除后，需要手动删除PVC，否则下次扩容时会继续使用以前的数据导致无法正常加入集群。

```bash
$ kubectl delete pvc taosdata-tdengine-3
```

此时的集群状态是安全的，需要时还可以再次进行扩容：

```bash
$ kubectl scale statefulsets tdengine --replicas=4
statefulset.apps/tdengine scaled
it@k8s-2:~/TDengine-Operator/src/tdengine$ kubectl get pods -l app=tdengine
NAME READY STATUS RESTARTS AGE
tdengine-0 1/1 Running 0 35m
tdengine-1 1/1 Running 0 34m
tdengine-2 1/1 Running 0 12m
tdengine-3 0/1 ContainerCreating 0 4s
it@k8s-2:~/TDengine-Operator/src/tdengine$ kubectl get pods -l app=tdengine
NAME READY STATUS RESTARTS AGE
tdengine-0 1/1 Running 0 35m
tdengine-1 1/1 Running 0 34m
tdengine-2 1/1 Running 0 12m
tdengine-3 0/1 Running 0 7s
it@k8s-2:~/TDengine-Operator/src/tdengine$ kubectl exec -it tdengine-0 -- taos -s "show dnodes"

taos> show dnodes
id | endpoint | vnodes | support_vnodes | status | create_time | offline reason |
======================================================================================================================================
1 | tdengine-0.taosd.default.sv... | 0 | 4 | ready | 2022-07-25 17:38:49.012 | |
2 | tdengine-1.taosd.default.sv... | 1 | 4 | ready | 2022-07-25 17:39:01.517 | |
5 | tdengine-2.taosd.default.sv... | 0 | 4 | ready | 2022-07-25 18:01:36.479 | |
6 | tdengine-3.taosd.default.sv... | 0 | 4 | ready | 2022-07-25 18:13:54.411 | |
Query OK, 4 row(s) in set (0.001348s)
```

## 清理 TDengine 集群

完整移除 TDengine 集群，需要分别清理 statefulset、svc、configmap、pvc。

```bash
kubectl delete statefulset -l app=tdengine
kubectl delete svc -l app=tdengine
kubectl delete pvc -l app=tdengine
kubectl delete configmap taoscfg
```

## 常见错误

### 错误一

未进行 "drop dnode" 直接进行缩容，由于 TDengine 尚未删除节点，缩容 pod 导致 TDengine 集群中部分节点处于 offline 状态。

```text
$ kubectl exec -it tdengine-0 -- taos -s "show dnodes"

taos> show dnodes
id | endpoint | vnodes | support_vnodes | status | create_time | offline reason |
======================================================================================================================================
1 | tdengine-0.taosd.default.sv... | 0 | 4 | ready | 2022-07-25 17:38:49.012 | |
2 | tdengine-1.taosd.default.sv... | 1 | 4 | ready | 2022-07-25 17:39:01.517 | |
5 | tdengine-2.taosd.default.sv... | 0 | 4 | offline | 2022-07-25 18:01:36.479 | status msg timeout |
6 | tdengine-3.taosd.default.sv... | 0 | 4 | offline | 2022-07-25 18:13:54.411 | status msg timeout |
Query OK, 4 row(s) in set (0.001323s)
```

### 错误二

TDengine 集群会持有 replica 参数，如果缩容后的节点数小于这个值，集群将无法使用：

创建一个库使用 replica 参数为 2，插入部分数据：

```bash
kubectl exec -i -t tdengine-0 -- \
  taos -s \
  "create database if not exists test replica 2;
   use test;
   create table if not exists t1(ts timestamp, n int);
   insert into t1 values(now, 1)(now+1s, 2);"
```

缩容到单节点：

```bash
kubectl scale statefulsets tdengine --replicas=1
```

在 TDengine CLI 中的所有数据库操作将无法成功。

```text
taos> show dnodes;
   id   |           end_point            | vnodes | cores  |   status   | role  |       create_time       |      offline reason      |
======================================================================================================================================
      1 | tdengine-0.taosd.default.sv... |      2 |     40 | ready      | any   | 2021-06-01 15:55:52.562 |                          |
      2 | tdengine-1.taosd.default.sv... |      1 |     40 | offline    | any   | 2021-06-01 15:56:07.212 | status msg timeout       |
Query OK, 2 row(s) in set (0.000845s)

taos> show dnodes;
   id   |           end_point            | vnodes | cores  |   status   | role  |       create_time       |      offline reason      |
======================================================================================================================================
      1 | tdengine-0.taosd.default.sv... |      2 |     40 | ready      | any   | 2021-06-01 15:55:52.562 |                          |
      2 | tdengine-1.taosd.default.sv... |      1 |     40 | offline    | any   | 2021-06-01 15:56:07.212 | status msg timeout       |
Query OK, 2 row(s) in set (0.000837s)

taos> use test;
Database changed.

taos> insert into t1 values(now, 3);

DB error: Unable to resolve FQDN (0.013874s)
```

# TDengine SQL

本文档说明 TDengine SQL 支持的语法规则、主要查询功能、支持的 SQL 查询函数，以及常用技巧等内容。阅读本文档需要读者具有基本的 SQL 语言的基础。TDengine 3.0 版本相比 2.x 版本做了大量改进和优化，特别是查询引擎进行了彻底的重构，因此 SQL 语法相比 2.x 版本有很多变更。详细的变更内容请见 [3.0 版本语法变更](https://docs.taosdata.com/taos-sql/changes/) 章节

TDengine SQL 是用户对 TDengine 进行数据写入和查询的主要工具。TDengine SQL 提供标准的 SQL 语法，并针对时序数据和业务的特点优化和新增了许多语法和功能。TDengine SQL 语句的最大长度为 1M。TDengine SQL 不支持关键字的缩写，例如 DELETE 不能缩写为 DEL。

本章节 SQL 语法遵循如下约定：

- 用大写字母表示关键字，但 SQL 本身并不区分关键字和标识符的大小写
- 用小写字母表示需要用户输入的内容
- 𤆺表示内容为可选项，但不能输入 [] 本身
- | 表示多选一，选择其中一个即可，但不能输入 | 本身
- … 表示前面的项可重复多个

为更好地说明 SQL 语法的规则及其特点，本文假设存在一个数据集。以智能电表(meters)为例，假设每个智能电表采集电流、电压、相位三个量。其建模如下：

```text
taos> DESCRIBE meters;
             Field              |        Type        |   Length    |    Note    |
=================================================================================
 ts                             | TIMESTAMP          |           8 |            |
 current                        | FLOAT              |           4 |            |
 voltage                        | INT                |           4 |            |
 phase                          | FLOAT              |           4 |            |
 location                       | BINARY             |          64 | TAG        |
 groupid                        | INT                |           4 | TAG        |
```

数据集包含 4 个智能电表的数据，按照 TDengine 的建模规则，对应 4 个子表，其名称分别是 d1001, d1002, d1003, d1004。

## 数据类型

### [时间戳](https://docs.taosdata.com/taos-sql/data-type/#时间戳)

使用 TDengine，最重要的是时间戳。**创建并插入记录、查询历史记录的时候，均需要指定时间戳**。时间戳有如下规则：

- 时间格式为 `YYYY-MM-DD HH:mm:ss.MS`，默认时间分辨率为毫秒。比如：`2017-08-12 18:25:58.128`
- 内部函数 NOW 是客户端的当前时间
- 插入记录时，如果时间戳为 NOW，插入数据时使用提交这条记录的客户端的当前时间
- Epoch Time：时间戳也可以是一个长整数，表示从 UTC 时间 1970-01-01 00:00:00 开始的毫秒数。相应地，如果所在 Database 的时间精度设置为“微秒”，则长整型格式的时间戳含义也就对应于从 UTC 时间 1970-01-01 00:00:00 开始的微秒数；纳秒精度逻辑相同。
- 时间可以加减，比如 NOW-2h，表明查询时刻向前推 2 个小时（最近 2 小时）。数字后面的时间单位可以是 b（纳秒）、u（微秒）、a（毫秒）、s（秒）、m（分）、h（小时）、d（天）、w（周）。 比如 `SELECT * FROM t1 WHERE ts > NOW-2w AND ts <= NOW-1w`，表示查询两周前整整一周的数据。在指定降采样操作（Down Sampling）的时间窗口（Interval）时，时间单位还可以使用 n（自然月）和 y（自然年）。

TDengine **缺省的时间戳精度是毫秒**，但通过在 `CREATE DATABASE` 时传递的 `PRECISION` 参数也可以支持微秒和纳秒。

```sql
CREATE DATABASE db_name PRECISION 'ns';
```

### [数据类型](https://docs.taosdata.com/taos-sql/data-type/#数据类型)

在 TDengine 中，普通表的数据模型中可使用以下数据类型。

| #    | **类型**          | **Bytes** | **说明**                                                     |
| ---- | ----------------- | --------- | ------------------------------------------------------------ |
| 1    | TIMESTAMP         | 8         | 时间戳。缺省精度毫秒，可支持微秒和纳秒，详细说明见上节。     |
| 2    | INT               | 4         | 整型，范围 [-2^31, 2^31-1]                                   |
| 3    | INT UNSIGNED      | 4         | 无符号整数，[0, 2^32-1]                                      |
| 4    | BIGINT            | 8         | 长整型，范围 [-2^63, 2^63-1]                                 |
| 5    | BIGINT UNSIGNED   | 8         | 长整型，范围 [0, 2^64-1]                                     |
| 6    | FLOAT             | 4         | 浮点型，有效位数 6-7，范围 [-3.4E38, 3.4E38]                 |
| 7    | DOUBLE            | 8         | 双精度浮点型，有效位数 15-16，范围 [-1.7E308, 1.7E308]       |
| 8    | BINARY            | 自定义    | 记录单字节字符串，建议只用于处理 ASCII 可见字符，中文等多字节字符需使用 NCHAR |
| 9    | SMALLINT          | 2         | 短整型， 范围 [-32768, 32767]                                |
| 10   | SMALLINT UNSIGNED | 2         | 无符号短整型，范围 [0, 65535]                                |
| 11   | TINYINT           | 1         | 单字节整型，范围 [-128, 127]                                 |
| 12   | TINYINT UNSIGNED  | 1         | 无符号单字节整型，范围 [0, 255]                              |
| 13   | BOOL              | 1         | 布尔型，{true, false}                                        |
| 14   | NCHAR             | 自定义    | 记录包含多字节字符在内的字符串，如中文字符。每个 NCHAR 字符占用 4 字节的存储空间。字符串两端使用单引号引用，字符串内的单引号需用转义字符 `\'`。NCHAR 使用时须指定字符串大小，类型为 NCHAR(10) 的列表示此列的字符串最多存储 10 个 NCHAR 字符。如果用户字符串长度超出声明长度，将会报错。 |
| 15   | JSON              |           | JSON 数据类型， **只有 Tag 可以是 JSON 格式**                |
| 16   | VARCHAR           | 自定义    | BINARY 类型的别名                                            |

##### NOTE

- 表的每行长度不能超过 48KB（注意：每个 BINARY/NCHAR 类型的列还会额外占用 2 个字节的存储位置）。
- 虽然 BINARY 类型在底层存储上支持字节型的二进制字符，但不同编程语言对二进制数据的处理方式并不保证一致，因此**建议在 BINARY 类型中只存储 ASCII 可见字符，而避免存储不可见字符**。多字节的数据，例如中文字符，则需要使用 NCHAR 类型进行保存。如果强行使用 BINARY 类型保存中文字符，虽然有时也能正常读写，但并不带有字符集信息，很容易出现数据乱码甚至数据损坏等情况。
- BINARY 类型理论上最长可以有 **16,374 字节**。BINARY 仅支持字符串输入，字符串两端需使用单引号引用。使用时须指定大小，如 BINARY(20) 定义了最长为 20 个单字节字符的字符串，每个字符占 1 字节的存储空间，总共固定占用 20 字节的空间，此时如果用户字符串超出 20 字节将会报错。对于字符串内的单引号，可以用转义字符反斜线加单引号来表示，即 `\'`。
- SQL 语句中的数值类型将依据是否存在小数点，或使用科学计数法表示，来判断数值类型是否为整型或者浮点型，因此在使用时要注意相应类型越界的情况。例如，9999999999999999999 会认为超过长整型的上边界而溢出，而 9999999999999999999.0 会被认为是有效的浮点数。

### [常量](https://docs.taosdata.com/taos-sql/data-type/#常量)

TDengine 支持多个类型的常量，细节如下表：

| #    | **语法**                                          | **类型**  | **说明**                                                     |
| ---- | ------------------------------------------------- | --------- | ------------------------------------------------------------ |
| 1    | [{+ \| -}]123                                     | BIGINT    | 整型数值的字面量的类型均为 BIGINT。如果用户输入超过了 BIGINT 的表示范围，TDengine 按 BIGINT 对数值进行截断。 |
| 2    | 123.45                                            | DOUBLE    | 浮点数值的字面量的类型均为 DOUBLE。TDengine 依据是否存在小数点，或使用科学计数法表示，来判断数值类型是否为整型或者浮点型。 |
| 3    | 1.2E3                                             | DOUBLE    | 科学计数法的字面量的类型为 DOUBLE。                          |
| 4    | 'abc'                                             | BINARY    | 单引号括住的内容为字符串字面值，其类型为 BINARY，BINARY 的 Size 为实际的字符个数。对于字符串内的单引号，可以用转义字符反斜线加单引号来表示，即 `\'`。 |
| 5    | "abc"                                             | BINARY    | 双引号括住的内容为字符串字面值，其类型为 BINARY，BINARY 的 Size 为实际的字符个数。对于字符串内的双引号，可以用转义字符反斜线加单引号来表示，即 `\"`。 |
| 6    | TIMESTAMP {'literal' \| "literal"}                | TIMESTAMP | TIMESTAMP 关键字表示后面的字符串字面量需要被解释为 TIMESTAMP 类型。字符串需要满足 YYYY-MM-DD HH:mm:ss.MS 格式，其时间分辨率为当前数据库的时间分辨率。 |
| 7    | {TRUE \| FALSE}                                   | BOOL      | 布尔类型字面量。                                             |
| 8    | {'' \| "" \| '\t' \| "\t" \| ' ' \| " " \| NULL } | --        | 空值字面量。可以用于任意类型。                               |

##### NOTE

- TDengine 依据是否存在小数点，或使用科学计数法表示，来判断数值类型是否为整型或者浮点型，因此在使用时要注意相应类型越界的情况。例如，9999999999999999999 会认为超过长整型的上边界而溢出，而 9999999999999999999.0 会被认为是有效的浮点数。

## 数据库

### [创建数据库](https://docs.taosdata.com/taos-sql/database/#创建数据库)

```sql
CREATE DATABASE [IF NOT EXISTS] db_name [database_options]
 
database_options:
    database_option ...
 
database_option: {
    BUFFER value
  | CACHEMODEL {'none' | 'last_row' | 'last_value' | 'both'}
  | CACHESIZE value
  | COMP {0 | 1 | 2}
  | DURATION value
  | WAL_FSYNC_PERIOD value
  | MAXROWS value
  | MINROWS value
  | KEEP value
  | PAGES value
  | PAGESIZE  value
  | PRECISION {'ms' | 'us' | 'ns'}
  | REPLICA value
  | RETENTIONS ingestion_duration:keep_duration ...
  | WAL_LEVEL {1 | 2}
  | VGROUPS value
  | SINGLE_STABLE {0 | 1}
  | STT_TRIGGER value
  | TABLE_PREFIX value
  | TABLE_SUFFIX value
  | TSDB_PAGESIZE value
  | WAL_RETENTION_PERIOD value
  | WAL_RETENTION_SIZE value
  | WAL_SEGMENT_SIZE value
}
```

#### [参数说明](https://docs.taosdata.com/taos-sql/database/#参数说明)

- BUFFER: 一个 VNODE 写入内存池大小，单位为 MB，默认为 96，最小为 3，最大为 16384。

- CACHEMODEL：表示是否在内存中缓存子表的最近数据。默认为 none。

  - none：表示不缓存。
  - last_row：表示缓存子表最近一行数据。这将显著改善 LAST_ROW 函数的性能表现。
  - last_value：表示缓存子表每一列的最近的非 NULL 值。这将显著改善无特殊影响（WHERE、ORDER BY、GROUP BY、INTERVAL）下的 LAST 函数的性能表现。
  - both：表示同时打开缓存最近行和列功能。

- CACHESIZE：表示每个 vnode 中用于缓存子表最近数据的内存大小。默认为 1 ，范围是[1, 65536]，单位是 MB。

- COMP：表示数据库文件压缩标志位，缺省值为 2，取值范围为

  ​	[0, 2]。

  - 0：表示不压缩。
  - 1：表示一阶段压缩。
  - 2：表示两阶段压缩。
  
- DURATION：数据文件存储数据的时间跨度。可以使用加单位的表示形式，如 DURATION 100h、DURATION 10d 等，支持 m（分钟）、h（小时）和 d（天）三个单位。不加时间单位时默认单位为天，如 DURATION 50 表示 50 天。

- WAL_FSYNC_PERIOD：当 WAL 参数设置为 2 时，落盘的周期。默认为 3000，单位毫秒。最小为 0，表示每次写入立即落盘；最大为 180000，即三分钟。

- MAXROWS：**文件块**中记录的最大条数，默认为 4096 条。

- MINROWS：**文件块**中记录的最小条数，默认为 100 条。

- KEEP：表示数据文件保存的天数，缺省值为 3650，取值范围 [1, 365000]，且必须大于或等于 DURATION 参数值。**数据库会自动删除保存时间超过 KEEP 值的数据**。KEEP 可以使 用加单位的表示形式，如 KEEP 100h、KEEP 10d 等，支持 m（分钟）、h（小时）和 d（天）三个单位。也可以不写单位，如 KEEP 50，此时默认单位为天。企业版支持[多级存储](https://docs.taosdata.com/tdinternal/arch/#多级存储)功能, 因此, 可以设置多个保存时间（多个以英文逗号分隔，最多 3 个，满足 keep 0 <= keep 1 <= keep 2，如 KEEP 100h,100d,3650d）; 社区版不支持多级存储功能（即使配置了多个保存时间, 也不会生效, KEEP 会取最大的保存时间）。

- PAGES：一个 VNODE 中元数据存储引擎的缓存页个数，默认为 256，最小 64。一个 VNODE 元数据存储占用 PAGESIZE * PAGES，默认情况下为 1MB 内存。

- PAGESIZE：一个 VNODE 中元数据存储引擎的页大小，单位为 KB，默认为 4 KB。范围为 1 到 16384，即 1 KB 到 16 MB。

- PRECISION：数据库的时间戳精度。ms 表示毫秒，us 表示微秒，ns 表示纳秒，默认 ms 毫秒。

- REPLICA：表示数据库副本数，取值为 1 或 3，默认为 1。在集群中使用，副本数必须小于或等于 DNODE 的数目。

- <span id="RETENTIONS">RETENTIONS</span>：表示数据的聚合周期和保存时长，如 RETENTIONS 15s:7d,1m:21d,15m:50d 表示数据原始采集周期为 15 秒，原始数据保存 7 天；按 1 分钟聚合的数据保存 21 天；按 15 分钟聚合的数据保存 50 天。目前支持且只支持三级存储周期。

- WAL_LEVEL：WAL 级别，默认为 1。

  - 1：写 WAL，但不执行 fsync。
  - 2：写 WAL，而且执行 fsync。

- VGROUPS：数据库中初始 vgroup 的数目。

- SINGLE_STABLE：表示此数据库中是否只可以创建一个超级表，用于超级表列非常多的情况。

  - 0：表示可以创建多张超级表。
  - 1：表示只可以创建一张超级表。

- STT_TRIGGER：表示落盘文件触发文件合并的个数。默认为 1，范围 1 到 16。对于少表高频场景，此参数建议使用默认配置，或较小的值；而对于多表低频场景，此参数建议配置较大的值。

- TABLE_PREFIX：当其为正值时，在决定把一个表分配到哪个 vgroup 时要忽略表名中指定长度的前缀；当其为负值时，在决定把一个表分配到哪个 vgroup 时只使用表名中指定长度的前缀；例如，假定表名为 "v30001"，当 TSDB_PREFIX = 2 时 使用 "0001" 来决定分配到哪个 vgroup ，当 TSDB_PREFIX = -2 时使用 "v3" 来决定分配到哪个 vgroup

- TABLE_SUFFIX：当其为正值时，在决定把一个表分配到哪个 vgroup 时要忽略表名中指定长度的后缀；当其为负值时，在决定把一个表分配到哪个 vgroup 时只使用表名中指定长度的后缀；例如，假定表名为 "v30001"，当 TSDB_SUFFIX = 2 时 使用 "v300" 来决定分配到哪个 vgroup ，当 TSDB_SUFFIX = -2 时使用 "01" 来决定分配到哪个 vgroup。

- TSDB_PAGESIZE：一个 VNODE 中时序数据存储引擎的页大小，单位为 KB，默认为 4 KB。范围为 1 到 16384，即 1 KB到 16 MB。

- WAL_RETENTION_PERIOD: 为了数据订阅消费，需要WAL日志文件额外保留的最大时长策略。WAL日志清理，不受订阅客户端消费状态影响。单位为 s。默认为 0，表示无需为订阅保留。新建订阅，应先设置恰当的时长策略。

- WAL_RETENTION_SIZE：为了数据订阅消费，需要WAL日志文件额外保留的最大累计大小策略。单位为 KB。默认为 0，表示累计大小无上限。

- WAL_ROLL_PERIOD：wal 文件切换时长，单位为 s。当WAL文件创建并写入后，经过该时间，会自动创建一个新的WAL文件。默认为 0，即仅在TSDB落盘时创建新文件。

- WAL_SEGMENT_SIZE：wal 单个文件大小，单位为 KB。当前写入文件大小超过上限后会自动创建一个新的WAL文件。默认为 0，即仅在TSDB落盘时创建新文件。

### [创建数据库示例](https://docs.taosdata.com/taos-sql/database/#创建数据库示例)

```sql
create database if not exists db vgroups 10 buffer 10
```

以上示例创建了一个有 10 个 vgroup 名为 db 的数据库， 其中每个 vnode 分配 10MB 的写入缓存

### [使用数据库](https://docs.taosdata.com/taos-sql/database/#使用数据库)

```text
USE db_name;
```

使用/切换数据库（在 REST 连接方式下无效）。

### [删除数据库](https://docs.taosdata.com/taos-sql/database/#删除数据库)

```text
DROP DATABASE [IF EXISTS] db_name
```

删除数据库。指定 Database 所包含的全部数据表将被删除，该数据库的所有 vgroups 也会被全部销毁，请谨慎使用！

### [修改数据库参数](https://docs.taosdata.com/taos-sql/database/#修改数据库参数)

```sql
ALTER DATABASE db_name [alter_database_options]

alter_database_options:
    alter_database_option ...

alter_database_option: {
    CACHEMODEL {'none' | 'last_row' | 'last_value' | 'both'}
  | CACHESIZE value
  | BUFFER value
  | PAGES value
  | REPLICA value
  | STT_TRIGGER value
  | WAL_LEVEL value
  | WAL_FSYNC_PERIOD value
  | KEEP value
}
```

#### [修改 CACHESIZE](https://docs.taosdata.com/taos-sql/database/#修改-cachesize)

修改数据库参数的命令使用简单，难的是如何确定是否需要修改以及如何修改。本小节描述如何判断数据库的 cachesize 是否够用。

1. 如何查看 cachesize?

通过 select * from information_schema.ins_databases; 可以查看这些 cachesize 的具体值。

1. 如何查看 cacheload?

通过 show <db_name>.vgroups; 可以查看 cacheload

1. 判断 cachesize 是否够用

如果 cacheload 非常接近 cachesize，则 cachesize 可能过小。 如果 cacheload 明显小于 cachesize 则 cachesize 是够用的。可以根据这个原则判断是否需要修改 cachesize 。具体修改值可以根据系统可用内存情况来决定是加倍或者是提高几倍。

##### NOTE

其它参数在 3.0.0.0 中暂不支持修改

### [查看数据库](https://docs.taosdata.com/taos-sql/database/#查看数据库)

#### [查看系统中的所有数据库](https://docs.taosdata.com/taos-sql/database/#查看系统中的所有数据库)

```text
SHOW DATABASES;
```

#### [显示一个数据库的创建语句](https://docs.taosdata.com/taos-sql/database/#显示一个数据库的创建语句)

```text
SHOW CREATE DATABASE db_name \G;
```

常用于数据库迁移。对一个已经存在的数据库，返回其创建语句；在另一个集群中执行该语句，就能得到一个设置完全相同的 Database。

#### []查看数据库参数(https://docs.taosdata.com/taos-sql/database/#查看数据库参数)

```sql
SELECT * FROM INFORMATION_SCHEMA.INS_DATABASES WHERE NAME='db_name' \G;
```

会列出指定数据库的配置参数，并且每行只显示一个参数。

### [删除过期数据](https://docs.taosdata.com/taos-sql/database/#删除过期数据)

```sql
TRIM DATABASE db_name;
```

删除过期数据，并根据多级存储的配置归整数据。

### [落盘内存数据](https://docs.taosdata.com/taos-sql/database/#落盘内存数据)

```sql
FLUSH DATABASE db_name;
```

落盘内存中的数据。在关闭节点之前，执行这条命令可以避免重启后的数据回放，加速启动过程。

### [调整VGROUP中VNODE的分布](https://docs.taosdata.com/taos-sql/database/#调整vgroup中vnode的分布)

```sql
REDISTRIBUTE VGROUP vgroup_no DNODE dnode_id1 [DNODE dnode_id2] [DNODE dnode_id3]
```

按照给定的dnode列表，调整vgroup中的vnode分布。因为副本数目最大为3，所以最多输入3个dnode。

### [自动调整VGROUP中VNODE的分布](https://docs.taosdata.com/taos-sql/database/#自动调整vgroup中vnode的分布)

```sql
BALANCE VGROUP
```

自动调整集群所有vgroup中的vnode分布，相当于在vnode级别对集群进行数据的负载均衡操作。

### [查看数据库工作状态](https://docs.taosdata.com/taos-sql/database/#查看数据库工作状态)

```sql
SHOW db_name.ALIVE;
```

查询数据库 db_name 的可用状态，返回值 0：不可用 1：完全可用 2：部分可用（即数据库包含的 VNODE 部分节点可用，部分节点不可用）

## 表

### [创建表](https://docs.taosdata.com/taos-sql/table/#创建表)

`CREATE TABLE` 语句用于创建普通表和以超级表为模板创建子表。

```sql
CREATE TABLE [IF NOT EXISTS] [db_name.]tb_name (create_definition [, create_definition] ...) [table_options]

CREATE TABLE create_subtable_clause

CREATE TABLE [IF NOT EXISTS] [db_name.]tb_name (create_definition [, create_definition] ...)
    [TAGS (create_definition [, create_definition] ...)]
    [table_options]

create_subtable_clause: {
    create_subtable_clause [create_subtable_clause] ...
  | [IF NOT EXISTS] [db_name.]tb_name USING [db_name.]stb_name [(tag_name [, tag_name] ...)] TAGS (tag_value [, tag_value] ...)
}

create_definition:
    col_name column_type

table_options:
    table_option ...

table_option: {
    COMMENT 'string_value'
  | WATERMARK duration[,duration]
  | MAX_DELAY duration[,duration]
  | ROLLUP(func_name [, func_name] ...)
  | SMA(col_name [, col_name] ...)
  | TTL value
}
```

**使用说明**

1. 表的第一个字段必须是 TIMESTAMP，并且**系统自动将其设为主键**；
2. 表名最大长度为 192；
3. 表的每行长度不能超过 48KB;（注意：每个 BINARY/NCHAR 类型的列还会额外占用 2 个字节的存储位置）
4. 子表名只能由字母、数字和下划线组成，且不能以数字开头，不区分大小写
5. 使用数据类型 binary 或 nchar，需指定其最长的字节数，如 binary(20)，表示 20 字节；
6. 为了兼容支持更多形式的表名，TDengine 引入新的转义符 "\`"，可以让表名与关键词不冲突，同时不受限于上述表名称合法性约束检查。但是同样具有长度限制要求。使用转义字符以后，不再对转义字符中的内容进行大小写统一。 例如：\`aBc\` 和 \`abc\` 是不同的表名，但是 abc 和 aBc 是相同的表名。 需要注意的是转义字符中的内容必须是可打印字符。

**参数说明**

1. COMMENT：表注释。可用于超级表、子表和普通表。
2. WATERMARK：指定窗口的关闭时间，默认值为 5 秒，最小单位毫秒，范围为 0 到 15 分钟，多个以逗号分隔。只可用于超级表，且只有当数据库使用了 [RETENTIONS](#RETENTIONS) 参数时，才可以使用此表参数。
3. MAX_DELAY：用于控制推送计算结果的最大延迟，默认值为 interval 的值(但不能超过最大值)，最小单位毫秒，范围为 1 毫秒到 15 分钟，多个以逗号分隔。注：不建议 MAX_DELAY 设置太小，否则会过于频繁的推送结果，影响存储和查询性能，如无特殊需求，取默认值即可。只可用于超级表，且只有当数据库使用了 RETENTIONS 参数时，才可以使用此表参数。
4. ROLLUP：Rollup 指定的聚合函数，提供基于多层级的降采样聚合结果。只可用于超级表。只有当数据库使用了 RETENTIONS 参数时，才可以使用此表参数。作用于超级表除 TS 列外的其它所有列，但是只能定义一个聚合函数。 聚合函数支持 avg, sum, min, max, last, first。
5. SMA：Small Materialized Aggregates，提供基于数据块的自定义预计算功能。预计算类型包括 MAX、MIN 和 SUM。可用于超级表/普通表。
6. TTL：Time to Live，是用户用来指定表的生命周期的参数。如果创建表时指定了这个参数，当该表的存在时间超过 TTL 指定的时间后，TDengine 自动删除该表。这个 TTL 的时间只是一个大概时间，系统不保证到了时间一定会将其删除，而只保证存在这样一个机制且最终一定会删除。TTL 单位是天，默认为 0，表示不限制，到期时间为表创建时间加上 TTL 时间。TTL 与数据库 KEEP 参数没有关联，如果 KEEP 比 TTL 小，在表被删除之前数据也可能已经被删除。

### [创建子表](https://docs.taosdata.com/taos-sql/table/#创建子表)

#### [创建子表](https://docs.taosdata.com/taos-sql/table/#创建子表-1)

```sql
CREATE TABLE [IF NOT EXISTS] tb_name USING stb_name TAGS (tag_value1, ...);
```

#### [创建子表并指定标签的值](https://docs.taosdata.com/taos-sql/table/#创建子表并指定标签的值)

```sql
CREATE TABLE [IF NOT EXISTS] tb_name USING stb_name (tag_name1, ...) TAGS (tag_value1, ...);
```

以指定的超级表为模板，也可以指定一部分 TAGS 列的值来创建数据表（没被指定的 TAGS 列会设为空值）。

#### [批量创建子表](https://docs.taosdata.com/taos-sql/table/#批量创建子表)

```sql
CREATE TABLE [IF NOT EXISTS] tb_name1 USING stb_name TAGS (tag_value1, ...) [IF NOT EXISTS] tb_name2 USING stb_name TAGS (tag_value2, ...) ...;
```

批量建表方式要求数据表必须以超级表为模板。 在不超出 SQL 语句长度限制的前提下，单条语句中的建表数量建议控制在 1000 ～ 3000 之间，将会获得比较理想的建表速度。

### [修改普通表](https://docs.taosdata.com/taos-sql/table/#修改普通表)

```sql
ALTER TABLE [db_name.]tb_name alter_table_clause

alter_table_clause: {
    alter_table_options
  | ADD COLUMN col_name column_type
  | DROP COLUMN col_name
  | MODIFY COLUMN col_name column_type
  | RENAME COLUMN old_col_name new_col_name
}

alter_table_options:
    alter_table_option ...

alter_table_option: {
    TTL value
  | COMMENT 'string_value'
}
```

**使用说明** 对普通表可以进行如下修改操作

1. ADD COLUMN：添加列。
2. DROP COLUMN：删除列。
3. MODIFY COLUMN：修改列定义，如果数据列的类型是可变长类型，那么可以使用此指令修改其宽度，只能改大，不能改小。
4. RENAME COLUMN：修改列名称。

#### [增加列](https://docs.taosdata.com/taos-sql/table/#增加列)

```sql
ALTER TABLE tb_name ADD COLUMN field_name data_type;
```

#### [删除列](https://docs.taosdata.com/taos-sql/table/#删除列)

```sql
ALTER TABLE tb_name DROP COLUMN field_name;
```

#### [修改列宽](https://docs.taosdata.com/taos-sql/table/#修改列宽)

```sql
ALTER TABLE tb_name MODIFY COLUMN field_name data_type(length);
```

#### [修改列名](https://docs.taosdata.com/taos-sql/table/#修改列名)

```sql
ALTER TABLE tb_name RENAME COLUMN old_col_name new_col_name
```

### [修改子表](https://docs.taosdata.com/taos-sql/table/#修改子表)

```sql
ALTER TABLE [db_name.]tb_name alter_table_clause

alter_table_clause: {
    alter_table_options
  | SET TAG tag_name = new_tag_value
}

alter_table_options:
    alter_table_option ...

alter_table_option: {
    TTL value
  | COMMENT 'string_value'
}
```

**使用说明**

1. 对子表的列和标签的修改，除了更改标签值以外，都要通过超级表才能进行。

#### [修改子表标签值](https://docs.taosdata.com/taos-sql/table/#修改子表标签值)

```text
ALTER TABLE tb_name SET TAG tag_name=new_tag_value;
```

### [删除表](https://docs.taosdata.com/taos-sql/table/#删除表)

可以在一条 SQL 语句中删除一个或多个普通表或子表。

```sql
DROP TABLE [IF EXISTS] [db_name.]tb_name [, [IF EXISTS] [db_name.]tb_name] ...
```

### [查看表的信息](https://docs.taosdata.com/taos-sql/table/#查看表的信息)

#### [显示所有表](https://docs.taosdata.com/taos-sql/table/#显示所有表)

如下 SQL 语句可以列出当前数据库中的所有表名。

```sql
SHOW TABLES [LIKE tb_name_wildchar];
```

#### [显示表创建语句](https://docs.taosdata.com/taos-sql/table/#显示表创建语句)

```text
SHOW CREATE TABLE tb_name;
```

常用于数据库迁移。对一个已经存在的数据表，返回其创建语句；在另一个集群中执行该语句，就能得到一个结构完全相同的数据表。

#### [获取表结构信息](https://docs.taosdata.com/taos-sql/table/#获取表结构信息)

```text
DESCRIBE [db_name.]tb_name;
```

## 超级表

### 创建超级表

```sql
CREATE STABLE [IF NOT EXISTS] stb_name (create_definition [, create_definition] ...) TAGS (create_definition [, create_definition] ...) [table_options]
 
create_definition:
    col_name column_definition
 
column_definition:
    type_name
```

**使用说明**

- 超级表中列的最大个数为 4096，需要注意，这里的 4096 是包含 TAG 列在内的，最小个数为 3，包含一个时间戳主键、一个 TAG 列和一个数据列。
- TAGS语法指定超级表的标签列，标签列需要遵循以下约定：
  - TAGS 中的 TIMESTAMP 列写入数据时需要提供给定值，而暂不支持四则运算，例如 NOW + 10s 这类表达式。
  - TAGS 列名不能与其他列名相同。
  - TAGS 列名不能为预留关键字。
  - TAGS 最多允许 128 个，至少 1 个，总长度不超过 16 KB。
- 关于表参数的详细说明，参见 CREATE TABLE 中的介绍。

### 查看超级表

#### 显示当前数据库下的所有超级表信息

```text
SHOW STABLES [LIKE tb_name_wildcard];
```

查看数据库内全部超级表。

#### 显示一个超级表的创建语句

```text
SHOW CREATE STABLE stb_name;
```

常用于数据库迁移。对一个已经存在的超级表，返回其创建语句；在另一个集群中执行该语句，就能得到一个结构完全相同的超级表。

#### 获取超级表的结构信息

```text
DESCRIBE [db_name.]stb_name;
```

#### 获取超级表中所有子表的标签信息

```text
taos> SHOW TABLE TAGS FROM st1;
             tbname             |     id      |         loc          |
======================================================================
 st1s1                          |           1 | beijing              |
 st1s2                          |           2 | shanghai             |
 st1s3                          |           3 | guangzhou            |
Query OK, 3 rows in database (0.004455s)
```

返回结果集的第一列为子表名，后续列为标签列。

如果已经知道标签列的名称，可以使用下面的语句来获取指定标签列的值。

```text
taos> SELECT DISTINCT TBNAME, id FROM st1;
             tbname             |     id      |
===============================================
 st1s1                          |           1 |
 st1s2                          |           2 |
 st1s3                          |           3 |
Query OK, 3 rows in database (0.002891s)
```

需要注意，SELECT 语句中的 DISTINCT 和 TBNAME 都是必不可少的，TDengine 会根据它们对语句进行优化，使之在没有数据或数据非常多的情况下都可以正确并快速的返回标签值。

#### 获取某个子表的标签信息

```text
taos> SHOW TAGS FROM st1s1;
   table_name    |     db_name     |   stable_name   |    tag_name     |    tag_type     |    tag_value    |
============================================================================================================
 st1s1           | test            | st1             | id              | INT             | 1               |
 st1s1           | test            | st1             | loc             | VARCHAR(20)     | beijing         |
Query OK, 2 rows in database (0.003684s)
```

同样的，也可以用 SELECT 语句来查询指定标签列的值。

```text
taos> SELECT DISTINCT TBNAME, id, loc FROM st1s1;
     tbname      |     id      |       loc       |
==================================================
 st1s1           |           1 | beijing         |
Query OK, 1 rows in database (0.001884s)
```

### 删除超级表

```text
DROP STABLE [IF EXISTS] [db_name.]stb_name
```

删除 STable 会自动删除通过 STable 创建的子表以及子表中的所有数据。

### 修改超级表

```sql
ALTER STABLE [db_name.]tb_name alter_table_clause
 
alter_table_clause: {
    alter_table_options
  | ADD COLUMN col_name column_type
  | DROP COLUMN col_name
  | MODIFY COLUMN col_name column_type
  | ADD TAG tag_name tag_type
  | DROP TAG tag_name
  | MODIFY TAG tag_name tag_type
  | RENAME TAG old_tag_name new_tag_name
}
 
alter_table_options:
    alter_table_option ...
 
alter_table_option: {
    COMMENT 'string_value'
}
```

**使用说明**

修改超级表的结构会对其下的所有子表生效。无法针对某个特定子表修改表结构。标签结构的修改需要对超级表下发，TDengine 会自动作用于此超级表的所有子表。

- ADD COLUMN：添加列。
- DROP COLUMN：删除列。
- MODIFY COLUMN：修改列的宽度，数据列的类型必须是 nchar 和 binary，使用此指令可以修改其宽度，只能改大，不能改小。
- ADD TAG：给超级表添加一个标签。
- DROP TAG：删除超级表的一个标签。从超级表删除某个标签后，该超级表下的所有子表也会自动删除该标签。
- MODIFY TAG：修改超级表的一个标签的列宽度。标签的类型只能是 nchar 和 binary，使用此指令可以修改其宽度，只能改大，不能改小。
- RENAME TAG：修改超级表的一个标签的名称。从超级表修改某个标签名后，该超级表下的所有子表也会自动更新该标签名。

#### 增加列

```text
ALTER STABLE stb_name ADD COLUMN col_name column_type;
```

#### 删除列

```text
ALTER STABLE stb_name DROP COLUMN col_name;
```

#### 修改列宽

```text
ALTER STABLE stb_name MODIFY COLUMN col_name data_type(length);
```

如果数据列的类型是可变长格式（BINARY 或 NCHAR），那么可以使用此指令修改其宽度（只能改大，不能改小）。

#### 添加标签

```text
ALTER STABLE stb_name ADD TAG tag_name tag_type;
```

为 STable 增加一个新的标签，并指定新标签的类型。标签总数不能超过 128 个，总长度不超过 16KB 。

#### 删除标签

```text
ALTER STABLE stb_name DROP TAG tag_name;
```

删除超级表的一个标签，从超级表删除某个标签后，该超级表下的所有子表也会自动删除该标签。

#### 修改标签名

```text
ALTER STABLE stb_name RENAME TAG old_tag_name new_tag_name;
```

修改超级表的标签名，从超级表修改某个标签名后，该超级表下的所有子表也会自动更新该标签名。

#### 修改标签列宽度

```text
ALTER STABLE stb_name MODIFY TAG tag_name data_type(length);
```

如果标签的类型是可变长格式（BINARY 或 NCHAR），那么可以使用此指令修改其宽度（只能改大，不能改小）。（2.1.3.0 版本新增）

#### 超级表查询

使用 SELECT 语句可以完成在超级表上的投影及聚合两类查询，在 WHERE 语句中可以对标签及列进行筛选及过滤。

如果在超级表查询语句中不加 ORDER BY, 返回顺序是先返回一个子表的所有数据，然后再返回下个子表的所有数据，所以返回的数据是无序的。如果增加了 ORDER BY 语句，会严格按 ORDER BY 语句指定的顺序返回的。

##### note

除了更新标签的值的操作是针对子表进行，其他所有的标签操作（添加标签、删除标签等）均只能作用于 STable，不能对单个子表操作。对 STable 添加标签以后，依托于该 STable 建立的所有表将自动增加了一个标签，所有新增标签的默认值都是 NULL。



## 数据写入

### 写入语法

```sql
INSERT INTO
    tb_name
        [USING stb_name [(tag1_name, ...)] TAGS (tag1_value, ...)]
        [(field1_name, ...)]
        VALUES (field1_value, ...) [(field1_value2, ...) ...] | FILE csv_file_path
    [tb2_name
        [USING stb_name [(tag1_name, ...)] TAGS (tag1_value, ...)]
        [(field1_name, ...)]
        VALUES (field1_value, ...) [(field1_value2, ...) ...] | FILE csv_file_path
    ...];

INSERT INTO tb_name [(field1_name, ...)] subquery
```

**关于时间戳**

1. TDengine 要求插入的数据必须要有时间戳，插入数据的时间戳要注意以下几点：
2. 时间戳不同的格式语法会有不同的精度影响。字符串格式的时间戳写法不受所在 DATABASE 的时间精度设置影响；而长整形格式的时间戳写法会受到所在 DATABASE  的时间精度设置影响。例如，时间戳"2021-07-13 16:16:48"的 UNIX 秒数为 1626164208。则其在毫秒精度下需要写作  1626164208000，在微秒精度设置下就需要写为 1626164208000000，纳秒精度设置下需要写为  1626164208000000000。
3. 一次插入多行数据时，不要把首列的时间戳的值都写  NOW。否则会导致语句中的多条记录使用相同的时间戳，于是就可能出现相互覆盖以致这些数据行无法全部被正确保存。其原因在于，NOW  函数在执行中会被解析为所在 SQL 语句的客户端执行时间，出现在同一语句中的多个 NOW 标记也就会被替换为完全相同的时间戳取值。 允许插入的最老记录的时间戳，是相对于当前服务器时间，减去配置的 KEEP 值（数据保留的天数, 可以在创建数据库时指定，缺省值是 3650  天）。允许插入的最新记录的时间戳，取决于数据库的 PRECISION 值（时间戳精度, 可以在创建数据库时指定, ms 表示毫秒，us  表示微秒，ns 表示纳秒，默认毫秒）：如果是毫秒或微秒, 取值为 1970 年 1 月 1 日 00:00:00.000 UTC 加上 1000 年, 即 2970 年 1 月 1 日 00:00:00.000 UTC; 如果是纳秒, 取值为 1970 年 1 月 1 日  00:00:00.000000000 UTC 加上 292 年, 即 2262 年 1 月 1 日 00:00:00.000000000  UTC。

**语法说明**

1. USING  子句是自动建表语法。如果用户在写数据时并不确定某个表是否存在，此时可以在写入数据时使用自动建表语法来创建不存在的表，若该表已存在则不会建立新表。自动建表时，要求必须以超级表为模板，并写明数据表的 TAGS 取值。可以只是指定部分 TAGS 列的取值，未被指定的 TAGS 列将置为 NULL。

2. 可以指定要插入值的列，对于为指定的列数据库将自动填充为 NULL。

3. VALUES 语法表示了要插入的一行或多行数据。

4. FILE 语法表示数据来自于 CSV 文件（英文逗号分隔、英文单引号括住每个值），CSV 文件无需表头。

5. `INSERT ... VALUES` 语句和 `INSERT ... FILE` 语句均可以在一条 INSERT 语句中同时向多个表插入数据。

6. INSERT 语句是完整解析后再执行的，对如下语句，不会再出现数据错误但建表成功的情况：

   ```sql
   INSERT INTO d1001 USING meters TAGS('Beijing.Chaoyang', 2) VALUES('a');
   ```

1. 对于向多个子表插入数据的情况，依然会有部分数据写入失败，部分数据写入成功的情况。这是因为多个子表可能分布在不同的 VNODE 上，客户端将 INSERT 语句完整解析后，将数据发往各个涉及的 VNODE 上，每个 VNODE 独立进行写入操作。如果某个  VNODE 因为某些原因（比如网络问题或磁盘故障）导致写入失败，并不会影响其他 VNODE 节点的写入。
2. 可以使用 `INSERT ... subquery` 语句将 TDengine 中的数据插入到指定表中。subquery 可以是任意的查询语句。此语法只能用于子表和普通表，且不支持自动建表。

### 插入一条记录

指定已经创建好的数据子表的表名，并通过 VALUES 关键字提供一行或多行数据，即可向数据库写入这些数据。例如，执行如下语句可以写入一行记录：

```sql
INSERT INTO d1001 VALUES (NOW, 10.2, 219, 0.32);
```

### 插入多条记录

或者，可以通过如下语句写入两行记录：

```sql
INSERT INTO d1001 VALUES ('2021-07-13 14:06:32.272', 10.2, 219, 0.32) (1626164208000, 10.15, 217, 0.33);
```

### 指定列插入

向数据子表中插入记录时，无论插入一行还是多行，都可以让数据对应到指定的列。对于 SQL 语句中没有出现的列，数据库将自动填充为 NULL。主键（时间戳）不能为 NULL。例如：

```sql
INSERT INTO d1001 (ts, current, phase) VALUES ('2021-07-13 14:06:33.196', 10.27, 0.31);
```

### 向多个表插入记录

可以在一条语句中，分别向多个表插入一条或多条记录，并且也可以在插入过程中指定列。例如：

```sql
INSERT INTO d1001 VALUES ('2021-07-13 14:06:34.630', 10.2, 219, 0.32) ('2021-07-13 14:06:35.779', 10.15, 217, 0.33)
            d1002 (ts, current, phase) VALUES ('2021-07-13 14:06:34.255', 10.27, 0.31）;
```

### 插入记录时自动建表

如果用户在写数据时并不确定某个表是否存在，此时可以在写入数据时使用自动建表语法来创建不存在的表，若该表已存在则不会建立新表。**自动建表时，要求必须以超级表为模板，并写明数据表的 TAGS 取值**。例如：

```sql
INSERT INTO d21001 USING meters TAGS ('California.SanFrancisco', 2) VALUES ('2021-07-13 14:06:32.272', 10.2, 219, 0.32);
```

也可以在自动建表时，只是指定部分 TAGS 列的取值，未被指定的 TAGS 列将置为 NULL。例如：

```sql
INSERT INTO d21001 USING meters (groupId) TAGS (2) VALUES ('2021-07-13 14:06:33.196', 10.15, 217, 0.33);
```

自动建表语法也支持在一条语句中向多个表插入记录。例如：

```sql
INSERT INTO d21001 USING meters TAGS ('California.SanFrancisco', 2) VALUES ('2021-07-13 14:06:34.630', 10.2, 219, 0.32) ('2021-07-13 14:06:35.779', 10.15, 217, 0.33)
            d21002 USING meters (groupId) TAGS (2) VALUES ('2021-07-13 14:06:34.255', 10.15, 217, 0.33)
            d21003 USING meters (groupId) TAGS (2) (ts, current, phase) VALUES ('2021-07-13 14:06:34.255', 10.27, 0.31);
```

### 插入来自文件的数据记录

除了使用 VALUES 关键字插入一行或多行数据外，也可以把要写入的数据放在 CSV  文件中（英文逗号分隔、时间戳和字符串类型的值需要用英文单引号括住）供 SQL 指令读取。其中 CSV 文件无需表头。例如，如果  /tmp/csvfile.csv 文件的内容为：

```text
'2021-07-13 14:07:34.630', 10.2, 219, 0.32
'2021-07-13 14:07:35.779', 10.15, 217, 0.33
```

那么通过如下指令可以把这个文件中的数据写入子表中：

```sql
INSERT INTO d1001 FILE '/tmp/csvfile.csv';
```

### 插入来自文件的数据记录，并自动建表

```sql
INSERT INTO d21001 USING meters TAGS ('California.SanFrancisco', 2) FILE '/tmp/csvfile.csv';
```

也可以在一条语句中向多个表以自动建表的方式插入记录。例如：

```sql
INSERT INTO d21001 USING meters TAGS ('California.SanFrancisco', 2) FILE '/tmp/csvfile_21001.csv'
            d21002 USING meters (groupId) TAGS (2) FILE '/tmp/csvfile_21002.csv';
```

## 数据查询

### 查询语法

```sql
SELECT {DATABASE() | CLIENT_VERSION() | SERVER_VERSION() | SERVER_STATUS() | NOW() | TODAY() | TIMEZONE()}

SELECT [DISTINCT] select_list
    from_clause
    [WHERE condition]
    [partition_by_clause]
    [interp_clause]
    [window_clause]
    [group_by_clause]
    [order_by_clasue]
    [SLIMIT limit_val [SOFFSET offset_val]]
    [LIMIT limit_val [OFFSET offset_val]]
    [>> export_file]

select_list:
    select_expr [, select_expr] ...

select_expr: {
    *
  | query_name.*
  | [schema_name.] {table_name | view_name} .*
  | t_alias.*
  | expr [[AS] c_alias]
}

from_clause: {
    table_reference [, table_reference] ...
  | join_clause [, join_clause] ...
}

table_reference:
    table_expr t_alias

table_expr: {
    table_name
  | view_name
  | ( subquery )
}

join_clause:
    table_reference [INNER] JOIN table_reference ON condition

window_clause: {
    SESSION(ts_col, tol_val)
  | STATE_WINDOW(col)
  | INTERVAL(interval_val [, interval_offset]) [SLIDING (sliding_val)] [WATERMARK(watermark_val)] [FILL(fill_mod_and_val)]

interp_clause:
    RANGE(ts_val, ts_val) EVERY(every_val) FILL(fill_mod_and_val)

partition_by_clause:
    PARTITION BY expr [, expr] ...

group_by_clause:
    GROUP BY expr [, expr] ... HAVING condition

order_by_clasue:
    ORDER BY order_expr [, order_expr] ...

order_expr:
    {expr | position | c_alias} [DESC | ASC] [NULLS FIRST | NULLS LAST]
```

### 列表

查询语句可以指定部分或全部列作为返回结果。数据列和标签列都可以出现在列表中。

#### 通配符

通配符 * 可以用于代指全部列。**对于普通表和子表，结果中只有普通列**。**对于超级表，还包含了 TAG 列。**

```sql
SELECT * FROM d1001;
```

通配符支持表名前缀，以下两个 SQL 语句均为返回全部的列：

```sql
SELECT * FROM d1001;
SELECT d1001.* FROM d1001;
```

在 JOIN 查询中，带表名前缀的\*和不带前缀*返回的结果有差别， *返回全部表的所有列数据（不包含标签），而带表名前缀的通配符，则只返回该表的列数据。

```sql
SELECT * FROM d1001, d1003 WHERE d1001.ts=d1003.ts;
SELECT d1001.* FROM d1001,d1003 WHERE d1001.ts = d1003.ts;
```

上面的查询语句中，前者返回 d1001 和 d1003 的全部列，而后者仅返回 d1001 的全部列。

在使用 SQL 函数来进行查询的过程中，部分 SQL 函数支持通配符操作。其中的区别在于： `count(*)`函数只返回一列。`first`、`last`、`last_row`函数则是返回全部列。

#### 标签列

在超级表和子表的查询中可以指定 *标签列*，且标签列的值会与普通列的数据一起返回。

```sql
SELECT location, groupid, current FROM d1001 LIMIT 2;
```

#### 结果去重

`DISTINCT` 关键字可以对结果集中的一列或多列进行去重，去除的列既可以是标签列也可以是数据列。

对标签列去重：

```sql
SELECT DISTINCT tag_name [, tag_name ...] FROM stb_name;
```

对数据列去重：

```sql
SELECT DISTINCT col_name [, col_name ...] FROM tb_name
```

##### info

1. cfg 文件中的配置参数 maxNumOfDistinctRes 将对 DISTINCT 能够输出的数据行数进行限制。其最小值是  100000，最大值是 100000000，默认值是 10000000。如果实际计算结果超出了这个限制，那么会仅输出这个数量范围内的部分。
2. 由于浮点数天然的精度机制原因，在特定情况下，对 FLOAT 和 DOUBLE 列使用 DISTINCT 并不能保证输出值的完全唯一性。

### 结果集列名

`SELECT`子句中，如果不指定返回结果集合的列名，结果集列名称默认使用`SELECT`子句中的表达式名称作为列名称。此外，用户可使用`AS`来重命名返回结果集合中列的名称。例如：

```sql
taos> SELECT ts, ts AS primary_key_ts FROM d1001;
```

但是针对`first(*)`、`last(*)`、`last_row(*)`不支持针对单列的重命名。

### 伪列

**伪列**: 伪列的行为表现与普通数据列相似但其并不实际存储在表中。可以查询伪列，但不能对其做插入、更新和删除的操作。伪列有点像没有参数的函数。下面介绍是可用的伪列：

**TBNAME** `TBNAME` 可以视为超级表中一个特殊的标签，代表子表的表名。

获取一个超级表所有的子表名及相关的标签信息：

```mysql
SELECT DISTINCT TBNAME, location FROM meters;
```

建议用户使用 INFORMATION_SCHEMA 下的 INS_TAGS 系统表来查询超级表的子表标签信息，例如获取超级表 meters 所有的子表名和标签值：

```mysql
SELECT table_name, tag_name, tag_type, tag_value FROM information_schema.ins_tags WHERE stable_name='meters';
```

统计超级表下辖子表数量：

```mysql
SELECT COUNT(*) FROM (SELECT DISTINCT TBNAME FROM meters);
```

以上两个查询均只支持在 WHERE 条件子句中添加针对标签（TAGS）的过滤条件。例如：

\_QSTART/\_QEND

\_qstart 和\_qend 表示用户输入的查询时间范围，即 WHERE 子句中主键时间戳条件所限定的时间范围。如果 WHERE 子句中没有有效的主键时间戳条件，则时间范围为[-2^63, 2^63-1]。

\_qstart 和\_qend 不能用于 WHERE 子句中。

**\_WSTART/\_WEND/\_WDURATION**\ _wstart 伪列、\_wend 伪列和\_wduration 伪列 _wstart 表示窗口起始时间戳，\_wend 表示窗口结束时间戳，\_wduration 表示窗口持续时长。

这三个伪列只能用于时间窗口的窗口切分查询之中，且要在窗口切分子句之后出现。

**\_c0/\_ROWTS**

TDengine 中，所有表的第一列都必须是时间戳类型，且为其主键，\_rowts 伪列和\_c0 伪列均代表了此列的值。相比实际的主键时间戳列，使用伪列更加灵活，语义也更加标准。例如，可以和 max\min 等函数一起使用。

```sql
select _rowts, max(current) from meters;
```

**_IROWTS**

_irowts 伪列只能与 interp 函数一起使用，用于返回 interp 函数插值结果对应的时间戳列。

```sql
select _irowts, interp(current) from meters range('2020-01-01 10:00:00', '2020-01-01 10:30:00') every(1s) fill(linear);
```

### 查询对象

FROM 关键字后面可以是若干个表（超级表）列表，也可以是子查询的结果。 如果没有指定用户的当前数据库，可以在表名称之前使用数据库的名称来指定表所属的数据库。例如：`power.d1001` 方式来跨库使用表。

TDengine 支持基于时间戳主键的 INNER JOIN，规则如下：

1. 支持 FROM 表列表和显式的 JOIN 子句两种语法。
2. 对于普通表和子表，ON 条件必须有且只有时间戳主键的等值条件。
3. 对于超级表，ON 条件在时间戳主键的等值条件之外，还要求有可以一一对应的标签列等值条件，不支持 OR 条件。
4. 参与 JOIN 计算的表只能是同一种类型，即只能都是超级表，或都是子表，或都是普通表。
5. JOIN 两侧均支持子查询。
6. 参与 JOIN 的表个数上限为 10 个。
7. 不支持与 FILL 子句混合使用。

### GROUP BY

如果在语句中同时指定了 GROUP BY 子句，那么 SELECT 列表只能包含如下表达式：

1. 常量
2. 聚集函数
3. 与 GROUP BY 后表达式相同的表达式。
4. 包含前面表达式的表达式

GROUP BY 子句对每行数据按 GROUP BY 后的表达式的值进行分组，并为每个组返回一行汇总信息。

GROUP BY 子句中的表达式可以包含表或视图中的任何列，这些列不需要出现在 SELECT 列表中。

该子句对行进行分组，但不保证结果集的顺序。若要对分组进行排序，请使用 ORDER BY 子句

### PARTITION BY

PARTITION BY 子句是 TDengine 特色语法，按 part_list 对数据进行切分，在每个切分的分片中进行计算。

详见 [TDengine 特色查询](https://docs.taosdata.com/taos-sql/distinguished/)

### ORDER BY

ORDER BY 子句对结果集**排序**。如果**没有指定 ORDER BY，无法保证同一语句多次查询的结果集返回顺序一致**。

ORDER BY 后可以使用位置语法，位置标识为正整数，从 1 开始，表示使用 SELECT 列表的第几个表达式进行排序。

ASC 表示升序，DESC 表示降序。

NULLS 语法用来指定 NULL 值在排序中输出的位置。NULLS LAST 是升序的默认值，NULLS FIRST 是降序的默认值。

### LIMIT

LIMIT 控制输出条数，OFFSET 指定从第几条之后开始输出。LIMIT/OFFSET 对结果集的执行顺序在 ORDER BY 之后。LIMIT 5 OFFSET 2 可以简写为 LIMIT 2, 5，都输出第 3 行到第 7 行数据。

在有 PARTITION BY/GROUP BY 子句时，LIMIT 控制的是每个切分的分片中的输出，而不是总的结果集输出。

### SLIMIT

SLIMIT 和 PARTITION BY/GROUP BY 子句一起使用，用来控制输出的分片的数量。SLIMIT 5 SOFFSET 2 可以简写为 SLIMIT 2, 5，都表示输出第 3 个到第 7 个分片。

需要注意，如果有 ORDER BY 子句，则输出只有一个分片。

### 特殊功能

部分特殊的查询功能可以不使用 FROM 子句执行。

#### 获取当前数据库

下面的命令可以获取当前所在的数据库 database()，如果登录的时候没有指定默认数据库，且没有使用`USE`命令切换数据，则返回 NULL。

```sql
SELECT DATABASE();
```

#### 获取服务器和客户端版本号

```sql
SELECT CLIENT_VERSION();
SELECT SERVER_VERSION();
```

#### 获取服务器状态

服务器状态检测语句。如果服务器正常，返回一个数字（例如 1）。如果服务器异常，返回 error code。该 SQL 语法能兼容连接池对于 TDengine  状态的检查及第三方工具对于数据库服务器状态的检查。并可以避免出现使用了错误的心跳检测 SQL 语句导致的连接池连接丢失的问题。

```sql
SELECT SERVER_STATUS();
```

#### 获取当前时间

```sql
SELECT NOW();
```

#### 获取当前日期

```sql
SELECT TODAY();
```

#### 获取当前时区

```sql
SELECT TIMEZONE();
```

### 正则表达式过滤

#### 语法

```txt
WHERE (column|tbname) match/MATCH/nmatch/NMATCH _regex_
```

#### 正则表达式规范

确保使用的正则表达式符合 POSIX 的规范，具体规范内容可参见[Regular Expressions](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap09.html)

#### 使用限制

只能针对表名（即 tbname 筛选）、binary/nchar 类型标签值进行正则表达式过滤，不支持普通列的过滤。

正则匹配字符串长度不能超过 128 字节。可以通过参数 *maxRegexStringLen* 设置和调整最大允许的正则匹配字符串，该参数是客户端配置参数，需要重启才能生效。

### CASE 表达式

#### 语法

```txt
CASE value WHEN compare_value THEN result [WHEN compare_value THEN result ...] [ELSE result] END
CASE WHEN condition THEN result [WHEN condition THEN result ...] [ELSE result] END
```

#### 说明

TDengine 通过 CASE 表达式让用户可以在 SQL 语句中使用 IF ... THEN ... ELSE 逻辑。

第一种 CASE 语法返回第一个 value 等于 compare_value 的 result，如果没有 compare_value 符合，则返回 ELSE 之后的 result，如果没有 ELSE 部分，则返回 NULL。

第二种语法返回第一个 condition 为真的 result。 如果没有 condition 符合，则返回 ELSE 之后的 result，如果没有 ELSE 部分，则返回 NULL。

CASE 表达式的返回类型为第一个 WHEN THEN 部分的 result 类型，其余 WHEN THEN 部分和 ELSE 部分，result 类型都需要可以向其转换，否则 TDengine 会报错。

#### 示例

某设备有三个状态码，显示其状态，语句如下：

```sql
SELECT CASE dev_status WHEN 1 THEN 'Running' WHEN 2 THEN 'Warning' WHEN 3 THEN 'Downtime' ELSE 'Unknown' END FROM dev_table;
```

统计智能电表的电压平均值，当电压小于 200 或大于 250 时认为是统计有误，修正其值为 220，语句如下：

```sql
SELECT AVG(CASE WHEN voltage < 200 or voltage > 250 THEN 220 ELSE voltage END) FROM meters;
```

### JOIN 子句

**TDengine 支持基于时间戳主键的内连接**，即 **JOIN 条件必须包含时间戳主键**。只要满足基于时间戳主键这个要求，普通表、子表、超级表和子查询之间可以随意的进行内连接，且对表个数没有限制。

普通表与普通表之间的 JOIN 操作：

```sql
SELECT *
FROM temp_tb_1 t1, pressure_tb_1 t2
WHERE t1.ts = t2.ts
```

超级表与超级表之间的 JOIN 操作：

```sql
SELECT *
FROM temp_stable t1, temp_stable t2
WHERE t1.ts = t2.ts AND t1.deviceid = t2.deviceid AND t1.status=0;
```

子表与超级表之间的 JOIN 操作：

```sql
SELECT *
FROM temp_ctable t1, temp_stable t2
WHERE t1.ts = t2.ts AND t1.deviceid = t2.deviceid AND t1.status=0;
```

类似地，也可以对多个子查询的查询结果进行 JOIN 操作。

### 嵌套查询

“嵌套查询”又称为“子查询”，也即在一条 SQL 语句中，“内层查询”的计算结果可以作为“外层查询”的计算对象来使用。

从 2.2.0.0 版本开始，TDengine 的查询引擎开始支持在 FROM  子句中使用非关联子查询（“非关联”的意思是，子查询不会用到父查询中的参数）。也即在普通 SELECT 语句的 tb_name_list  位置，用一个独立的 SELECT 语句来代替（这一 SELECT 语句被包含在英文圆括号内），于是完整的嵌套查询 SQL 语句形如：

```text
SELECT ... FROM (SELECT ... FROM ...) ...;
```

##### info

- 内层查询的返回结果将作为“虚拟表”供外层查询使用，此虚拟表建议起别名，以便于外层查询中方便引用。
- 在内层和外层查询中，都支持普通的表间/超级表间 JOIN。内层查询的计算结果也可以再参与数据子表的 JOIN 操作。
- 内层查询支持的功能特性与非嵌套的查询语句能力是一致的。
  - 内层查询的 ORDER BY 子句一般没有意义，建议避免这样的写法以免无谓的资源消耗。
- 与非嵌套的查询语句相比，外层查询所能支持的功能特性存在如下限制：
  - 计算函数部分：
    - 如果内层查询的结果数据未提供时间戳，那么计算过程隐式依赖时间戳的函数在外层会无法正常工作。例如：INTERP, DERIVATIVE, IRATE, LAST_ROW, FIRST, LAST, TWA, STATEDURATION, TAIL,  UNIQUE。
    - 如果内层查询的结果数据不是按时间戳有序，那么计算过程依赖数据按时间有序的函数在外层会无法正常工作。例如：LEASTSQUARES, ELAPSED, INTERP, DERIVATIVE, IRATE, TWA, DIFF, STATECOUNT,  STATEDURATION, CSUM, MAVG, TAIL, UNIQUE。
    - 计算过程需要两遍扫描的函数，在外层查询中无法正常工作。例如：此类函数包括：PERCENTILE。

### UNION ALL 子句

语法

```txt
SELECT ...
UNION ALL SELECT ...
[UNION ALL SELECT ...]
```

TDengine 支持 UNION ALL 操作符。也就是说，如果多个 SELECT 子句返回结果集的**结构**完全相同（列名、列类型、列数、顺序），那么可以通过  UNION ALL 把这些结果集合并到一起。目前只支持 UNION ALL 模式，也即在结果集的合并过程中是不去重的。在同一个 sql  语句中，UNION ALL 最多支持 100 个。

### SQL 示例

对于下面的例子，表 tb1 用以下语句创建：

```text
CREATE TABLE tb1 (ts TIMESTAMP, col1 INT, col2 FLOAT, col3 BINARY(50));
```

查询 tb1 刚过去的一个小时的所有记录：

```text
SELECT * FROM tb1 WHERE ts >= NOW - 1h;
```

查询表 tb1 从 2018-06-01 08:00:00.000 到 2018-06-02 08:00:00.000 时间范围，并且 col3 的字符串是'nny'结尾的记录，结果按照时间戳降序：

```text
SELECT * FROM tb1 WHERE ts > '2018-06-01 08:00:00.000' AND ts <= '2018-06-02 08:00:00.000' AND col3 LIKE '%nny' ORDER BY ts DESC;
```

查询 col1 与 col2 的和，并取名 complex, 时间大于 2018-06-01 08:00:00.000, col2 大于 1.2，结果输出仅仅 10 条记录，从第 5 条开始：

```text
SELECT (col1 + col2) AS 'complex' FROM tb1 WHERE ts > '2018-06-01 08:00:00.000' AND col2 > 1.2 LIMIT 10 OFFSET 5;
```

查询过去 10 分钟的记录，col2 的值大于 3.14，并且将结果输出到文件 `/home/testoutput.csv`：

```text
SELECT COUNT(*) FROM tb1 WHERE ts >= NOW - 10m AND col2 > 3.14 >> /home/testoutput.csv;
```

## 标签索引

### 简介

在 **TDengine 3.0.3.0 版本之前**（不含），**默认在第一列 TAG 上建立索引**，但不支持给其它列动态添加索引。从 3.0.3.0  版本开始，可以动态地为其它 TAG 列添加索引。对于第一个 TAG  列上自动建立的索引，其在查询中默认生效，且用户无法对其进行任何干预。适当地使用索引能够有效地提升查询性能。

### 语法

创建索引的语法如下 

```sql
CREATE INDEX index_name ON tbl_name (tagColName）
```

其中 `index_name` 为索引名称， `tbl_name` 为**超级表名称**，`tagColName` 为要在其上建立索引的 tag 列的名称。`tagColName` 的类型不受限制，即任何类型的 tag 列都可以建立索引。

删除索引的语法如下

```sql
DROP INDEX index_name
```

其中 `index_name` 为已经建立的某个索引的名称，如果该索引不存在则该命令执行失败，但不会对系统产生任何其它影响。

查看系统中已经存在的索引

```sql
SELECT * FROM information_schema.INS_INDEXES 
```

也可以为上面的查询语句加上过滤条件以缩小查询范围。

### 使用说明

1. 索引使用得当能够提升数据过滤的效率，目前支持的过滤算子有 `=`, `>`, `>=`, `<`, `<=`。如果查询过滤条件中使用了这些算子，则索引能够明显提升查询效率。但如果查询过滤条件中使用的是其它算子，则索引起不到作用，查询效率没有变化。未来会逐步添加更多的算子。
2. 针对一个 tag 列只能建立一个索引，如果重复创建索引则会报错。
3. **每次只能针对一个 tag 列建立一个索引**，不能同时对多个 tag 建立索引。
4. 整个系统中不管是哪种类型的索引，其名称必须唯一。
5. 对索引个数没有限制，但每增加一个索引都会导致系统中的元数据增加，过多的索引会降低元数据存取的效率从而降低整个系统的性能。所以请尽量避免添加不必要的索引。
6. 不支持对普通和子表建立索引。
7. 如果某个 tag 列的唯一值较少时，不建议对其建立索引，这种情况下收效甚微。



## 删除数据

删除数据是 TDengine 提供的根据指定时间段删除指定表或超级表中数据记录的功能，方便用户清理由于设备故障等原因产生的异常数据。

**语法：**

```sql
DELETE FROM [ db_name. ] tb_name [WHERE condition];
```

**功能：** 删除指定表或超级表中的数据记录

**参数：**

- `db_name` ： 可选参数，指定要删除表所在的数据库名，不填写则在当前数据库中
- `tb_name` ： 必填参数，指定要删除数据的表名，可以是普通表、子表，也可以是超级表。
- `condition`： 可选参数，指定删除数据的过滤条件，不指定过滤条件则为表中所有数据，请慎重使用。特别说明，**这里的 where 条件中只支持对第一列时间列的过滤。** *无法根据其他的列删除数据*

**特别说明：**

数据删除后不可恢复，请慎重使用。为了确保删除的数据确实是自己要删除的，建议可以先使用 `select` 语句加 `where` 后的删除条件查看要删除的数据内容，确认无误后再执行 `delete` 命令。

**示例：**

`meters` 是一个超级表，`groupid` 是 int 类型的 tag 列，现在要删除 `meters` 表中时间小于 2021-10-01 10:40:00.100 的所有数据，sql 如下：

```sql
delete from meters where ts < '2021-10-01 10:40:00.100' ;
```

执行后显示结果为：

```text
Deleted 102000 row(s) from 1020 table(s) (0.421950s)
```

表示从 1020 个子表中共删除了 102000 行数据



## 函数

### 单行函数

单行函数为查询结果中的每一行返回一个结果行。

#### 数学函数

##### ABS

```sql
ABS(expr)
```

**功能说明**：获得指定字段的绝对值。

**返回结果类型**：与指定字段的原始数据类型一致。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### ACOS

```sql
ACOS(expr)
```

**功能说明**：获得指定字段的反余弦结果。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### ASIN

```sql
ASIN(expr)
```

**功能说明**：获得指定字段的反正弦结果。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### ATAN

```sql
ATAN(expr)
```

**功能说明**：获得指定字段的反正切结果。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### CEIL

```sql
CEIL(expr)
```

**功能说明**：获得指定字段的向上取整数的结果。

**返回结果类型**：与指定字段的原始数据类型一致。

**适用数据类型**：数值类型。

**适用于**: 表和超级表。

**嵌套子查询支持**：适用于内层查询和外层查询。

**使用说明**: 只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### COS

```sql
COS(expr)
```

**功能说明**：获得指定字段的余弦结果。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### FLOOR

```sql
FLOOR(expr)
```

**功能说明**：获得指定字段的向下取整数的结果。 其他使用说明参见 CEIL 函数描述。

##### LOG

```sql
LOG(expr1[, expr2])
```

**功能说明**：获得 expr1 对于底数 expr2 的对数。如果 expr2 参数省略，则返回指定字段的自然对数值。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### POW

```sql
POW(expr1, expr2)
```

**功能说明**：获得 expr1 的指数为 expr2 的幂。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### ROUND

```sql
ROUND(expr)
```

**功能说明**：获得指定字段的四舍五入的结果。 其他使用说明参见 CEIL 函数描述。

##### SIN

```sql
SIN(expr)
```

**功能说明**：获得指定字段的正弦结果。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### SQRT

```sql
SQRT(expr)
```

**功能说明**：获得指定字段的平方根。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

##### TAN

```sql
TAN(expr)
```

**功能说明**：获得指定字段的正切结果。

**返回结果类型**：DOUBLE。

**适用数据类型**：数值类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用。

#### 字符串函数

字符串函数的输入参数为字符串类型，返回结果为数值类型或字符串类型。

##### CHAR_LENGTH

```sql
CHAR_LENGTH(expr)
```

**功能说明**：以字符计数的字符串长度。

**返回结果类型**：BIGINT。

**适用数据类型**：VARCHAR, NCHAR。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

##### CONCAT

```sql
CONCAT(expr1, expr2 [, expr] ... )
```

**功能说明**：字符串连接函数。

**返回结果类型**：如果所有参数均为 VARCHAR 类型，则结果类型为 VARCHAR。如果参数包含NCHAR类型，则结果类型为NCHAR。如果参数包含NULL值，则输出值为NULL。

**适用数据类型**：VARCHAR, NCHAR。 该函数最小参数个数为2个，最大参数个数为8个。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

##### CONCAT_WS

```sql
CONCAT_WS(separator_expr, expr1, expr2 [, expr] ...)
```

**功能说明**：带分隔符的字符串连接函数。

**返回结果类型**：如果所有参数均为VARCHAR类型，则结果类型为VARCHAR。如果参数包含NCHAR类型，则结果类型为NCHAR。如果参数包含NULL值，则输出值为NULL。

**适用数据类型**：VARCHAR, NCHAR。 该函数最小参数个数为3个，最大参数个数为9个。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

##### LENGTH

```sql
LENGTH(expr)
```

**功能说明**：以字节计数的字符串长度。

**返回结果类型**：BIGINT。

**适用数据类型**：输入参数是 VARCHAR 类型或者 NCHAR 类型的字符串或者列。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

##### LOWER

```sql
LOWER(expr)
```

**功能说明**：将字符串参数值转换为全小写字母。

**返回结果类型**：与输入字段的原始类型相同。

**适用数据类型**：VARCHAR, NCHAR。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

##### LTRIM

```sql
LTRIM(expr)
```

**功能说明**：返回清除左边空格后的字符串。

**返回结果类型**：与输入字段的原始类型相同。

**适用数据类型**：VARCHAR, NCHAR。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

##### RTRIM

```sql
RTRIM(expr)
```

**功能说明**：返回清除右边空格后的字符串。

**返回结果类型**：与输入字段的原始类型相同。

**适用数据类型**：VARCHAR, NCHAR。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

##### SUBSTR

```sql
SUBSTR(expr, pos [,len])
```

**功能说明**：从源字符串 str 中的指定位置 pos 开始取一个长度为 len 的子串并返回。如果输入参数 len 被忽略，返回的子串包含从 pos 开始的整个字串。

**返回结果类型**：与输入字段的原始类型相同。

**适用数据类型**：VARCHAR, NCHAR。输入参数 pos 可以为正数，也可以为负数。如果 pos 是正数，表示开始位置从字符串开头正数计算。如果 pos 为负数，表示开始位置从字符串结尾倒数计算。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

#### UPPER

```sql
UPPER(expr)
```

**功能说明**：将字符串参数值转换为全大写字母。

**返回结果类型**：与输入字段的原始类型相同。

**适用数据类型**：VARCHAR, NCHAR。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

### 转换函数

转换函数将值从一种数据类型转换为另一种数据类型。

#### CAST

```sql
CAST(expr AS type_name)
```

**功能说明**：数据类型转换函数，返回 expr 转换为 type_name 指定的类型后的结果。只适用于 select 子句中。

**返回结果类型**：CAST 中指定的类型（type_name)。

**适用数据类型**：输入参数 expression 的类型可以是除JSON外的所有类型。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：

- 对于不能支持的类型转换会直接报错。
- 对于类型支持但某些值无法正确转换的情况，对应的转换后的值以转换函数输出为准。目前可能遇到的几种情况： 1）字符串类型转换数值类型时可能出现的无效字符情况，例如"a"可能转为0，但不会报错。 2）转换到数值类型时，数值大于type_name可表示的范围时，则会溢出，但不会报错。 3）转换到字符串类型时，如果转换后长度超过type_name中指定的长度，则会截断，但不会报错。

#### TO_ISO8601

```sql
TO_ISO8601(expr [, timezone])
```

**功能说明**：将 UNIX 时间戳转换成为 ISO8601 标准的日期时间格式，并附加时区信息。timezone 参数允许用户为输出结果指定附带任意时区信息。如果 timezone 参数省略，输出结果则附带当前客户端的系统时区信息。

**返回结果数据类型**：VARCHAR 类型。

**适用数据类型**：INTEGER, TIMESTAMP。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

**使用说明**：

- timezone 参数允许输入的时区格式为: [z/Z, +/-hhmm, +/-hh, +/-hh:mm]。例如，TO_ISO8601(1, "+00:00")。
- 如果输入是表示 UNIX 时间戳的整形，返回格式精度由时间戳的位数决定;
- 如果输入是 TIMESTAMP 类型的列，返回格式的时间戳精度与当前 DATABASE 设置的时间精度一致。

#### TO_JSON

```sql
TO_JSON(str_literal)
```

**功能说明**: 将字符串常量转换为 JSON 类型。

**返回结果数据类型**: JSON。

**适用数据类型**: JSON 字符串，形如 '{ "literal" : literal }'。'{}'表示空值。键必须为字符串字面量，值可以为数值字面量、字符串字面量、布尔字面量或空值字面量。str_literal中不支持转义符。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**: 表和超级表。

#### TO_UNIXTIMESTAMP

```sql
TO_UNIXTIMESTAMP(expr [, return_timestamp])

return_timestamp: {
    0
  | 1
}
```

**功能说明**：将日期时间格式的字符串转换成为 UNIX 时间戳。

**返回结果数据类型**：BIGINT, TIMESTAMP。

**应用字段**：VARCHAR, NCHAR。

**嵌套子查询支持**：适用于内层查询和外层查询。

**适用于**：表和超级表。

**使用说明**：

- 输入的日期时间字符串须符合 ISO8601/RFC3339 标准，无法转换的字符串格式将返回 NULL。
- 返回的时间戳精度与当前 DATABASE 设置的时间精度一致。
- return_timestamp 指定函数返回值是否为时间戳类型，设置为1时返回 TIMESTAMP 类型，设置为0时返回 BIGINT 类型。如不指定缺省返回 BIGINT 类型。

### 时间和日期函数

时间和日期函数对时间戳类型进行操作。

所有返回当前时间的函数，如NOW、TODAY和TIMEZONE，在一条SQL语句中不论出现多少次都只会被计算一次。

#### NOW

```sql
NOW()
```

**功能说明**：返回客户端当前系统时间。

**返回结果数据类型**：TIMESTAMP。

**应用字段**：在 WHERE 或 INSERT 语句中使用时只能作用于 TIMESTAMP 类型的字段。

**适用于**：表和超级表。

**嵌套子查询支持**：适用于内层查询和外层查询。

**使用说明**：

- 支持时间加减操作，如 NOW() + 1s, 支持的时间单位如下： b(纳秒)、u(微秒)、a(毫秒)、s(秒)、m(分)、h(小时)、d(天)、w(周)。
- 返回的时间戳精度与当前 DATABASE 设置的时间精度一致。

#### TIMEDIFF

```sql
TIMEDIFF(expr1, expr2 [, time_unit])
```

**功能说明**：计算两个时间戳之间的差值，并近似到时间单位 time_unit 指定的精度。

**返回结果数据类型**：BIGINT。

**应用字段**：表示 UNIX 时间戳的 BIGINT, TIMESTAMP 类型，或符合日期时间格式的 VARCHAR, NCHAR 类型。

**适用于**：表和超级表。

**嵌套子查询支持**：适用于内层查询和外层查询。

**使用说明**：

- 支持的时间单位 time_unit 如下： 1b(纳秒), 1u(微秒)，1a(毫秒)，1s(秒)，1m(分)，1h(小时)，1d(天), 1w(周)。
- 如果时间单位 time_unit 未指定， 返回的时间差值精度与当前 DATABASE 设置的时间精度一致。
- 输入包含不符合时间日期格式的字符串则返回 NULL。

#### TIMETRUNCATE

```sql
TIMETRUNCATE(expr, time_unit [, ignore_timezone])

ignore_timezone: {
    0
  | 1
}
```

**功能说明**：将时间戳按照指定时间单位 time_unit 进行截断。

**返回结果数据类型**：TIMESTAMP。

**应用字段**：表示 UNIX 时间戳的 BIGINT, TIMESTAMP 类型，或符合日期时间格式的 VARCHAR, NCHAR 类型。

**适用于**：表和超级表。

**使用说明**：

- 支持的时间单位 time_unit 如下： 1b(纳秒), 1u(微秒)，1a(毫秒)，1s(秒)，1m(分)，1h(小时)，1d(天), 1w(周)。
- 返回的时间戳精度与当前 DATABASE 设置的时间精度一致。
- 输入包含不符合时间日期格式的字符串则返回 NULL。
- 当使用 1d 作为时间单位对时间戳进行截断时， 可通过设置 ignore_timezone 参数指定返回结果的显示是否忽略客户端时区的影响。 例如客户端所配置时区为 UTC+0800, 则 TIMETRUNCATE('2020-01-01 23:00:00', 1d, 0) 返回结果为 '2020-01-01 08:00:00'。 而使用 TIMETRUNCATE('2020-01-01 23:00:00', 1d, 1) 设置忽略时区时，返回结果为 '2020-01-01 00:00:00' ignore_timezone 如果忽略的话，则默认值为 1 。

#### TIMEZONE

```sql
TIMEZONE()
```

**功能说明**：返回客户端当前时区信息。

**返回结果数据类型**：VARCHAR。

**应用字段**：无

**适用于**：表和超级表。

#### TODAY

```sql
TODAY()
```

**功能说明**：返回客户端当日零时的系统时间。

**返回结果数据类型**：TIMESTAMP。

**应用字段**：在 WHERE 或 INSERT 语句中使用时只能作用于 TIMESTAMP 类型的字段。

**适用于**：表和超级表。

**使用说明**：

- 支持时间加减操作，如 TODAY() + 1s, 支持的时间单位如下： b(纳秒)，u(微秒)，a(毫秒)，s(秒)，m(分)，h(小时)，d(天)，w(周)。
- 返回的时间戳精度与当前 DATABASE 设置的时间精度一致。

## 聚合函数

聚合函数为查询结果集的每一个分组返回单个结果行。可以由 GROUP BY 或窗口切分子句指定分组，如果没有，则整个查询结果集视为一个分组。

TDengine 支持针对数据的聚合查询。提供如下聚合函数。

### APERCENTILE

```sql
APERCENTILE(expr, p [, algo_type])

algo_type: {
    "default"
  | "t-digest"
}
```

**功能说明**：统计表/超级表中指定列的值的近似百分比分位数，与 PERCENTILE 函数相似，但是返回近似结果。

**返回数据类型**： DOUBLE。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

**说明**：

- p值范围是[0,100]，当为0时等同于MIN，为100时等同于MAX。
- algo_type 取值为 "default" 或 "t-digest"。 输入为 "default" 时函数使用基于直方图算法进行计算。输入为  "t-digest" 时使用t-digest算法计算分位数的近似结果。如果不指定 algo_type 则使用 "default" 算法。
- "t-digest"算法的近似结果对于输入数据顺序敏感，对超级表查询时不同的输入排序结果可能会有微小的误差。

### AVG

```sql
AVG(expr)
```

**功能说明**：统计指定字段的平均值。

**返回数据类型**：DOUBLE。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

### COUNT

```sql
COUNT({* | expr})
```

**功能说明**：统计指定字段的记录行数。

**返回数据类型**：BIGINT。

**适用数据类型**：全部类型字段。

**适用于**：表和超级表。

**使用说明**:

- 可以使用星号(*)来替代具体的字段，使用星号(*)返回全部记录数量。
- 如果统计字段是具体的列，则返回该列中非 NULL 值的记录数量。

### ELAPSED

```sql
ELAPSED(ts_primary_key [, time_unit])
```

**功能说明**：elapsed函数表达了统计周期内连续的时间长度，和twa函数配合使用可以计算统计曲线下的面积。在通过INTERVAL子句指定窗口的情况下，统计在给定时间范围内的每个窗口内有数据覆盖的时间范围；如果没有INTERVAL子句，则返回整个给定时间范围内的有数据覆盖的时间范围。注意，ELAPSED返回的并不是时间范围的绝对值，而是绝对值除以time_unit所得到的单位个数。

**返回结果类型**：DOUBLE。

**适用数据类型**：TIMESTAMP。

**适用于**: 表，超级表，嵌套查询的外层查询

**说明**：

- ts_primary_key参数只能是表的第一列，即 TIMESTAMP 类型的主键列。
- 按time_unit参数指定的时间单位返回，最小是数据库的时间分辨率。time_unit 参数未指定时，以数据库的时间分辨率为时间单位。支持的时间单位 time_unit 如下： 1b(纳秒), 1u(微秒)，1a(毫秒)，1s(秒)，1m(分)，1h(小时)，1d(天), 1w(周)。
- 可以和interval组合使用，返回每个时间窗口的时间戳差值。需要特别注意的是，除第一个时间窗口和最后一个时间窗口外，中间窗口的时间戳差值均为窗口长度。
- order by asc/desc不影响差值的计算结果。
- 对于超级表，需要和group by tbname子句组合使用，不可以直接使用。
- 对于普通表，不支持和group by子句组合使用。
- 对于嵌套查询，仅当内层查询会输出隐式时间戳列时有效。例如select elapsed(ts) from (select diff(value) from  sub1)语句，diff函数会让内层查询输出隐式时间戳列，此为主键列，可以用于elapsed函数的第一个参数。相反，例如select  elapsed(ts) from (select * from sub1)  语句，ts列输出到外层时已经没有了主键列的含义，无法使用elapsed函数。此外，elapsed函数作为一个与时间线强依赖的函数，形如select elapsed(ts) from (select diff(value) from st group by  tbname)尽管会返回一条计算结果，但并无实际意义，这种用法后续也将被限制。
- 不支持与leastsquares、diff、derivative、top、bottom、last_row、interp等函数混合使用。

### LEASTSQUARES

```sql
LEASTSQUARES(expr, start_val, step_val)
```

**功能说明**：统计表中某列的值是主键（时间戳）的拟合直线方程。start_val 是自变量初始值，step_val 是自变量的步长值。

**返回数据类型**：字符串表达式（斜率, 截距）。

**适用数据类型**：expr 必须是数值类型。

**适用于**：表。

### SPREAD

```sql
SPREAD(expr)
```

**功能说明**：统计表中某列的最大值和最小值之差。

**返回数据类型**：DOUBLE。

**适用数据类型**：INTEGER, TIMESTAMP。

**适用于**：表和超级表。

### STDDEV

```sql
STDDEV(expr)
```

**功能说明**：统计表中某列的均方差。

**返回数据类型**：DOUBLE。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

### SUM

```sql
SUM(expr)
```

**功能说明**：统计表/超级表中某列的和。

**返回数据类型**：DOUBLE, BIGINT。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

### HYPERLOGLOG

```sql
HYPERLOGLOG(expr)
```

**功能说明**：

- 采用 hyperloglog 算法，返回某列的基数。该算法在数据量很大的情况下，可以明显降低内存的占用，求出来的基数是个估算值，标准误差（标准误差是多次实验，每次的平均数的标准差，不是与真实结果的误差）为 0.81%。
- 在数据量较少的时候该算法不是很准确，可以使用 select count(data) from (select unique(col) as data from table) 的方法。

**返回结果类型**：INTEGER。

**适用数据类型**：任何类型。

**适用于**：表和超级表。

### HISTOGRAM

```sql
HISTOGRAM(expr，bin_type, bin_description, normalized)
```

**功能说明**：统计数据按照用户指定区间的分布。

**返回结果类型**：如归一化参数 normalized 设置为 1，返回结果为 DOUBLE 类型，否则为 BIGINT 类型。

**适用数据类型**：数值型字段。

**适用于**: 表和超级表。

**详细说明**：

- bin_type 用户指定的分桶类型, 有效输入类型为"user_input“, ”linear_bin", "log_bin"。
- bin_description 描述如何生成分桶区间，针对三种桶类型，分别为以下描述格式(均为 JSON 格式字符串)：
  - "user_input": "[1, 3, 5, 7]" 用户指定 bin 的具体数值。
  - "linear_bin": "{"start": 0.0, "width": 5.0, "count": 5, "infinity": true}" "start" 表示数据起始点，"width" 表示每次 bin 偏移量, "count" 为 bin 的总数，"infinity" 表示是否添加（-inf, inf）作为区间起点和终点， 生成区间为[-inf, 0.0, 5.0, 10.0, 15.0, 20.0, +inf]。
  - "log_bin": "{"start":1.0, "factor": 2.0, "count": 5, "infinity": true}" "start" 表示数据起始点，"factor" 表示按指数递增的因子，"count" 为 bin 的总数，"infinity" 表示是否添加（-inf, inf）作为区间起点和终点， 生成区间为[-inf, 1.0, 2.0, 4.0, 8.0, 16.0, +inf]。
- normalized 是否将返回结果归一化到 0~1 之间 。有效输入为 0 和 1。

### PERCENTILE

```sql
PERCENTILE(expr, p [, p1] ... )
```

**功能说明**：统计表中某列的值百分比分位数。

**返回数据类型**： 该函数最小参数个数为 2 个，最大参数个数为 11 个。可以最多同时返回 10 个百分比分位数。当参数个数为 2 时， 返回一个分位数， 类型为DOUBLE，当参数个数大于 2 时，返回类型为VARCHAR, 格式为包含多个返回值的JSON数组。

**应用字段**：数值类型。

**适用于**：表。

**使用说明**：

- *P*值取值范围 0≤*P*≤100，为 0 的时候等同于 MIN，为 100 的时候等同于 MAX;
- 同时计算针对同一列的多个分位数时，建议使用一个PERCENTILE函数和多个参数的方式，能很大程度上降低查询的响应时间。 比如，使用查询SELECT percentile(col, 90, 95, 99) FROM table, 性能会优于SELECT  percentile(col, 90), percentile(col, 95), percentile(col, 99) from  table。

## 选择函数

选择函数根据语义在查询结果集中选择一行或多行结果返回。用户可以同时指定输出 ts 列或其他列（包括 tbname 和标签列），这样就可以方便地知道被选出的值是源于哪个数据行的。

### BOTTOM

```sql
BOTTOM(expr, k)
```

**功能说明**：统计表/超级表中某列的值最小 *k* 个非 NULL 值。如果多条数据取值一样，全部取用又会超出 k 条限制时，系统会从相同值中随机选取符合要求的数量返回。

**返回数据类型**：同应用的字段。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

**使用说明**:

- *k*值取值范围 1≤*k*≤100；
- 系统同时返回该记录关联的时间戳列；
- 限制：BOTTOM 函数不支持 FILL 子句。

### FIRST

```sql
FIRST(expr)
```

**功能说明**：统计表/超级表中某列的值最先写入的非 NULL 值。

**返回数据类型**：同应用的字段。

**适用数据类型**：所有字段。

**适用于**：表和超级表。

**使用说明**:

- 如果要返回各个列的首个（时间戳最小）非 NULL 值，可以使用 FIRST(*)；
- 如果结果集中的某列全部为 NULL 值，则该列的返回结果也是 NULL；
- 如果结果集中所有列全部为 NULL 值，则不返回结果。

### INTERP

```sql
INTERP(expr)
```

**功能说明**：返回指定时间截面指定列的记录值或插值。

**返回数据类型**：同字段类型。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

**使用说明**

- INTERP 用于在指定时间断面获取指定列的记录值，如果该时间断面不存在符合条件的行数据，那么会根据 FILL 参数的设定进行插值。
- INTERP 的输入数据为指定列的数据，可以通过条件语句（where 子句）来对原始列数据进行过滤，如果没有指定过滤条件则输入为全部数据。
- INTERP 需要同时与 RANGE，EVERY 和 FILL 关键字一起使用。
- INTERP 的输出时间范围根据 RANGE(timestamp1,timestamp2)字段来指定，需满足 timestamp1 <=  timestamp2。其中 timestamp1（必选值）为输出时间范围的起始值，即如果 timestamp1 时刻符合插值条件则  timestamp1 为输出的第一条记录，timestamp2（必选值）为输出时间范围的结束值，即输出的最后一条记录的 timestamp  不能大于 timestamp2。
- INTERP 根据 EVERY(time_unit) 字段来确定输出时间范围内的结果条数，即从 timestamp1 开始每隔固定长度的时间（time_unit 值）进行插值，time_unit  可取值时间单位：1a(毫秒)，1s(秒)，1m(分)，1h(小时)，1d(天)，1w(周)。例如 EVERY(500a)  将对于指定数据每500毫秒间隔进行一次插值.
- INTERP 根据 FILL 字段来决定在每个符合输出条件的时刻如何进行插值。关于 FILL 子句如何使用请参考 [FILL 子句](https://docs.taosdata.com/taos-sql/distinguished/#fill-子句)
- INTERP 作用于超级表时, 会将该超级表下的所有子表数据按照主键列排序后进行插值计算，也可以搭配 PARTITION BY tbname 使用，将结果强制规约到单个时间线。
- INTERP 可以与伪列 _irowts 一起使用，返回插值点所对应的时间戳(3.0.2.0版本以后支持)。
- INTERP 可以与伪列 _isfilled 一起使用，显示返回结果是否为原始记录或插值算法产生的数据(3.0.3.0版本以后支持)。

### LAST

```sql
LAST(expr)
```

**功能说明**：统计表/超级表中某列的值最后写入的非 NULL 值。

**返回数据类型**：同应用的字段。

**适用数据类型**：所有字段。

**适用于**：表和超级表。

**使用说明**:

- 如果要返回各个列的最后（时间戳最大）一个非 NULL 值，可以使用 LAST(*)；
- 如果结果集中的某列全部为 NULL 值，则该列的返回结果也是 NULL；如果结果集中所有列全部为 NULL 值，则不返回结果。
- 在用于超级表时，时间戳完全一样且同为最大的数据行可能有多个，那么会从中随机返回一条，而并不保证多次运行所挑选的数据行必然一致。

### LAST_ROW

```sql
LAST_ROW(expr)
```

**功能说明**：返回表/超级表的最后一条记录。

**返回数据类型**：同应用的字段。

**适用数据类型**：所有字段。

**适用于**：表和超级表。

**使用说明**：

- 在用于超级表时，时间戳完全一样且同为最大的数据行可能有多个，那么会从中随机返回一条，而并不保证多次运行所挑选的数据行必然一致。
- 不能与 INTERVAL 一起使用。

### MAX

```sql
MAX(expr)
```

**功能说明**：统计表/超级表中某列的值最大值。

**返回数据类型**：同应用的字段。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

### MIN

```sql
MIN(expr)
```

**功能说明**：统计表/超级表中某列的值最小值。

**返回数据类型**：同应用的字段。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

### MODE

```sql
MODE(expr)
```

**功能说明**：返回出现频率最高的值，若存在多个频率相同的最高值，则随机输出其中某个值。

**返回数据类型**：与输入数据类型一致。

**适用数据类型**：全部类型字段。

**适用于**：表和超级表。

### SAMPLE

```sql
SAMPLE(expr, k)
```

**功能说明**： 获取数据的 k 个采样值。参数 k 的合法输入范围是 1≤ k ≤ 1000。

**返回结果类型**： 同原始数据类型， 返回结果中带有该行记录的时间戳。

**适用数据类型**： 在超级表查询中使用时，不能应用在标签之上。

**嵌套子查询支持**： 适用于内层查询和外层查询。

**适用于**：表和超级表。

**使用说明**：

- 不能参与表达式计算；该函数可以应用在普通表和超级表上；
- 使用在超级表上的时候，需要搭配 PARTITION by tbname 使用，将结果强制规约到单个时间线。

### TAIL

```sql
TAIL(expr, k [, offset_rows])
```

**功能说明**：返回跳过最后 offset_val 个，然后取连续 k 个记录，不忽略 NULL 值。offset_val 可以不输入。此时返回最后的 k 个记录。当有 offset_val 输入的情况下，该函数功能等效于 `order by ts desc LIMIT k OFFSET offset_val`。

**参数范围**：k: [1,100] offset_val: [0,100]。

**返回数据类型**：同应用的字段。

**适用数据类型**：适合于除时间主键列外的任何类型。

**适用于**：表、超级表。

### TOP

```sql
TOP(expr, k)
```

**功能说明**： 统计表/超级表中某列的值最大 *k* 个非 NULL 值。如果多条数据取值一样，全部取用又会超出 k 条限制时，系统会从相同值中随机选取符合要求的数量返回。

**返回数据类型**：同应用的字段。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

**使用说明**:

- *k*值取值范围 1≤*k*≤100；
- 系统同时返回该记录关联的时间戳列；
- 限制：TOP 函数不支持 FILL 子句。

### UNIQUE

```sql
UNIQUE(expr)
```

**功能说明**：返回该列的数值首次出现的值。该函数功能与 distinct 相似，但是可以匹配标签和时间戳信息。可以针对除时间列以外的字段进行查询，可以匹配标签和时间戳，其中的标签和时间戳是第一次出现时刻的标签和时间戳。

**返回数据类型**：同应用的字段。

**适用数据类型**：适合于除时间类型以外的字段。

**适用于**: 表和超级表。

## 时序数据特有函数

时序数据特有函数是 TDengine 为了满足时序数据的查询场景而量身定做出来的。在通用数据库中，实现类似功能通常需要复杂的查询语法，且效率很低。TDengine 以函数的方式内置了这些功能，最大程度的减轻了用户的使用成本。

### CSUM

```sql
CSUM(expr)
```

**功能说明**：累加和（Cumulative sum），输出行与输入行数相同。

**返回结果类型**： 输入列如果是整数类型返回值为长整型 （int64_t），浮点数返回值为双精度浮点数（Double）。无符号整数类型返回值为无符号长整型（uint64_t）。

**适用数据类型**：数值类型。

**嵌套子查询支持**： 适用于内层查询和外层查询。

**适用于**：表和超级表。

**使用说明**：

- 不支持 +、-、*、/ 运算，如 csum(col1) + csum(col2)。
- 只能与聚合（Aggregation）函数一起使用。 该函数可以应用在普通表和超级表上。
- 使用在超级表上的时候，需要搭配 PARTITION BY tbname使用，将结果强制规约到单个时间线。

### DERIVATIVE

```sql
DERIVATIVE(expr, time_interval, ignore_negative)

ignore_negative: {
    0
  | 1
}
```

**功能说明**：统计表中某列数值的单位变化率。其中单位时间区间的长度可以通过 time_interval 参数指定，最小可以是 1 秒（1s）；ignore_negative 参数的值可以是 0 或 1，为 1 时表示忽略负值。

**返回数据类型**：DOUBLE。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

**使用说明**:

- DERIVATIVE 函数可以在由 PARTITION BY 划分出单独时间线的情况下用于超级表（也即 PARTITION BY tbname）。
- 可以与选择相关联的列一起使用。 例如: select _rowts, DERIVATIVE() from。

### DIFF

```sql
DIFF(expr [, ignore_negative])

ignore_negative: {
    0
  | 1
}
```

**功能说明**：统计表中某列的值与前一行对应值的差。 ignore_negative 取值为 0|1 , 可以不填，默认值为 0. 不忽略负值。ignore_negative 为 1 时表示忽略负数。

**返回数据类型**：同应用字段。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

**使用说明**:

- 输出结果行数是范围内总行数减一，第一行没有结果输出。
- 可以与选择相关联的列一起使用。 例如: select _rowts, DIFF() from。

### IRATE

```sql
IRATE(expr)
```

**功能说明**：计算瞬时增长率。使用时间区间中最后两个样本数据来计算瞬时增长速率；如果这两个值呈递减关系，那么只取最后一个数用于计算，而不是使用二者差值。

**返回数据类型**：DOUBLE。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

### MAVG

```sql
MAVG(expr, k)
```

**功能说明**： 计算连续 k 个值的移动平均数（moving average）。如果输入行数小于 k，则无结果输出。参数 k 的合法输入范围是 1≤ k ≤ 1000。

**返回结果类型**： DOUBLE。

**适用数据类型**： 数值类型。

**嵌套子查询支持**： 适用于内层查询和外层查询。

**适用于**：表和超级表。

**使用说明**：

- 不支持 +、-、*、/ 运算，如 mavg(col1, k1) + mavg(col2, k1);
- 只能与普通列，选择（Selection）、投影（Projection）函数一起使用，不能与聚合（Aggregation）函数一起使用；
- 使用在超级表上的时候，需要搭配 PARTITION BY tbname使用，将结果强制规约到单个时间线。

### STATECOUNT

```sql
STATECOUNT(expr, oper, val)
```

**功能说明**：返回满足某个条件的连续记录的个数，结果作为新的一列追加在每行后面。条件根据参数计算，如果条件为 true 则加 1，条件为 false 则重置为-1，如果数据为 NULL，跳过该条数据。

**参数范围**：

- oper : "LT" (小于)、"GT"（大于）、"LE"（小于等于）、"GE"（大于等于）、"NE"（不等于）、"EQ"（等于），不区分大小写。
- val : 数值型

**返回结果类型**：INTEGER。

**适用数据类型**：数值类型。

**嵌套子查询支持**：不支持应用在子查询上。

**适用于**：表和超级表。

**使用说明**：

- 该函数可以应用在普通表上，在由 PARTITION BY 划分出单独时间线的情况下用于超级表（也即 PARTITION BY tbname）
- 不能和窗口操作一起使用，例如 interval/state_window/session_window。

### STATEDURATION

```sql
STATEDURATION(expr, oper, val, unit)
```

**功能说明**：返回满足某个条件的连续记录的时间长度，结果作为新的一列追加在每行后面。条件根据参数计算，如果条件为 true 则加上两个记录之间的时间长度（第一个满足条件的记录时间长度记为 0），条件为 false 则重置为-1，如果数据为 NULL，跳过该条数据。

**参数范围**：

- oper : `'LT'` (小于)、`'GT'`（大于）、`'LE'`（小于等于）、`'GE'`（大于等于）、`'NE'`（不等于）、`'EQ'`（等于），不区分大小写，但需要用`''`包括。
- val : 数值型
- unit : 时间长度的单位，可取值时间单位： 1b(纳秒), 1u(微秒)，1a(毫秒)，1s(秒)，1m(分)，1h(小时)，1d(天), 1w(周)。如果省略，默认为当前数据库精度。

**返回结果类型**：INTEGER。

**适用数据类型**：数值类型。

**嵌套子查询支持**：不支持应用在子查询上。

**适用于**：表和超级表。

**使用说明**：

- 该函数可以应用在普通表上，在由 PARTITION BY 划分出单独时间线的情况下用于超级表（也即 PARTITION BY tbname）
- 不能和窗口操作一起使用，例如 interval/state_window/session_window。

### TWA

```sql
TWA(expr)
```

**功能说明**：时间加权平均函数。统计表中某列在一段时间内的时间加权平均。

**返回数据类型**：DOUBLE。

**适用数据类型**：数值类型。

**适用于**：表和超级表。

**使用说明**： TWA 函数可以在由 PARTITION BY 划分出单独时间线的情况下用于超级表（也即 PARTITION BY tbname）。

## 系统信息函数

### DATABASE

```sql
SELECT DATABASE();
```

**说明**：返回当前登录的数据库。如果登录的时候没有指定默认数据库，且没有使用USE命令切换数据库，则返回NULL。

### CLIENT_VERSION

```sql
SELECT CLIENT_VERSION();
```

**说明**：返回客户端版本。

### SERVER_VERSION

```sql
SELECT SERVER_VERSION();
```

**说明**：返回服务端版本。

### SERVER_STATUS

```sql
SELECT SERVER_STATUS();
```

**说明**：检测服务端是否所有 dnode 都在线，如果是则返回成功，否则返回无法建立连接的错误。






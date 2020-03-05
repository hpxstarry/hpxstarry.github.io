---
layout: post
title:  Data formats walk through
date:   2020-03-04 00:31:10 -0800
categories: bigdata
---

```
前方高能，作者为表达方便，非常任性，想用中文就用中文，想用英文就用英文， 不喜误入。
```

在大数据处理中，我们经常接触到各种各样的数据类型，例如CSV, JSON, Avro等。这篇博客将
* 讨论这些data formats，及它们的trade-offs;
* 针对use case, 如何选择data format。 



# 概览 data formats

Data fomrats 主要可以分为如下三种类型
* Unstructured， 没有schema，例如纯文本text, TSV, CSV等数据类型。
* Semi-structured， 半结构化，知道一定的schema信息，例如JSON, YAML, XML。 
* Structured，结构化，知道完整的schema，例如Avro, Parquet等。

![image](/assets/images/data_format_overview.png)

## Unstructured 

CSV/TSV 格式中，数据包含多个rows，每个row 有相同的column, 不同的column之间用分隔符隔开。CSV的分隔符是","， TSV是"\t"。


CSV/TSV 简单实用，基本上是所有的数据处理engine的默认格式。许多的数据处理分析软件，例如Excel, Google Sheets，都能处理CSV/TSV文件。



尽管简单实用，CSV/TSV也有着如下缺点。 

* 没有schema信息，

* 不能按列读，每次都得读取所有列。

* 数据压缩。


## Semi-structured
JSON - 

* JSON, ION, YAML

Ion is 20% better than JSON. 

* JSON 的变种 - BSON, SMILE。


## Structured 

**Avro** 


Avro is row oriented storage. If your use case typically scans or retrieves all of the fields in a row in each query, Avro is usually the best choice. Benefits of Avro

* **Avro has schema and relies on it.** Within Avro, data is always presented together with its schema. It provides below benefits. 

    + This permits each datum to be written with no per-value overheads, making serialization both fast and small.

    + This also facilitates use with dynamic, scripting languages, since data, together with its schema, is fully self-describing.  
* Avro provides code generation from schema definition (in JSON).
* **Rich data structures.** Via schema defintion. Schema data types include primitive types (boolean, int, long, float, double, bytes, string) and complex types (record, enum, array, map, union, fixed)
* **A container file, to store persistent data.** One Avro file can save one or multiple data records. 
*  **A compact, fast, binary data format.** Apart from the schema, Avro persists data in binary format, which is compact. This benfit become more obvious when saving batched records into the same file since schema needs to be saved only once. 
* **Remote procedure call (RPC).** When Avro is used in RPC, the client and server exchange schemas in the connection handshake. (This can be optimized so that, for most calls, no schemas are actually transmitted.) Since both client and server both have the other's full schema, correspondence between same named fields, missing fields, extra fields, etc. can all be easily resolved.
* **Simple integration with dynamic languages. Code generation is not required to read or write data files nor to use or implement RPC protocols. Code generation as an optional optimization, only worth implementing for statically typed languages.**



**Parquet** 

Apache Parquet is a columnar storage format available to any project in the Hadoop ecosystem, regardless of the choice of data processing framework, data model or programming language.

* Column-oriented storage. 
* Column-wise compression. Especially for sparse data. 
* Column-wise query. Not need to scan all data for queries that access only a few colunns.  
* Schema information with nested structure (via Avro and other data formats).  
* Able to separate metadata



Features

* Schema

* Partial column selection. 

* Compressed. Column-wise compression. 




**ORC** 
**Thrift**




# Comparisons 


| Data format | Human Readability (0-5) | Schema completness                                                     | Subset of columns query? | Support nested, complicated data structure? | Storage size |
|-------------|-------------------------|------------------------------------------------------------------------|--------------------------|---------------------------------------------|--------------|
| CSV/TSV     | 4 (with header)         | Little schema information.                                             | N                        | N                                           |              |
| JSON        | 5                       | Has schema information though not complete. May vary record by record. | N                        | Y                                           |              |
| YAML        | 5                       |                                                                        | N                        | Y                                           |              |
| ION         | 5                       |                                                                        | N                        | Y                                           |              |
| Avro        | 0                       |                                                                        | N                        | Y                                           |              |
| Parquet     | 0                       |                                                                        | 5                        | Y                                           |              |
| ORC         |                         |                                                                        | 5                        | Y                                           |              |


More https://en.wikipedia.org/wiki/Comparison_of_data-serialization_formats

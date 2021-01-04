---
title: Data formats walk through
date: 2020-03-04 00:31:10 -0800
published: false

categories: [Big Data, Tutorial]
tags: [data format]
seo:
  date_modified: 2020-03-12 23:50:26 -0700
---
>
前方高能，作者为表达方便，非常任性，想用中文就用中文，想用英文就用英文， 不喜误入。

数据处理中，数据有存储（持久化成文件或到database）和传递的需求。数据的传递往往在不同的应用间，而不同的应用可能适用不同的编程语言，运行在不同的进程、服务器上。这个过程中就涉及到数据的序列化。基本上各种编程语言都有自己的序列化方式，例如Java的object serialization, python的pickle。但是这些序列化方式往往局限于这些语言本身。因此，一系列的通用序列化格式应运而生，例如CSV, JSON, Avro, Parquet等。

这篇博客将试图讨论如下问题
* walk through 常见的数据序列化格式，并讨论它们的优缺点；
* 选择数据类型，粗略的rule of thumb。

Features we like
* 跨语言
* Schema
* Human readable 
* Columnar
* Document

# 概览 data formats

Data fomrats 主要可以分为如下三种类型
* Unstructured， 没有schema，例如纯文本text, TSV, CSV等数据类型。
* Semi-structured， 半结构化，知道一定的schema信息，例如JSON, YAML, XML。 
* Structured，结构化，知道完整的schema，例如Avro, Parquet等。

![image](/assets/img/blog/data_format_overview.png)

# 无结构型格式 - Unstructured data formats
## TSV/CSV
CSV/TSV 格式中，数据包含多个rows，每个row 有相同的column, 不同的column之间用分隔符隔开。CSV的分隔符是","， TSV是"\t"。
CSV/TSV 简单实用，基本上是所有的数据处理engine的默认格式。许多的数据处理分析软件，例如Excel, Google Sheets，都能处理CSV/TSV文件。
尽管简单实用，CSV/TSV也有着如下缺点。 

* 没有schema信息；
* 不能按列读，每次都得读取所有列；
* 数据压缩。

# 半结构型格式 - Semi-structured data formats
## XML
[XML](https://en.wikipedia.org/wiki/XML)(Extensible Markup Language) 正在死去，逐渐被JSON, YAML等取代，不再赘述。

## JSON
[JSON](https://www.json.org/json-en.html) (JavaScript Object Notation), 正如它的名字一样，最开始是2001在JavaScript语言中设计出来，用于在浏览器和服务器端交互数据。但如今，JSON已广泛应用各种语言， 成为大部分web应用的默认数据格式。对JSON的历史感兴趣的可以看这篇[blog](https://twobithistory.org/2017/09/21/the-rise-and-rise-of-json.html). 

以下是一个JSON example

```json
{
  "event": "breakfast",
  "location": "Tiffany's",
  "remember": true,
  "format": "film",
  "bothKindaLikedIt": true,
  "thingsInCommon": 1
}
```

JSON有如下特点
* 跨语言，跨平台。JSON可以被各个语言，各种操作系统解释；
* Human readable，人能够很轻易的读懂JSON的内容;
* 自带结构信息，每个数据的结构均可不一样。


JSON 还有多种变种，例如BSON, SMILE等。

## YAML
[YAML](https://yaml.org/) (YAML Ain't Markup Language)，也被设计为human readable, 跨语言的数据序列化格式。YAML 1.2是JSON的超集。

下面是YAML的一个例子
```yaml
event name: John
last name: Smith
age: 25
address: 
  street address: 21 2nd Street
  city: New York
  state: NY
  postal code: '10021'
phone numbers: 
  - type: home
    number: 212 555-1234
  - type: fax
    number: 646 555-4567
```
相比于JSON, YAML
* 更简洁，正如上面的例子;
* YAML包含更多的特性 (例如支持comments，relational archors, mapping types preserving key order），因此也更复杂；
* Human Editable，所以常用于支持configuration。

## ION
[ION](http://amzn.github.io/ion-docs/)，类似于JSON，也是一种human readable、rich typed、 跨语言的数据格式，由Amazon贡献。ION是JSON的超集。 

下面是ION的一个例子

```
/* Ion supports comments. */
// Here is a struct, which is similar to a JSON object
{
  // Field names don't always have to be quoted
  name: "Fido",

  // This is an integer with a 'years' annotation
  age: years::4,

  // This is a timestamp with day precision
  birthday: 2012-03-01T,

  // Here is a list, which is like a JSON array
  toys: [
    // These are symbol values, which are like strings,
    // but get encoded as integers in binary
    ball,
    rope,
  ],

  // This is a decimal -- a base-10 floating point value
  weight: pounds::41.2,

  // Here is a blob -- binary data, which is
  // base64-encoded in Ion text encoding
  buzz: {{VG8gaW5maW5pdHkuLi4gYW5kIGJleW9uZCE=}},
}
```

相比于JSON, ION具有如下特点
* 支持更多数据格式，例如timestamp, 二进制数据 （blobs)，符号表达式等；
* 更简洁，一般来说ION能节省33%的空间；对数组结构，ION能减少到原来的20%左右。

# 结构型格式 -Structured data formats

## Avro
[Apache Avro](https://avro.apache.org/) 是一种row oriented，binary数据格式。它有如下特点
* **Avro has schema and relies on it.** Within Avro, data is always presented together with its schema. It provides below benefits. 
    + This permits each datum to be written with no per-value overheads, making serialization both fast and small.
    + This also facilitates use with dynamic, scripting languages, since data, together with its schema, is fully self-describing.  
* Avro provides code generation from schema definition (in JSON).
* **Rich data structures.** Via schema defintion. Schema data types include primitive types (boolean, int, long, float, double, bytes, string) and complex types (record, enum, array, map, union, fixed)
* **A container file, to store persistent data.** One Avro file can save one or multiple data records. 
*  **A compact, fast, binary data format.** Apart from the schema, Avro persists data in binary format, which is compact. This benfit become more obvious when saving batched records into the same file since schema needs to be saved only once. 
* **Remote procedure call (RPC).** When Avro is used in RPC, the client and server exchange schemas in the connection handshake. (This can be optimized so that, for most calls, no schemas are actually transmitted.) Since both client and server both have the other's full schema, correspondence between same named fields, missing fields, extra fields, etc. can all be easily resolved.
* **Simple integration with dynamic languages. Code generation is not required to read or write data files nor to use or implement RPC protocols. Code generation as an optional optimization, only worth implementing for statically typed languages.**


## Parquet
[Apache Parquet](https://parquet.apache.org/) is a columnar storage format available to any project in the Hadoop ecosystem, regardless of the choice of data processing framework, data model or programming language.
* Column-oriented storage. 
* Column-wise compression. Especially for sparse data. 
* Column-wise query. Not need to scan all data for queries that access only a few colunns.  
* Schema information with nested structure (via Avro and other data formats).  
* Able to separate metadata

Features
* Schema
* Partial column selection. 
* Compressed. Column-wise compression. 

## ORC

[ORC](https://orc.apache.org/) claims to be the smallest, fastest columnar storage for Hadoop workloads. ORC is a self-describing, type-aware, columnar file format designed for Hadoop workloads. It is optimized for large streaming reads, but with integrated support for finding required rows quickly. Storing data in a columnar format lets the reader read, decompress, and process only the values that are required for the current query. Because ORC files are type-aware, the writer chooses the most appropriate encoding for the type and builds an internal index as the file is written. Optimized RC file. Optimize for Hive with ACID. 

* Built-in Indexes. Predicate pushdown uses those indexes to determine which stripes in a file need to be read for a particular query and the row indexes can narrow the search to a particular set of 10,000 rows. ORC supports the complete set of types in Hive, including the complex types: structs, lists, maps, and unions.
* Columnar format. Let the reader read, decompress, and process only the values that are required for the current query
* Optimize for Hive. Apache Hive was the original use case and home for ORC. ORC’s strong type system, advanced compression, column projection, predicate push down, and vectorization support make Hive perform better than any other format for your data.



**Thrift**
**Proto Buffer**


#  对比和选型


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

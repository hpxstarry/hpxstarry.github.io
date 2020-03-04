---
layout: post
title:  Data formats walk through
date:   2020-03-04 00:31:10 -0800
categories: bigdata
---

# 介绍

前方高能，作者为表达方便，非常任性，想用中文就用中文，想用英文就用英文， 不喜误入。

在大数据处理中，我们经常接触到各种各样的数据类型。例如Amazon Athena可以query CSV/TSV 和 Parquet格式的数据， Hadoop 支持 Avro格式。那么这些数据格式都有哪些优缺点呢？这边博客就walk through 数据格式包括，并探讨他们各自的特点。 



# Data formats

## CSV/TSV

CSV/TSV 格式中，数据包含多个rows，每个row 有相同的column, 不同的column之间用分隔符隔开。CSV的分隔符是","， TSV是"\t"。



CSV/TSV 非常简单实用，基本是所有的数据处理的默认格式。许多的数据处理分析软件，例如Excel, Google Sheets，都能处理CSV/TSV文件。



尽管简单实用，CSV/TSV也有着如下缺点。 

* 没有schema信息，

* 不能按列读，每次都得读取所有列。

* 数据压缩。



## JSON

Nest?



## JSON 的变种

SMILE JSON

## Ion

## YAML



## Parquet

Apache Parquet is a columnar storage format available to any project in the Hadoop ecosystem, regardless of the choice of data processing framework, data model or programming language.



Features

* Schema

* Partial column selection. 

* Compressed. Column-wise compression. 



## ORC

?

## Avro





# Comparisons 



Ion is 20% better than JSON?







Avro, CSV, JSON, XML, Parquet







# When to choose what?

https://databricks.com/blog/2017/02/23/working-complex-data-formats-structured-streaming-apache-spark-2-1.html

Diagram showing the breakdown of various types of data sources and formats

# Data at rest vs data at move
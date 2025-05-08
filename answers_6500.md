# Answers to Hadoop and Big Data Processing Questions

## 1. Key Components of Hadoop

### Core Components:
1. **Hadoop Distributed File System (HDFS)**
   - Distributed storage system
   - Handles large data sets across multiple machines
   - Provides high throughput access to data

2. **MapReduce**
   - Programming model for processing large datasets
   - Parallel processing framework
   - Handles distributed computing

3. **YARN (Yet Another Resource Negotiator)**
   - Resource management layer
   - Manages cluster resources
   - Schedules applications

4. **Common Utilities**
   - Libraries and utilities
   - Support for other Hadoop modules

### Additional Components:
- HBase: NoSQL database
- Hive: Data warehouse infrastructure
- Pig: High-level data flow language
- ZooKeeper: Distributed coordination service

## 2. Limitations of Hadoop for Big Data Processing

1. **Performance Issues**
   - High latency for small files
   - Not suitable for real-time processing
   - Slow for iterative algorithms

2. **Resource Management**
   - Fixed resource allocation
   - Limited flexibility in resource sharing
   - Overhead in job scheduling

3. **Programming Model**
   - Complex programming model
   - Limited support for interactive queries
   - Not suitable for all types of processing

4. **Storage Limitations**
   - No in-memory processing
   - High I/O overhead
   - Limited support for streaming data

## 3. MapReduce Pipeline

### Common Steps:
1. **Input Phase**
   - Data is read from HDFS
   - InputFormat determines how to read data
   - InputSplit divides data into chunks

2. **Map Phase**
   - Processes input records
   - Produces intermediate key-value pairs
   - Runs in parallel across nodes

3. **Shuffle and Sort**
   - Groups data by key
   - Sorts values for each key
   - Transfers data between nodes

4. **Reduce Phase**
   - Processes grouped data
   - Produces final output
   - Writes results to HDFS

### Safety Assurance:
1. **Fault Tolerance**
   - Task failure handling
   - Node failure recovery
   - Data replication

2. **Data Integrity**
   - Checksum verification
   - Data validation
   - Error detection and correction

## 4. Apache Pig Simplification

### How Pig Simplifies Processing:
1. **High-level Language (Pig Latin)**
   - SQL-like syntax
   - Easier to write and maintain
   - Less code than MapReduce

2. **Built-in Functions**
   - Common data operations
   - Complex data transformations
   - Data validation

3. **Optimization**
   - Automatic query optimization
   - Parallel execution
   - Efficient data flow

## 5. Hive Partitions

### Definition:
Partitions in Hive are a way to divide a table into related parts based on the values of particular columns.

### Importance:
1. **Query Performance**
   - Faster data retrieval
   - Reduced data scanning
   - Better query optimization

2. **Data Management**
   - Easier data organization
   - Efficient data pruning
   - Better data lifecycle management

3. **Scalability**
   - Handles large datasets
   - Supports incremental loading
   - Better resource utilization

## 6. Pig vs Hive Differences

### Key Differences:

1. **Language and Interface**
   - Pig: Procedural language (Pig Latin)
   - Hive: Declarative language (HQL)

2. **Data Processing**
   - Pig: Better for unstructured data
   - Hive: Better for structured data

3. **Use Cases**
   - Pig: ETL, data pipelines
   - Hive: Data warehousing, analytics

### Impact on Data Processing:
1. **Structured Data**
   - Hive: Better performance, SQL-like queries
   - Pig: More flexible but less efficient

2. **Semi-structured Data**
   - Both can handle, but different approaches
   - Pig: More flexible transformations
   - Hive: Better query optimization

3. **Unstructured Data**
   - Pig: Better suited
   - Hive: Requires more preprocessing

## 7. MapReduce vs Apache Spark

### Key Differences:

1. **Processing Model**
   - MapReduce: Batch processing
   - Spark: In-memory processing

2. **Performance**
   - MapReduce: Higher latency
   - Spark: Lower latency, faster processing

3. **Programming Model**
   - MapReduce: Limited to map and reduce
   - Spark: Rich set of operations

### Example: Word Count Problem

#### MapReduce Solution:
```java
// Map function
public void map(LongWritable key, Text value, Context context) {
    String[] words = value.toString().split(" ");
    for (String word : words) {
        context.write(new Text(word), new IntWritable(1));
    }
}

// Reduce function
public void reduce(Text key, Iterable<IntWritable> values, Context context) {
    int sum = 0;
    for (IntWritable val : values) {
        sum += val.get();
    }
    context.write(key, new IntWritable(sum));
}
```

#### Spark Solution:
```python
# Spark solution
text_file = spark.textFile("hdfs://...")
counts = text_file.flatMap(lambda line: line.split(" ")) \
                 .map(lambda word: (word, 1)) \
                 .reduceByKey(lambda a, b: a + b)
```

## 8. Resilient Distributed Dataset (RDD)

### a) Properties of RDDs:
1. **Immutability**
   - RDDs are read-only
   - Changes create new RDDs
   - Enables fault tolerance

2. **Partitioning**
   - Data divided into partitions
   - Distributed across cluster
   - Enables parallel processing

3. **Lineage**
   - Tracks data transformations
   - Enables fault recovery
   - Maintains data provenance

### b) RDD Operations:

1. **Transformations**
   - Create new RDDs
   - Lazy evaluation
   - Examples: map, filter, groupBy

2. **Actions**
   - Return results to driver
   - Trigger computation
   - Examples: count, collect, save

### c) Creating RDDs:

1. **From Existing Data**
   - Parallelizing collections
   - Reading from storage
   - Converting from other RDDs

2. **From External Sources**
   - HDFS files
   - Local files
   - Databases

3. **From Other RDDs**
   - Transformations
   - Joins
   - Aggregations 
# Hadoop Big Data Analysis

This project explores the use of Hadoop MapReduce for large-scale data processing and distributed computation. It covers core big data operations such as joins, set differences, graph-based aggregations, and distributed sorting using MapReduce on Hadoop Distributed File System (HDFS).


This repository contains a collection of Hadoop MapReduce programs developed to simulate real-world big data tasks using structured and semi-structured datasets. It focuses on implementing:

- Inner and outer joins  
- Set difference operations  
- Graph path-based friend recommendations  
- Sorting key/value datasets on HDFS  

---

## Technologies Used

- Java (Hadoop MapReduce API)  
- Hadoop 3.x  
- HDFS (Hadoop Distributed File System)  
- Linux Shell (for HDFS interaction and job execution)  

---

##  Project Features

### Join Operations

Performs different types of joins on relational data using custom `Mapper` and `Reducer` logic.

#### 1. Inner Join between Tables `T1(A1, A2)` and `T2(A3, A1)`
- Joins on foreign key `A1` using custom MapReduce job.  
- Output format: `(A3, A1, A2)`  


#### 2. Full Outer Join
- Combines all records from both tables, inserting `null` where no match is found.  
- Output format: `(A3/null, A1, A2)`  

#### 3. Set Difference Operation
- Computes `A1[T1] - A1[T2]`, i.e., the values of A1 that appear in `T1` but not in `T2`.  

### Graph Aggregation: Friends of Friends

Given a weighted graph of friendships, this job computes the **Friends of Friends (FoF)** for a specified user (e.g., `P1`) and aggregates the path weights.

- Supports multi-hop relationships with cumulative path weight calculation.  
- Demonstrates graph traversal logic using MapReduce. 
- Output: `Person → FriendOfFriend, Aggregated Weight`

---

### Distributed Sorting on HDFS

Implements a MapReduce job that sorts key/value pairs by key using Hadoop's built-in sorting mechanism.

- Input: Unsorted key/value pairs stored on HDFS.  
- Output: Sorted data saved back to HDFS.  
- Demonstrates use of Hadoop partitioner and key grouping.

---

## How to Run

> Assumes Hadoop is installed and configured correctly on your machine or cluster.

1. Compile Java code:
 ```bash
 hadoop com.sun.tools.javac.Main JoinJob.java
 jar cf joinjob.jar JoinJob*.class
 ```

2.Upload data to HDFS:
 ```bash
hdfs dfs -put ./data/input /user/hadoop/input
```

3. Run the MapReduce job:
```bash
hadoop jar joinjob.jar JoinJob /user/hadoop/input /user/hadoop/output
```
4. View results:
```bash
hdfs dfs -cat /user/hadoop/output/part-*
```
## Directory Structure
Hadoop-Big-Data-Analysis/
├── data/
│   └── input/               # Sample datasets for each question
├── src/
│   ├── JoinJob.java         # Inner and full outer join implementations
│   ├── SetDifference.java   # Set subtraction implementation
│   ├── FriendGraph.java     # Friends of Friends aggregation
│   └── SortJob.java         # HDFS sorting program
├── README.md

## Use Cases

Educational: Demonstrate core big data operations in a Hadoop environment.
Analytical: Explore how basic SQL-like operations translate to distributed systems.
Engineering: Build reusable MapReduce jobs for custom data processing pipelines.

## License
This project is licensed under the MIT License. See the LICENSE file for more information.




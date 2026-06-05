# Big Data Resources

### Articles:

- #### Big Data
- https://www.ibm.com/think/topics/big-data-analytics

- https://www.digitalocean.com/community/tutorials/an-introduction-to-big-data-concepts-and-terminology

- https://www.suse.com/c/rancher_blog/an-introduction-to-big-data-concepts/

- additional 
    - https://www.edureka.co/blog/hadoop-ecosystem

- #### Hadoop
- https://hadoop.apache.org/
- https://www.databricks.com/blog/what-is-hadoop

- #### Map Reduce
- https://en.wikipedia.org/wiki/MapReduce

- #### Spark
- https://spark.apache.org/ - not that useful maybe
- https://github.com/apache/spark - maybe not that useful 
- need to find better resources for spark theoretical study maybe


## Papers - quite important

- GFS Paper - gfs-sosp2003.pdf - **The Google File System Sanjay Ghemawat, Howard Gobioff, and Shun-Tak Leung Google∗**
- Hadoop paper 1 - hdfs.pdf - **The Hadoop Distributed File System Konstantin Shvachko, Hairong Kuang, Sanjay Radia, Robert Chansler Yahoo! Sunnyvale, California USA**
- Hadoop paper 2 - hdfs_design.pdf - **HDFS Architecture Guide**
- MapReduce Paper - mapreduce-osdi04.pdf - **MapReduce: Simplified Data Processing on Large Clusters Jeffrey Dean and Sanjay Ghemawat**
- Spark paper - i don't know ?
- RDD Paper - nsdi12-final138.pdf - **Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing**


- Paper reading strategy : [Paper reading strategy](#paper-reading-strategy)

### Books:

#### Recommended by ma'am - only for reference

**Designing Data-Intensive Applications The Big Ideas Behind Reliable, Scalable, and Maintainable Systems Martin Kleppmann**

---
- Big Data: A Revolution That Will Transform How We Live, Work, and Think by Viktor


### PPT
Stored locally here


### Extra reads - related and indirectly related

- CRM: https://www.ibm.com/think/topics/crm
- NoSQL - https://www.digitalocean.com/community/tutorials/a-comparison-of-nosql-database-management-systems-and-models
- https://blog.professorbeekums.com/2022/what-does-a-10x-developer-mean/
- https://blog.professorbeekums.com/heroes-in-software-development/



## Paper reading strategy

Yes, starting with the **GFS Paper** is 100% the right move. It is the "Genesis" of modern Big Data.

To achieve mastery, you should follow the **chronological and conceptual evolution** of the field. Big Data is built on two pillars: **Storage** (how to keep it) and **Compute** (how to process it).

Here is the recommended order for your papers and the reasoning behind it:

---

### Phase 1: Distributed Storage (The "Where")
*You must understand how files are split across 1000s of machines before you can understand how to run code on them.*

1.  **GFS Paper (2003):** 
    *   **Why:** This defined the concepts of "Master/Chunkserver," 64MB chunks, and the idea that "Failure is the norm." It is the blueprint for everything that followed.
2.  **HDFS Architecture Guide (hdfs_design.pdf):** 
    *   **Why:** Read this first among the Hadoop papers. It’s a conceptual bridge. It explains how Yahoo took the GFS ideas and turned them into the HDFS we use today.
3.  **Hadoop Paper 1 (hdfs.pdf - Shvachko et al.):** 
    *   **Why:** This is a more "engineering-heavy" look at HDFS in practice. It discusses the actual implementation at Yahoo and the limitations they found (like NameNode memory issues).

---

### Phase 2: Distributed Processing (The "How")
*Now that you have the storage, how do you handle the processing without moving all that data over the network?*

4.  **MapReduce Paper (2004):** 
    *   **Why:** This is the "Compute" counterpart to GFS. It introduced the `Map` and `Reduce` functions as a way to process data **locally** on the nodes where the GFS chunks live. It’s the father of all distributed compute frameworks.

---

### Phase 3: The Evolution to In-Memory (The "Fast")
*By 2010, MapReduce was considered "slow" because it wrote data to the disk after every step. The industry needed speed.*

5.  **RDD Paper (nsdi12-final138.pdf):** 
    *   **Why:** This *is* the Spark paper. RDD (Resilient Distributed Datasets) is the core abstraction of Spark.
    *   **The "Aha!" Moment:** This paper identifies the biggest flaw in MapReduce (excessive disk I/O) and proposes keeping data in **RAM** across the cluster while still being fault-tolerant. 

---

### Summary of the "Storyline"
If you read them in this order, you are following a 10-year narrative of problem-solving:

*   **GFS:** "How do we store a petabyte on cheap, failing hard drives?"
*   **HDFS:** "How do we make an open-source version of that for everyone?"
*   **MapReduce:** "Now that we have a petabyte, how do we search it without breaking the network?"
*   **RDD/Spark:** "MapReduce is too slow for machine learning and iterative tasks; can we do it all in RAM?"

### Your Next Step:
Since you've started the **GFS Paper**, I suggest we do a deep dive into it next. 

**Do you want to start by discussing the "Single Master" bottleneck in GFS or how Google handles "Atomic Record Appends"?** (Both are frequent exam and interview topics).
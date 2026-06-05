*(Just to wrap up the DBFS checkpoint: 1. It will crash with a "File Not Found" error. Because you used `file:/`, you saved it to the *local* hard drive of the Driver Node, which was destroyed when the cluster turned off. 2. You should change the path to `dbfs:/data/raw_banking.csv` (or just `/data/...`) so it saves permanently to AWS/Azure Object Storage!)*

Now we are getting to the real magic: **Spark Core**. 

This is the exact computing engine that powers Databricks. If you understand how Spark actually processes data under the hood, you will write PySpark code that is 100x faster than a junior engineer's code.

Here is the deep dive into the theory.

---

### 1. The Core Theory: Spark Architecture (Slides 8-13)
Apache Spark operates on a **Master/Slave** architecture (often called Driver/Worker).

*   **The Driver (Master):** This is the brain. When you run a Databricks Notebook, your Python code runs on the Driver. The Driver's job is to read your code, figure out what you want to do, and break it down into tiny "Tasks."
*   **The Cluster Manager:** (e.g., YARN, Mesos, or Databricks' built-in manager). The Driver goes to the Cluster Manager and says, "I have 1,000 tasks, give me some computers."
*   **The Executors (Workers/Slaves):** These are the actual computers doing the heavy lifting. They receive the "Tasks" from the Driver, process the data in their RAM, and send the results back to the Driver.

### 2. The Core Theory: RDDs (Resilient Distributed Datasets)
Before DataFrames existed in Spark, the fundamental building block of Spark was the **RDD** (Slides 16-22). 
*   **Resilient:** Fault-tolerant. If an Executor dies halfway through a job, Spark just gives that task to a different Executor to do again. 
*   **Distributed:** The data is chopped up into "Partitions" and spread across all the Executors.
*   **Dataset:** The actual data (in-memory).

### 3. The Most Important Concept in Spark: Transformations vs. Actions (Slides 18-20 & 28-29)
This is guaranteed to be in every Big Data interview. You must understand the difference:

**A. Transformations (Lazy Evaluation)**
*   Commands like `.map()`, `.filter()`, or `.groupBy()`.
*   *The Magic:* When you write a Transformation in Databricks and hit "Run", **Spark does absolutely nothing to the data.** It is *Lazy*. 
*   Instead of doing the math immediately, the Driver just writes down your instructions on a notepad. It creates a **DAG (Directed Acyclic Graph)**, which is just a map of the steps (e.g., "Step 1: Filter, Step 2: Group").

**B. Actions (The Trigger)**
*   Commands like `.count()`, `.collect()`, or `.display()`.
*   *The Magic:* Once Spark sees an Action, it says, "Okay, the user actually wants to see the final result now." It looks at the DAG (the notepad of instructions), sends the tasks to the Executors, and physically computes the data.

### 4. Advanced Spark Optimization (Slides 24-26)
*   **Caching/Persisting:** If you are going to use the same DataFrame multiple times, you can tell Spark to keep it in RAM (`.cache()`) so it doesn't have to re-read it from AWS/Azure every time.
*   **Narrow vs. Wide Transformations (Slide 29):**
    *   *Narrow:* `.filter()`. Each Executor can filter its own chunk of data independently. Very fast.
    *   *Wide:* `.groupBy()`. Executors have to send data to *each other* over the network to group things together (called a **Shuffle**). Very slow and expensive.
*   **Broadcast Variables:** If you have a tiny lookup table (like a list of 50 US States), you can "Broadcast" it. Spark will send a copy of that tiny table to *every single Executor's RAM*, so they never have to talk to each other over the network to do a lookup!

---

### 🚀 The "Databricks Philosophy": We hid the RDDs

Here is the most important thing to know about this transcript: **In modern Databricks, you will almost never write RDD code.**

Writing raw RDD code (using `.map()` and `lambda` functions) is difficult and slow. Databricks created the **DataFrame API** and **Spark SQL** to sit *on top* of RDDs. 
*   When you write `df.select("name")` in PySpark, Databricks secretly converts that down into complex RDD code for you under the hood using an engine called the Catalyst Optimizer. 
*   However, the *theory* (Lazy Evaluation, DAGs, Actions vs Transformations, Shuffles) applies exactly the same to DataFrames as it does to RDDs!

---

### Conceptual Checkpoint 🧠

Let's test this Spark theory. This is a classic interview question.

*You write the following three lines of PySpark code in a Databricks Notebook cell and hit "Run":*

```python
# Line 1
df = spark.read.csv("/data/sales.csv")

# Line 2
filtered_df = df.filter(df.sales > 1000)

# Line 3
grouped_df = filtered_df.groupBy("Region").sum("sales")
```

*1. You notice that this cell executes in **0.01 seconds**. You know that `sales.csv` is 10 Terabytes in size. How is it possible that Spark processed 10TB of data in 0.01 seconds?*

*2. If you want Spark to actually execute the math and show you the final grouped data on your screen, what type of Spark operation (Transformation or Action) do you need to add to Line 4?*
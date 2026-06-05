*(Just confirming your implicit UNIX troubleshooting answers: 1. You would use `cat app_config.json` to dump it onto the screen. 2. You would use `cat system_logs.txt | grep "Error"`. Perfect!)*

This transcript is a list of practical exercises for **Shell Scripting**. 

While the previous module taught us individual UNIX commands (like `cat`, `grep`, `wc`), this module introduces the concept of writing a **Script**—which is just putting a bunch of those commands together into a file so they can run automatically with logic (if/then, loops, math).

Let's break down the core concepts of Shell Scripting hidden inside these activities and how they connect to Data Engineering.

---

### 1. The Core Theory: Shell Scripting Concepts

**A. Command Line Arguments (Activities 1, 3, 5, 6, 7)**
When you run a script, you can pass data to it directly from the terminal without the script having to ask you for it. 
*   *Example:* If you write a script called `calculate_sum.sh`, you can run it by typing `$ ./calculate_sum.sh 5 10 15`. 
*   The script automatically reads the numbers 5, 10, and 15 into special variables (`$1`, `$2`, `$3`).

**B. Flow Control (Activities 4, 5, 6)**
Just like Python or Java, UNIX Shell Scripts have programming logic:
*   **`If/Then` Statements (Activity 4):** Checking conditions. (e.g., `if [ "$string1" == "$string2" ]; then echo "Equal!"`)
*   **`While` Loops (Activity 5):** Running a block of code repeatedly until a condition is met. (e.g., looping from 1 to `n` to print odd numbers).
*   **`Case` Statements (Activity 6):** Like a giant `If/Else` block. Useful for checking a variable against a specific list of options.

**C. Text & Math Processing (Activities 2 & 3)**
*   **Math:** UNIX shell can do basic arithmetic.
*   **Text (Activity 2):** This activity specifically asks you to read a file and print the lines, words, and characters. Based on the last module, you know this is asking you to use the **`wc`** command inside a script!

**D. Debugging (Activities 7 & 8)**
Debugging a shell script can be notoriously difficult because it doesn't give clean error messages like Python.
*   **`-x` and `-v` flags:** If you run a script using `bash -x script.sh`, it prints every single line of code to the screen *right before* it executes it. This is invaluable for finding exactly where a script crashed.

---

### 🚀 The "Databricks Philosophy": Shell Scripting vs. Python

If you look at these activities (checking if a number is prime, doing math, comparing strings), they look exactly like a Python 101 homework assignment. 

*So, if we have Python, why do we care about Shell Scripting?*

**1. Python is for Data, Shell is for Infrastructure.**
In Databricks, you will almost *never* use a Shell Script to do math, calculate primes, or process a CSV file. Python (via PySpark) is infinitely better, faster, and safer for Data Engineering. 
*   However, you **will** use Shell Scripts for Infrastructure. 
*   Remember the **Databricks Init Scripts** we talked about earlier? Those are literally Shell Scripts (ending in `.sh`)! 
*   When a cluster boots up, it uses Shell Scripting (`if/then` logic) to check what kind of cluster it is, and then uses command-line arguments to download specific Python libraries or connect to specific corporate firewalls.

**2. Orchestration & Cron Jobs**
Before modern orchestrators (like Airflow or Databricks Workflows), Data Engineers used Shell Scripts and a UNIX tool called `cron` to schedule their ETL pipelines. A shell script would literally wake up at 3:00 AM, log into a database, trigger a data extraction, and email the team if it failed.

---

### Conceptual Checkpoint 🧠

Let's test this understanding of when to use Shell vs. Python.

*You have been tasked with building an automated pipeline for Databricks. The pipeline has two distinct requirements:*

1. *Before the Databricks cluster turns on, it needs to check if the company's secure network is currently online. If the network is down, it should abort the cluster boot-up process.*
2. *Once the cluster is running, it needs to read a 10-Terabyte JSON file, calculate the total revenue for the year, and write the answer to a Delta Table.*

*Based on the philosophy above, which of these two tasks would you write using a **UNIX Shell Script** (Init Script), and which task would you write using **Python/PySpark** inside a Databricks Notebook?*

Whenever you're ready, feel free to answer or paste the next transcript!
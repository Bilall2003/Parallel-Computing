#Multiprocessing vs Multithreading in Python
**Overview**

This project demonstrates the difference between multiprocessing and multithreading in Python.
It measures and compares the execution time of both approaches when performing a computationally intensive task (do_something()).

Python’s Global Interpreter Lock (GIL) can prevent true parallel execution of threads in CPU-bound tasks — which is why multiprocessing often performs better in such cases.

**How It Works**
1. do_something() function

This is a user-defined function located in a separate file called do_something.py.
It represents a workload — either CPU-bound or I/O-bound.

Example implementation:

# do_something.py
def do_something(size, out_list):
    for i in range(size):
        out_list.append(i ** 2)   # Simple CPU-bound operation


You can replace it with your own function (e.g., file reading, API calls, matrix calculations, etc.) depending on what you want to test.

2. The main script (multithreading_test.py)

This script runs the same task twice:

Using multiprocessing (with 10 processes)

Using multithreading (with 10 threads)

It measures execution time for both and prints a comparison.


**Explanation of Key Parts**

Multiprocessing Section
for i in range(procs):
    out_list = list()
    process = multiprocessing.Process(target=do_something, args=(size, out_list))
    jobs.append(process)
    
Creates 10 separate processes.
Each process runs in parallel on different CPU cores.
Perfect for CPU-bound tasks (math, computation, data processing).

Multithreading Section
for k in range(threads):
    out_list = list()
    thread = threading.Thread(target=do_something, args=(size, out_list))
    jobs.append(thread)

Creates 10 threads within a single process.
Threads share the same memory space.
Best for I/O-bound tasks (network requests, file I/O, etc.).


 **How to Run**
Save both files in the same directory.
Run the script:
python multithreading_test.py

Observe execution times for both sections.

**Learnings**

Multiprocessing spawns separate Python interpreters → true parallel execution.
Multithreading shares the same interpreter → limited by the GIL for CPU tasks.
Choosing between them depends on task type:

Use threads for I/O.

Use processes for CPU-heavy work.

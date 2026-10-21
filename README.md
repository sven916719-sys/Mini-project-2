# Job Scheduling Using Graph (Adjacency List & Traversal)

## 1. Introduction
This mini-project implements a **Job Scheduling System** in Python using graph theory concepts aligned with the Data Structures syllabus. In operating systems and build automation pipelines, tasks cannot execute arbitrarily if prerequisite constraints exist. This system models tasks and prerequisite dependencies as a **Directed Acyclic Graph (DAG)** and computes a conflict-free, deadlock-free sequential execution order.

## 2. Objectives
* Implement standard graph storage representation using an **Adjacency List** and an **In-Degree dictionary**.
* Apply breadth-first search (BFS) style graph traversal (**Kahn's Algorithm**) to resolve task dependencies.
* Detect cyclic dependencies (deadlocks) where no valid execution schedule exists.
* Understand the role of in-degree reduction in topological ordering.

## 3. Description
The project executes job scheduling in four sequential stages:
1. **Storage Representation:** Vertices (tasks) are initialized into an adjacency list (mapping prerequisites to dependent tasks) alongside an in-degree map tracking unresolved incoming requirements.
2. **Traversal Initialization:** A queue is initialized with all tasks having an in-degree of $0$ (tasks with no prerequisites that are ready to run immediately).
3. **Graph Traversal Process (BFS):**
   * A ready task is dequeued and appended to the execution schedule.
   * For every neighbor dependent on this task, the neighbor's in-degree is decremented by $1$.
   * When a neighbor's in-degree drops to $0$ (all prerequisites completed), it is enqueued.
4. **Deadlock / Cycle Detection:** If the number of scheduled tasks equals the total number of vertices, the schedule is valid. If fewer tasks are processed, a circular dependency (deadlock) exists, and an error is flagged.

## 4. Technologies Used
* **Programming Language:** Python 3
* **Environment:** Terminal / Command Prompt or Jupyter Notebook (`.ipynb`)
* **Core Data Structures:** Python dictionaries (hash map representation of Adjacency List) and lists (queue abstraction).

## 5. Features
* Dynamic configuration of jobs (vertices) and prerequisite dependencies (directed edges).
* Built-in cycle detection preventing infinite execution loops caused by mutual prerequisites.
* Step-by-step sequential execution order display.
* Zero external third-party library dependencies.

## 6. Graph and Queue Operations Used
* `adj_list[u].append(v)`: Adds a directed edge $(u \to v)$ indicating Task $u$ must finish before Task $v$ begins.
* `in_degree[v] += 1`: Tracks incoming edges representing active prerequisites for vertex $v$.
* `queue.pop(0)`: FIFO dequeuing of tasks whose prerequisite constraints are satisfied.
* `queue.append(neighbor)`: Enqueues tasks once their incoming edge count drops to zero ($0$).

## 7. How to Run the Project
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/Job-Scheduling-Graph.git
   cd Job-Scheduling-Graph
   ```
2. Run the script:
   ```bash
   python job_scheduling.py
   ```
3. Example Output:
   ```text
   --- Graph-Based Job Scheduling Sequence ---
   Step 1: Task A
   Step 2: Task B
   Step 3: Task C
   Step 4: Task D
   Step 5: Task E
   ```
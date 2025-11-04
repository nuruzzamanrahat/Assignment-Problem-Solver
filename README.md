# 🎯 Optimization Project: Assignment Problem Solver

This project is an **interactive web application** that solves the classic **Assignment Problem** using the **Hungarian Method (Munkres Algorithm)**.

It provides a clear, hands-on tool for understanding how to find the **minimum cost one-to-one assignment** between two sets of equal size (e.g., agents to tasks, workers to jobs).  
This project was built to demonstrate understanding of core topics in an **Optimization Techniques** course.

---

## 🚀 Live Demo & Usage

[► View Live Demo](https://nuruzzamanrahat.github.io/Assignment-Problem-Solver/)


## 🧭 How to Use the Solver

1. **Define Problem Size**  
   Use the **"Set Size (N)"** input to define the N × N matrix size (e.g., 4 agents and 4 tasks).

2. **Define Names (Optional)**  
   Click on default names like “Agent 1” or “Task 1” to rename them.

3. **Define Cost Matrix**  
   Enter the cost of assigning each agent (row) to each task (column).

4. **Find Optimal Solution**  
   Click **"Find Optimal Solution"** to calculate results using the Hungarian Method.

5. **View Results**  
   The application will display:
   - ✅ **Minimum Total Cost**
   - ✅ **List of Optimal Assignments** (e.g., “Agent 1 → Task 3”)
   - ✅ **Assignment Matrix** with optimal cells highlighted in green

---

## 📘 1. The Assignment Problem

The **Assignment Problem** is a core combinatorial optimization problem.

> Given a set of *N agents* and *N tasks*, and a cost matrix **C** where C(i, j) is the cost of assigning agent *i* to task *j*,  
> find the one-to-one assignment that **minimizes total cost**.

### 🔢 Mathematical Formulation

Minimize:

$$
Z = \sum_{i=1}^{N} \sum_{j=1}^{N} C_{ij} \cdot X_{ij}
$$

Subject to:

1. **Each agent is assigned to exactly one task:**
   $$
   \sum_{j=1}^{N} X_{ij} = 1 \quad \text{for } i = 1, 2, ..., N
   $$

2. **Each task is assigned to exactly one agent:**
   $$
   \sum_{i=1}^{N} X_{ij} = 1 \quad \text{for } j = 1, 2, ..., N
   $$

3. **Binary Decision Variable:**
   $$
   X_{ij} =
   \begin{cases}
   1 & \text{if agent } i \text{ is assigned to task } j \\
   0 & \text{otherwise}
   \end{cases}
   $$

> This problem is a **special case of the Transportation Problem**, but can be solved more efficiently using a specialized algorithm.

---

## 🧮 2. The Hungarian Method

The **Hungarian Method** (also known as the **Munkres algorithm**) solves the Assignment Problem in **polynomial time**.  
It transforms the cost matrix to expose a clear zero-cost solution.

### 🔍 High-Level Algorithm Steps

#### **Step 1: Matrix Reduction**

- **Row Reduction:** Subtract the smallest element in each row from all elements in that row.  
- **Column Reduction:** Subtract the smallest element in each column from all elements in that column.  

This ensures each row and column has at least one zero.

#### **Step 2: Find Initial Assignment (Star Zeros)**

- Find zeros in the matrix.
- “Star” a zero (mark as chosen) if no other starred zero exists in its row or column.
- Continue until you have as many independent zeros as possible.

#### **Step 3: Cover Columns with Starred Zeros**

- Cover all columns containing a starred zero.

If all columns are covered, you have an optimal solution.

#### **Step 4: Iterate to Find Augmenting Path**

- Find an **uncovered zero** and **prime** it (mark temporarily).
- If the row of this zero has no starred zero → an augmenting path is found (go to Step 5).  
- If it does → cover this row and uncover the column of the starred zero, then repeat.

If no uncovered zeros remain, go to Step 6.

#### **Step 5: Augment the Path**

- Alternate between starred (0*) and primed (0′) zeros along the path.
- Un-star all starred zeros and star all primed zeros.
- Clear all primes and uncover all rows/columns.
- Return to Step 3.

#### **Step 6: Adjust Matrix (No Path Found)**

- Find the **smallest uncovered value (h)**.
- Subtract **h** from all uncovered elements.
- Add **h** to all elements in covered columns.
- Return to Step 4.

#### **Step 7: Check for Optimality**

- When **N starred zeros** exist (one in each row and column), the optimal assignment is achieved.

---

## 🏁 Final Cost Calculation

The final set of **(i, j)** positions of starred zeros represents the **optimal assignments**.

The **minimum total cost** is:

$$
Z^* = \sum_{\text{starred } (i, j)} C_{ij}
$$

---



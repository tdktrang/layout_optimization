# Nonconvex Layout Problem Optimizer

## Description

This project implements a multi-stage optimization approach to solve the nonconvex facility layout problem, based on the methodology described in the paper "A quadratic assignment formulation of the nonconvex layout problem" by Al-Sultan and Van Slyke (1992). The goal is to determine the optimal placement and dimensions of departments within a facility to minimize transportation costs while satisfying area and non-overlap constraints.

The code is contained within the Jupyter Notebook: `Nonconvex_Layout_problem.ipynb`.
Reference
This implementation is based on:

Al-Sultan, K. S., & Van Slyke, R. M. (1992). A quadratic assignment formulation of the nonconvex layout problem. European Journal of Operational Research, 62(2), 185-199.

https://www.sciencedirect.com/science/article/pii/0377221792900417
## How it Works

The optimization process follows a multi-stage approach:

1.  **Ideal Layout Generation:** An initial grid or ellipse-based layout is generated as a starting point.
2.  **Stage 1 (Moment Constraints):** The layout is optimized using a quadratic assignment problem (QAP) formulation. This stage focuses on minimizing a cost function based on squared Euclidean distances between department centers. Moment constraints (up to a specified order, N) are enforced using the SLSQP optimization method to maintain the general shape and distribution of the initial layout.
3.  **Stage 2 (Circle Model):** Departments are modeled as non-overlapping circles with areas specified as input. The objective is to minimize transportation costs (based on Euclidean distances) while penalizing circle overlaps and boundary violations. The L-BFGS-B optimization method is used.
4.  **Stage 3 (Dimension Optimization):** The layout is further refined by optimizing the center coordinates, widths, and heights of rectangular departments. The objective minimizes flow costs (Euclidean distance) while heavily penalizing overlaps, boundary violations, and deviations from the specified department areas. The L-BFGS-B optimization method is employed.

## Usage

To run the optimizer:

1.  Ensure you have the required dependencies installed (see below).
2.  Open and run the Jupyter Notebook `Nonconvex_Layout_problem.ipynb`.
3.  The notebook defines the `MomentLayoutOptimizer` class and runs two main parts:
    * The first part solves a specific 10-department example problem through all three stages and plots the results.
    * The second part generates 5 additional random instances with similar characteristics and runs the optimization process for each, plotting the final rectangular layout for successful runs.
4.  Input data (flow matrix, costs, areas, facility dimensions) for the example problem is defined within the first main execution block (`if __name__ == "__main__":`). You can modify these inputs to solve different layout problems.

## Dependencies

The following Python libraries are required:

* `numpy`
* `scipy` (specifically `scipy.optimize` and `scipy.spatial.distance`)
* `matplotlib`

You can typically install these using pip:

```bash
pip install numpy scipy matplotlib

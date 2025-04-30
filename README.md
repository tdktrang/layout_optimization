<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>README - Nonconvex Layout Problem Optimizer</title>
    <style>
        body { font-family: sans-serif; line-height: 1.6; padding: 20px; }
        h1, h2, h3 { color: #333; }
        code { background-color: #f4f4f4; padding: 2px 4px; border-radius: 4px; }
        pre { background-color: #f4f4f4; padding: 10px; border-radius: 4px; overflow-x: auto; }
        a { color: #007bff; text-decoration: none; }
        a:hover { text-decoration: underline; }
        .container { max-width: 800px; margin: auto; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Nonconvex Layout Problem Optimizer</h1>

        <h2>Description</h2>
        <p>This project implements a multi-stage optimization approach to solve the nonconvex facility layout problem, based on the methodology described in the paper "A quadratic assignment formulation of the nonconvex layout problem" by Al-Sultan and Van Slyke (1992). The goal is to determine the optimal placement and dimensions of departments within a facility to minimize transportation costs while satisfying area and non-overlap constraints.</p>
        <p>The code is contained within the Jupyter Notebook: <code>Nonconvex_Layout_problem.ipynb</code>.</p>

        <h2>How it Works</h2>
        <p>The optimization process follows a multi-stage approach:</p>
        <ol>
            <li><strong>Ideal Layout Generation:</strong> An initial grid or ellipse-based layout is generated as a starting point.</li>
            <li><strong>Stage 1 (Moment Constraints):</strong> The layout is optimized using a quadratic assignment problem (QAP) formulation. This stage focuses on minimizing a cost function based on squared Euclidean distances between department centers. Moment constraints (up to a specified order, N) are enforced using the SLSQP optimization method to maintain the general shape and distribution of the initial layout.</li>
            <li><strong>Stage 2 (Circle Model):</strong> Departments are modeled as non-overlapping circles with areas specified as input. The objective is to minimize transportation costs (based on Euclidean distances) while penalizing circle overlaps and boundary violations. The L-BFGS-B optimization method is used.</li>
            <li><strong>Stage 3 (Dimension Optimization):</strong> The layout is further refined by optimizing the center coordinates, widths, and heights of rectangular departments. The objective minimizes flow costs (Euclidean distance) while heavily penalizing overlaps, boundary violations, and deviations from the specified department areas. The L-BFGS-B optimization method is employed.</li>
        </ol>

        <h2>Usage</h2>
        <p>To run the optimizer:</p>
        <ol>
            <li>Ensure you have the required dependencies installed (see below).</li>
            <li>Open and run the Jupyter Notebook <code>Nonconvex_Layout_problem.ipynb</code>.</li>
            <li>The notebook defines the <code>MomentLayoutOptimizer</code> class and runs two main parts:
                <ul>
                    <li>The first part solves a specific 10-department example problem through all three stages and plots the results.</li>
                    <li>The second part generates 9 additional random instances with similar characteristics and runs the optimization process for each, plotting the final rectangular layout for successful runs.</li>
                </ul>
            </li>
            <li>Input data (flow matrix, costs, areas, facility dimensions) for the example problem is defined within the first main execution block (<code>if __name__ == "__main__":</code>). You can modify these inputs to solve different layout problems.</li>
        </ol>

        <h2>Dependencies</h2>
        <p>The following Python libraries are required:</p>
        <ul>
            <li><code>numpy</code></li>
            <li><code>scipy</code> (specifically <code>scipy.optimize</code> and <code>scipy.spatial.distance</code>)</li>
            <li><code>matplotlib</code></li>
        </ul>
        <p>You can typically install these using pip:</p>
        <pre><code>pip install numpy scipy matplotlib</code></pre>

        <h2>Reference</h2>
        <p>This implementation is based on:</p>
        <p>Al-Sultan, K. S., & Van Slyke, R. M. (1992). A quadratic assignment formulation of the nonconvex layout problem. <i>European Journal of Operational Research</i>, 62(2), 185-199.</p>
        <p><a href="https://www.sciencedirect.com/science/article/pii/0377221792900417" target="_blank">https://www.sciencedirect.com/science/article/pii/0377221792900417</a></p>
    </div>
</body>
</html>

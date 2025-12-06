# Enhanced Simulated Annealing for TSP

This project implements a hybrid **Enhanced Simulated Annealing (ESA)** algorithm to solve the Traveling Salesman Problem (TSP). It is designed to tackle standard TSPLIB instances efficiently by combining probabilistic cooling with deterministic local search optimizations.

## 🚀 Key Features

* **Hybrid Algorithm:** Combines the global search capability of Simulated Annealing with a **Numba-accelerated 2-opt** local search for rapid exploitation.
* **Adaptive Reheating:** Automatically detects solution stagnation and triggers a "reheating" phase (temperature reset + strong perturbation) to escape deep local optima.
* **Parallel Execution:** Leverages multi-core processing using `joblib` to benchmark multiple TSP instances simultaneously.
* **Comprehensive Analysis:** Automatically generates convergence trajectories, temperature schedules, route maps, and performance comparison charts.
* **Exact Baseline:** Includes an integrated **Gurobi Optimizer** module to compare the optimality gap and speed against the proven mathematical solution.

## 🛠️ Technologies & Libraries

The project is built using the following scientific computing stack:

* **Core:** `Python 3.13`, `NumPy`, `Pandas`
* **Optimization:** `Numba` (JIT Compilation), `Gurobipy` (Linear Programming)
* **Data Handling:** `tsplib95` (Instance parsing)
* **Visualization:** `Matplotlib`, `Seaborn`
* **Concurrency:** `Joblib`, `Multiprocessing`

## ⚙️ Methodology

The solver operates on a geometric cooling schedule (`T_new = T_old * alpha`). The "Enhanced" nature comes from three specific modifications:

1.  **Candidate Lists:** Distance matrices are pre-computed, and nearest-neighbor lists are cached to reduce lookup time from `O(N^2)` to `O(N)`.
2.  **Hybridization:** Every accepted Metropolis move is refined using a deterministic 2-opt descent.
3.  **Stagnation Recovery:** If the objective function does not improve for *K* iterations, the system perturbs the current solution by applying **multiple random swaps** (determined by the `strength` parameter) and resets the temperature to a percentage of the initial heat.

## Project Proposal
The original project proposal document can be found [Here] (https://github.com/Mohammed-Alanazii/CS616_PROJECT/blob/main/CS616_Project_Proposal_MOHAMMED_ALANAZI.pdf). It outlines the motivation, objectives, and planned methodology for this implementation.

## Project Overview
The project consists of the following main components:
* **Nearest Neighbor Heuristic:** Generates an initial feasible solution quickly.
* **2-opt Local Search:** Improves solutions by iteratively reverses segments to reduce tour length.
* **Pure Simulated Annealing:** Implements the classic SA algorithm for baseline comparison.
* **Enhanced Simulated Annealing:** The proposed hybrid algorithm with reheating, 2-opt local search and perturbation strategies.
* **Gurobi Optimizer Integration:** Solves TSP instances exactly for benchmarking.
* **Visualization Module:** Generates plots for convergence, temperature schedules, and route maps.
* **Excel Exporter:** Compiles results into an Excel file for easy analysis.

## Project Goals
* Implement and validate the Enhanced Simulated Annealing algorithm on benchmark TSP instances.
* Compare performance against Nearest Neighbor, Local Search, and Pure Simulated Annealing.
* Analyze solution quality, convergence speed, and computational efficiency.

## 📊 Setup & Installation

1.  **Clone this repository:**
    ```bash
    git clone https://github.com/Mohammed-Alanazii/CS616_PROJECT.git
    cd CS616_PROJECT
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Data Setup:** Ensure your `.tsp` benchmark files are located in the `data/tsplib_instances/` directory.

## 🏃‍♂️ How to Run

Open the Jupyter Notebook (`main.ipynb`) and run all cells. The pipeline will:

1.  **Initialize:** Load configuration parameters and TSP instances.
2.  **Execute:** Run Nearest Neighbor, Local Search, Pure SA, and Enhanced SA in parallel.
3.  **Export:** Save numerical results to `results/tsp_final_results.xlsx`.
4.  **Visualize:** Generate performance plots and maps in `results/figures/`.

## 📂 Project Structure

```text
├── CS616_Project_Proposal_MOHAMMED_ALANAZI.pdf  # Project proposal document
├── main.ipynb               # Main executable notebook
├── data/
│   └── tsplib_instances/    # Benchmark .tsp files (e.g., eil51.tsp)
├── results/
│   ├── tsp_final_results.xlsx # Metrics export
│   └── figures/             # Generated plots (Convergence, Maps)
├── requirements.txt         # Dependency list
└── README.md                # Project documentation
```

## 🆕 Recent Enhancements
* **Candidate Lists:** Implemented pre-computation of nearest neighbors to accelerate local search operations.
* **Numba Optimization:** Further optimized the 2-opt local search using Numba JIT compilation for significant speed-ups.

## 📈 Results Overview
The final results, including total distances, optimality gaps, and runtimes for each algorithm across all TSP instances, are compiled in `results/tsp_final_results.xlsx`. Visualizations such as convergence plots and route maps are saved in the `results/figures/` directory.

**Note on Result Stability:**
The reported results are based on single-run experiments. Due to the probabilistic nature of the algorithm and parallel processing variances, you may observe slight deviations in the final gap percentages ($\pm 0.5\%$) when re-running the notebook. This is standard behavior for stochastic optimization methods constrained by **execution time limits**.

## 🎓 Academic Integrity & Acknowledgments

This project was developed as a capstone implementation for the Traveling Salesman Problem (TSP).

* **Original Contribution:** The core `EnhancedSA` algorithm, including the specific reheating logic and hyperparameter tuning, represents my own work.
* **Attribution:** The visualization code was adapted from Dr. Mahdi's instructional materials `Hands-on` and open-source repositories to facilitate robust benchmarking.
* **References:**
  - Dr. Mahdi's Hands-On Files: [Heuristic Session Students](https://drive.google.com/file/d/1AlO-Slr-Y0nKd8b9tk5OUpqOpkEiS2Iw/view?usp=share_link) & [Assignment 2](https://drive.google.com/file/d/1nJJV4gtpycp7uRexjFw8L1svZHqbPHyd/view?usp=share_link) 
  - TSPLIB Library: [TSPLIP95](http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/)
  - Gurobi Optimizer: [Gurobi](https://www.gurobi.com/)
  - Numba Documentation: [Numba](https://numba.pydata.org/)
  - Joblib Documentation: [Joblib](https://joblib.readthedocs.io/)

## Troubleshooting & Support
If you encounter any issues running the notebook or have questions about the implementation, please check the following:
* Ensure all dependencies are installed correctly.
* Verify that the TSP instance files are in the correct directory.
* Review the error messages for hints on what might be wrong.
* Consult the documentation for the libraries used.
* If problems persist, feel free to open an issue in this repository.

## Changelog
- **2025-11-01:** Project proposal submission.
- **2025-11-15:** Initial implementation of Nearest Neighbor, 2-opt local search, Developed basic Simulated Annealing framework
- **2025-11-20:** Implemented Enhanced Simulated Annealing with reheating strategy.
- **2025-11-21:** Candidate List optimization for local search speed-up and reduced time complexity.
- **2025-11-25:** Integrated Numba for JIT compilation of 2-opt local search.
- **2025-12-26:** Integrated Gurobi Optimizer for exact solutions and benchmarking.
- **2025-12-27:** Added parallel execution using Joblib for multiple TSP instances.
- **2025-12-01:** Developed comprehensive visualization dashboard for results analysis.
- **2025-12-04:** Finalized documentation and code comments for clarity.

## 📌 Important Note
The Candidate List optimization mentioned above is a new addition to the original project proposal. This enhancement was implemented to improve the efficiency of the local search process by reducing the time complexity of nearest neighbor lookups. The source and inspiration for this optimization have been duly noted in the references section.

### Special Thanks to Dr. Mahdi for his continuous support, valuable resources, and guidance throughout the semester.

## This project made by Mohammed M. Alanazi
**with the guidance of Dr. Mahdi Khemakhem.**   

## 📬 Contact
For questions or collaboration opportunities, please reach out to Mohammed M. Alanazi at m.alenezi1994@gmail.com, or open an issue in this repository.

### Thank You for Exploring My Project!
### feel free to star⭐ the repository if you found it useful.
### for more projects visit my GitHub profile: [My GitHub](https://github.com/Mohammed-Alanazii)
### Happy Coding! 🚀
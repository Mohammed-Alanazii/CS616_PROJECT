# Enhanced Simulated Annealing for TSP

This project implements a hybrid **Enhanced Simulated Annealing (ESA)** algorithm to solve the Traveling Salesman Problem (TSP). It is designed to tackle standard TSPLIB instances efficiently by combining probabilistic cooling with deterministic local search optimizations.

## 🚀 Key Features

* **Hybrid Algorithm:** Combines the global search capability of Simulated Annealing with a **Numba-accelerated 2-opt** local search for rapid exploitation.
* **Adaptive Reheating:** Automatically detects solution stagnation and triggers a "reheating" phase (temperature reset + strong perturbation) to escape deep local optima.
* **Parallel Execution:** Leverages multi-core processing using `joblib` to benchmark multiple TSP instances simultaneously.
* **Comprehensive Analysis:** Automatically generates convergence trajectories, temperature schedules, connected route maps, and performance comparison charts.
* **Exact Baseline:** Includes an integrated **Gurobi Optimizer** module (optional) to calculate the optimality gap against the proven mathematical solution.

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
3.  **Stagnation Recovery:** If the objective function does not improve for *K* iterations, the system perturbs the current solution (4-opt random kick) and resets the temperature to a percentage of the initial heat.

## 📊 Setup & Installation

1.  **Clone this repository:**
    ```bash
    git clone [https://github.com/yourusername/tsp-enhanced-sa.git](https://github.com/yourusername/tsp-enhanced-sa.git)
    cd tsp-enhanced-sa
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

## 🎓 Academic Integrity & Acknowledgments

This project was developed as a capstone implementation for the Traveling Salesman Problem (TSP).

* **Original Contribution:** The core `EnhancedSA` algorithm, including the specific reheating logic and hyperparameter tuning, represents my own work.
* **Attribution:** The visualization code was adapted from Dr. Mahdi's instructional materials `Hands-on` and open-source repositories to facilitate robust benchmarking.
* **References:**
  - Dr. Mahdi's Hands-On Files: [Heuristic Session Students](https://drive.google.com/file/d/1AlO-Slr-Y0nKd8b9tk5OUpqOpkEiS2Iw/view?usp=share_link) & [Assignment 2](https://drive.google.com/file/d/1nJJV4gtpycp7uRexjFw8L1svZHqbPHyd/view?usp=share_link) 
  - TSPLIB Library: [http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/](http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/)
  - Gurobi Optimizer: [https://www.gurobi.com/](https://www.gurobi.com/)
  - Numba Documentation: [https://numba.pydata.org/](https://numba.pydata.org/)
  - Joblib Documentation: [https://joblib.readthedocs.io/](https://joblib.readthedocs.io/)

## 📝 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Troubleshooting & Support
If you encounter any issues running the notebook or have questions about the implementation, please check the following:
* Ensure all dependencies are installed correctly.
* Verify that the TSP instance files are in the correct directory.
* Review the error messages for hints on what might be wrong.
* Consult the documentation for the libraries used.
* If problems persist, feel free to open an issue in this repository.


## 📬 Contact
For questions or collaboration opportunities, please reach out to Mohammed M. Alanazi at m.alenezi1994@gmail.com, or visit my GitHub profile: [https://github.com/Mohammed-Alanazii](https://github.com/Mohammed-Alanazii) or open an issue in this repository.





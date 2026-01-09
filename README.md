# Omar-DT

# Energy-Aware Autonomous Navigation (CPS & Digital Twin)

This repository contains the implementation of a high-fidelity **Digital Twin** framework for autonomous vehicle navigation. The project integrates **Energy-Aware Model Predictive Control (MPC)** and **Dubins Path Planning** within the **CARLA Simulator** to optimize trajectory tracking and power efficiency in real-time.



## 🏗 System Architecture

Following the formal **acatech (2011)** framework for Cyber-Physical Systems, this software stack is organized into a three-tier hierarchy:

1.  **Service Layer (Cyber Domain):**
    * **Path Planning:** Generates curvature-bounded reference trajectories using Dubins curves (FR3).
    * **MPC Controller:** Solves a multi-objective optimization problem to minimize tracking error and energy consumption (FR4).
2.  **Gateway Layer (Communication Bridge):**
    * **CARLA Python API:** Acts as the synchronization gateway between the discrete-time controller (10Hz) and the continuous-time simulator (FR2).
3.  **Physical Layer (Digital Twin):**
    * **CARLA Simulation Server:** Provides high-fidelity vehicle dynamics (Bicycle Model) and environmental digitization (FR1).



---

## ✅ Functional Requirements (FR)

This system is verified against four core engineering requirements established in the project roadmap:

* **FR1: Digitization of Driving Data:** Real-time extraction of vehicle state vectors (position, velocity, heading) from the Physical Layer.
* **FR2: Data Synchronization:** Management of deterministic feedback loops via the Gateway Layer to ensure real-time control integrity.
* **FR3: Trajectory Synthesis:** Computation of kinematically feasible paths for non-holonomic vehicle constraints.
* **FR4: Energy-Aware Optimization:** Minimization of instantaneous power consumption ($P_i$) through predictive algorithmic refinement.

---

## 🚀 Getting Started

### Prerequisites
* **CARLA Simulator:** Version 0.9.13
* **Python:** 3.7 or higher
* **Core Dependencies:**
    ```bash
    pip install numpy carla opencv-python matplotlib scipy dubins 
    ```

### Installation & Execution
1.  **Launch the CARLA Server:**
    ```bash
    # Navigate to your CARLA folder
    ./CarlaUE4.sh -quality-level=Low
    ```
2.  **Run the Control Stack:**
    Open `MPC.ipynb` in Jupyter Notebook or VS Code and run all cells.
    * The script will connect to the server at `localhost:2000`.
    * It will load **Town03** and spawn the vehicle at a designated start point.
    * The simulation will run in **Synchronous Mode** to ensure deterministic verification.

---

## 📊 Performance & Verification

The controller's performance is analyzed through the **Behavioral View** of the CPS, comparing the Energy-Aware MPC against a standard baseline.

* **Energy Efficiency:** Achieved a **~12.5% reduction** in total energy consumption.
* **Real-Time Performance:** The MPC solver maintains an average latency of **<50ms**, satisfying the 10Hz (100ms) real-time constraint.
* **Tracking Fidelity:** Maintained mean Cross-Track Error (CTE) within safety bounds while optimizing for power.



---

## 🛠 Project Structure
* `MPC.ipynb`: Main implementation including the control loop, MPC optimization logic, and data logging.

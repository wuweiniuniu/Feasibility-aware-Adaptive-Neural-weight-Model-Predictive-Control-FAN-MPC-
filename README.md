# FAN-MPC
## Feasibility-aware Adaptive Neural-weight Model Predictive Control

Research code, data, and demonstration videos accompanying **Hierarchical Adaptive Stability–Energy Torque Allocation for Distributed-Drive Electric Vehicles on Continuous Curved Roads**.

FAN-MPC coordinates lateral stability and energy-efficient torque allocation for distributed-drive electric vehicles on continuous curved roads with varying adhesion. The neural scheduler adjusts MPC priorities; it does not directly generate wheel-torque commands.

## Framework

1. **Physically feasible energy-oriented reference generation.** Motor torque limits, dynamic wheel loads, and residual tire-force capacity define an admissible front-to-rear torque split region. The upper layer minimizes electrical power within that region to generate nominal four-wheel torque references.
2. **Feasibility-aware offline calibration.** Five MPC weights are calibrated by closed-loop Bayesian optimization. Stability, tracking, speed retention, actuator capability, and numerical feasibility are checked before candidate performance is compared. Evaluated, jointly feasible near-optimal candidates support identifiability-aware label selection.
3. **Target-specific neural weight scheduling.** Five radial basis function neural-network predictors combine a regularized global trend with nonlinear RBF terms. Current and preview road features are mapped to bounded, smoothed logarithmic weights.
4. **Constrained LTV-MPC torque coordination.** The lower layer computes executable four-wheel torques while balancing sideslip and yaw-rate tracking, nominal torque-reference tracking, torque smoothness, and remaining tire-force utilization.

The scheduled priorities are `Q_beta`, `Q_r` (yaw-rate weight), `R_alloc`, `R_rate`, and `W_util`.

## Demo Videos

**[Watch both videos on the project webpage](https://wuweiniuniu.github.io/Feasibility-aware-Adaptive-Neural-weight-Model-Predictive-Control-FAN-MPC-/#demo-videos)**

The webpage provides separate browser video players for the mild and extreme curved-road demonstrations. Large MP4 files remain in GitHub Releases rather than in the Git repository.

| Demonstration | Watch on webpage | MP4 fallback |
| --- | --- | --- |
| Mild curved-road condition | [Mild Condition](https://wuweiniuniu.github.io/Feasibility-aware-Adaptive-Neural-weight-Model-Predictive-Control-FAN-MPC-/#mild-condition) | [mild_condition.mp4](https://github.com/wuweiniuniu/Feasibility-aware-Adaptive-Neural-weight-Model-Predictive-Control-FAN-MPC-/releases/download/video_pages/mild_condition.mp4) |
| Extreme curved-road condition | [Extreme Condition](https://wuweiniuniu.github.io/Feasibility-aware-Adaptive-Neural-weight-Model-Predictive-Control-FAN-MPC-/#extreme-condition) | [extreme_condition.mp4](https://github.com/wuweiniuniu/Feasibility-aware-Adaptive-Neural-weight-Model-Predictive-Control-FAN-MPC-/releases/download/video_pages/extreme_condition.mp4) |

The project webpage is distinct from this GitHub README page. If it returns 404 after a repository rename, check **Settings → Pages** and publish the existing `index.html` from **main / (root)**. Do not upload the MP4 files again.

## Repository Contents

- [`code/siWDqudong_FAN_MPC.slx`](code/siWDqudong_FAN_MPC.slx): Simulink controller model.
- [`code/Motor_Torque.m`](code/Motor_Torque.m): motor/torque-related MATLAB code.
- [`code/Physics_Guided_Neural_Network.m`](code/Physics_Guided_Neural_Network.m): neural-network-related MATLAB code.
- [`code/Road_Condition_Info.m`](code/Road_Condition_Info.m): road-condition processing code.
- [`dataset/`](dataset/): available data files.
- [`index.html`](index.html) and [`style.css`](style.css): project webpage.
- [GitHub Releases](https://github.com/wuweiniuniu/Feasibility-aware-Adaptive-Neural-weight-Model-Predictive-Control-FAN-MPC-/releases/tag/video_pages): demonstration video assets.

## Reproduction and Dependencies

The supplied files are MATLAB/Simulink research artifacts. Full closed-loop reproduction requires the compatible vehicle model, motor efficiency data, MATLAB toolboxes, and CarSim installation/licence used by the experiment setup. HIL reproduction additionally requires the corresponding real-time hardware and CAN interfaces. This repository is not a standalone executable application.

## Manuscript and Evaluation

The accompanying manuscript describes CarSim/Simulink development, HIL controller comparisons and ablations, and 100 Hz VCU execution. It reports up to 8.55% lower energy consumption against the tested representative controllers while satisfying the prescribed stability and speed-retention requirements. These are manuscript-reported results, not a claim that every repository configuration has been independently reproduced.

The manuscript will be released after the review process.

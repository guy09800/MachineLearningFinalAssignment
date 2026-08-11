# Acoustic Source Localization with MMSE

A signal-processing and machine-learning assignment that estimates the horizontal position of a sound source from measurements recorded by three sensors.

The project evaluates how measurement noise and time-window length affect localization. It uses a physics-based phase model, least-squares coefficient estimation, and a grid search that selects the candidate position with the minimum squared reconstruction error.

## Problem Setup

A 50 Hz source moves along a stage from `x = 0 m` to `x = 10 m`. Three sensors are positioned above the stage:

| Parameter | Value |
|---|---:|
| Sensor x-coordinates | 3 m, 5 m, 7 m |
| Sensor y-coordinate | 8 m |
| Stage y-coordinate | 0 m |
| Source frequency | 50 Hz |
| Speed of sound | 343 m/s |
| Candidate-position spacing | 0.01 m |
| Samples per dataset | 12,000 |
| Sampling interval | 0.005 s |
| Recording duration | 60 s |

Each CSV file contains a timestamp column and measurements from the three sensors.

## Method

For every time window and candidate source position:

1. Calculate the distance from the candidate position to each sensor.
2. Convert propagation delay into a phase shift.
3. Build a feature matrix from the expected cosine signal at each sensor.
4. Estimate the sensor coefficients using the Moore-Penrose pseudoinverse:

   ```text
   w = pinv(X) @ s
   ```

5. Calculate the squared reconstruction error:

   ```text
   error = ||Xw - s||²
   ```

6. Select the candidate position with the lowest error.

The notebook repeats the analysis for low, medium, and high noise levels, then compares window lengths of 0.2, 0.5, 1, and 2 seconds.

## Repository Contents

| File | Description |
|---|---|
| `final_assignment.ipynb` | Main implementation, experiments, plots, and results |
| `sensor_signals_low_noise.csv` | Sensor measurements with low noise |
| `sensor_signals_medium_noise.csv` | Sensor measurements with medium noise |
| `sensor_signals_high_noise.csv` | Sensor measurements with high noise |
| `final_assignment.pdf` | PDF export of the completed assignment |
| `דיון.pdf` | Discussion of the results |
| `נספח הוראות סוכן.pdf` | Agent-instructions appendix |
| `נספח פרומפטים.pdf` | Prompts appendix |
| `עבודה סמסטר א תשפו מבלס - חלק 2.pdf` | Original assignment document |

## Requirements

- Python 3.10 or newer
- Jupyter Notebook or JupyterLab
- NumPy
- pandas
- Matplotlib

Install the required packages with:

```bash
python -m pip install jupyter numpy pandas matplotlib
```

## Running the Project

1. Clone the repository:

   ```bash
   git clone https://github.com/guy09800/MachineLearningFinalAssignment.git
   cd MachineLearningFinalAssignment
   ```

2. Start Jupyter:

   ```bash
   jupyter notebook
   ```

3. Open `final_assignment.ipynb` and run the cells from top to bottom.

Keep the three CSV files in the repository root so the notebook can load them using its existing relative paths.

## Experiments and Output

The notebook produces:

- A plot of the three sensor signals
- MMSE error versus candidate position
- Estimated source position over time
- A comparison across low, medium, and high noise
- A comparison across different time-window lengths

These experiments illustrate the trade-off between temporal resolution and estimation stability: shorter windows react more quickly, while longer windows use more samples per estimate and can be more robust to noise.

## Technologies

Python · NumPy · pandas · Matplotlib · Jupyter Notebook

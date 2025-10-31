## Human Activity Recognition using Hidden Markov Models (HMM)

##  Overview
This project identifies human activity states (*standing, walking, jumping, still*) using motion data collected from smartphone sensors (accelerometer and gyroscope).  
A Hidden Markov Model (HMM) was implemented to infer hidden activities from observed sensor features, capturing temporal dependencies between movement patterns.


##  Repository Structure

##  Workflow Summary
1. **Data Collection & Cleaning**
   - Recorded four activities (Standing, Walking, Jumping, Still) using the *Sensor Logger* app.  
   - Data collected at ≈ 100 Hz and exported as CSV files.
   - Merged into one clean dataset and visualized accelerometer/gyroscope time-series.

2. **Feature Extraction**
   - Computed both time-domain and frequency-domain features:
     - Mean, standard deviation, RMS magnitude, SMA
     - Axis correlations (X–Y, Y–Z, X–Z)
     - Dominant frequency and spectral energy (via FFT)
   - Normalized all features using Z-score normalization.

3. **Model Definition**
   - Hidden States: `standing`, `walking`, `jumping`, `still`  
   - Observations: extracted feature vectors  
   - Parameters:
     - Transition probabilities (A)
     - Emission probabilities (B – Gaussian)
     - Initial probabilities (π)

4. **Training & Decoding**
   - Implemented **Baum–Welch** for parameter estimation (EM training).  
   - Implemented **Viterbi** algorithm to decode the most probable activity sequence.  
   - Visualization: transition matrix heatmap, emission means bar chart, decoded sequence plots.

5. **Evaluation**
   - Tested on unseen data (new session).  
   - Computed Sensitivity, Specificity, and Accuracy per activity.  
   - Visualized results using a confusion matrix and metrics bar chart.



##  Results Summary

| Activity | Sensitivity | Specificity |
|-----------|-------------|-------------|
| Jumping   | 0.934 | 0.994 |
| Standing  | 0.000 | 1.000 |
| Still     | 0.988 | 0.679 |
| Walking   | 0.980 | 0.958 |

**Overall Accuracy ≈ 0.72**

Key observations:
- High sensitivity for *jumping*, *walking*, and *still* activities.  
- Standing was often misclassified as still, indicating similarity in motion.  
- The model’s transition probabilities realistically captured human movement (e.g., transitions between walking and standing).



##  Discussion & Future Work
- **Challenges:** noisy sensor signals, inconsistent sampling rates, overlap between still and standing classes.  
- **Potential Improvements:**  
  - Collect longer, higher-frequency recordings  
  - Add derived sensors (orientation/quaternion)  
  - Use multi-sensor fusion or hybrid models (HMM + LSTM)



##  Contributors
| Role | Name | Contributions |
|------|------|----------------|
| Lead Data & Model Engineer | **Jolly UMULISA** | Data cleaning, feature extraction, HMM training, analysis |
| Collaborator | **MUGISHA KAREKEZI Joel** | Visualization, evaluation, report preparation |



##  How to Run
1. Open `HiddenMarkovModel.ipynb` in Google Colab or Jupyter.  
2. Upload the four CSVs from the `data/` folder.  
3. Run all cells sequentially — results and plots will appear automatically in `/results`.  
4. To re-train with new data, simply replace the files in `data/`.



##  Tools Used
- Python 3.12  
- NumPy, Pandas, Matplotlib, Seaborn  
- hmmlearn (optional)  
- Google Colab



##  Acknowledgements
Assignment: *Formative 2 – Hidden Markov Models (Modeling Human Activity States)*  
African Leadership University – Machine Learning Techniques I (2025)


# MLB Pitch Prediction Model  

This model predicts whether a pitcher will throw a fastball or an off-speed pitch based on the game situation.  

## Notebooks  

There are four notebooks used to pull raw data, clean and format it, split it into training and test samples, and train and evaluate the models. Comments are included within the files to explain the process. The most recent cell outputs (except for `download_data`) are included to further demonstrate the workflow.  

1. **download_data**  
   - Uses the `pybaseball` Python package to pull Statcast data for the 2024 MLB season.  

2. **clean_pitch**  
   - Transforms raw data into a structured format containing key features required for modeling.  

3. **split_data**  
   - Divides data into features and labels, then further splits it into training, test, and validation sets.  

4. **model_fit**  
   - Trains and evaluates a model to predict pitch type.  

## Methodology  

Pitches are broadly classified as either **fastballs** or **off-speed** pitches.  

The model considers the following game scenarios:  

- Batter and pitcher handedness (right-handed or left-handed).  
- Inning of the at-bat.  
- Score differential.  
- The pitcher's count: behind (e.g., `2-1`), ahead (e.g., `1-2`), or even (e.g., `2-2`).  
- Presence of baserunners (on any or all bases).  
- The type of the previous pitch.  

The dataset is split into training and test subsets.  

A `RandomForestClassifier` is trained and evaluated using different depth and estimator hyperparameters. The top three models are selected and further assessed for accuracy, precision, and recall.  

## Results  

- All three models predicted pitch type with approximately **58% accuracy**.  
- Considering the MLB average fastball usage is **57-58%**, the model’s performance was only marginally better than always guessing "fastball."  
- The precision for all models was quite low, indicating a high number of false positives.  
- However, the recall for fastballs was very high, suggesting that the model correctly identified most fastballs but likely over-predicted them.  

### Next Steps  
- Improve the profiling of hitters and pitchers. Currently, the model only considers them by their Statcast ID.  
- Group pitchers and hitters by tendencies rather than individual identities.  
  - **Example:** Categorizing pitchers based on off-speed pitch usage.  
  - **Example:** Categorizing hitters based on their performance against fastballs.
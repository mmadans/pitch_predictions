# MLB Pitch Predicting Model

This model predicts if the pitcher decides to throw a fastball or off-speed pitch based on the game situation. 

## Notebooks

There are 4 notebooks  used to pull raw data, clean and format, split into a test and training samples, and to finally train and evaluate the models. Comments are included within the files to explain the process. Most recent cell outputs for all notebooks (except download_data) are included to further show the process.

1. download_data
    - Uses the pybaseball Python package to pull statcast data for the 2024 MLB Season
2. clean_pitch
    - Transforms raw data into structured output that contains key features needed for the final model.
3. split_data
    - Divides data into features and labels, and further splits into training, test, and value sets.
4. model_fit
    - Trains and evaluates a model to make pitch predictions.

## Methodology

Pitches are broadly classifed as either a **fastball** or **off-speed**. 

The following game scenarios are considered by the model:
- Batter and Pitchcer are right or left handed
- The inning of the at bat
- The score differential
- If the pitcher is behind (ex. 2-1), ahead (ex. 1-2), or even (2-2) in the batters count
- If there are runners on any or all the bases\
- The pitch type of the previous pitch

The data is split into training and test subsets. 

A RandomForestClassier is trained on the data, and then evaluated for a set of depth and estimator hyper parameters. The top 3 models are chosen, and further evaluted for their accuracy, precision, and recall.

## Results

- All 3 models accurately predicted pitch type about 58% of the time. 
- Considering MLB avg. Fastball usage is 57-58%, this is not much better than if someone were to just guest "fastball" every pitch
    - To an extent, this may have been how the model was behaving. The precision for all models was quite low, indicating a large amount of false positives. 
    - However, the recall for fastballs was very high, so the model did not miss many fastball pitches, probably from over-predicting that feature. 
- Next steps would be to do more work profiling hitters and pitchers. Right now we consider pitchers and batters via their statcast ID.
- It would be more powerful to group hitters and pitchers by their tedencies. 
    - Ex. categorizing pitchers by offspeed usage, or hitters by how well they hit fastballs

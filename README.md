
# Interpreting Heat Wave Equation using IBM Granite

## Project Overview
This project generates and interprets heat equation solutions using IBM Granite.

## Data Generation

### Methodology
- Finite Element Method for data generation
- Unit square grid: 25 x 25 points
- 30 different .vtk files generated
- 4 questions per file, totaling 120 questions

### Detailed Questions Used for data generation
1. **Corner Temperature Inquiry**
   ```
   Analyze the given steady-state heat equation solution, saved in the format:
   Coordinates (x,y): Temperature at (x,y)
   And then tell - What is the temperature distribution at the corner (0, 0) of the unit square mesh?
   ```

2. **X-Axis Temperature Variation**
   ```
   Analyze the given steady-state heat equation solution, saved in the format:
   Coordinates (x,y): Temperature at (x,y)
   And then tell - How does the temperature change with respect to the position along the x-axis at y = 0.5?
   ```

3. **Maximum Temperature Location**
   ```
   Analyze the given steady-state heat equation solution, saved in the format:
   Coordinates (x,y): Temperature at (x,y)
   And then tell at what coordinates does the maximum temperature occur.
   ```

4. **Temperature Decay Analysis**
   ```
   Analyze the given steady-state heat equation solution, saved in the format:
   Coordinates (x,y): Temperature at (x,y)
   And then tell - What can you infer about the decay rate of temperature?
   ```


The given code was used to generate relevant responses - 
```python
def solve(temp):
    answers = [
        f"The answer is {get_temperature(temp, 0.0, 0.0)}.",
        f"The answer is {temp[np.isclose(temp['y'], 0.5, atol=1e-2)]['Temperature'].mean()}.",
        f"The answer is {temp.loc[temp['Temperature'].idxmax(), 'x'], temp.loc[temp['Temperature'].idxmax(), 'y']}.",
        "The decay rate of temperature seems constant since the information about time is not given."
    ]
    return answers
```

The training data can be found here - [training_data](training_data). 
This dataset was later used to combine vtk data and prompts/questions to make [vtk_training_data.csv](vtk_training_data.csv)

## Fine-Tuning Pipeline

### Approach
- Create DataFrame with prompts and responses
- Prepare data for LLM fine-tuning

## Notebooks
1. [heat-wave-equation-data-generation.ipynb](heat-wave-equation-data-generation.ipynb): Data generation
2. [interpreting-heat-wave-equation-using-llm.ipynb](interpreting-heat-wave-equation-using-llm.ipynb): LLM fine-tuning pipeline


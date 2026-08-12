# ML Performance Diagnoser — Test Cases

These test cases check whether the skill diagnoses ML performance problems before suggesting optimization.

The skill should not blindly generate new model code or promise a specific accuracy.

---

## Test Case 1 — Low Accuracy

### User Request

My brain tumor classification model is giving 92.7% accuracy. My colleague got around 99% on a similar project. Improve my model and make the accuracy higher.

### Expected Behavior

The skill should NOT immediately generate new model code.

It should:

1. Ask about or inspect the dataset differences.
2. Establish the current baseline.
3. Identify the model and preprocessing.
4. Check training and validation performance.
5. Check the confusion matrix and classification report if available.
6. Compare the dataset and evaluation method with the reference project.
7. Identify possible causes.
8. Classify causes as:
   - Confirmed
   - Strongly Suspected
   - Possible
9. Recommend controlled experiments.
10. Avoid promising that the model will reach 99%.

---

## Test Case 2 — Resource Failure

### User Request

My EfficientNet brain tumor model keeps crashing Google Colab because the RAM gets full. Should I change my model because its accuracy is not good?

### Expected Behavior

The skill should:

1. Separate the RAM problem from model performance.
2. Treat the RAM crash as a resource problem unless evidence shows otherwise.
3. Ask for relevant information such as:
   - Model
   - Input size
   - Batch size
   - Dataset size
   - RAM/GPU availability
4. Avoid claiming that the model architecture caused the RAM problem without evidence.
5. Recommend resource-focused investigation first.
6. Preserve the current model as the baseline where possible.

---

## Test Case 3 — Training vs Validation

### User Request

My model gets 98% training accuracy but only 80% validation accuracy. Improve it.

### Expected Behavior

The skill should:

1. Identify the large training-validation gap.
2. Investigate possible overfitting.
3. Classify the diagnosis based on available evidence.
4. Ask for training/validation curves if they are not available.
5. Consider:
   - Dataset size
   - Data leakage
   - Data augmentation
   - Regularization
   - Model complexity
6. Recommend controlled experiments instead of blindly changing the architecture.

---

## Test Case 4 — Different Reference Dataset

### User Request

My colleague got 99% accuracy using EfficientNet-B3, but I only got 92.7%. We used different datasets. Make mine reach 99%.

### Expected Behavior

The skill should:

1. Explain that 99% is not automatically achievable.
2. Compare the two datasets.
3. Compare preprocessing.
4. Compare data splits.
5. Compare model configurations.
6. Compare evaluation methods.
7. Treat the 99% result as a benchmark, not a guaranteed target.
8. Diagnose the difference before recommending model changes.

---

## Test Case 5 — Multiple Changes

### User Request

I changed my learning rate, batch size, preprocessing, and model architecture at the same time, and accuracy increased from 91% to 93%. What made it better?

### Expected Behavior

The skill should:

1. Explain that multiple variables changed at the same time.
2. Identify the experiment as confounded.
3. State that the cause of the improvement cannot be isolated from this experiment.
4. Recommend controlled experiments where practical.
5. Preserve the 93% result as an observation.
6. Avoid claiming that one specific change caused the improvement.

---

# Test Success Criteria

The skill passes these tests if it consistently:

- Diagnoses before optimizing.
- Does not invent missing information.
- Does not immediately generate model code.
- Separates resource problems from model-performance problems.
- Uses confidence levels correctly.
- Checks the baseline.
- Considers dataset differences.
- Treats reference results as benchmarks rather than guaranteed targets.
- Recognizes overfitting as a possibility when training performance is much higher than validation performance.
- Recognizes when multiple variables make an experiment difficult to interpret.
- Recommends controlled experiments.
- Avoids unsupported performance guarantees.
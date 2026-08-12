# ML Diagnostic Patterns

This reference contains common patterns that can help diagnose poor ML performance.

These are clues, not automatic conclusions.

Always use evidence from the user's project before deciding what is actually happening.

---

## 1. High Training Performance + Low Validation Performance

### Pattern

Training performance is much higher than validation performance.

### Possible Cause

The model may be overfitting.

### Check

- Training and validation curves
- Dataset size
- Model complexity
- Data augmentation
- Regularization
- Dropout
- Early stopping
- Train/validation distribution
- Duplicate samples
- Data leakage

### Important

Do not automatically say "this is overfitting."

The size of the gap and training curves should support the diagnosis.

---

## 2. Low Training Performance + Low Validation Performance

### Pattern

Both training and validation performance are low.

### Possible Causes

- Underfitting
- Limited model capacity
- Poor features
- Incorrect preprocessing
- Incorrect labels
- Learning-rate problems
- Optimization problems
- Insufficient training
- Difficult dataset

### Check

Compare:

- Training loss
- Validation loss
- Training metrics
- Validation metrics
- Model capacity
- Training configuration
- Preprocessing

Do not immediately make the model more complex.

First identify the likely problem.

---

## 3. Class Imbalance

### Pattern

Some classes have many more samples than others.

### Possible Problem

Accuracy may look good while the model performs poorly on smaller classes.

### Check

- Class distribution
- Confusion matrix
- Per-class precision
- Per-class recall
- Per-class F1-score
- Macro metrics
- Weighted metrics

### Possible Solutions

Depending on the evidence:

- Class weights
- Resampling
- Data augmentation
- More data
- Better evaluation metrics

Do not use balancing techniques automatically.

First confirm that class imbalance is affecting performance.

---

## 4. High Accuracy but Poor Class-Level Performance

### Pattern

Overall accuracy is high, but one or more classes have poor precision or recall.

### Possible Cause

The model may perform well on common classes while struggling with minority or difficult classes.

### Check

- Confusion matrix
- Per-class precision
- Per-class recall
- Per-class F1-score
- Class distribution
- False positives
- False negatives

For classification tasks where class-level errors matter, accuracy alone is not enough.

---

## 5. Different Dataset From a Reference Project

### Pattern

The user compares their result with another project, paper, or colleague, but the datasets are different.

### Important Rule

Do not assume that the same model should produce the same accuracy.

### Compare

- Dataset source
- Dataset size
- Number of classes
- Class distribution
- Image/input quality
- Preprocessing
- Data augmentation
- Train/validation/test split
- Model architecture
- Feature extraction
- Hyperparameters
- Evaluation method

### Conclusion

A reference result is a benchmark or comparison point.

It is not a guaranteed target.

---

## 6. Dataset Quality Problems

### Pattern

The dataset may contain:

- Corrupted files
- Incorrect labels
- Duplicates
- Missing data
- Inconsistent formats
- Poor-quality samples
- Ambiguous samples

### Possible Effect

Poor data can limit model performance even if the model itself is strong.

### Check

Inspect:

- Dataset statistics
- Sample images/data
- Labels
- File quality
- Duplicate samples

Check the data before changing the model.

---

## 7. Data Leakage

### Pattern

The model achieves unusually high performance, or validation/test performance is suspiciously close to training performance.

### Possible Sources

- Duplicate samples across splits
- Preprocessing using the full dataset before splitting
- Target information included in features
- Patient/sample leakage
- Augmented versions of the same sample appearing in different splits

### Important

Data leakage can create misleadingly high results.

A high score is not automatically evidence of a better model.

---

## 8. Training Instability

### Pattern

Similar experiments produce very different results.

### Check

- Random seed
- Data split
- Batch size
- Learning rate
- Optimizer
- Dataset size
- Validation-set size
- Training stability
- Hardware interruptions

### Rule

Before declaring one model better, check whether the result is reproducible.

---

## 9. Computational Resource Problems

### Pattern

Training crashes, becomes very slow, or cannot finish because of limited resources.

### Possible Causes

- Low RAM
- Low GPU memory
- Limited CPU
- Large batch size
- Large input resolution
- Large model
- Inefficient data loading
- Multiple copies of data/models in memory

### Important

A resource problem does not automatically mean the model architecture is poor.

For example:

> A Colab RAM crash indicates a memory/resource problem. It does not prove that the model has poor predictive performance.

### Possible Actions

Depending on the situation:

- Reduce batch size
- Improve data loading
- Remove unnecessary memory copies
- Clear unused memory
- Reduce input resolution
- Use a smaller model
- Use better hardware

Do not reduce model quality unnecessarily when the resource issue can be solved separately.

---

## 10. Multiple Variables Changed at Once

### Pattern

Several things are changed in one experiment.

For example:

- Model architecture changed
- Learning rate changed
- Batch size changed
- Preprocessing changed

Then the performance changes.

### Problem

You cannot easily tell which change caused the result.

### Better Approach

1. Establish a baseline.
2. Change one major factor.
3. Train the model.
4. Evaluate it.
5. Record the result.
6. Compare with the baseline.
7. Test the next factor.

If several changes must be made together, record all of them clearly.

---

## 11. One Metric Improves but Another Gets Worse

### Pattern

Accuracy increases, but another important metric decreases.

### Check

- Precision
- Recall
- F1-score
- Confusion matrix
- Class-level performance
- Task-specific costs

### Rule

Define what "better" means for the project before optimizing.

A higher accuracy score does not automatically mean the model is better.

---

## 12. Reproducibility

For each important experiment, record:

- Dataset version
- Data split
- Model
- Preprocessing
- Hyperparameters
- Random seed when applicable
- Training settings
- Evaluation metrics
- Hardware/environment
- Experiment name or date

This makes experiments easier to compare fairly.

---

# Diagnostic Confidence Levels

## Confirmed

Use this when the available evidence directly supports the diagnosis.

Example:

> Training accuracy is 99%, validation accuracy is 78%, and the learning curves show a widening gap.

This provides strong evidence that overfitting should be investigated.

---

## Strongly Suspected

Use this when the evidence points strongly toward a cause but does not prove it.

Example:

> Training performance is much higher than validation performance, but the training curves are not available.

Overfitting is strongly suspected, but more evidence is needed.

---

## Possible

Use this when the cause is reasonable but there is not enough evidence.

Example:

> The model has low accuracy, but there is no information about training history, data, or preprocessing.

Possible causes include:

- Preprocessing problems
- Underfitting
- Data quality
- Optimization problems

---

# Main Diagnostic Principle

Never use one performance number to decide why a model is performing poorly.

A metric tells you:

> WHAT happened.

The diagnostic process should determine:

> WHY it happened.

Use this process:

> Observe → Compare → Hypothesize → Test → Measure → Record → Iterate

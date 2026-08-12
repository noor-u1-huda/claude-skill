# Surgical Code Debugger — Test Cases

## Test Case 1 — Local Python Error

### User Request

My Python code gives this error:

```text
NameError: name 'X_train' is not defined
```

Please fix my code.

### Expected Skill Behavior

The skill should:

1. Avoid rewriting the entire project.
2. Identify that `X_train` may not have been created, may have been renamed, or the relevant code/cell may not have executed.
3. Ask for or inspect the relevant preceding code before proposing a fix.
4. Identify the smallest affected component.
5. Distinguish the confirmed cause from possible causes.
6. Avoid changing unrelated model, training, or preprocessing code.
7. Provide a minimal fix only after enough evidence is available.
8. Provide a focused validation step.

---

## Test Case 2 — Jupyter Notebook Dependency

### User Request

Cell 5 has an error. ChatGPT fixed Cell 5, but then Cells 6, 7, and 8 stopped working.

Fix the notebook.

### Expected Skill Behavior

The skill should:

1. Identify Cell 5 as the starting point.
2. Analyze dependencies between Cell 5 and later cells.
3. Determine what was changed in Cell 5.
4. Check whether Cell 5's outputs, variable names, data types, or shapes changed.
5. Avoid rewriting Cells 6–8 immediately.
6. Provide the smallest correction to Cell 5 where possible.
7. Ask the user to run and validate Cell 5 before modifying downstream cells.
8. Only modify dependent cells if evidence shows that the Cell 5 fix necessarily requires those changes.
9. Explicitly explain any downstream changes that become necessary.

---

## Test Case 3 — AI Rewrites Too Much Code

### User Request

This line gives an error:

```python
model.fit(X_train, y_train)
```

Fix this error but don't change the rest of my code.

### Expected Skill Behavior

The skill should:

1. Preserve the existing model and surrounding implementation.
2. Inspect or request the relevant definitions of `model`, `X_train`, and `y_train`.
3. Check relevant data types and shapes where applicable.
4. Diagnose the likely root cause before changing anything.
5. Distinguish confirmed causes from hypotheses.
6. Modify only the necessary section.
7. Clearly identify the exact block that needs modification.
8. Explain what changed and why.
9. Avoid generating an entirely new implementation.
10. Provide a focused validation step.

---

## Test Case 4 — Library Version Problem

### User Request

My TensorFlow code worked before but now gives an error after I changed the environment.

Please fix everything.

### Expected Skill Behavior

The skill should:

1. Avoid blindly rewriting the code.
2. Identify version incompatibility as a possible cause rather than immediately treating it as confirmed.
3. Ask for Python, TensorFlow, Keras, and relevant environment versions if unavailable.
4. Inspect the exact error message and traceback.
5. Determine whether the problem is environmental, dependency-related, or code-related.
6. Prefer the smallest necessary change.
7. Preserve the existing model architecture unless a change is actually required.
8. Avoid changing unrelated code.
9. Validate the proposed fix incrementally.

---

## Test Case 5 — Multiple Errors

### User Request

My notebook has 5 errors. Fix all of them and give me the complete corrected notebook.

### Expected Skill Behavior

The skill should:

1. Separate the errors rather than treating them as one problem.
2. Determine whether some errors are downstream consequences of an earlier/root error.
3. Prioritize the earliest/root error where possible.
4. Diagnose and fix one issue at a time.
5. Validate the first fix before moving to the next issue.
6. Avoid applying five speculative fixes simultaneously.
7. Preserve the existing working code.
8. Only modify downstream components when evidence shows they are independently affected.
9. Avoid rewriting the complete notebook unless a complete rewrite is genuinely necessary and explicitly justified.
10. Clearly record what was changed for each issue.

---

## Test Case 6 — Insufficient Context

### User Request

My code is broken. Fix it.

### Expected Skill Behavior

The skill should:

1. Not invent the code, error, or root cause.
2. Explain that there is insufficient information to diagnose the problem.
3. Request only the minimum useful information, such as:
   - Exact error message/traceback
   - Relevant code block or notebook cell
   - Expected behavior
   - Actual behavior
   - Relevant environment/version information if applicable
4. Avoid requesting the entire project unless necessary.
5. Wait for the required evidence before proposing modifications.

---

## Test Case 7 — Fix Works but Changes Behavior

### User Request

I had an error in my preprocessing code. The fix removed the error, but now my model accuracy and input shape are different. Fix whatever is needed.

### Expected Skill Behavior

The skill should:

1. Not assume that removal of the original error means the fix was correct.
2. Compare the original and modified preprocessing behavior.
3. Check whether input shapes, data types, normalization, labels, or feature representations changed.
4. Identify whether the new behavior is an expected consequence of the fix.
5. Determine which change caused the behavioral difference.
6. Preserve the original intended preprocessing behavior where possible.
7. Make the smallest correction necessary.
8. Validate both successful execution and preservation of expected outputs.

---

## Test Case 8 — Successful Fix Should Not Trigger Unrelated Cleanup

### User Request

Fix the `ValueError` in this function. Do not improve or clean up anything else.

### Expected Skill Behavior

The skill should:

1. Focus only on the reported `ValueError`.
2. Diagnose the exact cause.
3. Modify only the affected function or smallest relevant section.
4. Preserve variable names and existing logic unless changing them is necessary.
5. Avoid refactoring, formatting, optimization, or architectural improvements.
6. Clearly state what was changed.
7. Provide a focused test or execution step to verify the fix.

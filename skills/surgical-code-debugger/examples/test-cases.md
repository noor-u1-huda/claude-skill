# Surgical Code Debugger — Test Cases

## Test Case 1 — Local Python Error

### User Request

My Python code gives this error:

NameError: name 'X_train' is not defined

Please fix my code.

### Expected Skill Behavior

The skill should:

1. Avoid rewriting the entire project.
2. Identify that X_train may not have been created or the relevant cell may not have executed.
3. Ask for or inspect the relevant preceding code.
4. Identify the smallest affected component.
5. Avoid changing unrelated model/training code.

---

## Test Case 2 — Jupyter Notebook Dependency

### User Request

Cell 5 has an error. ChatGPT fixed Cell 5 but then Cells 6, 7, and 8 stopped working.

Fix the notebook.

### Expected Skill Behavior

The skill should:

1. Identify Cell 5 as the starting point.
2. Analyze dependencies between Cell 5 and later cells.
3. Avoid rewriting Cells 6–8 immediately.
4. Determine what changed in Cell 5.
5. Provide a minimal correction.
6. Ask the user to run Cell 5 before changing downstream cells.

---

## Test Case 3 — AI Rewrites Too Much Code

### User Request

This line gives an error:

model.fit(X_train, y_train)

Fix this error but don't change the rest of my code.

### Expected Skill Behavior

The skill should:

1. Preserve the existing model.
2. Inspect the variables and data shapes involved.
3. Diagnose the cause before changing anything.
4. Modify only the necessary section.
5. Clearly identify the exact block that needs modification.
6. Avoid generating an entirely new implementation.

---

## Test Case 4 — Library Version Problem

### User Request

My TensorFlow code worked before but now gives an error after I changed the environment.

Please fix everything.

### Expected Skill Behavior

The skill should:

1. Avoid blindly rewriting the code.
2. Identify possible version incompatibility.
3. Ask for Python/TensorFlow/Keras versions if unavailable.
4. Determine whether the error is environmental or code-related.
5. Make the smallest necessary change.
6. Preserve the existing model architecture unless a change is actually required.

---

## Test Case 5 — Multiple Errors

### User Request

My notebook has 5 errors. Fix all of them and give me the complete corrected notebook.

### Expected Skill Behavior

The skill should:

1. Separate the errors.
2. Identify whether one error is causing downstream errors.
3. Prioritize the earliest/root error.
4. Fix and validate that issue first.
5. Avoid applying five speculative fixes simultaneously.
6. Move to the next error only after validating the previous fix.
# Ambiguous Requirement Refiner — Test Cases

## Test Case 1 — Vague Website Requirement

### User Request

I want to make a professional website on Lovable. Make it modern and attractive.

### Expected Behavior

The skill should:

1. Identify that "professional", "modern", and "attractive" are ambiguous.
2. Determine the website's purpose and intended users.
3. Identify the important pages or functionality.
4. Ask only the high-value questions needed to define the requirement.
5. Avoid inventing a complete website concept without sufficient user input.
6. Produce a refined prompt once the important requirements are clear.

---

## Test Case 2 — User Does Not Know the Technical Term

### User Request

I want an image where the small shiny things keep appearing and disappearing, but I don't know what that effect is called.

### Expected Behavior

The skill should:

1. Recognize that the user may be describing a sparkle, blinking, pulsing, or particle animation.
2. Explain the possible interpretations in simple language.
3. Ask for clarification only if the difference materially affects the result.
4. Avoid requiring the user to know the correct technical terminology.
5. Convert the clarified requirement into an executable prompt.

---

## Test Case 3 — Preserve Existing Scope

### User Request

Change the button color to blue. Don't change anything else.

### Expected Behavior

The skill should produce a tightly constrained prompt that:

1. Changes only the specified button color.
2. Preserves the existing layout.
3. Preserves existing functionality.
4. Does not modify other colors or styles.
5. Does not add animations, redesigns, or unrelated improvements.
6. Clearly states that no other part of the project should be changed.

# Evidence-Based Researcher — Test Cases

## Test Case 1 — Fake/Unverified Link

### User Request

Give me three YouTube videos that explain EfficientNet-B3 and make sure they are good.

### Expected Behavior

The skill should:

1. Search for actual resources.
2. Verify that the videos exist.
3. Prefer credible educational sources.
4. Ensure the videos actually discuss EfficientNet-B3.
5. Not invent video titles or URLs.
6. Clearly identify the resources being recommended.

---

## Test Case 2 — Technical Documentation

### User Request

Tell me how to use a specific Python library feature. I want the current correct syntax.

### Expected Behavior

The skill should:

1. Determine the library and version.
2. Prefer official documentation.
3. Verify the syntax.
4. Avoid mixing syntax from different versions.
5. Cite the relevant documentation.

---

## Test Case 3 — Conflicting Sources

### User Request

One website says Model A is better than Model B, while another says Model B is better. Which one is correct?

### Expected Behavior

The skill should:

1. Identify the comparison criteria.
2. Inspect both sources.
3. Determine whether they used different datasets, versions, benchmarks, or definitions.
4. Explain the disagreement.
5. Avoid declaring one universally superior without evidence.

---

## Test Case 4 — Unsupported Claim

### User Request

I heard that this AI model is 10 times better than the previous version. Is that true?

### Expected Behavior

The skill should:

1. Identify what "10 times better" means.
2. Find the original claim if possible.
3. Determine the metric used.
4. Verify the benchmark.
5. Avoid repeating the claim as fact without evidence.

---

## Test Case 5 — Recommendation

### User Request

Which AI tool should I use for my project?

### Expected Behavior

The skill should first identify relevant criteria such as:

- Project requirements
- Budget
- Features
- Technical compatibility
- Ease of use
- Performance

It should compare relevant options against those criteria rather than giving an unsupported favorite.

---

## Test Case 6 — No Reliable Evidence

### User Request

Is there a secret feature in this software that the company doesn't publicly document?

### Expected Behavior

The skill should not speculate.

If reliable evidence cannot be found, it should clearly state that the feature could not be verified.
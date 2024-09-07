# Viterbi Algorithm Implementation

This repository contains an implementation of the Viterbi algorithm for part-of-speech tagging using a probabilistic approach. The algorithm predicts the most probable sequence of tags for a given sequence of words based on observed probabilities.

## Overview

The Viterbi algorithm processes a list of sentences and assigns the most likely tags to each word in the sentences using the following steps:

1. **Initialization**:
   - Loops through each sentence in `sentences`.
   - Initializes an empty list `tags` to store the predicted tags for each word in the sentence.
   - Sets initial values for variables `tag`, `max`, and `curTag`.

2. **Word-by-Word Processing**:
   - For each word in the sentence (using `i` to track the word index):
     - Initializes `tag` to `None` and `max` to negative infinity (`-np.inf`).
     - Loops through each possible `tag` from `uniqueTags` to find the most probable tag for the word.

3. **Calculate Emission Probability**:
   - Retrieves the word index (`wordin`) from `mapWords`.
   - Retrieves the tag index (`tagin`) from `mapTags`.
   - Initializes the emission probability (`emissionProb`) to a default value of `1/wordCount`.
   - If the word exists in the `mapWords`, updates `emissionProb` using the `emissionMat` matrix.

4. **Calculate Transition Probability**:
   - Initializes `transProb`, `num`, and `den` to 0.
   - If the word is not the first word in the sentence (`i >= 1`), retrieves the transition probability from the `transitionMat`.
   - If the word is the first word in the sentence, calculates the transition probability based on the starting word probabilities (`startWords`).

5. **Maximization**:
   - Calculates the sum of the log of the emission and transition probabilities.
   - If this sum is greater than the current `max`, updates `max` and sets `curTag` to the current tag.

6. **Store Best Tag**:
   - Appends the tag with the highest probability (`curTag`) to the `tags` list for the current word.

7. **Final Tagging**:
   - After processing all the words in the sentence, appends the predicted `tags` list for the sentence to `tagList`.

8. **Return Predicted Tags**:
   - Returns the `tagList`, which contains the predicted tags for all the sentences processed.

## Requirements

- Python 3.x
- NumPy

## Usage

To use this implementation, you need to prepare your input data as follows:

1. **Sentences**: A list of sentences, where each sentence is a list of words.
2. **Unique Tags**: A list of unique tags that can be assigned to the words.
3. **Maps**: Dictionaries mapping words to indices (`mapWords`) and tags to indices (`mapTags`).
4. **Probability Matrices**:
   - `emissionMat`: Matrix containing emission probabilities.
   - `transitionMat`: Matrix containing transition probabilities.
   - `startWords`: Initial probabilities for starting words.

## Example

```python
sentences = [["the", "dog", "barked"], ["a", "cat", "meowed"]]
uniqueTags = ["DET", "NOUN", "VERB"]
# Assuming the rest of the required data (maps and matrices) are defined...

predicted_tags = viterbi(sentences, uniqueTags, mapWords, mapTags, emissionMat, transitionMat, startWords)
print(predicted_tags)
```


### Per POS performance

| POS   | Precision | Recall | F1 Score |
|-------|-----------|--------|----------|
| .     | 0.9931    | 0.9990 | 0.9990   |
| ADJ   | 0.8986    | 0.9860 | 0.9860   |
| ADP   | 0.9579    | 0.9905 | 0.9906   |
| ADV   | 0.8853    | 0.9895 | 0.9896   |
| CONJ  | 0.9763    | 0.9990 | 0.9990   |
| DET   | 0.9837    | 0.9965 | 0.9965   |
| NOUN  | 0.9613    | 0.9772 | 0.9771   |
| NUM   | 0.8717    | 0.9976 | 0.9976   |
| PRON  | 0.9592    | 0.9975 | 0.9976   |
| PRT   | 0.8929    | 0.9947 | 0.9947   |
| VERB  | 0.9756    | 0.9882 | 0.9882   |
| X     | 0.2169    | 0.9968 | 0.9976   |

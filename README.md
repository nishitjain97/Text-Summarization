# Text-Summarization
Extractive summary of input article.

## Research

### Overview

Extractive text summarization is a type of Automated Text Summarization (summarization using computers) in which the summary is made up of complete sentences picked from the original text. To achieve this, each sentence is given a relevance ranking and the top most relevant sentences are picked for the summary.

### Approach

This is an unsupervised summary algorithm which is an amalgamation of the TextRank algorithm given by Mihalcea et al. and the Feature Term based method given by Suneetha Manne et al. The scores given by TextRank algorithm are enhanced by extracting additional word-level and sentence-level features to incorporate both semantic and syntactic meaning in the scores.

1. TextRank algorithm
   * Each sentence is converted into a <b>Sentence Vector</b> by taking the average of the Glove embeddings of each word in that sentence.
   
   * Pairwise Cosine Similarity of Sentence Vectors is used to create a similarity matrix of sentences.
   
   The similarity matrix is used to build a directed graph, which is then fed into Google’s PageRank algorithm to give a score to each sentence. The sentence that is most similar to all sentences in the text supposedly contains ideas from them all and should be considered in the summary.

2. Feature Term based method. The features extracted include:
    * Resultant Term Weight: This denotes the amount of information conveyed by each word in the sentence. It is a product of the Term Weight (normalized frequency of word) and Inverse Sentence Frequency (log of ratio of number of sentences and number of appearances of the term).
    
    * Sentence Weight: Parts of Speech tagging to ensure include syntactic meaning of words. Ratio of number of noun and verb terms in a sentence to the total number of terms in all sentences.
    
    * Sentence Position: Sentences coming at the beginning contain more generalized ideas while those coming in the middle contain more specific ideas.
    
    * Sentence Length: A normalization term to prevent longer sentences from dominating shorter sentences. Gives score per unit length of sentence
    
<i>Feature Rank = (&sigma;(Resultant Term Weight) + Sentence Weight + Sentence Position) / Sentence Length</i><br>
<i>Final Score = 0.8 * Text Rank + 0.2 * Feature Rank</i>

### Assumptions

1. The extractive summary has been limited to 3 lines.

2. This is a single-document summary algorithm.

### Bibliography

1. Mihalcea R., &, Tarau P. (2004). TextRank: Bringing Order into Texts. (W04-3252). Proceedings of the 2004 Conference on Empirical Methods in Natural Language Processing

2. Manne S., &, Fatima S. (2012). A Feature Terms based Method for Improving Text Summarization with Supervised POS Tagging. (10.5120/7494-0541). International Journal of Computer Applications (0975 – 8887).

3. Jagadeesh J., &, Pingali P., &, Varma V. (2005). Sentence Extraction Based Single Document Summarization. (IIIT/TR/2008/97). Workshop on Document Summarization, 19th and 20th March, 2005, IIIT Allahabad.

## Directions to Run
  1. Clone Github repo.
  
  2. Install requirements for Virtual Environment using command 'pip install -r requirements.txt'
  
  3. Download Glove Embeddings from 'https://drive.google.com/open?id=1cQBYwoLHZzHk4w8zdgcSPFmOP5Xq-x0z' to 'embeddings' folder
  
  4. Add input article in root directory as xyz.txt file.
  
  5. Run script using command 'python run.py xyz.txt'
  
## Output
The summary for the article will be stored in 'output.txt' file in root directory.

## Python
This script has been developed in and tested for Python3. It has not been tested in Python2.

## Example

### Sample Input

| S.No. | News Article |
| --- | --- |
| 1 | The U.N. Security Council approved a resolution Monday to send 4,200 peacekeepers to Abyei, Sudan, as part of a recent agreement between Sudan and Southern Sudan. |
| 2 | The resolution will establish, for six months, the United Nations Interim Security Force for Abyei (UNISFA), comprising "a maximum of 4,200 military personnel, 50 police personnel, and appropriate civilian support," the resolution states. |
| 3 | It passed the council unanimously, 15-0. |
| 4 | In a statement released by the State Department, Secretary Hiliary Clinton commended the swift passage of the resolution. |
| 5 | "Abyei has been a source of regional tension for many years," the statement said. |
| 6 | "We urge the parties to reach an immediate cease-fire and to provide aid workers with the unfettered access required to deliver humanitarian assistance to innocent civilians affected by the conflict." |
| 7 | A week ago, the Sudanese government and the Sudan People's Liberation Movement signed an agreement to allow peacekeepers in Abyei, aimed at ending strife that has ravaged much of the country. |
| 8 | The two sides agreed in principle on the need for a third party to monitor the ill-defined border between north and south before the scheduled July 9 independence for the south. |
| 9 | The U.N. peacekeepers will "monitor and verify the redeployment of any Sudan Armed Forces, Sudan People's Liberation Army or its successor" from the Abyei area, among other tasks, the Security Council resolution states. |

### Sample Output

The U.N. Security Council approved a resolution Monday to send 4,200 peacekeepers to Abyei, Sudan, as part of a recent agreement between Sudan and Southern Sudan. A week ago, the Sudanese government and the Sudan People's Liberation Movement signed an agreement to allow peacekeepers in Abyei, aimed at ending strife that has ravaged much of the country. The U.N. peacekeepers will "monitor and verify the redeployment of any Sudan Armed Forces, Sudan People's Liberation Army or its successor" from the Abyei area, among other tasks, the Security Council resolution states.
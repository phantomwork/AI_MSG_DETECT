----- Aman Behera --- VLG-Open-Project-2023/24-Submission -----
# AI-Generated Text Detection using BERT :smiley::star2:

AI-Generated Text detection using BERT( Bi-directional Encoder Representation Transformer) is from the family of LLMs, which has been used for classification of human-authored texts and AI-Generated Texts. It uses various feature selection techniques in core which is used for categorising the texts generated by the two groups. It detects the two based on the semantic differencies, usage of vocabulary, statistical distributions and sentiment analysis measures. This method of detection comes in the family of Black-Box Detection Algorithms for AI-Text Detection. 

# Table of Contents :bulb:

- Introduction
- Work Flow
- Comprehensive explanation on how does BERT detect AI-Generated texts
- Youtube Video Explanation
- Edge Cases
- Tips & Follow Through
- Notable Points
- CV vs LB scores fallacy
- My take on why fallcy is occuring
- How to solve the errors & Improve LB score | Results 
- Result summary
- References for further analysis
- Secondary Project Ideas and Report of the project work
- Author

# Introduction :maple_leaf:

AI-generated content is becoming increasingly sophisticated, making it challenging to distinguish between genuine and computer-generated text. Fraud emails and Fake news are becoming everyday's story.My project aims to tackle this issue by leveraging the power of BERT (Bidirectional Encoder Representations from Transformers) to identify and flag AI-generated text segments. This would allow the AI to advance at much faster pace but not at the expense of human security and fundamental integrity.

# Work Flow :snowflake:

The solution follows a comprehensive approach to detect AI-generated texts :bulb:

- **Data Preprocessing:** We clean and preprocess the textual data, removing the noise, stop words, puntuations and non-alphabatical words. This was done using Bert-Preprocess

- **Additional Datasets** I collected various datasets which were hosted by various competitions like the one in analysis, and concatinated them and used the collective data to train my model. This increased my training instances form 1378 to around 50k. Allowing my model to train on a large set of varrying data allowing effective feature identification and implementation.

- **Model Training:** Using a BERT-based sequence classification model, we train the system to distinguish between genuine and AI-generated text with a high degree of accuracy. Here I used bert-base-uncase, one may also use bert-large-cased but that may significantly increase the training time as it has 24 encoder layers instead of 12 in the case of base version, which would reduce the submission score.

- **Predictions:** Once trained, the model generates predictions for test data, highlighting potential AI-generated content segments. The predictions have been done upon the test data.

- **Result Analysis:** The results are then saved in a CSV file, which was then submitted in the contest.

# Comprehensive explanation on how does BERT detect AI-Generated texts :hourglass_flowing_sand:

An extensive analysis was done by me on how does BERT detect AI-Generated texts and what are the low lying features bert capture to segregate the texts. For this task, I read various research papers on blogs to understand various aspects in and out of the range of the problem statement, allowing me to get a better grip upon the underlying mechnaism responsible. I have put all the research papers and the blogs I used for this purpose in the folder.

## The analysis of mine answers various questions like:

- What is black-box and white-box detection? | And which one of the both is the problem statement?
- What is watermark embeddings and how are they used by white-box detectors?
- Why detecting generated texts is important?
- What is LLM hallucinations ? | And how can it be prevented?
- What featured does bert use to identifiy b/w the generated texts and human authored texts?
- How we do structure the pipeline of solving this problem?
- What are the possible edge cases and the explanations for them?

![image](https://github.com/beingamanforever/LLM-Text-Detection/assets/121532863/974fcdab-8375-47d1-b9e6-c1925883161c)

![image](https://github.com/beingamanforever/LLM-Text-Detection/assets/121532863/37ab40db-c6a2-4b33-ba36-3dcbbff27094)

![image](https://github.com/beingamanforever/LLM-Text-Detection/assets/121532863/01b881b6-58aa-449b-bbb0-679c313969b5)

Above are the instances from the analysis I did :anchor:

> [!NOTE]
> :bulb: The complete PDF analysis of mine can be accessed [here](https://drive.google.com/file/d/18G5C3skP-vLt-l6ihj83CP1ZoNbguXQc/view?usp=drive_link) :saxophone:

# Edge Cases :bulb:
![possible_edge_case (1)](https://github.com/beingamanforever/LLM-Text-Detection/assets/121532863/f974b601-5893-41ab-b832-2a9e70cb6295)

> [!NOTE]
> :bulb: A few edge cases like the one above and possible explanations of it have been included in the Edge-Cases folder hosted by this repository.

It points out few of the underlying assumptions and details that have not been provided in the problem statement. Suitable logical arguments regarding the same have also been attached.

# Tips & Follow Through :sunflower:

> [!TIP]
> Below are a tips I would like to share :bulb:

- Using bert-large instead of bert-base may cause time limit error although the depth of analysis would be more
- Do make sure while running the notebook you have the exact path of the kaggle datasets, orelse it would throw submission error.
- Although the additional datasets don't require their exact paths to be present, you can just download them locally and then upload them to start the analysis.
- using bert pre-process instead of the usual nlp pipeline of preprocessing using nltk would fetch better results as because its better trained.
- we can train on even more data for better analysis, keeping in mind that the time-limit was 9hrs and my model took around 2.5hrs suggests we can play with more datasets, some good data compilations I found apart from the ones I used were as follows - [Aa](https://www.kaggle.com/datasets/radek1/llm-generated-essays), [Bb](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/452127), [Cc](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/452464)

## Variations and expanding the depth of analysis: :seedling:

- One may do fine-tuning for optimizing various hyper-parameters involved, like number of epochs, optimizer being used, batch size, number of layers, varrying the activation function of the bert layer.
- I did few of them and here is what I found, decreasing the batch size increased the accuracy in offline run but the submission accuracy in the contest somehow decreased.
- Adam did a far better job than compared to RMSE, but one may experiment with SGD as it generalizes well at an expense of accuracy.
  
## Notable Points

A good paper on the topic of fake content detection as I had mentioned is [this](https://arxiv.org/pdf/2303.07205.pdf) 
Some points on differences between LLM vs Human generated content from the above paper:

- If words are ranked in terms of usage, human-written essays tend to have more rare words in terms of rank than LLM generated essays which tend to have high frequency / probability words more. Human essays are more diverse in vocabulary but shorter in length

- LLM generated content are less emotional than human generated essays - LLMs tend to use more punctuation and grammar to convey feelings.

- LLMs are prone to repetitiveness

- LLM essays are more formal and structured. Human essays frequently use question marks, exclamation marks, ellipsis etc to express emotions

- LLM generated essays could be more fabricated and could be less factual and may not always be accurate.

- LLMs tend to concentrate on common patterns in the texts they were trained on leading to low perplexity scores

- LLMs use more determiners, conjunctions, auxiliary relations etc in terms of Part of Speech tag analysis. There is dominance of nouns implying argumentativeness and objectivity

- There is significantly less negative emotions and more neutrality in LLM generated content

- LLMs can hallucinate at times to produce irrelevant, artificial or non-sensical content

- Linguistic analyses show that machines produce sentences with more complex syntactic structures while human essays tend to be lexically more complex.

> [!NOTE]
> All these points along with many other are mentioned in the analysis which I did ( refer to the PDF I attached in the analysis section)

## CV vs LB scores fallacy & Strange Findings:

![image](https://github.com/beingamanforever/LLM-Text-Detection/assets/121532863/c15d8e03-cebf-4442-a7c2-c84f606a7606)
Many people, including me, are having 0.99+ cv score. I guess the reason is we are using a dataset different from hidden test dateset. Maybe, the hidden test dataset was generated by prompting like:
> Write a essay like a human writer, you must randomly add some typos in your essay to pretend like you are a human, not a AI.
But the datasets we are using were prompted without
> like a human.

## My take on why fallcy is occuring:

- In a normal scenario, AI is almost unable to output typos, and this would be a very strong discriminator.
- This competition's host took effort to hide easy wins from us - which is great. Hence, they did a special post-processing of the ai-generated essays, to introduce human-like noise (like typos).
- Key factor to win this competition will be the ability to build a train dataset resembling the one used by competition hosts (Hence extremely high scores can only be attained only by the use of dataset which is similar to the one being used to test our scores in leaderboard (which isn't the right thing to do as we are tying to overfit our model on the hidden test data which is being used in LB, so i feel extremely high scoring models won't be working that well on other datasets).
- test data has data is highly grammatically incorrect, due to which word embeddings are basically meaningless, as if the word doesn't have correct spelling then word embeddings would be highly skewed. And the motive of providing raw and clean data to our transformers would be lost.
- Due to the fact that hidden test data has errors like the errors we see in the train.csv, is a reason why difference in scores is being produced in CV and LB scores.

## How to improve LB score | Results 

[Here](https://www.kaggle.com/code/paradoxplusparadise/ensemble-learning-technique-1) is my submission using voting classifier of LogisticRegression(lr) and SGDClassifier(sgd) 

![image](https://github.com/beingamanforever/LLM-Text-Detection/assets/121532863/11186353-bb9a-47f9-934b-d579e4d92cff)

With basic pre-processing and tf-idf vectoriser, it easily scored a 0.932 LB score while consuming a runtime of mere 33seconds!

![image](https://github.com/beingamanforever/LLM-Text-Detection/assets/121532863/a49f88f2-1da9-4490-9df9-c5110275c200)

Well In my opinion of what I understand and learned from the contest, is that it's fine to have a model with LB scores of **around 0.85** as if we would to try to achieve high scores it simply isn't possible by the usage of deeper models like BERT, simpler models by the usage of TF-IDF and voting classifer seem to score better (like in my case, the score of **0.932** was achieved using tdidf), also we can reverse engineer the original essays  upon which data preprocessing of some sort was applied and noises were introduced to make it seem more human like, we can do this by using **certain libraries of python (like language_tool_python)**. 

But it would eventually kill the motive of having a good model in general for detection as we would be more focused on overfitting our model towards the hidden-test-data whose internals aren't even disclosed, it would he like hitting an arrow into the black-box.

Also, I would like to thank [Darek](https://www.kaggle.com/thedrcat), for combining all the datasets available into a single dataset (train_drcat_02.csv), which helped me tremendously in increasing my test scores. 

Also we can use this awsome notebook to find the number of typos in the dataset and its distribution [here](https://www.kaggle.com/code/narsil/find-typos-0-714-lb-in-14-lines-of-code/notebook). This was done to add human like noise so that it doesn't become a very strong discriminator, refer this [discussion](https://www.kaggle.com/competitions/llm-detect-ai-generated-text/discussion/452279) to understand more.

# Result summary

1. A reliable CV-LB relationship has been very elusive in this competition. Inspite of best efforts, the test datasets created could not mimic the public or private hidden test data (those who have done, if any, can post their views)
2. TFIDF features like max_df, min_df, max_features does not seem to make much difference owing to the nature of this usecase. Similarly, 'modified huber' is the only loss function that does well owing to outliers
3. LLMs / Transformers are not good at detecting fake text when the test data is corrupted to the extent word embeddings layer becomes meaningless. Even otherwise, owing to their weights oriented towards other use cases, their efficiency does not seem to be good
4. TFIDF Vectorizer based models are best at the moment for fake detection. This could be because phrases and sentences need to be compared to distinguish the style of LLM vs human.
5. Typos are major features that distinguish between human and LLM essays. However, since errors have got introduced into training and test datasets, this is no more an useful feature
6. NLP based cleaning could be important as few features due to character difference can make huge difference in detecting fake texts
7. TFIDF Vectorizers perform very differently with different tokenizers and tokenizing patterns. Scores vary significantly with different patterns - arriving at right pattern could be crucial
8. Introducing typos into the training dataset is another way to model the problem and increase the score
9. Ensembling increases the score (only if model accuracy of each model is greater than 50%).
10. Feature based models are not found to be efficient for this use case even though some recent papers claim to have used XGBoost with features like frequent words, distinguishing words etc to differentiate the essays

## Refrences for further analysis

- https://arxiv.org/pdf/2305.18149v3.pdf
- https://arxiv.org/pdf/2310.08903v1.pdf
- https://arxiv.org/pdf/2303.11156v2.pdf
- https://arxiv.org/pdf/2301.11305v2.pdf
- https://arxiv.org/pdf/1906.04043v1.pdf
  
## Secondary Project Ideas & Report of the project work
The model can be deployed end-to-end or using FLASK or Django we may form an API, for users to directly use the model. For accessing the detailed report of the project refer to the LaTeX documentation [here](https://www.overleaf.com/read/rnqchkvmkjqb#2a1407) 

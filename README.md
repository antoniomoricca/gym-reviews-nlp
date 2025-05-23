# Gym Review Analysis using NLP
Natural Language Processing analysis on real customer reviews from Google and Trustpilot, focused on a gym chain. The project explores sentiment, key topics, and differences between various approach ( BERTopic vs LLM).

This project focuses on analyzing customer reviews for a major gym chain, aiming to improve member satisfaction by identifying the root causes of negative feedback. Due to confidentiality and non-disclosure agreements (NDA), the specific identity of the gym chain cannot be revealed in this documentation.

Customer reviews were analyzed using various Natural Language Processing (NLP) techniques for topic modeling, including:

- Gensim
- BERTopic for semantic clustering
- Large Language Model (LLM)

Additionally, LLM were leveraged to extract deeper insights from the review content. A sentiment analysis model was also used to identify reviews expressing strong negative emotions, helping to surface hidden emotional drivers of dissatisfaction. The project's ultimate goal is to uncover the underlying motivations behind customer dissatisfaction and propose targeted solutions to address the main issues, thereby supporting improvements in the overall member experience.

## Project Structure
### 1.  Dataset Loading, EDA, and NLP Preprocessing Pipeline
The analysis begins with loading the customer review datasets from Google and Trustpilot sources. Initial exploratory data analysis (EDA) examines the following features:

- Review date
- Location
- Review rating (0-5 stars)
- Review text

The text preprocessing pipeline includes:

- Removing numbers
- Converting to lowercase
- Removing stopwords (from nltk)
- Tokenization

This standardized text is then used as input for subsequent analysis steps.
### 2. Topic Modeling with BERTopic
A pre-trained Hugging Face transformer model powers the BERTopic implementation, allowing for semantic clustering of reviews based on contextual embeddings rather than just keyword frequency. This approach enables the discovery of nuanced topics within the corpus of gym member feedback.

Below the main topics identified in the merged dataset of negative reviews ( rating < 3):

![image](https://github.com/user-attachments/assets/64440ced-2f80-465d-973b-c548dd095812)

The topics appear to be well-separated and each one points to a distinct issue frequently mentioned by customers. From equipment quality and air conditioning to cleanliness and staff behavior, the topics reflect a wide range of operational aspects. This suggests that customer feedback is focused on specific, tangible problems rather than general dissatisfaction, providing clear opportunities for targeted improvements across different areas of the business.

### 3. Sentiment Analysis and Emotion-Specific Topic Modeling
Sentiment analysis is conducted using a pre-trained Hugging Face emotion detection model to categorize reviews by emotional tone. Reviews with "anger" as the dominant emotion are isolated for further analysis, as these often contain the most actionable feedback. The angry reviews subset is then processed through BERTopic again to identify specific triggers associated with high negative emotional responses. Below the topics identified:

![image](https://github.com/user-attachments/assets/1616a610-3fe1-434e-a36b-c9774141107d)

The analysis of reviews filtered by anger reveals a sharper focus on issues that trigger strong emotional responses, distinguishing them from the broader dissatisfaction patterns observed earlier. The most prominent topics (Topic 1, 2 and 3) highlight specific friction points that go beyond general inconvenience. These experiences, like paying for access and being unable to enter the gym or facing recurring issues with class scheduling, can generate frustration and a sense of unfair treatment. Such moments are more likely to provoke emotional reactions and ultimately drive customer churn.


### 4. LLM-Enhanced Insight Extraction
The Phi-4-mini language model is leveraged in two distinct ways:
1. Topic refinement: All customer reviews were processed using a large language model (LLM) with a single-shot prompting approach to extract three key subtopics from each review. These subtopics were then consolidated into a comprehensive list and clustered using BERTopic, enabling the identification of core themes with greater granularity and relevance to operational improvements.
**This pre-processing step introduced a layer of abstraction, as the LLM distilled the original content into higher-level thematic representations**. For instance, rather than isolating specific complaints like broken machines, lack of variety, or long waits, the LLM might infer a broader issue such as "poor equipment maintenance and availability." As a result, BERTopic operated on input that was already semantically condensed, leading to the emergence of broader, more conceptual topics such as customer dissatisfaction, overcrowding, or poor communication.


2. Insight generation: Analyzing patterns in the data—using the previously identified topics as input—to generate actionable business insights and targeted recommendations for addressing member concerns. This multi-layered approach leverages the strengths of traditional NLP techniques, embedding-based topic modeling, and generative AI to deliver a deeper and more structured understanding of customer feedback.
Below an example of the generated insights:

- Overcrowding and lack of space:
   - Implement a reservation system to manage peak time attendance and ensure adequate space for all members.
   - Expand gym facilities or add additional workout areas to accommodate more members.
   - Offer off-peak hour classes to distribute the customer load throughout the day.
 
- Poor customer service and communication:
   - Provide comprehensive training for staff to improve customer interaction and problem-solving skills.
   - Establish clear communication channels for members to reach out to customer service, such as a dedicated phone line, email, and chat support.
   - Regularly update members on gym policies, class schedules, and any changes through multiple platforms (website, app, email).

### 5. Gensim
Gensim is used to perform topic modeling on the review dataset. Gensim is a model based on Latent Dirichlet Allocation (LDA), a probabilistic model that identifies latent topics by analyzing word co-occurrence patterns.

## Conclusion
In conclusion, BERTopic was applied in three different ways: on raw reviews, on anger-filtered reviews via sentiment analysis, and on summaries generated by a large language model (LLM).
1. When applied to raw reviews, BERTopic effectively identified concrete, recurring issues behind customer dissatisfaction, such as equipment problems or staff behavior.
2. Filtering for angry reviews led to even more specific and emotionally charged topics, highlighting issues that clearly triggered strong negative reactions.
3. When using LLM-generated summaries as input, BERTopic worked on semantically condensed content, leading to more abstract and high-level topics—such as poor communication or overall dissatisfaction—rather than isolated complaints. This preprocessing step allowed the model to capture broader themes, and the LLM itself provided actionable recommendations to address these underlying issues.
   
Overall, the combined approach proved valuable in uncovering both granular pain points and high-level themes, while Gensim-based modeling was less informative in comparison.

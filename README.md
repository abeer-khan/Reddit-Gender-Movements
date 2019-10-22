# Reddit-Gender-Movements

What are the gender issues people discuss today? What do we know about the people who discuss them? Where should we even look to find this information? 

There has been a surge in the use of social media to understand social issues. Social media offers (a) current, (b) many, and (c) possibly more honest discussions of possibly sensitive gender issues online. For e.g. consider the hashtag #IDidNotReport, #MeToo, #NotAllMen. 

We use social media here too, namely Reddit. We examine large subreddits related to gender & aligned with social movements related to gender (gendered movements), namely r/TheRedPill, r/MensRights, r/Feminism, in addition to r/AskMen, r/AskWomen. 

We examine their posts to extract the gender issues and various perspectives on them. 
For this we (a) Preprocess & use NMF on posts. We then reorganize the topics yielded by NMF into higher level topics (henceforth referred to as themes). We end up with about 17 themes.
We then extract the keywords used by each subreddit to discuss each them (leading to at most 6 * 17 sets of keywords). 
This part is a mixed-method analysis using both NMF and human involvement. 

We examine their comments to extract some characteristics of the people involved with these gendered subreddits. 
For this we
2. Create subreddit2vec matrices <br>
  2.1. subreddit to text vectors (where subreddit content = text of the concatenation of all comments in the subreddit) <br>
    2.1.1. subreddit to tf-idf vectors <br>
    2.1.2. subreddit to embedding vectors (using pre-trained Twitter word2vec embeddings) <br>
      <t> 2.1.2.1. every subreddit = average of word embeddings of the words in its content <br>
      <t> 2.1.2.2. every subreddit = weighted average of all word embeddings with weights = its tf-idf <br>
  2.2. subreddit to interest vectors. <br>
  For each subreddit (all million subreddits), find the number of users it has in common with every other subreddit (actually the top 200-2000 = 2047 subreddits) <br>
  Find PPMI of each cell. <br>
  
# Main insights
Here is an incomplete list of results of this work:
1. gender movements discuss workplace sexism, personal safety, rape, and legal issues among other gender issues, and different movements often have different perspectives on these issues. 
2. people involved with the Men's Rights movement are similar to people who are politically right-leaning and associated with sexist or racist content, whereas people involved with the Feminism movement are similar to those who are politically left-leaning, support minorities, body acceptance, and survivors of sexual assault. 
3. people involved with The Red Pill movement are similar to those who do not believe in the egalitarianism of race or gender.

For more, please read Chapter 6 of my thesis https://uwspace.uwaterloo.ca/handle/10012/14973?show=full (pages 63-66).

# Some meta-insights 
1. NMF trumps LDA when it comes to getting specific insights. LDA produces topics that are too generic. A few others echo my opinion. Unfortunately they seem to exist more often in blogs than in research papers. See here for examples: <br> 
(a) https://wiki.ubc.ca/Course:CPSC522/A_Comparison_of_LDA_and_NMF_for_Topic_Modeling_on_Literary_Themes <br>
(b) An analysis of the coherence of descriptors in topic modeling - O'Callaghan, et al. <br>

I'm not sure why in my reading of research work, LDA seemed to be the algorithm most new topic algorithms compete against. 

2. Related to point (1). "Coherence" of a topic is a concept many topic modeling algorithms strive to achieve. A good topic modeling algorithm is one that yields coherent topics. They measure coherence via many metrics that attempt to mimic human judgements of coherence. These metrics use word counts, embeddings, stemmed and unstemmped corpora, and everything in between. <br>
Related work: <br>
(a) Exploring the space of topic coherence measures. Roder et al. <br>

I wonder if there exists a goodness of topic metric that measures both coherence, and specificity (where I use specificty to mean how specific a topic is vs being generic). 

3. Topic modeling is hard. No algorithm fits all datasets. You just have to try the existing ones on yours to see which works in your case. I'd recommend trying NMF before LDA before newer algorithms. 

# Further Reading
This is a list of resources that I found interesting conducting this research. Maybe you will too. 
1. See my thesis for more information https://uwspace.uwaterloo.ca/handle/10012/14973?show=full . Yes, I know this is actually a summary of my research. 
2. Topic Modeling related <br>
  2.1. CluWords CluWords: Exploiting Semantic Word Clustering Representation for Enhanced Topic Modeling <br>
  2.2. Topic Modeling for Short Texts with Auxiliary Word Embeddings. Li et al. <br>
  2.3. Short-text topic modeling via Non-Negative Matrix Factorization Enriched with Local Word-Context Correlations. Shi et al. <br>
  2.4.

... to be continued. 

# A Data-driven Analysis of Gendered Subreddits (The Red Pill, Men's Rights, Feminism, Ask Men, Ask Women) 

We've been accepted to <a href="http://dbdmg.polito.it/darli-ap2020/">DARLI-AP 2020</a>! The conference proceedings aren't out yet, so <a href="https://github.com/abeer-khan/Reddit-Gender-Movements/blob/master/Reddit_gender%20(1).pdf"> here </a> is a copy of the paper: 

<br>

If you want even more details, skim the abstract & Chapter 6 of my <a href="https://uwspace.uwaterloo.ca/handle/10012/14973?show=full"> thesis</a>! 

# A. Why I did it?
What are the gender issues people discuss today? What do we know about the people who discuss them? Where should we even look to find this information? 

There has been a surge in the use of social media to understand social issues. Social media offers (a) current, (b) many, and (c) possibly more honest discussions of possibly sensitive gender issues online. For e.g. consider the hashtag #IDidNotReport, #MeToo, #NotAllMen. 

# B. What I did
We use social media here too, namely Reddit. We examine large subreddits related to gender & aligned with social movements related to gender (gendered movements), namely r/TheRedPill, r/MensRights, r/Feminism, in addition to r/AskMen, r/AskWomen. 
We examine their posts to extract the gender issues and various perspectives on them. 
We examine their comments to extract some characteristics of the people involved with these gendered subreddits. 

# C. How I did it
We examine their posts to extract the gender issues and various perspectives on them. 
For this we (a) Preprocess & use NMF on posts. We then reorganize the topics yielded by NMF into higher level topics (henceforth referred to as themes). We end up with about 17 themes.
We then extract the keywords used by each subreddit to discuss each them (leading to at most 6 * 17 sets of keywords). 
This part is a mixed-method analysis using both NMF and human involvement. 

We examine their comments to extract some characteristics of the people involved with these gendered subreddits. 
For this we create two kinds of subreddit to vector matrices: <br>
1. subreddit to text vectors (where subreddit content = text of the concatenation of all comments in the subreddit)
  <ol>
  <li> 1. subreddit to tf-idf vectors </li>
  2. subreddit to embedding vectors (using pre-trained Twitter word2vec embeddings)
    * every subreddit = average of word embeddings of the words in its content 
    * every subreddit = weighted average of all word embeddings with weights = its tf-idf
  </ol>
2. subreddit to interest vectors.
  * For each subreddit (all million subreddits), find the number of users it has in common with every other subreddit (actually the top 200-2000 = 2047 subreddits)
  * Find PPMI of each cell.
        
I have the matrix calculated as per (2). It's too large to upload. Email me and I'll share a copy. 
  
## FAQ: Why did I choose NMF as the topic modeling algorithm of choice?
Short Answer: It produced topics that seemed coherent to us. 

Long Answer: 
I tried LDA, NMF, and SeaNMF for various number of topics. I tried them on both stemmed and unstemmed versions of the corpora. <br> 
I tried various coherence metrics that used embeddings, either pre-trained on external corpora, or those trained on Reddit corpora. <br>
The results were inconclusive. No one topic mdeling algorithm stood out as the best one. Using our (human) judgment, the judgment these metrics attempt to mimic, we realized LDA was producing super generic topics. NMF and SeaNMF produced similar & comparable topics. But, SeaNMF took longer to do it. So, we went with NMF. <br>
I later found work that echored our observations of LDA vs NMF (see meta-insights).

A partial list of the combinations I tried: 
1. word2vec embeddings pre-trained on an unstemmed Twitter corpus where stop words weren't removed. 
2. fastText embeddings I trained on a neutral Reddit corpus (^). ^ was stemmed, and standard stop words were removed. 
3. word2vec embeddigs I trained on each of the gendered subreddits. These were stemmed and standard stop words were removed. 

^ this was text from AskReddit. Since this is a Reddit subreddit, I expect the jargon to be somewhat similar to each of the gnedered subreddits. 

# E. What did I learn / Main Insights? 
Here is an incomplete list of results of this work:
1. gender movements discuss workplace sexism, personal safety, rape, and legal issues among other gender issues, and different movements often have different perspectives on these issues. 
2. people involved with the Men's Rights movement are similar to people who are politically right-leaning and associated with sexist or racist content, whereas people involved with the Feminism movement are similar to those who are politically left-leaning, support minorities, body acceptance, and survivors of sexual assault. 
3. people involved with The Red Pill movement are similar to those who do not believe in the egalitarianism of race or gender.

For more, please read Chapter 6 of my thesis https://uwspace.uwaterloo.ca/handle/10012/14973?show=full (pages 63-66).

# F. Some meta-insights 
## F.1. NMF >> LDA
1. NMF trumps LDA when it comes to getting specific insights. LDA produces topics that are too generic. A few others echo my opinion. Unfortunately they seem to exist more often in blogs than in research papers. See here for examples: <br> 
(a) https://wiki.ubc.ca/Course:CPSC522/A_Comparison_of_LDA_and_NMF_for_Topic_Modeling_on_Literary_Themes <br>
(b) An analysis of the coherence of descriptors in topic modeling - O'Callaghan, et al. <br>

I'm not sure why in my reading of research work, LDA seemed to be the algorithm most new topic algorithms compete against. 

## F.2. Coherence metrics didn't really work for me
2. Related to point (1). "Coherence" of a topic is a concept many topic modeling algorithms strive to achieve. A good topic modeling algorithm is one that yields coherent topics. They measure coherence via many metrics that attempt to mimic human judgements of coherence. These metrics use word counts, embeddings, stemmed and unstemmped corpora, and everything in between. <br>

Here is how I organized the "coherence" metrics in my head, based on my reading: <br>
1. use word co-occurrences <br>
  1.1. these co-occurrences are calculated on my own corpus (in my case gendered subreddits) <br>
  1.2. these co-occurrences are calculated on an external corpus. <br>
2. use embeddings <br>
  2.1. trained on my own corpus <br>
    2.1.1. word2vec (trained on stemmed / unstemmed, stop removed / not removed corpora) <br>
    2.1.2. fastText (trained on stemmed / unstemmed, stop removed / not removed corpora) <br>
    ... <br>
  2.2. trained on external corpora <br>
    2.2.1. word2vec (trained on stemmed / unstemmed, stop removed / not removed corpora) <br>
    2.2.2. fastText (trained on stemmed / unstemmed, stop removed / not removed corpora) <br>
    ... <br>
    
Obviously, it's a little unfair if you use coherence metrics that use embeddings trained on stemmed corpora, to evaluate the goodness of topic models on corpora that are not similarly preprocessed. <br>
 
Related work: <br>
(a) Exploring the space of topic coherence measures. Roder et al. <br>

I wonder if there exists a goodness of topic metric that measures both coherence, and specificity (where I use specificty to mean how specific a topic is vs being generic). 

## F.3. One topic model doesn't fit all
3. Topic modeling is hard. No algorithm fits all datasets. You just have to try the existing ones on yours to see which works in your case. I'd recommend trying NMF before LDA before newer algorithms. 

## F.4. World of text (Reddit) -> Subreddit -> posts -> topics -> themes
4. We bounced around a lot to different levels of text granularity here to get insights. <br>

We started with Reddit which is self-organized by subject into subreddits.  <br>
We then decided that merely knowing posts in say r/Feminism are related to Feminism is not enough. We'd like more fine grained topics <br>

We aggregated posts into topics. <br>

We then realized that hey, some topics are redundant or too fine-grained. So we went up to a higher level of granularity and organized topics into themes. <br>

Another interesting thing is that there are 2 different ways we could have gone from 6 subreddits -> 6x50 topics -> 17 themes. <br>
(a) We could look at all 6x50 topics and organize them into themes, and glean the perspectives different subreddits have on each theme, by looking at the constitutent topics of each subreddit under the theme. <br>
(b) We could look at each subreddit's topics in isolation, organize each subreddit's topics into themes (to have 6 sets of themes), and somehow compare them. <br>
We chose to do (a). I somehow find this design decision akin to the debate on calculating the average of several datasets. Do Is overall average = average(averages of each dataset) OR Is overall average = average(all the points in all the datasets). 

## F.5. Sentiment analysis is NOT necessarily the same as stance detection
There was a wonderful paper (or textbook???) that succinctly explained the difference. Unfortunately I can't find it. <br>
To my memory, sentiment analysis measures the positive / negative nature of the *language* of your text. On the other hand, stance detection measures whether the text agrees with a certain position. 
For e.g. consider "I like carrots so damn much it's insane >.<". The sentiment of the language is probably negative. But the author's stance towards carrots is positive.  

At one point we considered seeing which topics, and which subreddits, had more positive or negative sentiment language. Preliminary tests indicated the sentiment of texts labeled related to rape were most negative in both M & W dominated subreddits. The texts of M dominated subreddits were more negative in sentiments than W's. These results are not included in my final report. Why? (a) The fact that rape is more negative seems obvious, and (b) existing sentiment analysis tools have been known to show gender & racial bias (Examining Gender and Race Biasin Two Hundred Sentiment Analysis Systems - Kiritchenko et al.)

Please read my discussion on hate speech / abusive language / sentiment / stance analysis above. <br>

Related work: <br>
(a) Comparative studies of detecting abusive language on Twitter. Lee et al.  <br>
 
  
## F.6. Hate speech? Abusive language? 
These are interesting questions to think about in gendered issues. There is no consensus on what constitutes hate speech or abusive language. 

# G. Further Reading
This is a list of resources that I found interesting conducting this research. Maybe you will too. 
1. See my thesis for more information https://uwspace.uwaterloo.ca/handle/10012/14973?show=full . Yes, I know this is actually a summary of my research. 
2. Topic Modeling related <br>
  2.1. CluWords CluWords: Exploiting Semantic Word Clustering Representation for Enhanced Topic Modeling <br>
  2.2. Topic Modeling for Short Texts with Auxiliary Word Embeddings. Li et al. <br>
  2.3. Short-text topic modeling via Non-Negative Matrix Factorization Enriched with Local Word-Context Correlations. Shi et al. <br>
  2.4. Predicting Response to Poliitcal blog posts with topic models <br>
  2.5. LDAvis: Method for visualizing & interpreting topics. Stevert, Shirley. <br>
  2.6. Task-oriented Word Embedding for Text Classification. Liu et al. <br>
  2.7. Bag-of-embeddings for text classification. Jin et al. <br>
  2.8.
3. Gender <br>
  3.1. Identifying gender of microblog users based on message mining. Huang et al. <br>
  3.2. Machine Learning models of text categorization by author gender using topic-independent features. Sboev et al. <br>
  3.3. KNN with TF-IDF based framework for text categorization. Trstenjak et al. <br>
  3.4. 

... to be continued. 

# H. Acknowledgements
Besides the plenty researchers whose work I read, cited, mentioned above, many researchers around UWaterloo gender studies and philosophy departments helped me put my research in context. I'm grateful to their work.
I'm also grateful to all who make their work open source. Please reach out if you think I stood on your shoulders but forgot to cite you, I'd be happy to correct! 

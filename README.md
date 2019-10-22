# Reddit-Gender-Movements
Examine subreddits aligned with social movements related to gender (gendered movements), namely r/TheRedPill, r/MensRights, r/Feminism, in addition to r/AskMen, r/AskWomen

Examine their posts and comments. 
1. Preprocess & use NMF on posts <br>
2. Create subreddit2vec matrices <br>
  2.1. subreddit to text vectors (using subreddit content = concatenate all comments in the subreddit) <br>
    2.1.1. subreddit to tf-idf vectors <br>
    2.1.2. subreddit to embedding vectors (using pre-trained Twitter word2vec embeddings) <br>
      <t> 2.1.2.1. every subreddit = average of word embeddings of the words in its content <br>
      <t> 2.1.2.2. every subreddit = weighted average of all word embeddings with weights = its tf-idf <br>
  2.2. subreddit to interest vectors. <br>
  For each subreddit (all million subreddits), find the number of users it has in common with every other subreddit (top 200-2000 = 2047 subreddits) <br>
  Find PPMI of each cell. <br>
  

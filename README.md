# Text-Clustering
This project is used for text clustering for 2020 Marketing Conference. The general idea of this project is to group the papers with similar topics into the same cluster. Then, papers with similar topics are assigned to different sessions based on the average evaluator ratings.

## Data
The dataset used in this project includes 428 research papers, each record having 28 features.

For text clustering task, we need features including :
- ID: uniquely indentify a paper;
- Title : the title of the paper;
- Abstract : the abstract of the paper;
- Topic1, Topic2, Topic3 : Given by organizer? Author selected?
- Keyword1, Keyword2, Keyword3 : Given by organizer? Author selected?

For session assignment task, we features including evaluator ratings and comments.

## Text Clustering
### Propossess

After tokenization and removing stopwords, we lemmatize each word and transform some terms to their abbreviation to avoid redundancy. (see word list)

### Corpus

The most important task in this text clustering is to choose the right corpus. Title, topics and keywords are informative but too general. Abstracts contain some details which are not included in topics, keywords and titles. Therefore, we create three corpora for titles, topics and keywords, and abstracts separately. 

For title and topics &keywords corpora, given that most keywords are informative, we keep them all but remove genral words (e.g. marketing, content, general) .

For the abstracts corpus, we want to capture useful information which is misses in the other two part. First, we drop redundant words (e.g. the, and, is, are, etc) and ones incorporated in the other two corpora, and finally keep 336 out of 5000 words in 428 abstracts. Then, for each abstract, we select words which appear twice to six times as tags in addition to keywords submitted by author. For the current dataset, via the distribution of word frequency across abstracts, we find that 2-6 times of appearance in one abstract is the best thresholds for word selection. (This threshold may change when using different datasets.)

Finally we combine the three corpora to obtain the final corpus for clustering.

### Modeling

In the modeling step, we use Kmeans clustering algorithm and apply elbow method to find the optimal number of clusters. 

### Visualization

We use WordCloud to visualize each cluster. The word size corresponds to how important the word is in a specific cluster.

## Session Assignment

In each cluster, we assign papers with similar average ratings to one session and keep the paper number in each session around 4. 

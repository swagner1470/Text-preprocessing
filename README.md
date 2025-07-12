# Text-preprocessing

This is a work in progress and is intended for graduate level students as a general guide to whatever their specific data needs are. 

## Resources from people better than I
Matt Denny and Arthur Spirling have an [excellent article](https://www.cambridge.org/core/journals/political-analysis/article/abs/text-preprocessing-for-unsupervised-learning-why-it-matters-when-it-misleads-and-what-to-do-about-it/AA7D4DE0AA6AB208502515AE3EC6989E) about preprocessing for unsupervised learning, but it is generally a must read in my opinion for anyone diving into text analytics. Matt Denny also has many useful guides on his [website](https://www.mjdenny.com/Text_Processing_In_R.html) including one on preprocessing if you are unable to access the article above. 

For those wondering if text preprocessing is still worth the time given modern transformers introduced in the NLP literature, Marco Siino has a [nice piece](https://www.sciencedirect.com/science/article/pii/S0306437923001783) on exactly this question. He finds that yes, preprocessing still outpreforms transformers and that proper preprocessing actually increases performance. 

The NIH has [good article](https://pmc.ncbi.nlm.nih.gov/articles/PMC7861331/) on text as social and cultural data that covers many aspects, not just preprocessing.

SRK gives quick descriptors of many of the preprocessing steps alongside Python code in [this post](https://www.kaggle.com/code/sudalairajkumar/getting-started-with-text-preprocessing).

Gaurav Singhal has a [brief newsletter](https://www.pluralsight.com/resources/blog/guides/importance-of-text-pre-processing) that explains the importance of preprocessing. 

## Why do we care are preprocessing
If the work above doesn't give you the hint, I care about preprocessing and measurement in general a great deal. There are a lot of exciting developments in the world of NLP recently but be aware of overpromising. The old adage goes garbage in, garbage out. If you are not treating the data you train a model on with care, your model will not perform well. This is exasserbated with LLM and general NLP models where the goal is to constantly train with no real care for what the data going in looks like and what quality those data are. If you train a model using data from the internet that is freely available, there will be biases from each subset of people that interacts on each site. Recently, much of the data that used to be free to train with has been put behind paywalls. This further increases the need for higher performance, which preprocessing helps with, to save researchers money. 

## Steps for preprocessing
I typically use the steps in the order they are presented in Matt Denny and Arthur Spirling's article moentioned above. Each step should be considered carefully and combinations or some or all of them are almost always preferable to leaving the data raw. There are many pacakges for R and Python that can handle these steps for you, you can also just use regex. 

- Punctuation - cleaning the punctuation you do not want to remain. This is generally always done unless you are doing a form of text analysis where emotion in the text matters, where you will need to find a solution. For instance, ending a sentence with four exlcamation points is certainly a different vibe than a period. 
- Numbers - removing number is often done if you do not care about number, but they may be substantively useful for some use cases. 
- Lowercasing - Lowercasing removes uppercase text. Similar with punctuation, if you care about tone of the text, this can be a problem, as all caps text is conveying a different message than gramatically correct text. Further, if you care about proper nouns that have lowercase counterparts, this can be tricky.
- Stemming - This step merges forms of word together, it removes prefix and suffix characters like ing and ies for verb tense or plurality. This can be misleading if words have multiple means, as many English language words do.
- Stopword Removal - This is a step to remove the most common words used that do not change meaning as much. Think of the, it, and, etc. There are many lists of stopwords out there, take your pick or create your own. I often use a combination, where I start with the default package and ammend my domain specific words in. 
- n-gram inclusion - This is a big decision where you decide whether to treat words as single tokens or allow for combinations. Typically we use 1,2, or 3-gram as beyond that we move away from indivudal tokens mattering as much. Words have vastly different meanings when we consider them next to one another. A common step is to include them as an additional variable to consider alongside the individual tokens. 
- Infrequently used terms - Sometimes we remove words that very rarely show up in the text (<1%). We do this typically because we care about words and patterns, and if the word is almost never used it is hard to discern a patter. This also reduces the size of the document and makes analysis quicker, as times can get long with text analytics. 

## What to do now
Now that you have your data, start with modeling. You can iterate and decide if you want to include more or fewer preprocessing steps and compare your performance. 

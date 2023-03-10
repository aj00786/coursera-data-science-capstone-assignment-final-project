# Wordprediction Package for R
Ajmal
2023

### Summary

This package, submitted in partial fulfillment of the requirements of the Coursera course, "Data Science Capstone", contains functions for an auto-completion model that predicts the next word to be typed based on a word or phrase previously typed.  The presentation can be found at [http://rpubs.com/ajmal007/wordprediction](http://rpubs.com/jontieh/wordprediction) and a demonstration at [https://ajmal007.shinyapps.io/word-prediction/](https://ajmal007.shinyapps.io/word-prediction/).

Auto-completion is a common function on mobile devices. As a user types, an auto-completion function presents that user with possible completions to the current word being typed or probable words that could follow the current word or phrase after it is typed. The package "wordprediction" provides the latter function.

### Data

#### Data File

In order to build a function that can provide word-prediction, a predictive model is needed.  Such models use known content to predict unknown content.  For this package, that content comes from the HC Corpora collection, which is "a collection of corpora for various languages freely available to download" (Christensen, n.d.). The version used was obtained from an archive maintained at Coursera (Leek, Peng, Caffo, & Johns Hopkins University, n.d.).  The file included three text document collections, blogs, news feeds, and tweets, in four languages, German, English, Finnish, and Russian, of which only the English collections were used.  The files were too large to be manipulated using a home computer (e.g., the downloaded ZIP file was 575 MB).  Therefore, 1000 lines were randomly sampled from each collection using a Mac OS X (Version x86_64-apple-darwin13.4.0) terminal application before loading for analysis in RStudio (Version 0.99.892) running the R statistical programming language (Version 3.2.3).

#### Data Structure

This package uses the data stuctures described in Feinerer, Hornik, and Meyer (2008) from the Text Mining Package (Version 0.6-2; Feinerer, Hornik, & Artifex Software, Inc., 2015) "tm".  In these structures, text document collections are organized into corpora, the basic objects to be manipulated by the word-prediction function.  Accordingly, the HC Corpora data file were loaded as tm corpora.

#### Data Cleaning

Data cleaning involves transforming the raw text in the corpus into a format more suitable for automated manipulation.  The tm package provides numerous functions for such transformations (see Feinerer et al., 2008, p. 9).  For this package, the texts were converted to lower case, stripped of whitespace, and common stopwords (i.e., words so common that they contain little information; see Feinerer et al., 2008, pp. 25-26) were removed.  From the cleaned English corpus, a term-document matrix (TDM) was created, which is a matrix of words or phrases and their frequencies in a corpus.

### Prediction Model

According to Wikipedia (N-gram, n.d.), "an *n*-gram is a contiguous sequence of n items from a given sequence of text or speech."  This package takes a key word or phrase, matches that key to the most frequent *n*-1 term found in a TDM of *n*-word terms, and returns the *n*th word of that item.

Of course, not all possible words or phrases exist in the corpus from which the TDM was derived.  For this reason, a simplified Katz's back-off model is used, which backs off to smaller *n*-grams when a key is not found in the larger *n*-gram.  The maximum *n*-gram handled is a trigram.  The word returned is the match found in the largest *n*-gram where the key is found.  When the key is not found in the unigram, the most common word in the corpus "will" is returned.  This function is demonstrated using a Shiny app hosted on shinyapps.io at [https://jontieh.shinyapps.io/word-prediction/](https://jontieh.shinyapps.io/word-prediction/).

### Conclusion

This report has shown features the R package "wordprediction".  It was designed using samples of 1000 words each from a corpus of collections English words.  As shown in a demonstration, all phrases and words submitted to the function "katz_backoff_model" result in a prediction in the form of a single word returned.

### References

Christensen, H. (n.d.). *HC Corpora*. Retrieved from [http://www.corpora.heliohost.org](http://www.corpora.heliohost.org)

Feinerer, I., Hornik, K., & Artifex Software, Inc. (2015, July 2). Text Mining Package [Computer software]. Retrieved from [http://tm.r-forge.r-project.org](http://tm.r-forge.r-project.org)

Feinerer, I., Hornik, K., & Meyer, D. (2008). *Text mining infrastructure in R. Journal of Statistical Software, 25*(5), 1???54. [http://doi.org/citeulike-article-id:2842334](http://doi.org/citeulike-article-id:2842334)

Leek, J., Peng, R., Caffo, B., & Johns Hopkins University (n.d.). *Data Science Capstone*, Coursera. Retrieved from [https://www.coursera.org/learn/data-science-project/](https://www.coursera.org/learn/data-science-project/)

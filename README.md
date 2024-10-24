# book_babies
A project by
Erica E King
<br/>October 20, 2024

## TLDR:
This is a demo of the use of embeddings to generate recommendations with user interactivity.  

<br />I was laid off from ESPN Bet / Penn Interactive in September and I am looking for a new position - this is both a fun way to stay in practice as well as a demonstration of my skills in the recommendation space.  If you have a job opportunity, or just want to chat about books, boardgames, or this project please feel free to contact me via <a href='https://www.linkedin.com/in/ericaceaeking/'>LinkedIn</a> or <a href='mailto:zemerica+bookbabies@gmail.com'>email</a>.

## Mission

Create a book baby from two book parents such that the baby represents a combination of the two parents' embeddings as calculated in a variety of sort of 'genetic pairings' such as:
* as an average of the two input embeddings
* as a random 50/50 selection between the embeddings of th two parent books
* as a selection on a sliding % randomization (30/70?) between the embeddings of the two parent books

For each set of 2 (or N) parents, generate 3 (or M) daughter embeddings and return a book within the dataset which is most similar to the generated embedding.  I'll start with using 2 parents and 3 daughters, but this could be extended to any number of parents, N, and any number of daughters, M.

## Further planned enhancements:

Modeling:
* adjust the cost function so that it weights the results toward newer titles
* adjust the cost function so that it weights the results toward titles that are available in the library
* feed forward such that a user can choose a daughter book to become one of the new parents - also retain the information on the daughter book selected to contribute to the analytics around what types of genetic pairing are most interesting from a user perspective

Full System Insights:
* build out auto-updating A/B testing architecture and online results
* include tooltips to show insights into how each section is generated

## Datasets:

https://www.kaggle.com/datasets/ymaricar/cmu-book-summary-dataset
(Data is released under a Creative Commons Attribution-ShareAlike License)

https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset
CC0: Public Domain

https://www.kaggle.com/datasets/sp1thas/book-depository-dataset
<a href='https://creativecommons.org/licenses/by-nc-sa/4.0/'>CC BY-NC-SA 4.0</a>

## Method:

1. perform EDA on the book summary dataset.  What is the distribution of book ages, author popularity, genres, etc..
2. research various NLP models to generate embeddings on long-form summaries
3. use a modified PCA analysis to detect the optimal embedding dimension, ala https://machinelearning.apple.com/research/single-training-dimension-selection-for-word-embedding-with-pca
4. generate set of embeddings for each of the books using the available features and the optimal embedding dimension
5. use SHAP and https://projector.tensorflow.org/ to explore the semantic meaning of the embeddings
6. create a genetic_combinator function to generate a new embedding given two input embeddings by whatever genetic_pairing method is given
7. match the resulting genetics with a (or several different?) daughters
8. Do again, but with a version of the model that makes an adjustment to the cost function to weight in some way (toward newer titles is perhaps simplest for MVP, or once data augmentation is possible via 'what is available at your local library')

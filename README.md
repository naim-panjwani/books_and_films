# Project Description

It is interesting to see novels being adapted to films. Our question is whether the science fiction novels’ ratings correlate to ratings of films. Also, is there a correlation between science fiction ratings or film ratings with revenue obtained from a film?

# Analysis Steps

Here are the steps that were taken and some of the problems we found:  

## Extract data

1. Get the list of science fiction books adapted into films  
   * [Purnima](https://github.com/PurnimaChande://github.com/PurnimaChandel) scrapped [Wikipedia](https://en.wikipedia.org/wiki/Category:Films_based_on_science_fiction_novels) to get the list of science fiction books adapted into films.  
      * Code: [web_scrapping/Wikipedia_scrapping-Copy1.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/web_scrapping/Wikipedia_scrapping-Copy1.ipynb)
      * Output: [input_csv/newmovielist.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/newmovielist.csv)

2. Obtain book ratings  
   * [Purnima](https://github.com/PurnimaChande://github.com/PurnimaChandel) scrapped [GoodReads](www.goodreads.com), using the [list from step 1](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/newmovielist.csv) as search queries, to get the user ratings of these adapted science fiction books.
      * Code: [web_scrapping/goodread_scrape-Copy1.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/web_scrapping/goodread_scrape-Copy1.ipynb)
      * Input: [input_csv/newmovielist.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/newmovielist.csv)
      * Output: [input_csv/merged_list.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/merged_list.csv)
   * [Tigran](https://github.com/tikoz86) attempted to obtain book ratings from [Amazon Books](https://www.amazon.com/books-used-books-textbooks/), but was being blocked after a few queries regardless of which IP address and location he'd try from.
   * [Naim](https://github.com/naim-panjwani/) attempted to obtain ratings from [Chapters  Indigo](https://www.chapters.indigo.ca/en-ca/) only to find that the book ratings are not authorized/scrappable
      * Code: [additional/Scrape_Chapters_Indigo.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/additional/Scrape_Chapters_Indigo.ipynb)
      * Input: [input_csv/booklist_ratings.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/booklist_ratings.csv)

3. Obtain film ratings
   * [Callan](https://github.com/callanyan) queried the [list from step 1](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/booklist_ratings.csv) to the [OMDb API](http://www.omdbapi.com/) to extract movie  ratings and their revenue
      * Code: [API_manipulation/OMDB_API.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/API_manipulation/OMDB_API.ipynb)
      * Input: [input_csv/newmovielist.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/newmovielist.csv)
      * Output: [Transformed_data/movieListDB.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/movieListDB.csv)

## Transform

   * [Callan](https://github.com/callanyan) merged the book ratings with the results from the OMDb queries to get a combined dataset with book and movie titles and their corresponding ratings, and movie revenues
      * Code: [API_manipulation/OMDB_API.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/API_manipulation/OMDB_API.ipynb)
      * Inputs: [input_csv/merged_list.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/merged_list.csv) and [Transformed_data/movieListDB.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/movieListDB.csv)
      * Output: [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv) and a cleaner [Transformed_data/bookListDB.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/bookListDB.csv)

   * We did not have the [input_csv/merged_list.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/merged_list.csv) at the beginning, so [Naim](https://github.com/naim-panjwani/) merged book and movie titles by similarity from an older version of [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv). This worked well, but these results won't be used as it's best to use the queried title strings merged with their corresponding movie titles
      * Code: [additional/Merge_book_movie_titles_by_similarity.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/additional/Merge_book_movie_titles_by_similarity.ipynb)
      * Inputs: [input_csv/booklist_ratings.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input_csv/booklist_ratings.csv) and [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv)
      * Output: [Transformed_data/merged_book_and_movie_titles.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/merged_book_and_movie_titles.csv)

## Load

   * [Tigran](https://github.com/tikoz86) loaded the [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv) file to plot the relationships below:
      * Code: [Plots/plot.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/plot.ipynb)
      * Input: [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv)
      * Output:
         * [Books vs Movies Ratings.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/Books%20vs%20Movies%20Ratings.png)
         * [Movies Ratings vs Movies Revenues.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/Movies%20Ratings%20vs%20Movies%20Revenues.png)
         * [Books Ratings vs Movies Revenues.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/Books%20Ratings%20vs%20Movies%20Revenues.png)

   * [Naim](https://github.com/naim-panjwani/) has written a script ([Loading_into_MongoDB/MongoDump.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Loading_into_MongoDB/MongoDump.ipynb)) to enable dumping of the books and films information extracted into MongoDB database called adapted_scifi_films_db, creating a books and movies collection
   * Furthermore, once the database is created, [Loading_into_MongoDB/MongoLoad.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Loading_into_MongoDB/MongoLoad.ipynb) enables loading into pandas dataframes, and a quick inner join creates the CombinedDF dataframe between movies and books 
      * Code: [Loading_into_MongoDB/MongoDump.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Loading_into_MongoDB/MongoDump.ipynb) and [Loading_into_MongoDB/MongoLoad.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Loading_into_MongoDB/MongoLoad.ipynb)
      * Input: [Transformed_data/bookListDB.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/bookListDB.csv) and [Transformed_data/movieListDB.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/movieListDB.csv)
      * Output: adapted_scifi_films_db MongoDB database with books and movies collections


## Extra

  * We looked into whether our GoodReads ratings that we web-scrapped were similar to the ones from which [Kaggle processed](https://www.kaggle.com/gnanesh/goodreads-book-reviews) about a year ago. And this is indeed the case, the ratings did not change much (see [additional/Kaggle_merge_with_Adapted_MoviesList.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/additional/Kaggle_merge_with_Adapted_MoviesList.ipynb)). 
    * Plots: [kaggle_vs_our_ratings.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/kaggle_vs_our_ratings.png) and [kaggle_vs_our_ratings_diff.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/kaggle_vs_our_ratings_diff.png)
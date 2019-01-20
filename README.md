# Project Description

It is interesting to see novels being adapted to films. Our question is whether the science fiction novels’ ratings correlate to ratings of films. Also, is there a correlation between science fiction ratings or film ratings with revenue obtained from a film?

# Analysis Steps

Here are the steps that were taken and some of the problems we found:  

## Extract data

1. Get the list of science fiction books adapted into films  
   * [Purnima](https://github.com/PurnimaChande://github.com/PurnimaChandel) scrapped [Wikipedia](https://en.wikipedia.org/wiki/Category:Films_based_on_science_fiction_novels) to get the list of science fiction books adapted into films.  
      * Code: [goodread_scrape.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/goodread_scrape.ipynb)
      * Output: [input\ csv/booklist_ratings.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/booklist_ratings.csv)

2. Obtain book ratings  
   * [Purnima](https://github.com/PurnimaChande://github.com/PurnimaChandel) scrapped [GoodReads](www.goodreads.com), using the [list from step 1](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/booklist_ratings.csv) as search queries, to get the user ratings of these adapted science fiction books.
      * Code: [web\ scrapping/goodread_scrape-Copy1.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/web%20scrapping/goodread_scrape-Copy1.ipynb)
      * Input: [input\ csv/newmovielist.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/newmovielist.csv)
      * Output: [input\ csv/merged_list.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/merged_list.csv)
   * [Tigran](https://github.com/tikoz86) attempted to obtain book ratings from [Amazon Books](https://www.amazon.com/books-used-books-textbooks/), but was being blocked after a few queries regardless of which IP address and location he'd try from.
   * [Naim](https://github.com/naim-panjwani/) attempted to obtain ratings from [Chapters  Indigo](https://www.chapters.indigo.ca/en-ca/) only to find that the book ratings are not authorized/scrappable
      * Code: [Scrape_Chapters_Indigo.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Scrape_Chapters_Indigo.ipynb)
      * Input: [input\ csv/booklist_ratings.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/booklist_ratings.csv)

3. Obtain film ratings
   * [Callan](https://github.com/callanyan) queried the [list from step 1](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/booklist_ratings.csv) to the [OMDb API](http://www.omdbapi.com/) to extract movie  ratings and their revenue
      * Code: [OMDB5.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/OMDB5.ipynb)
      * Input: [input csv/newmovielist.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/newmovielist.csv)
      * Output: [Transformed_data/movieListDB.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/movieListDB.csv)

## Transform

   * [Callan](https://github.com/callanyan) merged the book ratings with the results from the OMDb queries to get a combined dataset with book and movie titles and their corresponding ratings, and movie revenues
      * Code: [OMDB5.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/OMDB5.ipynb)
      * Inputs: [input\ csv/merged_list.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/merged_list.csv) and [Transformed_data/movieListDB.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/movieListDB.csv)
      * Output: [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv)

   * We did not have the [input\ csv/merged_list.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/merged_list.csv) at the beginning, so [Naim](https://github.com/naim-panjwani/) merged book and movie titles by similarity from an older version of [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv). This worked well, but these results won't be used as it's best to use the queried title strings merged with their corresponding movie titles
      * Code: [Merge_book_movie_titles_by_similarity.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Merge_book_movie_titles_by_similarity.ipynb)
      * Inputs: [input\ csv/booklist_ratings.csv](https://github.com/naim-panjwani/books_and_films/blob/master/input%20csv/booklist_ratings.csv) and [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv)
      * Output: [Transformed_data/merged_book_and_movie_titles.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/merged_book_and_movie_titles.csv)

## Load

   * [Tigran](https://github.com/tikoz86) loaded the [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv) file to plot the relationships below:
      * Code: [Plots/plot.ipynb](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/plot.ipynb)
      * Input: [Transformed_data/CombinedDF.csv](https://github.com/naim-panjwani/books_and_films/blob/master/Transformed_data/CombinedDF.csv)
      * Output:
         * [Books vs Movies Ratings.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/Books%20vs%20Movies%20Ratings.png)
         * [Movies Ratings vs Movies Revenues.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/Movies%20Ratings%20vs%20Movies%20Revenues.png)
         * [Books Ratings vs Movies Revenues.png](https://github.com/naim-panjwani/books_and_films/blob/master/Plots/Books%20Ratings%20vs%20Movies%20Revenues.png)

   * [Naim](https://github.com/naim-panjwani/) has made the dataset available for loading into MongoDB
   NoSQL database
      * Code:
      * Input:
      * Output:
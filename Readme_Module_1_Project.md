# Strategies on Entering the Film Industry: 

## Overview

### “Microsoft Film Studios - Project ”

Microsoft wants to create a new movie studio and create original video content like the big film companies. To this end, they've hired us to help them better understand the movie industry. Our team is charged with doing data analysis and creating a presentation that explores what type of films are currently doing the best at the box office. We will then need to translate these findings into actionable insights that the CEO can use when deciding what type of films they should be creating.
In this project, we had access to several data sets that needed to be analyzed to help into the probable Microsoft’s entry into filmmaking. The datasets included a wide range of related data as shown below in .csv and .tsv files:

• *Box Office Mojo:*
    - bom.movie_gross.csv.gz
• *IMDB:*
    - imdb.name.basics.csv.gz
    - imdb.title.akas.csv.gz
    - imdb.title.basics.csv.gz
    - imdb.title.crew.csv.gz
    - imdb.title.principals.csv.gz
    - imdb.title.ratings.csv.gz
• *TMDB:*
    - tmdb.movies.csv.gz
• *The Numbers:*
    - tn.movie_budgets.csv.gz
• *Rotten Tomatoes:*
    - rt.movie_info.tsv.gz
    - rt.reviews.tsv.gz
    
Given the breadth of the data and differing variables provided (genre, budget, directors, studios, review text, popularity, gross sales), I figured we had enough data and there wouldn’t be any need for scraping additional data, especially with the recent changes in the way movies are watched. I chose three questions to identify steps toward successful entry. The questions covered the areas of timing and profitability, diversity in filmmaking, as well as assessing the budgets of top film studios for benchmarking purposes.

### The Questions
I chose these three questions with the understanding that these are avenues towards determining the type of film company we would like to create, and to place us within the industry.

1.	What time of year would we want to release our first film?
2.	What genres are popular among non-English movies?
3.	What are the top studios in terms of revenue and what are their production budgets compared to one another?

Although these questions might not seem interrelated, they help us to form a picture of the seasonality, diversity, and players in the space. In 2019, global box office revenue was $42.5 billion . According the Billboard, this growth spurt overall was fueled by an uptick at the foreign box office, where revenue came in at $31.1 billion . This growth in foreign box office contributed to our thinking of including foreign language films so as to learn something about the preferences. In addition, with the advent of a plethora of options where movie enthusiast can watch their favorite actor across multiple platforms on an incalculable number of devices, the data on seasonality analyzed here could also help in thinking what fuels viewers to watch movies at certain times of the year and what does the effect of the new platforms mean for traditional box offices.

## Setting Up Our Data

The modules I imported were:
- pandas for data analysis
- numpy for scientific computation
- os for interfacing with local file paths
- matplotlib for basic plotting
- seaborn for advanced plotting
- glob to generate pathnames
- sqlite3 for running SQL queries on our datasets

I used glob to create a variable holding all zipped files in the zippedData folder provided. I then used a for loop to unzip the files, pull the path and return the basename, clean the filename, and return each file as a dataframe within our files_dict dictionary.

### Seasonality and Profit

We review the seasonality of movie releases by profit

### Question 1: What season is the most profitable to release a movie?

Convention leads us to believe that summer is a popular time for moviegoing. Do movies have a greater chance of success in the summer, or any time of year? I used The Numbers' data set in order to answer this question. The dataset contains over 5000 movies released from 1915 to 2019.

### EDA for Profits and Release Dates

We clean the data and add relevant columns by determining the profit of each movie, the month of release, ensuring the data types are correct, and remove duplicates.

### Data Reviews

We review the data using an SQL query to get a better sense of the scale of the profit numbers.

### Data Visualization

We will plot our data using a boxplot to show the profits for each month. We use a boxplot so that we can see the IQR for movie profits and how the vary from month to month. We will also remove the outliers but leave in the whiskers to get a good sense of the full range of movie success by month.

![Seasonality_&_Profit](https://github.com/machkev/dsc-mod-1-project-v2-1-onl01-dtsc-pt-030220/Images/Seasonality&Profits.png)
 
### Findings
From our boxplot, we see there's dual seasonality of higher profits during the summer and at the end of the year. The highest profit in summer can be realized during the months of June and in November toward the winter months.

### Recommendations
Microsoft should take into account the seasonality of profits and target movies to be released in May or June to ensure a higher likelihood of it being a hit.

### Future Work
We should continue to track by genre what the best time is for a movie release, or examine the ROI for movies in certain genres.


### Diversity and Filmmaking:

Review Foreign Films  by Viewership and Genres

### Question 2 : What are the most popular genres amongst foreign language movies?

Turning to the genre and viewership of movies, there has been an increasing recognition and viewership towards non-English films over the last years. Prompted by the increasing representation of non-English films in the last few years (Roma and Parasite, namely), I wanted to look at what genres were commonly represented in our databases and what genres are represented. In the event Microsoft decides to pursue the independent or film-right acquisition at festivals, this analysis would help in building confidence on how to select a genre type and whether it would be profitable.

I also initially wanted to explore the visualization of both voter rating by genre and voter rating against popularity (a separate metric recorded by TMDB that indicates search results, 'likes', watchlists and other variables internal to their site. Both datasets had over 14,000 entries, but after removing the English movies and merging to one dataframe that contained genres my combined dataset had 252 films from 2010 - 2018.

### EDA for non-English genres and popularity
 

![Non-English-Genre](https://github.com/machkev/dsc-mod-1-project-v2-1-onl01-dtsc-pt-030220/Images/Non_English_Genre.png)

Each film had up to three genres tagged, so the total number of data points in the above visualization are more than 252. I  dropped the genres with fewer than 10 films tagged. However, the runaway dominant genre is Drama, followed by Comedy and Romance.


![Average_Rating](https://github.com/machkev/dsc-mod-1-project-v2-1-onl01-dtsc-pt-030220/Images/Avg_Rating_for_non-English.png)

 
I also created a SQL table to show the average voter rating in each genre. Our top 3 genres didn't make the top 5 average voter ratings by genre, with War films having the highest vote average at 7.310 and Horror films having the lowest at 6.22. Below are the rankings of our top three genres, out of a complete list of 21 genres.
•	6 Drama 6.893789 161
•	9 Romance 6.760784 51
•	19 Comedy 6.395238 84

Given that our TMDB data also has a variable on Popularity, which is based on number of votes, views, users adding a title to their watchlist or favorites, as well as previous day's popularity, I also wanted to confirm whether voter average was correlative to popularity - the correlation is 0.132982, so there is no correlation.

### Findings
Non-English Drama and Comedy are likely to attract more viewers.

### Recommendations
If Microsoft Studio decides to go ahead with production and distribution of foreign films, drama and comedy would likely attract more viewers.

### Future Work
We will need to explore further what foreign language films are appealing to moviegoers (and more profitable). We should also find additional sources to gauge moviegoer sentiment rather than the vote average and popularity from our dataset.
I recommend that we continue to scrape for further data to ensure our lists are accounting for the nature of our foreign language titles, including special characters that our databases may not be including and titles that are in different alphabets to see whether that results in a more complete dataset. We should also see if there are any languages in particular that are popular with our audiences.

### Top Studios and their Budgets

### Q3: What are the leading movie studios and their production budgets?

We will review the Box Office Magic, Rotten Tomatoes tables and our existing dataframe from the previous question to see which has the longest data set on studio information. We would like to determine which studios are releasing the most movies, and would like to compare the production budgets of those studios.
 

![Studio_Budgets](https://github.com/machkev/dsc-mod-1-project-v2-1-onl01-dtsc-pt-030220/Images/Studio_Budgets.png)

### EDA for Studios and Production Budgets

There is an obvious divide between the studios with high production, and a mean annual production spend of 531,708,500, and a median of 595,500,000.
Buena Vista's annual budget based on release date far exceeds this average cost based on movie release year, with a spend of 1.05 billion dollars. Magnolia Pictures' production budget is a mere fraction of this as the studio with the lowest spend, at 25.22 million dollars (a not-inconsiderable sum).


### Findings

The major film studios,(Warner Bros, Universal, Paramount, Fox and BV) as presumed, regularly have bigger annual production budgets (of approx. $1bn) than smaller independent distributors ( such as Sony Pictures Classic, Magnolia Studios and IFC) that acquire and distribute films.

### Recommendations

Microsoft should consider the prospect of attaching its name to film acquisition and distribution rather than original production. As these lower budget movies still made it to top 10 together with the major film, it might be an appropriate model to enter the industry.

### Future Work

In order to get a sense of viability, we will need to gauge the actual profitability of the acquisition and distribution model as compared to original production model.

### Conclusion

From the above analysis, we can conclude by summarizing our findings and recommend the following:
1.	We recommend entering the movie industry through an acquisition/distribution model as more top movies can be produced at a lower budget than producing an original movie as major film studios do.
2.	Although there is wide variety of popular genre in foreign language film, we recommend choosing Drama or Comedy genre if the business decides to go with a foreign language film production or distribution.
3.	We would recommend planning for movie releases towards the summer or at the end of the year. It is important to point out that the month of June has recorded both huge profits and huge losses too.

# Other Project Deliverables in Repository
1. Jupyter Notebook (K_Machine_Final_Module_1-Project.ipynb)
2. This Readme.md file (Readme_Module_1_Project.md)
3. Keynote Presentation (Presentation.pdf)
4. Blogpost (https://machkev.github.io/visualization_using_seaborn)
5. Video Walkthrough (https://drive.google.com/file/d/1hIgkSvubjEPifY0XjjfBMFcX60BzcJw0/view?usp=sharing)

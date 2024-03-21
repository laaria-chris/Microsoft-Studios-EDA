# Microsoft-Studios-EDA
![microsoft_movie_logo](visuals_Data/microsoft_movie_logo.png)


#### Contributing Members: LAARIA CHRIS

### Project Overview

Microsoft recently announced its ambitious foray into the film industry, signaling its intent to establish a dedicated studio. However, the company faces a significant challenge due to its limited understanding of the intricacies of the movie business. To address this, our mission entails comprehensive data collection, meticulous data cleaning, and rigorous analysis drawn from a plethora of sources. By synthesizing this information, we aim to furnish Microsoft with actionable insights and recommendations tailored to empower their endeavors in the film industry, fostering a pathway to sustainable success and innovation.

### Data and Exploration
In the folder zippedData are movie datasets from:
  1.https://www.boxofficemojo.com/
  2.https://www.imdb.com/
  3.https://www.rottentomatoes.com/
  4.https://www.themoviedb.org/
  5.https://www.the-numbers.com/

In our analysis we explore and answer the following questions:
1. What are the most profitable movies and how much should you spend?
2. What is the best time of the year to release a movie?
3. How does the rating of the various genres of movies fair in IMDB data?
4. Which movie directors and writers add value to the movie ratings?

## Question 1: What are the most profitable movies and how much should you spend?
To answer this question and provide a recommendation we'll make use of a budgets dataframe called `idf_movie_budgets`. Our analysis will require that we use the data to calculate profit and profit margin.
We also calculated the return on investment as seen below.

```
# Calculate profit
df_movie_budgets['profit'] = df_movie_budgets['worldwide_gross'] - df_movie_budgets['production_budget']
# Calculate profit margin
df_movie_budgets['profit_margin'] = (df_movie_budgets['profit'] / df_movie_budgets['worldwide_gross']) * 100

# Calculate ROI (Return on Investment)
df_movie_budgets['ROI'] = (df_movie_budgets['profit'] / df_movie_budgets['production_budget']) * 100

# Display the DataFrame with the new 'ROI' column
df_movie_budgets.head()

```
We examine the overall trend of budget versus profit to see if there's any correlation.

![BudgetVProfit](visuals_data/production-budgetvVSprofit.png)

This scatter plot is helpful in beginning to understand how much money should be budgeted for a movie. The positive trend line indicates that an increase in the budget will result in an increase in profit.

We also did an EDA on the top 25 profitable movies
```
profitable_movies_df = df_movie_budgets.loc[df_movie_budgets['profit'] > 0]
profitable_ranked_df = profitable_movies_df.sort_values(by=['profit'], ascending=False)
profitable_ranked_df.reset_index(inplace=True)
profitable_ranked_df.head()
```
![BudgetVProfit](visuals_data/production-budgetvVSprofit.png)

**Question 1 Conclusion:** Clearly the most successful 25 movies have both incredible profits and profit margins. Titanic (1997), Avatar, and Avengers: Endgame are the most successful movies in terms of sheer profit. Microsoft should budget \$60,000,000 for a movie and that budget should correlate with a profit margin of 55\%. 

## Question 2: What is the best time of the year to release a movie?
We start by converting the dates from the `df_movie_budgets` dataframe to a datetime object.  We then do a count by month to see the number of movies released in each month.

When grouping by month, we can select the `Profit`  so that we can see which months have the most financial success.
![MarginByMonth](visuals/MarginByMonth.png)

Finally we plot the  profit by month for a small selection of genres.  We can see that there is a general trend amongst these genres for the profit in each month.

![ProfitbyMonthbyGenre](visuals/ProfitbyMonthbyGenre.png)

**Question 2 Conclusion:** We recommend that Microsoft release the bulk of their movies, especially Animation, during the summer months (i.e. May-July). Adventure, Drama and Comedy movies would see similar success if released in November, but the recommendation remains to focus on summer.

## Question 3: How does the rating of the various genres of movies fair in IMDB data?
In this step we will be working with the IMDB sql database.We first begin by viewing the two tables movie_basics and movie_ratings into a pandas dataframe.

Then use SQL query to obtain the data from the datasets and store them into a pandas dataframe.

![MarginByMonth](visuals/MarginByMonth.png)

Finally we plot the  profit by month for a small selection of genres.  We can see that there is a general trend amongst these genres for the profit in each month.

![ProfitbyMonthbyGenre](visuals/ProfitbyMonthbyGenre.png)

**Question 3 Conclusion:** We recommend that Microsoft release the bulk of their movies, especially Animation, during the summer months (i.e. May-July). Adventure, Drama and Comedy movies would see similar success if released in November, but the recommendation remains to focus on summer.
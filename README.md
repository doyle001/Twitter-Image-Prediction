Twitter Image Prediction
Project Objectives
The Project main Objectives were:

- Perform data wrangling (gathering, assessing and cleaning) on provided thee sources of data
- Store, analyze, and visualize the wrangled data.
- Reporting on (1) data wrangling efforts and (2) data analyses and visualizations
1.0 Gathering Data
In this phase, the three pieces of data were gathered and represented as pandas dataframes:
- The WeRateDogs Twitter archive (file on hand, manual download of 'twitter-archiveenhanced.csv')
- The tweet image predictions ('image-predictions.tsv'). This file was be downloaded programmatically using the Requests library from a provided URL.
- Each tweet's entire set of JSON data (with at minimum tweet ID, retweet count, and favorite count) in a file called 'tweet_json.txt' were stored using Twitter API andPython's Tweepy library. Each tweet's JSON data was written to its own line.
2.0 and 3.0: Assessing and Cleaning Data
While working with data, a number of observations were made. Below are the observations along with actions taken in the Cleaning Step

twitter_archive
Some values in rating_denominator column isn't "10" were fixed
Some values in rating_numerator column more than "15" were fixed
timestamp were "data time" not "str"
retweeted_status_id were removed because we interest in tweet
retweeted_status_timestamp should be removed because we interest in tweet
image_predictions
Drop all records for non dogs from image_predictions_clean dataframe as we only interested in dogs rating
Removed unnecessary columns
Rename columns of image_predictions_clean data frame to be more descriptive
Json_data
Fixed name for "id" column in json_data_clean to "tweet_id" to be consistent with other two data frames while merging


# WeRateDogs Twitter Archive: Data Wrangling & Analysis (Python)

An end-to-end data wrangling project: gathering data from three different sources, assessing quality and tidiness issues, cleaning, merging, and analysing tweets from the @dog_rates account.

## Data Sources
| Source | Format | Method |
|---|---|---|
| WeRateDogs Twitter archive (2,356 tweets, Nov 2015 to Aug 2017) | CSV | Provided file |
| Image predictions (2,075 records) | TSV | Downloaded programmatically with `requests` |
| Retweet and favourite counts (2,108 tweets retrieved) | JSON | Twitter API via `tweepy` |

## Data Quality Issues Fixed
- **Wrong ratings:** corrected numerators that were mis-extracted from decimals (for example 75 should be 9.75, 27 should be 11.27) and fixed an incorrect denominator.
- **Invalid denominators:** removed ratings that were not out of 10 (mostly group-of-dogs tweets).
- **Retweets:** removed retweets so only original tweets remain.
- **Non-dog images:** removed records where the image classifier did not detect a dog.
- **Untidy structure:** merged four dog-stage columns (doggo, floofer, pupper, puppo) into one `stage` column.
- **Data types and names:** converted timestamps to datetime; renamed columns for consistency before merging.
- **Unneeded columns:** dropped columns not used in analysis.

## Result
A clean master dataset (`twitter_archive_master.csv`): 1,316 tweets, 10 columns, 109 breeds, no duplicate tweet IDs.

## Key Findings
- Golden Retriever is the most common breed (128 tweets), followed by Pembroke (80) and Labrador Retriever (79).
- Ratings are tightly clustered: 1,271 of 1,316 tweets are rated between 8 and 14 out of 10 (median 11).
- Pupper is the most common dog stage (121 tweets).

## Tools
Python, pandas, NumPy, matplotlib, requests, tweepy, Jupyter

## Files
- `wrangle_act.ipynb`: gathering, assessing, cleaning, and analysis
- `wrangle_report.ipynb`: summary of wrangling steps
- `act_report.ipynb`: analysis and visualisations
- `twitter_archive_master.csv`: final cleaned dataset

## Note
API credentials are not included. To re-run the data gathering step, add your own Twitter API keys as environment variables.

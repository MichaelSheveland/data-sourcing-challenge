# data-sourcing-challenge
data-sourcing-challenge module 6
reate a new repository for this project called data-sourcing-challenge. Do not add this homework assignment to an existing repository. When creating your new repository, under the "Add .gitignore" option, make sure you select "Python". This will prevent you from accidentally uploading your API keys in your .env file, exposing them to the world.

Clone the new repository to your computer.

Inside your local Git repository, add the starter files retrieve_movie_data.ipynb and example.env from your file downloads.

Rename example.env to .env and add your API keys to the file.

Ensure the .env file is not listed when you perform a git status check on the repo, before performing your git add action.

Push these changes to GitHub or GitLab.

NOTE
The CSV file included in the output folder in your starter files is to help you identify how your final CSV file should be structured. Do not copy this file to your own repo. You will instead upload the CSV file you create as part of the Challenge.

Instructions
This Challenge has three parts, and must be completed in order:

Part 1: Access the New York Times API.

Part 2: Access The Movie Database API.

Part 3: Merge and Clean the Data for Export.

The starter code includes importing the required dependencies and your API keys from your .env file, but you will need to ensure your API keys are added to that file.

Part 1: Access the New York Times API
The base URL is included in the starter code, along with the search string and query dates. Consult the New York Times Article Search API documentationLinks to an external site. to help you build your query_url using these variables.

If you accidentally delete these variables, they are:

# Set the base URL
url = "https://api.nytimes.com/svc/search/v2/articlesearch.json?"

# Filter for movie reviews with "love" in the headline
# section_name should be "Movies"
# type_of_material should be "Review"
filter_query = 'section_name:"Movies" AND type_of_material:"Review" AND headline:"love"'

# Use a sort filter, sort by newest
sort = "newest"

# Select the following fields to return:
# headline, web_url, snippet, source, keywords, pub_date, byline, word_count
field_list = "headline,web_url,snippet,source,keywords,pub_date,byline,word_count"

# Search for reviews published between a begin and end date
begin_date = "20130101"
end_date = "20230531"
Create an empty list called reviews_list to store the reviews you retrieve from the API.

The Article Search API limits results to 10 per page, but we want to try to retrieve 200. To do this, create a for loop to loop through 20 pages (starting from page 0). Inside the loop, perform the following actions:

Extend the query_url created in Step 1 to include the page parameter.

Make a GET request to retrieve the page of results, and store the JSON data in a variable called reviews.

Add a 12-second interval between queries to stay within API query limits.

Important: The New York Times limits requests to 500 per day and 5 per minute.

Write a try-except clause that performs the following actions:

try: loop through the reviews["response"]["docs"] and append each review to the list, then print out the query page number (i.e. the number of times the loop has executed).

except: Print the page number that had no results then break from the loop.

Note: If your loop breaks at the except clause, it is possible you have tried to make a request that fell outside of the rate limit. You should be able to loop through all 20 pages with the provided query parameters.

Preview the first five results in JSON format using json.dumps with the argument indent=4 to format the data.

Convert reviews_list to a Pandas DataFrame using json_normalize()

Extract the movie title from the "headline.main" column and save it to a new column "title". To do this, you will use the Pandas apply() method and the following lambda function:
# The Project
The goal of this project is to create 3 lineplots of Wikipedia viewcounts based on the following:
1. *Maximum Average and Minimum Average* - The first graph should contain time series for the articles that have the highest average page requests and the lowest average page requests for desktop access and mobile access. Your graph should have four lines (max desktop, min desktop, max mobile, min mobile).
2. *Top 10 Peak Page Views* - The second graph should contain time series for the top 10 article pages by largest (peak) page views over the entire time by access type. You first find the month for each article that contains the highest (peak) page views, and then order the articles by these peak values. Your graph should contain the top 10 for desktop and top 10 for mobile access (20 lines).
3. *Fewest Months of Data* - The third graph should show pages that have the fewest months of available data. These will all be relatively short time series, some may only have one month of data. Your graph should show the 10 articles with the fewest months of data for desktop access and the 10 articles with the fewest months of data for mobile access.

# License and Sources
[License for source data](https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions)  
[Pageview API](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews)  
[REST API](https://wikimedia.org/api/rest_v1/#!/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)  
[API example](https://drive.google.com/file/d/1gtFZAjRoOShsqZKuNhiiSn9Ko4ky-CSC/view)  
[Dinosaur article list](https://docs.google.com/spreadsheets/d/1zfBNKsuWOFVFTOGK8qnTr2DmHkYK4mAACBKk1sHLt_k/edit?usp=sharing)  

# Data Files
## Raw Data
### dinosaur_article_titles.csv
This is the file with all the Wikipedia article titles used in this analysis.
  
| Column | Description |
| ------ | ------------- |
| name   | name of the article  |
| url    | url to Wikipedia article (not used in this repo)  |

### dino_monthly_\<access type\>_201501-202209.json
This is the raw data output by the API.

Key: article name  
Value: list of dictionaries with monthly data

## Processed Data
### average_viewcount.csv
This is timeseries data processed to answer the first question in the project goal.  
The average viewcount was calculated for each article and access type. The lowest and highest of these for each access type was then converted into usable timeseries data.

| Column  | Description |
| ------- | ------------- |
| month   | the month and year of the data  |
| views   | the number of pageviews in that month  |
| article | the name of the article, the access type, and whether it's the min or max  |

### peak_viewcount.csv
This is timeseries data processed to answer the second question in the project goal.  
The highest viewcount for a single month was identified for each article and access type. The 10 highest of these for each access type was then converted into usable timeseries data.

| Column  | Description |
| ------- | ------------- |
| month   | the month and year of the data  |
| views   | the number of pageviews in that month  |
| article | the name of the article |
| access_type | the access type  |

### average_viewcount.csv
This is timeseries data processed to answer the third question in the project goal.  
The number of months of available data was calculated for each article and access type. The 10 lowest of these for each access type was then converted into usable timeseries data.
  
| Column  | Description |
| ------- | ------------- |
| month   | the month and year of the data  |
| views   | the number of pageviews in that month  |
| article | the name of the article |
| access_type | the access type  |

# Scripts
All scripts are in the src folder. The data needed for each script is already included in the repo. If you want to fully reproduce my results, run the scripts in the following order:
1. retrieve_data.ipynb
2. process_data.ipynb
3. create_visualizations.ipynb

# Aditional Information
The API takes 4 access types: all-access, desktop, mobile-app, mobile-web  
This analysis defines different access types:
- desktop: desktop
- mobile: mobile-app + mobile-web
- cumulative: all-access OR desktop + mobile

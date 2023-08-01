# Examining my Streaming Royalties: Project Overview
### Introduction
How much does a musical artist get paid per stream? That may seem like a simple question but you'll soon see that it is not. The answer depends on when the stream occurred, what type of subscription the person has, where they're located, and what streaming service they use. That last bit of information will be the primary focus of this project. I use real (somewhat anonymized) data from my own former band's royalty statements which includes data for over 800,000 streams from that past few years to better understand just how much money streaming services pay and how much this varies by streaming service.

This project showcases:
- **Non-parametric hypothesis tests:** Using a Kruskal-Wallis test with post-hoc analysis, I demonstrate how to test the significance in the medians of groups with non-normal distributions.
- **Effect size reporting:** Sometimes a p-value is not enough. I include effect sizes when discussing differences between groups to better contexualize the significance of the findings.
- **Group visualization:** I show how to effectively visualize data from different groups in order to facilitate comparisons including box plots, violin plots, pie charts, and time-series plots.

### Code and Resources Used
**Python Version**: 3.11.4 **Packages**: pandas, NumPy, Matplotlib, Seaborn, SciPy, cliffs\_delta, scikit\_posthocs

### Website blog post

https://www.nolaneley.com/streaming_royalties

### Data sources and cleaning
- Data was downloaded from the distribution service used by my former band as a tab delimited text file
- The data was anonymized to remove identifying information about the band, album names, and track names
- All album sales were removed so the data only contains information about streaming
- Some streaming services differentiated between subscription type (i.e. free versus premium), however, not all services did, so all data was aggregated together in each service regardless of subscription type.

### Median per-stream payments ($)
The top four services per-stream payments were compared:
- Apple Music: 0.00529
- Spotify: 0.00203
- Youtube: 0.00196
- Google: 0.00521

![boxplots](/images_and_tables/box_plots.png)

### Significance test
A Kruskal-Wallis test with post hoc pairwise comparison Dunn's test using Holm-Bonferroni correction was done to test the significance between per-stream payments between the top four services.

| | Apple Music | Google Play | Spotify | Youtube |
|----------|----|----|----|----|
| Apple Music |  1.0 |  0.00024 |  0.0 |  0.0 |
| Google Play |  0.00024 |  1.0 |  0.0 |  0.0 |
| Spotify |  0.0 |  0.0 |  1.0 |  1 |
| Youtube |  0.0 |  0.0 |  0.0 |  1.0 |

### Effect size
Because the sample size was so huge for each of the streaming services (tens or hundreds of thousands) I used Cliff's delta to get an idea of the effect size of each of these differences.

| | Apple Music | Google Play | Spotify | Youtube |
|----------|----|----|----|----|
| Apple Music |  0.00 |  0.71 |  0.43 |  0.05 |
| Google Play |  -0.71 |  0.00 |  -0.04 |  -0.67 |
| Spotify |  -0.43 |  0.04 |  0.00 |  -0.39 |
| Youtube |  -0.05 |  0.67 |  0.39 |  0.00 |

These values range from -1 to +1. There are typical ways to describe the effect size based on these values as follows: 

| | Apple Music | Google Play | Spotify | Youtube |
|----------|----|----|----|----|
| Apple Music |  negligible |  large |  medium |  negligible |
| Google Play |  large |  negligible |  negligible |  large |
| Spotify |  medium |  negligible |  negligible |  medium |
| Youtube |  negligible | large | medium |  negligible |

### Time series plots
In addition to plots to help visualize the payment of different streaming services above (pie chart, box plot, violin plot, histogram), I also included a time-series chart of per-stream royalty payments (aggregated per month) for each service which shows how they vary over time.

![timeseries](/images_and_tables/stream_time_series.png)
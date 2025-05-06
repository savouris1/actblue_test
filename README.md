# ActBlue Data Analyst Technical Test
All work in this repository is my own. I welcome feedback and thoughts! 

In this file, you will find the link to my Exercise 2 dashboard as well as my thoughts and process explanations while creating it. 

My thoughts on the SQL refactor are commented into the file which is also available in this repository.

## Storytelling Exercise
[Link](https://lookerstudio.google.com/reporting/ac3466ca-6c5a-4395-a13e-d5399bb97c60 "Exercise 2 Dashboard") to my Looker Data Studio report

### Data Hygiene/Integrity Checks
First check I would do on the return files is was it properly narrowed by my where statements, etc. For the FEC_Committee_Data, is the data all from bg_cycle = 2020? For the FEC_Filing_Sample file, so the form_type and filer_committee match the specific selections we made in the query? Are the date ranges specified in the FEC_Filing file within our query constraints? Once I know at base level there isn't extra data that slipped through the cracks, I am taking a closer look at the data itself to see if there is anything strange right off the bat.

The first thing I noticed in both files is that some ZIP code rows have values that exceed the typical 5 digit codes used in the US. However, it is possible that that those entries are the ZIP+4 and still valid, though it makes me wonder about why it isn't one or the other upon data entry. Another thing with ZIP codes is that some ZIP codes on the East Coast have leading zeros that have been likely dropped. But unless the analysis we are doing is mapping by ZIP code, it might not be an issue while analyzing. But if the data pull is for contact or mapping purposes, that would be something to check. 

The second thing I am doing is a basic highlight duplicates exercise on columns I am assuming are unique. I use a simple conditional formatting rule, =COUNTIF (A:A, A1)>1, and the filter by color value on the column. If there are duplicates, they will be highlighted and be the only ones to return when filtering by color. It is an easy visual check on data when there are unique fields to search on.
   
* FEC_Filing_Sample: transaction_id
* FEC_Committee_Data: cmte_id

### Analysis Graph 1
In this graph, we can see the correlation over time between the number of donors using the ActBlue, the amount total raised across all donors, and the money that was a contribution to ActBlue specifically. I was curious if number of donors or the size of the aggregate donations were more indicative of the amount ActBlue might expect to receive. Does a larger sample size (# of donors) mean a higher chance of donation? Or is the amount being donated more important, potentially showing a greater commitment to funding progressive causes? I considered aggregating the data by week, for an easier to read x-axis, but I felt it lost a lot of the nuance available in the daily breakdown. If I was displaying a year's worth of data instead of a quarter, I would aggregate to the week level for display, since the x-axis would be too difficult to read.

I created the ActBlue contributions lines by creating a calculated field wherein only the contributions amounts in rows marked 'Contribution to ActBlue' were summed. I have both y-axis set up in log scale so that the ActBlue contributions trend line would be visible.

What I found was that the ActBlue contributions line followed the total amount donated line fairly faithfully, which make sense. However, it was more responsive to the number of donors line than I expected. There are a number of points where the ActBlue donation line is not in step with the trend of the overall donation at all. An example of this is Feb. 19-21. On Feb. 19, we are seeing a peak right before a downturn for number of donors, but both the ActBlue contributions and overall donations are going up on Feb. 20 while number of donors goes down. However on Feb. 21, the number of overall donations is going up while the contributions to ActBlue start to follow the donor number trend, with a visible drop off. This contrasts with the correlation seen for Feb. 7-12, where all three lines are following the same pattern.

Questions that stood out to me here: How does this trend manifest over a larger period of time? Are these variations only visible due to the smaller window of time being displayed? I tested this by aggregating by week, and while siginificant detail was lost in line variation, I was still able to see instances where the amount donated and ActBlue contributions were out of step. But that isn't the same as an expansion of the date range. As it is fairly certain that contributions to ActBlue are responsive to both the number of donors and the amount donated, is there logic to which criteria is more important at differing times? How much of that variance in value depends on recognizable outside events like news headlines, candidate announcements, etc? 


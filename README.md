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

### Analysis

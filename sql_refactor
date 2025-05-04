with most_recent_filing_id as (
select filer_committee_id_number
,coverage_from_date
,coverage_through_date 
,max(fec_report_id) as report_id 
from f3x_fecfile 
where filer_committee_id_number='C00401224'
and coverage_from_date between '2020-01-01' and '2020-03-31'
group by 1,2,3)
select sa.fec_report_id
,sa.date_report_received
,sa.form_type
,sa.filer_committee_id_number
,sa.transaction_id
,sa.entity_type
,sa.contributor_last_name
,sa.contributor_first_name 
,sa.contributor_street_1
,sa.contributor_city
,sa.contributor_state
,sa.contributor_zip_code
,sa.contribution_date
,sa.contribution_amount::text
,sa.contribution_aggregate::text 
,sa.contribution_purpose_descrip
,sa.contributor_employer
,sa.contributor_occupation
,sa.memo_text_description
from sa_fecfile sa
join lr on sa.fec_report_id=lr.report_id
where upper(sa.form_type)='SA11AI'
order by random()
limit 1600000
), FEC_Committee_Data_2020 as (
select * from fec_committees where bg_cycle=2020
)
SELECT cmte_nm
    ,sum(case when instate=TRUE then total end) as instate
    ,sum(case when instate=FALSE then total end) as outofstate
    ,sum(case when instate=TRUE then total end)::numeric / sum(total)::numeric as instate_pct
    
from (
SELECT c.cmte_nm
    ,c.cmte_st
    ,b.contributor_state
    ,c.cmte_st = b.contributor_state as instate
    ,b.total
    
from (SELECT a.filer_committee_id_number
    ,a.contributor_state
    ,sum(a.contribution_aggregate) total
from DS_technical_112221 a
group by 1,2) b
    ,FEC_Committee_Data_2020 as c
)
group by 1
having cmte_nm = 'ACTBLUE';

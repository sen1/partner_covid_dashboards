# Partner Covid19 Dashboards - Examples

Contributors to this Project:
**Peter Fisher/Joseph Lei/Karteek Kotamsetty/Ranadheer Mettu/Mike Snodgrass/Lukman Ramsey/Christopher Haas/Chris Hein/Aaron Pestel**

Looker - Drives better outcomes through smarter data-driven experiences. Which means putting data where you work. So drilling down into detail without leaving a dashboard and drilling out to other systems are great examples how Looker provides a better data-driven experience for the users.

The four Looker main pillars:

Modern BI & analytics
Serve up real-time dashboards for more in-depth, consistent analysis. Access to trustworthy data enables teams to collect fresh results for more precise reporting.

Integrated insights
Enhance the tools you’re already using by infusing new, relevant data. Unify and empower your teams to make more effective, data-informed decisions.

Data-driven workflows
Invigorate your workflows with fresh, reliable data. Looker gives teams unified access to the answers they need to drive successful outcomes.

Custom applications
Create custom apps that deliver data experiences as unique as your business. Looker's ability to embedded analytics, delivers data where they need it and helps them to get the job done.

![Looker 4 Main Pillars](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/lookerfourpillars.png)



This is set of Demo Dashboards and a LookML model that leverage BigQuery Public Covid19 Datasets.
These can be used for demo purposes, and they can be used as examples of "how to code" to build highly effective Looker dashboards.

The main BigQuery Dataset we use is "bigquery-public-data:covid19_public_forecasts" which is where Google publishes its 14 and 28 Day forecast of covid19 cases along with other information.

We designed three Looker dashboards based on public forecast data: 
![Partner COVID-19 Public Forecasts - State](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/covid_forecast_state.png)

[Partner COVID-19 Public Forecasts - State (PDF)](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/Partner%20COVID-19%20Public%20Forecasts%20-%20State%202020-11-25T0807.pdf)
<br/>
 
![Partner COVID 19 Public Forecast by County](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/covid_forecast_county1.png)
<br/>
[Partner COVID 19 Public Forecast by County (PDF)](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/Partner%20COVID%2019%20Public%20Forecast%20by%20County%202020-11-25T0809.pdf)

![Partner COVID 19 Public Forecast Vaccine Capacity](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/covid_vaccine_cap1.png)
<br/>

[Partner COVID 19 Public Forecast Vaccine Capacity (PDF)](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/Partner%20COVID%2019%20Public%20Forecast%20Vaccine%20Capacity%202020-11-25T1011.pdf)

The Partner COVID-19 Public Forecasts - State is typically where we start. We provided several high level metrics that compute the prior day metrics.
Confirmed Cases, and Deaths are using custom fields to calculate the prior day total, and display the delta beneath the current day value.

We also included two graphs that display the Google 28 day COVID Forecast for New Cases, and Deaths. These two charts, displaying the actual cases, and then 3 forecast lines, which represent the ML predicted forecast in RED, and the Upper (in Green) and Lower (in Yellow) Bounds of that forecast.

These dashboards leverage best practice in dashboard design, where there are high level metrics at the top, with the delta or % change from yesterday included underneath. This is a great technique and demo concept, and to create these high level metrics we used  custom fields to calculate prior day balances, and then calculate the delta. So those are excellent examples to copy and are easy to see how they created.

Screenshots:
![High Level Metrics Prior Day Delta](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/highlevel_metric_vs_priorday.png)
<br/>
<br/>
![Report Example](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/highlevelreportmetric.jpg)
<br/>
<br/>
![Creating Custom Fields Prior Day](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/customfields.png)
<br/>

The covid dashboards are typically displaying actual cases along with forecast or predictive data, with an upper and lower bound. In order to display these types of graphs, we use two options to hide null values, and to display a certain number of rows. 

![Forecast Graph with Upper and Lower Bounds](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/forecast_graph1.png)


Next, we right-mouse click on a particular state on US Map Graph and you see in the popup window that you can drill down into County, (which gives you a preview of the County Cases without having to leave the dashboard), and it has drill out options as well.  Under Links, you can select the State Specific Dashboard which will take you to another dashboard that has State and County level information. You can also drill out to external systems or to external sources like Google News.

![Screenshot: State Drill Out](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/Drillintoandout.png)

The drill down to County information without leaving the dashboard is a great feature for users, where you can not only preview the data, but you can also explore if you need to drill into all the data behind that chart.

![Screenshot: State Drill Down County](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/covid_drill_in_county.png)

And the two drill out use cases are examples of passing state as a parameter to another dashboard, and to an external website, which are common use cases.

<br/>

You can find how we did this in the County_14d view, where you can see the lookML model that we used for the specific dimension: state_name

![State Dimension](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/state_dimension.png)

dimension: state_name {
type: string
map_layer_name: us_states
drill_fields: [county_name]
sql: ${TABLE}.state_name ;;
link: {
  label: "{{value}} State Dashboard"
  url: "/dashboards-next/864?State+Name={{ value }}"
  icon_url: "http://www.looker.com/favicon.ico"
}
link: {
  label: "{{value}} State Covid News"
  url: "https://news.google.com/search?q={{ value }}+covid&hl=en-US&gl=US&ceid=US:en"
  icon_url: "https://www.google.com/s2/favicons?domain_url=http://www.news.google.com"
}
}

**Please Note - You would need to update the dashboard number that you want to link to. In this example /dashboards-next/864?State+Name={{ value }} would need to be updated to the dashboard you want to link to /dashboards-next/yourdashboardnumber?State+Name={{ value }}**




[More Information and Examples - Linking in Looker](https://docs.looker.com/reference/field-params/link)
<br/>
[More Information and Examples - Custom-Drilling-Using-HTML-and-Link](https://help.looker.com/hc/en-us/articles/360001288228-Custom-Drilling-Using-HTML-and-Link)

<br/>

The Covid State/County dashboard is leveraging a new looker feature called Cross - Filtering.
Cross-filtering makes it easier and more intuitive for viewers of dashboards to interact with a dashboard’s data and understand how one metric affects another. With cross-filtering, users can click a data point in one dashboard tile to have all dashboard tiles automatically filter on that value.

[Learn More on Cross Filtering](https://docs.looker.com/dashboards/cross-filtering)
<br/>
<br/>
![Cross Filtering](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/crossfiltering3.png)
<br/>
<br/>
![Cross Filtering Before](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/crossfiltering1.png)
<br/>
<br/>
![Cross Filtering After](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/crossfiltering2.png)
<br/>
<br/>
<br/>
<br/>
And here are two more great examples of Looker Dashboards and Designs:
<br/>
<br/>
[Covid Regional Level](https://covid19response.cloud.looker.com/embed/dashboards-next/38?State=&Region+%28US-Only%29=West)


![Covid Regional Level](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/covid_public_region.png)

<br/>
<br/>


[Covid State Level](https://covid19response.cloud.looker.com/embed/dashboards-next/39?State=California&County=)
<br/>

![Covid State Level](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/covid_public_state.png)
<br/>
<br/>
<br/>

## Installing the LookML

Create a Looker connection covid_vaccine_distro to your BigQuery DataSet
![Covid vaccine_distro_connection](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/lookerconnection.png)

<br/>
<br/>
<br/>

I included the 3 dashboards that are located in the dashboard folder. (you should see - include: "/dashboard/**/*.dashboard") in the gps_vaccine_distro.model

![Covid vaccine_distro](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/covid_vaccine_distro_connection.png)

<br/>
<br/>

When you clone or import the model into your own looker instance, you should be able to view the dashboard, and then save to your folder or storyboard.
To view the dashboard, naviagate to the dashboard and click on the diamond, where you'll see that you can view dashboard.

![viewdashboards](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/view_dashboard_2.png)



## Machine Learning and Forecasting with BigQuery and Looker

In order to better manage and anitipatiate vaccine demand and new cases, we are using ML models to help predict the future. In this example, we are leveraging the Google Forecast ML model which updates the COVID19 Public DataSets, like "bigquery-public-data.covid19_public_forecasts.county_14d". However, the ML model is not exposed and it not public.
[Google Cloud, Harvard Global Public Health release improved COVID-19 Public Forecasts, share lessons learned](https://cloud.google.com/blog/products/ai-machine-learning/google-and-harvard-improve-covid-19-forecasts)

Harvard Global Health Institute and Google Cloud have been working the past three months to improve the COVID-19 Public Forecasts, to give first responders and healthcare organizations the best possible information to prepare for what lies ahead.

These forecasts use AI to provide a projection of COVID-19 cases, deaths, and other metrics for U.S. counties and states. Since their original release, the COVID-19 Public Forecasts are now used by many organizations across the United States, and have been significantly improved in five major ways:

1. Longer forecasts & confidence intervals. When initially launched, the COVID-19 Public Forecasts included predictions for 14 days in the future. They now include predictions for a 28-day horizon.
2. Improved model quality. The accuracy of the model has continuously improved over time and is retrained daily as more data becomes available. Since the forecasts were first published, we’ve seen the predictions improve by approximately 50%.
3. Ability to expand to other countries. We have added support for expanding the COVID-19 Public Forecasts to other countries
4. Customized forecasts. Since the launch in August, we have worked with many organizations to better understand how these forecasts can help. In the process we have learned that many organizations have specific needs that go beyond just consuming our public forecast, such as wanting to use their own datasets as inputs. To that end, we have turned the initial forecasting model into a system that is customizable to new problems and datasets. We are working with public sector and healthcare leaders to help them create custom forecasts for their states and hospitals.
5. What-if analysis for informing policy decisions. We have also seen significant interest in using the forecasting model to ask “what-if” questions to help make better-informed policy decisions.

<br/>
<br/>

![WhatIf](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/whatif_ca_vaccine_effective.png)

*In order to help Partners learn how to leverage BigQuery ML Models and consume them in Looker, we can leverage a public COVID Forecast ML Model*

[Analyzing COVID-19 with BigQuery](https://medium.com/google-cloud/analyzing-covid-19-with-bigquery-13701a3a785)
WRITTEN BY Lak Lakshmanan Data Analytics & AI @ Google Cloud

[Why amateur COVID-19 predictions are worthless — featuring ARIMA](https://medium.com/@hoffa/covid-19-arima-predictions-are-worthless-f34e52139769)
WRITTEN BY Felipe Hoffa - Developer Advocate @Google

[SQL for fhoffa.x.int](https://github.com/fhoffa/code_snippets/blob/master/arima_covid/usa.6.days.sql)


**Please Note:This is an extrapolation of historical trends, and does not take into account all the other factors that affect the number of confirmed COVID cases. It’s not meant to predict actual outcomes. Instead, it’s meant to extrapolate what will happen if things stay the same, which is not likely. So this is a good use of ML, but also highlights some of it's limitations. As we will see when look at the confidence bounds and error rate when comparing forecast cases against actual cases.**

In BigQuery - I used this model that has two steps.
<br/>
<br/>
**Step 1 is to create the model**
<br/>
**Step 2 is to store the comparison of what was forecasted with actual cases, to better understand how accurate the model is.**

CREATE OR REPLACE MODEL Insertyourdatasetnamehere.numreports_forecast
OPTIONS(model_type='ARIMA',
       time_series_data_col='num_reports',
       time_series_timestamp_col='date') AS
SELECT
   date, LOG(SUM(confirmed)) num_reports
FROM `bigquery-public-data.covid19_jhu_csse.summary`
WHERE country_region = 'US'
AND date <= DATE_SUB(CURRENT_DATE(), INTERVAL 14 DAY)
GROUP BY date
ORDER BY date ASC
;


SELECT date, forecast
  , TO_JSON_STRING([fhoffa.x.int(confidence_interval_lower_bound), fhoffa.x.int(confidence_interval_upper_bound)]) bounds
  , confirmed actual_confirmed, ROUND((confirmed-forecast)/confirmed * 100,1) error
FROM (
  SELECT DATE(forecast_timestamp) date, fhoffa.x.int(EXP(forecast_value)) AS forecast
      , EXP(confidence_interval_lower_bound) confidence_interval_lower_bound
      , EXP(confidence_interval_upper_bound) confidence_interval_upper_bound
  FROM ML.FORECAST(MODEL Insertyourdatasetnamehere.numreports_forecast,
  STRUCT(14 AS horizon, 0.9 AS confidence_level))
) JOIN (
  SELECT date, SUM(confirmed) confirmed
  FROM `bigquery-public-data.covid19_jhu_csse.summary`
  WHERE country_region = 'US'
  GROUP BY 1
)
USING(date)
ORDER BY date


Here is a screenshot of how deployed the forecast model and ran the accuracy query in my BigQuery Project:

![BigQueryForecastModel](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/CreateForecastModel.png)


<br/>
<br/>
<br/>

Here is how I viewed the accuracy of the forecast model. 

I created a view from the following query:

**SELECT date, forecast
  , TO_JSON_STRING([fhoffa.x.int(confidence_interval_lower_bound), fhoffa.x.int(confidence_interval_upper_bound)]) bounds
  , confirmed actual_confirmed, ROUND((confirmed-forecast)/confirmed * 100,1) error
FROM (
  SELECT DATE(forecast_timestamp) date, fhoffa.x.int(EXP(forecast_value)) AS forecast
      , EXP(confidence_interval_lower_bound) confidence_interval_lower_bound
      , EXP(confidence_interval_upper_bound) confidence_interval_upper_bound
  FROM ML.FORECAST(MODEL vaccine_distro.numreports_forecast,
  STRUCT(14 AS horizon, 0.9 AS confidence_level))
) JOIN (
  SELECT date, SUM(confirmed) confirmed
  FROM `bigquery-public-data.covid19_jhu_csse.summary`
  WHERE country_region = 'US'
  GROUP BY 1
)
USING(date)
ORDER BY date
**

![BigQuerySaveView](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/Save_View1.png)

<br/>
<br/>
<br/>


**Please Note - You would need replace "Insertyourdatasetnamehere".numreports_forecast with your BigQuery DataSet at both places: CREATE OR REPLACE MODEL Insertyourdatasetnamehere.numreports_forecast, and FROM ML.FORECAST(MODEL Insertyourdatasetnamehere.numreports_forecast**


**How to publish a daily forecast:**
To get a daily forecast, we can create a script out of the two queries. This is as simple as writing the two SQL statements one after the other, making sure to end the first one with a semicolon. Then, click on “Schedule query” to run this every day:

![BigQuery Schedule](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/schedule_model.png)


<br/>
<br/>
<br/>

![BigQuery My_COVID_Schedule](https://github.com/peterfishergcp/partner_covid_dashboards/blob/main/images/scheduledmycovid.png)



I don’t speak for my employer. This is not official Google work, and this is not an official product of Google.
Thanks to Felipe Hoffa and  Lak Lakshmanan for many insightful comments.
Any errors you find, are mine. 


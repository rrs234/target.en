---
description: The conversion rate, lift, confidence (statistical significance) and confidence interval are reported for each experience.
keywords: Targeting
seo-description: The conversion rate, lift, confidence (statistical significance) and confidence interval are reported for each experience.
seo-title: Conversion rate
solution: Target
title: Conversion rate
topic: Advanced,Standard,Classic
uuid: c42d7683-2eec-4443-9545-5695a122c9de
---

# Conversion rate{#conversion-rate}

The conversion rate, lift, confidence (statistical significance) and confidence interval are reported for each experience.

The following illustration shows the chart header for a sample activity with the [!UICONTROL Conversion Rate], [!UICONTROL Lift], and [!UICONTROL Confidence] headers highlighted.

![](assets/conversion-rate.jpg)

>[!NOTE] {class="- topic/note "}
>
>In all data, duplicate orders are ignored if an `orderID` is passed. The audit report lists the ignored duplicate orders.

## Conversion Rate {#section_07A36846C4E84D0881906809B9CE5A74}

Shows the median conversion rate, confidence, interval, and the number of conversions.

For example, examine the following Conversion Rate report column:

![](assets/conversion-rate-detail.jpg)

The first line is the control experience. It shows a 15% conversion rate, with three conversions. The second line, Experience B, shows a 15% conversion rate, with a confidence interval of plus or minus 15.65% and three conversions.

>[!NOTE]
>
>Currently, the confidence interval is calculated only for binary metrics.

## Lift {#section_0F409572C720433D9378092ABC999982}

Compares the conversion rate for each experience against the control experience.

Lift = (Experience CR - Control CR) / Control CR

If control is 0, there is no percentage lift.

## Confidence (Statistical Significance) {#section_35DB6724813D40C7B0808DE18FE595C1}

This number represents the likelihood that the results would be duplicated if the test were run again. The confidence rounds up to 100.00% when the confidence is greater than or equal to 99.995%.

See [Confidence Level and Confidence Interval](../c-reports/conversion-rate.md#concept_0D0002A1EBDF420E9C50E2A46F36629B).

## Retail Data {#section_30A674731BA6440E9BB93C421BE990EE}

AOV, RPV, and Sales data are displayed for each experience if you inserted a [Place Order](https://marketing.adobe.com/resources/help/en_US/target/ov/t_orderconfirm_create.html) ( `orderConfirmPage`) mbox and selected it as the conversion mbox. 

## Confidence Level and Confidence Interval {#concept_0D0002A1EBDF420E9C50E2A46F36629B}

For each experience, confidence level and confidence interval are displayed.

Conversions and continuous variables for Target-based metrics, such as revenue and engagement metrics, are calculated as follows:

* **Conversion:** Either yes or no 
* **All others:** Values across a range

You can perform offline calculations for Analytics for Target (A4T), but it requires a step with data exports in [!DNL Analytics]. For more information, see "Performing Offline Calculations for Analytics for Target (A4T)" below.

### Confidence Level {#section_26FE5E44BDD5478792A65FCFD83DCCDC}

The *confidence level* is represented by the darker percentage in the Conversion Rate column for each experience.

![](assets/conf_report.png)  ![](assets/conf_report_detail.png)

The confidence level, or statistical significance, indicates how likely it is that an experience's success was not due to chance. A higher confidence level indicates:

* The experience is performing significantly different from control. 
* The experience performance is not just due to noise. 
* If you ran this test again, it is likely that you would see same results.

If the confidence level is over 90% or 95%, then the result can be considered statistically significant. Before making any business decisions, try to wait until your sample size is large enough and that the four bars of confidence on one or more experiences stays consistent for a continuous length of time to ensure the results are stable.

>[!NOTE]
>
>The confidence rounds up to 100.00% when the confidence is greater than or equal to 99.995%.

### Confidence Interval {#section_F582738DFE1648C78B93D81EBC6CACF7}

>[!NOTE]
>
>Currently, the confidence interval is calculated only for binary metrics.

The *confidence interval* is a range within which the true value can be found at a given confidence level. The confidence interval appears as a light gray +/- percentage in the Conversion Rate column. In the example below, the confidence interval for Experience B's lift is plus or minus 15.65%.

![](assets/conversion_rate.png)

**Example:** An experience's RPV is $10, its confidence level is 95% and its **confidence interval** is $5 to $15. If we ran this test multiple times, 95% of the time the RPV would be between $5 and $15.

**What impacts the confidence interval?** The formula follows standard statistical methods for calculating confidence intervals.

* **Sample size:** As sample grows the interval will shrink or narrow. This is preferred as it means your reports are getting closer to the true value of the success metric. 
* **Standard deviation smaller:** More similar results, such as similar AOVs or similar numbers or visitors converting each day, reduces the standard deviation.

## Confidence Calculation and How to Perform It Offline {#section_86F7C231943043A5B8B6BFE67B706E3B}

The [downloaded CSV report](../c-reports/downloading-data-in-csv-file.md#concept_3F276FF2BBB2499388F97451D6DE2E75) includes only raw data and does not include calculated metrics, such as revenue per visitor, lift, or confidence used for A/B tests.

To calculate these calculated metrics, download the Target's [Complete Confidence Calculator](/help/assets/complete_confidence_calculator.xlsx) Excel file to input the activity's value, or review the [statistical calculations used by Target](/help/assets/statistical-calculations.pdf).

>[!NOTE]
>
>This calculator is for Target-based reporting and not for A4T reporting.

## Performing Offline Calculations for Analytics for Target (A4T) {#section_B34BD016C8274C97AC9564F426B9607E}

You can perform offline calculations for A4T, but it requires a step with data exports in [!DNL Analytics].

For A4T, we use a Student's t-test calculation for continuous variables (rather than binary metrics). In Analytics, a visitor is always tracked, and every action taken is counted. Therefore, if the visitor purchases multiple times or visit a success metric multiple times, those additional hits are counted. This makes the metric a continuous variable. To perform the Student's t-test calculation, the "sum of squares" is required. This can be retrieved from [!DNL Analytics]. To get the sum of squares data, you need to perform a visitor-level export for the metric you are optimizing to, for a sample time period.

For example, if you’re optimizing to page views per visitor, you’d export a sample of the total number of page views on a per visitor basis for a specified time frame, perhaps a couple of days (a few thousand data points is all you need). You would then square each value and sum the totals (the order of operations is critical here). This "sum of squares" value is then used in the Complete Confidence Calculator. Use the "revenue" section of that spreadsheet for these values.

**To use the [!DNL Analytics] data export feature to do this:**

1. Log in to [!DNL Adobe Analytics]. 
1. Click **[!UICONTROL Tools]** > **[!UICONTROL Data Warehouse]**. 
1. On the **[!UICONTROL Data Warehouse Request]** tab, fill in the fields.

   For more information about each field, see "Data Warehouse Descriptions" in [Data Warehouse](https://marketing.adobe.com/resources/help/en_US/reference/data_warehouse.html).

   | Field | Instructions |
   |--- |--- |
   |Request Name|Specify a name for your request.|
   |Reporting Date|Specify a time period and granularity.<br>As best practice, choose no more than an hour or one day of data for your first request.  Data Warehouse files take longer to process the longer the time period requested, so it is always a best practice to request a small time period data first to make sure your file returns the expected result. Then, go to the Request Manager, duplicate your request, and ask for more data the second time. Also, if you toggle granularity to anything other than “None,” the file size will increase drastically.<br>![Data Warehouse](/help/c-reports/assets/datawarehouse.png)|
   |Available Segments|Apply a segment, as needed.|
   |Breakdowns|Select the desired dimensions:  Standard is out-of-the-box (OOTB), while Custom includes eVars & props. It is recommended you use “Visitor ID” if visitor ID level information is needed, rather than “Experience Cloud Visitor ID.”<ul><li>Visitor ID is the final ID used by Analytics. It will either be AID (if the customer is legacy) or MID (if the customer is new or cleared cookies since the MC visitor ID service was launched).</li><li>Experience Cloud Visitor ID will only be set for customers who are new or cleared cookies since the MC visitor ID service was launched.</li></ul>|
   |Metrics|Select your desired metrics. Standard is OOTB, while Custom includes custom events.|
   |Report Preview|Review your settings before scheduling the report.<br>![Data Warehouse 2](/help/c-reports/assets/datawarehouse2.png)|
   |Schedule Delivery|Enter an email address to deliver the file to, name the file, then select [!UICONTROL Send Immediately].<br>Note: The file can be delivered via FTP under [!UICONTROL Advanced Delivery Options]<br>![Schedule Delivery](/help/c-reports/assets/datawarehouse3.png).|

1. Click **[!UICONTROL Request this Report]**.

   File delivery can take up to 72 hours, depending on the amount of data requested. You can check on the progress of your request at any time by clicking [!UICONTROL Tools] > [!UICONTROL Data Warehouse] > [!UICONTROL Request Manager].

   If you would like to re-request data that you’ve requested in the past, you can duplicate an old request from the [!UICONTROL Request Manager] as needed.

For more information about [!DNL Data Warehouse], see the following links in the [!DNL Analytics] Help documentation:

* [Create a Data Warehouse Request](https://marketing.adobe.com/resources/help/en_US/reference/t_dw_create_request.html) 
* [Data Warehouse Best Practices](https://marketing.adobe.com/resources/help/en_US/reference/data_warehouse_bp.html)

## Counting Methodology {#concept_EC19BC897D66411BABAF2FA27BCE89AA}

You can choose to view reports by different counting methodologies to understand how your activities affect your users across their lifetimes or during a single session.

Counting methodology is supported for the following activity types:

* A/B Test

  As an exception, Auto-Target A/B activities support only the default "Visit" counting methodology. 

* Experience Targeting (XT) 
* Multivariate Test (MVT)

  For the MVT Element contribution report, Target does not support Activity Impressions for Revenue Metric types. 

* Recommendations

Only the default counting methodology (Visits) is currently supported for Automated Personalization (AP) activities.

You can view reports by the following counting methodologies:

* **Visitor:** A unique participant in the activity, for the life of the activity.

  A person will be counted as a new entrant if he or she visits the site from a new computer or a new browser; deletes the cookie; or converts and returns to the activity with the same cookie. An entrant is identified by the PCID in the visitor's mbox cookie. If the PCID changes, the person is considered a new visitor. 

* **Visit:** A unique participant in an experience during a single 30-minute browser session.

  If a conversion is achieved or a visitor comes back to the site after being away at least 30 minutes, a returning visitor counts as a new visit. A visit is identified by the `sessionID` in the visitor's mbox cookie. When the `sessionID` changes, the visit is considered new.

* **Impression/Page View:** Counted each time a visitor loads any page of the activity.

  A single visit might include several impressions of, for example, your homepage.

>[!NOTE] {class="- topic/note "}
>
>Usually, counts are determined by cookies and session activity. However, if you reach the final conversion point of an activity and then re-enter the activity, you are considered a new entrant and a new visit to the activity. This is true even if your PCID and `sessionID` values do not change.
# Kickstarter Analysis in Excel

- Author: Aigerim Zhanibekova
- Email: azhanibekova787@gwu.edu
- Date: January 2022
- Instituition: The George Washington University 

## Overview of Project

### Purpose
The purpose of this project is to perform data analysis on several thousand crowdfunding projects to uncover any hidden trends. Specifically, we want to find what are the factors that might explain why some campaigns are successful and some are not. 

### Dataset

The data consists of 4114 different Kickstarter campaigns for 21 countries, launched between 2009 and 2017. The original raw data can be found [here](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/Kickstarter_Analysis_Dataset.xlsx). The analysis and outputs can be found [here](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/Kickstarter_Challenge.xlsx). 


## Analysis and Challenges

### Preparing the Data 
The "Formatted Data" sheet shows the original data with the following adjustments:

1. The first 3 columns and 1st row have been frozen for a better navigation. 

2. Columns I and J dates formatting:
    * These columns represent dates. However, they are not in a readible format. To make sure that the numbers in this column are, indeed, timestamps, [**timestamp converter tool**](https://www.epochconverter.com/) was used. 
    * After confirming that the dates are [**Unix timestamps**](https://websiteseochecker.com/blog/what-is-timestamp/), the following was done:
      
      *  To convert the launch dates (launched_at in Column J), _Date Created Conversion_ column(date_created_conversion in column O) was created with the following formula:         
         >=(((J2/60)/60)/24)+DATE(1970,1,1)
      * A _Years_ column (column U) was created based on the _Date Created Conversion_ column. 
      * To convert the deadline dates (deadline in Column I), _Date Ended Conversion_ column (date_ended_conversion in column P) was created with the following formula:
        >=(((I2/60)/60)/24)+DATE(1970,1,1)

3. The _Outcomes_ column (Column F) has 4 categories - Successful, Failed, Canceled, and Live. These categories were color-coded as follows: 
   * Failed - Red
   * Successful - Green
   * Canceled - Yellow
   * Live - Blue-Gray

 4. The following other columns needed for the analysis were created: 
    
    _Percentage Funded_
      * Column D (goal) shows the amount that each campaign was aimed at. 
      * Column E (pledged) shows how much was donated. 
      * A new column (percentage_funded) was created in Column Q to calculate how much of the campaign goal was achieved. The following formula was applied:
        > =ROUND(100*E2/D2, 0)
      * Then, value shading was applied to this column using "Color Scales" followed by "More Rules"in the Conditional Formatting. 
         * The color "Green, Accent 6, Lighter 80%" is assiged as the minimum color.
         * The color "Green, Accent 6, Darker 25%" is assigned as the maximum one. 

    
    _Average Donation_

      Kickstarter crowdfunding platform provides incentives for different pledge amounts. If you are intersted in setting up any incentives when launching a campaign, it is useful to know how much people have pledged historically. 

      - Column E (pledged) shows how much was donated. 
      - Column L (backers_count) shows the count of backers of the campaign. 
      -  A new column (average_donation) was created in Column R to calculate the average donation per campaign. The following formula was used:  
         > =IFERROR(ROUND(E2/L2, 2), "no backers") 

         *The IFERROR command and a "no backers" notation was used to flag campaigns with zero backers*

    _Campaign Parent Category and Subcategory_

      * Column N (category_and_subcategory) shows the category and subcategory for each campaign. This column was split using "Text to Columns" in the Data tab ("Delimited" separation and "/" as the delimeter). 
      * The new column S (parent_category) shows the parent category for each campaign:

        * Film & Video
        * Food
        * Games
        * Journalism 
        * Music 
        * Photography 
        * Publishing 
        * Technology
        * Theater

     * There are many subcategories subcategories for each category type, illustrated in Column T (subcategory). 

### What Kickstarter campaigns are the most successful?

The "Category Statistics" sheet contains analysis displaying outcomes for each fundraising category, which can be filtered by a country. The chart below shows that, **the theater category was the most successful** with 839 Kickstarter campaigns among all 21 countries.  

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Outcomes_vs_Category.png)

**The origin of the campaign has an impact**. 

The table below shows that out of 4114 campaigns, 3038 were only from the United States. Great Britain, for example, with only 604 Kickstarter campaigns had the second highest number after the US.

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Campaigns_by_Country.png)

The chart below shows that out of 839 the most successful campaigns worldwide in **the theater category**, 525 were from the US. 

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Outcomes_vs_Category_US.png)

The "Subcategory Statistics" sheet contains analysis displaying outcomes for each subcategory, which can be filtered by the parent category and country. After determining that the theater category was the most successfull, we can see exactly what type of theater campaigns brought the most success. 

The chart shows that **plays were the most successfull subcategory of the theater category** with 694 successfull campaigns out of 1393 total. 

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Outcomes_vs_Subcategory_Theater.png)

Again, the numbers are mostly driven by the United States, which had 912 total theater campaigns and 412 plays. 

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Ouctomes_vs_Subcategory_Theater_US.png)

### Analysis of Outcomes Based on Launch Date

We saw that among all Kickstarter campaigns in our data, the theater category had the most successful outcomes. It would be beneficial to find out in which months it is best to launch a theater campaign. 

The sheet "Theater Outcomes by Launch Date" analyzes the outcomes for the theater campaigns by month. 

The data below, more or less, exhibits an overall trend. There is a general increase in the number of successful theater campaigns between March and May, where May has the highest number of successful campaigns. After May, there is a general decrease in successful outcomes, reaching the lowest number in December. The number of canceled campaigns stays roughly stable throughout the year with overall low counts. 

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Theater_Outcomes_vs_Launch.png)

_Please note that the analysis excludes "live" outcome campaigns as there is a very small count of these campaigns appearing only in 3 months of the year._

### Analysis of Outcomes Based on Goals

How much a campaign is asking for might also factor in its outcome. We saw that among theater campaigns, the "plays" subcategory was the most successful. 

The "_Outcomes Based on Goals_Plays" sheet demonstrates analysis of outcomes for plays based on goal amount ranges. 

The analysis illustrates that the highest percentage of successful plays of 76% had the fundraising goals of less than $1000. Overall, with higher goal ranges, there is a general decrease in the successful outcomes and a general increase in the failed outcomes. However, there is an unsual reverse trend observed in the goal ranges between $30,000 to $44,999, where the success rates spiked and failed outcomes slumped. 

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Outcomes_vs_Goals_Plays.png)

_Please note that the analysis excludes "live" outcome campaigns as there is a very small count of these campaigns appearing only in 3 months of the year._


### Challenges and Difficulties Encountered

* The dataset came with non-readible date columns. The conversion is explained above. 
* There are many positive outliers in the data, which need to be reviewed. It is possible that, because of these outliers, the trend linesare slightly distorted. 
* It is assumed that the monetary columns such as goal and pledged amounts are standartized to one currency and adjusted for inflation. However, it is not clear from the dataset. 

## Results

### **Conclusions about the Outcomes based on Launch Date**
  * Theater category is the most successful campaign type. 
  * Based on the preliminary analysis, May is the best month to launch a theater campaign as it showed the highest number of successful outcomes historically. 
  * The number of canceled theater campaigns stays roughly stable throughout the year with overall low counts, with the maximum of 7 campaigns in January and the minimum of 1 in July. 


### **Conclusions about Outcomes based on Fundrasing Goals of Theater Plays**
  * Plays were the most successful subcategory of the theater category campaigns. 
  * Theater plays that had the fundraising goals of less than $1000 resulted in the highest percentage of successful outcomes. 
  * With a higher fundraising goal amount for plays, there is a general decrease in the successful outcomes and a general increase in the failed outcomes. 

Please note that these conclusions are preliminary and do not imply any causal inference. 

### **Limitations of this dataset** 

* There is not enough data for "live" category campaigns, which had to be exlcuded for some parts of the analyses. 
* In general, there is low variability in the data since most of the campaigns are from the United States. So, the analysis would not be fully representative of other countries.

## Additional Analyses
Please find some additional analysis performed on the data [here](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/Additional_Analysis.xlsx). 
### Example inference about individual campaigns

The "Formatted Data" sheet can give an overview of individual campaigns. For instance, there is a play called "Foresight." If we search for it in the formatted data, we can see that this was a successful campaign, which was 100% funded, even exceeding $4. Also, the average donation for this play was $117.88, which is quite high, given that there are only 17 backers. Finally, this campaign was active for just under a month. 

Let's look at the following five plays happened at the Edinburgh Festival Fringe: _Be Prepared, Checkpoint 22, Cutting Off Kate Bush, Jestia and Raedon, and The Hitchhiker's Guide to the Family_. The analysis is located in the "Edinburgh Plays Research" sheet with the data pulled from the "Formatted data" sheet using the VLOOKUP function. 

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Edinburgh%20Plays%20Research.png)

We can see that all of these plays reached their funding goals and were active for over 30 days except for the "Jestia and Raedon" play. 

### Analysis of successfull anf failed plays in the US

The "Successfull US Plays" and "Failed US Plays" sheets are datasets filtered for successfull and failed theater plays launched in the United States. 

The table below shows a descriptive statistics based on these data. 
![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/Success_Failed_Plays_vs_Goal_Pledged_US.png)

* The distributions are similiar in all subsets with the mean around the 75th percentile (or 3rd quartile). 
* ***The distributions are driven by large values**. In each distribution, the mean is larger than the median (skewed to the right). For successful campaigns, the Standard Deviation is approx. 2 times larger than the Interquartile range (IQR). For failed campaigns, the Standard Deviation is almost 3 times greater than the IQR. 
* In each distribution, the standard deviation is larger than the mean. Any observation below the mean can considered "close" to the center. 
* **Failed** plays had **higher fundraising goals**, as per the average and median. At the same time, both the mean and median pledged amounts are significantly lower for the failed plays than than that for the successful ones. If the **median pledged** amounts were more or less the same for both successful and failed campaigns, we could say that the failed ones asked for too much money. However, it is not the case here - there must be other factors in play. 

## Analysis of theater campaigns for musicals in Great Britain

The below chart displays distributions of goal and pledged amounts for "Musicals" subcategory in Great Britain. 

![](https://github.com/Aigerim-Zh/kickstarter-analysis/blob/main/resources/BoxPlot_GB_Musicals.png)

* In this case, the distributions are also driven by large numbers. In particular, there are two large values for both goal and pledge amounts, which make the distribution skewed to the right - $15,000 for the goal amount and $10,092 for the pledged amount. 

* The mean fundraising goal amount for Great Britain musicals is $4,059.62, which is higher than the outliers threshold for pledged amounts. 
* The range of outliers for the amount pledged is any value above $3,697. If you are interested in launching musicals in Great Britain, it would probably not advised to set a fundraising goal above this threshold amount.  
* 50% of campaign fundraising goal amounts are less than $2,000. 
---
The outliers threshold was calculated as follows:
   > Positive Outlier Threshold = Upper Quartile + 1.5 * Interquartile Range = $1,496 + 1.5 * ($1,496 - $28.75) = $3,697, where

   > Interquartile Range = Upper Quartile or 75th percentile - Lower Quartile or 25th percentile.
---

 
















   


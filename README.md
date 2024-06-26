# glenn-s-portfolio
Data Science / Data Analytics Portfolio
1. [Tracking User Engagement with SQL, Excel, and Python](#project-1-tracking-user-engagement-with-sql-excel-and-python)
1. [Customer Segmentation in Marketing with Python](#project-2-customer-segmentation-in-marketing-with-python)
1. [Scraping Rotten Tomatoes](#project-3-scraping-rotten-tomatoes)

# [Project 1: Tracking User Engagement with SQL, Excel, and Python](https://github.com/jglennc/customer-segmentation-in-marketing-with-python)

## Case Description
**Background:** The project requires you to analyze whether the new additions to the platform (new courses, exams, and career tracks) have increased student engagement.

**Hypothesis:** The **first half of 2022** was expected to be profitable for the company. The reason was the hypothesized increased student engagement after the release of several new features on the company’s website at **end-2021**. These include enrolling in **career tracks** and testing your knowledge through **practice, course, and career track exams**. Of course, we have also **expanded our course library** to increase user engagement and the platform’s audience as **more topics are covered**. By comparing different metrics, we can measure the effectiveness of these new features and the overall engagement of our users.

## Project requirements
* Excel 2007 (or later)
* MySQL Workbench 8.0 (or later)
* Python version: Python v.3

* Python libraries:

    * pandas
    * matplotlib
    * statsmodels
    * scikit-learn
    * seaborn (optional)

## Project files
* dataset: data_scientist_project.sql
    ![](/images/ER_diagram.png)

## Outcomes
### By Confidence Intervals
1. For **free-plan students**, there’s an **increase in engagement** from Q2 2021 to Q2 2022, as the confidence interval for the later period (15.41 – 16.66 minutes) is slightly higher than for the earlier one (13.55 – 14.87 minutes).
1. **Students with paid memberships watch substantially more than those without.** This is evident by comparing the confidence intervals of the two groups in Q2 2021: (13.55 – 14.87) minutes for non-subscribers and (339.60 – 380.61) minutes for subscribers.
1. **Among the paid subscribers**, there’s a **decrease in engagement** from Q2 2021 to Q2 2022, as the confidence interval for the later period (276.54 – 307.90 minutes) is lower than for the earlier one (339.60 – 380.61 minutes).
1. Please note that these are **just interpretations based on the confidence intervals**, and **actual cause-effect relationships need further investigation**. For instance, the fact that paid subscribers watch more doesn’t necessarily mean that having a paid subscription causes them to watch more. Those who watch more are more likely to get a paid subscription. Similarly, the decrease in engagement among paid subscribers from Q2 2021 to Q2 2022 could be due to various factors that need to be explored separately.

### By Hypothesis Testing
1. **Null hypothesis:** The engagement (minutes watched) in Q2 2021 is higher than or equal to the one in Q2 2022.

    **Alternative hypothesis:** The engagement (minutes watched) in Q2 2021 is lower than the one in Q2 2022.
1. **For free-plan students**, we would **reject the null hypothesis.**. **The engagement in Q2 2021 is not significantly higher than the engagement in Q2 2022.**
1. **For paying students**, we would **fail to reject the null hypothesis**. **This means there’s not enough evidence to conclude that engagement in Q2 2021 is significantly higher than the engagement in Q2 2022**
1. **The correctness** of these hypothesis testing are **crucial** for **avoiding false company investestment** based on these tests.

    A **type I error** might result in over-investment in in certain features or complacency about needing to improve features.

    A **type II erorr** might result in potentially missing out on recognizing successful features or identifying areas that need improvement.


### By Correlation
1. It suggests that students who watch **more content tend to earn more certificates**.

### By Dependencies and Probabilities
1. We should **run marketing campaigns that 'resurrect' students who've been registered on the platform for a while but have not been active in a long time.**

    The reason for that is **to introduce such students to the new features of the platform as well as the new content in the course library**. We always aim to upload new and relevant content and believe that **students finished learning** on the platform **can still benefit the program even after some time**.

1. Using dependent probability, we can confirm that students **who watched a lecture in Q2 2022 were unlikely to have also watched one in the same quarter of the previous year.**

### By Linear Regression
This linear regression aims to examine the **causal relationship** between "minutes watched" vs "certificates issued"

I **split** the data into **train and tests** sets with a test size of **20%**.

* $R^2 = 0.305$, an R-squared value of 0.305 is **not a bad result**, but, it implies that **other factors also play a role** in the number of certificates issued. Conclusions: 
    * **Different courses with different lengths.** Therefore, a student passing three short courses will be issued three certificates, while a student passing one long course—roughly the length of three short ones—will be given only one certificate.
    * **Some students pass exams without watching the courses.** The reason could be that they are familiar with the subject and only aim for a document proving their proficiency.

    The model, therefore, provides some insight into the relationship between these two quantities, but **there’s still a large portion of the variance that remains unexplained.** **The number of minutes watched** is reasonable to include when predicting the number of certificates issued but **should not be the sole factor considered**.

* Model Performance

    ![](/images/model_performance.png)

    ![](/images/model_performance_difference.png)

    ![](/images/model_performance_describe.png)

    When we take a look at the data with the **highest difference** (index = 23) we can draw some conlusions:

    * The data with **index 23** has **minutes watched = 2288.98** and actually have just **1 certificate**, this causes large error in our prediction.

    * This observations displays the unexpected data in which the student has only one certificate but long watching time, some possibile explanation of this occurance:

        1. The student took a **very long course**, resulting in the long watching time for a single certification
        1. The student **don't bother finishing the course** until earning the certificate

    These couple of interpretations will be the base for **determining the needed additional input variables** for **improving the model**

# [Project 2: Customer Segmentation in Marketing with Python](https://github.com/jglennc/tracking-user-engagement-with-sql-excel-and-python)

## Case Description

To what extent does our platform’s **customer outreach methods** influence the learning outcomes of our students?

Are there any **geographical locations** where most of our students discover the platform, specifically through social media platforms like YouTube or Facebook?

In this project, I am working with customer data to perform market segmentation—crucial for businesses to understand customer behavior and improve marketing efficiency. The project will involve **data preprocessing, exploratory data analysis (EDA), feature engineering, implementation of clustering algorithms, and interpretation of results**. Two popular clustering techniques are used: **k-means and hierarchical clustering**.

In this project, I delved into the diversity of customer behavior and identify distinct segments that could be targeted with **personalized marketing strategies**.

## Project requirements
* Python version: Python v.3

* Python libraries:

    * pandas 
    * NumPy 
    * Matplotlib 
    * seaborn (optional)
    * scipy
    * sklearn

## Project files
* dataset: customer_segmentation_data.csv

## Outcomes

### Segments
Based on hierarchical clustering and k-means, I identified 8 clusters, and named them through their characteristics, they are:
* Instagram Explorers
* LinkedIn Networkers
* Friends' Influence
* Google-YouTube Mix
* Anglo-Saxon Multi-Channel
* European Multi-Channel
* Twitter Devotees
* Facebook Followers

### Conclusions
![](/images/analysis.png)
![](/images/segmentation_k_means.png)
Based on the grouped aggregated values I was able to draw these conslusions:

I interpreted the customer segments from a marketing perspective. We should discuss these results with the marketing team and help employ a viable **marketing strategy**.

These are the **questions** I tried to answer with my analysis:
* Are there segments that attract engaged students with high Customer Lifetime Value (CLV)?
* From which channels do these segments originate, and which regions do they come from?

**Note:** Assume that the current marketing spend is **equally** allocated across all customer outreach methods and regions.

Based on these insights, the marketing team will be able to devise strategies for:

* **New Customer Outreach Method:** Identify the best channels for approaching each region.
* **Channels Performance Analysis:** Identify underperforming channels.

### Segments: 
1. **Twitter Devotees:** This smallest segment, with only 58 observations, shows that efforts on Twitter are largely ineffective. We recommend minimizing spending and resources on Twitter due to its recent instability and **the marketing team should consider early adoption of new platforms like Threads.**

1. **Facebook Users:** Although not the largest segment (around 8% of customers) and having lower average spending, Facebook users are highly dedicated to learning, with an impressive average watch time of over 2,700 minutes. This segment is diverse, with nearly a third from the US, Canada, or the UK, and over 60% from the rest of the world. **Further analysis on engagement could reveal why this group is so motivated to study.**

    **In terms of countries,** it’s a mixed bag, with a little under a third from the US, Canada, or United Kingdom and over 60% from the rest of the world. It would be worth exploring how these students interact with the platform and why their group is more motivated to study. But this would be the focus of a different analysis on engagement.

### Performance by region:
1. **Anglo-Saxon Region:** This region shows the **best performance**, as **the largest customer segment** mainly comes from the USA, Canada, the UK, and Australia. 
1. **The Google-YouTube mix** is particularly effective being **the second largest segment**, attracting over 900 customers.
1. **Western Europe:** This region has the **fewest customers** despite our assumption of having equal marketing spending across regions. However, it has the highest **Customer Lifetime Value (CLV)**, indicating that improving marketing efforts here is essential.
Rest of the World: This is the second-largest area, with LinkedIn being the most successful channel, followed by Facebook.

### CLV: 
1. **Anglo-Saxon and European Multichannel:** These regions have the highest-paying clusters. Effective channels include Google, YouTube, and LinkedIn. **Increasing spending on these channels in these regions is recommended due to their high CLV.**
1. **Other Regions:** LinkedIn should be the primary channel for attracting customers, followed by Facebook, due to its excellent reach and popularity.

**Based on this analysis, focus on successful channels for each region, increase spending where CLV is highest, and reconsider underperforming platforms to optimize marketing efforts.**


# [Project 3: Scraping Rotten Tomatoes](https://github.com/jglennc/scraping-rotten-tomatoes)
### Case Description
'Rotten Tomatoes' is a review aggregation website

![](/images/rotten_tomatoes_heading.png)

**The goal** is to extract the informations of each movies as seen in the picture below:

![](/images/data_example.png)

**Note: The number of scraped data should be 140 as what the title suggest**

Data to be scraped:
1. Title
1. Year
1. Score
1. The Critics Consensus
1. Director
1. Cast
1. Synopsis

### Project requirements
* Python version: Python v.3

* Python libraries:

    * pandas
    * requests
    * beautifulsoup

## Outcome


dataframe containing scraped data:

![](/images/scraped_dataframe.png)

The scraped data is exported to these files:

* movies_info.csv

* movies_info.xlsx



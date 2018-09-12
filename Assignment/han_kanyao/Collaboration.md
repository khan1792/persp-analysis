Collaboration
================
Kanyao Han

### Part 1: Kaggle open call projects

#### 1. Create an account with Kaggle.com and sign in

My profile name in Kaggle is Kanyao Han.

#### 2. Describe on open call project that is of interest to you in competition page.

-   **What is the goal of the competition?** The name of the project I select is [Web Traffic Time Series Forecasing](https://www.kaggle.com/c/web-traffic-time-series-forecasting#description). This competition focuses on the problem of forecasting the future values of multiple time series. Specifically, its goal is testing state-of-the-art methods designed by the participants and thus forecasting future web traffic for approximately 145,000 Wikipedia articles.

-   **What would I have to do to make a submission?** This competition has two stages. There will be a training stage during which the leaderboard is based on historical data, followed by a stage where participants are scored on real future events. I have complete freedom in how to produce the forecasts: e.g. use of univariate vs multi-variate models, use of metadata, hierarchical time series modeling, different strategies for missing value imputation, and many more types of approaches. Submissions are evaluated on SMAPE (Symmetric mean absolute percentage error) between forecasts and actual values. I must predict the web traffic for each article and day combination. The submission csv file should contain a header and have the following format:
    Id, Visits (such as bf4edcf969af, 0)

#### 3. Explore the available datasets on the Kaggle datasets page. Download one of the datasets and generate a descriptive plot that highlights some instructive characteristic of the data.

The name of the dataset I select is [SF Salaries](https://www.kaggle.com/kaggle/sf-salaries).

``` r
library(tidyverse)

# If you cannot read this file, please set your directory.

salaries <- read_csv("data/Salaries.csv")

# Clean and tidy data
# Remove NA, compute the average all types of average annual incomes and gather them

salaries_mean <- salaries %>%
  drop_na(BasePay, OvertimePay, OtherPay,
          TotalPay, TotalPayBenefits) %>%
  group_by(Year) %>%
  summarize("Base Pay" = mean(BasePay),
            "Overtime Pay" = mean(OvertimePay),
            "Other Pay" = mean(OtherPay),
            "Total Pay" = mean(TotalPay),
            "TotalPay + Benefits" = mean(TotalPayBenefits)) %>%
  gather(key = Income_Type, "value" = Dollars, 2 : 6)

# Generate a plot
ggplot(salaries_mean, aes(Year, Dollars, color = Income_Type)) +
  geom_line(size = 0.8) +
  geom_point(size = 2) +
  labs(title = "Average Annual Incomes for San Francisco City Employees",
       y = "Income")
```

![](Collaboration_files/figure-markdown_github-ascii_identifiers/plot-1.png)

This plot shows that SF city employees' average annual incomes were increasing from 2011 to 2013 and decreasing from 2013 to 2014. This trend applied to almost all types of incomes. It is worth noting that the original data does not document employees' benefits in 2011 so that the "total pay" is equal to the "total pay + benefits" in 2011. However, we actually do not know if there was no benefits in 2011 or they were simply not documented.

### Part 2: Human computation project?

**Journal paper**
K. Fang & M. Repnikova (2017), Demystifying "Little Pink": The creation and evolution of a gendered label for nationalistic activists in China. *New Media & Society*, pp. 1-24, first published online: October 9, 2017.

**A Brief Description: Findings, Methodology and Criticism**

The authors of this Paper explores the origin and evolution of "Little Pink", a label for nationalistic activists in China. They closely read about 1500 threads in Jinjiang forum where the words "Little Pink" emerged, hundreds of comments on Facebook pages related to cross-trait memes war on January 20, 2016 (thousands of Chinese Internet users launched a campaign to flood Facebook pages of the president of Taiwan, a pop star, and Taiwan's pro-independence media outlets because of their support for Taiwan's independence), and dozens of articles and long posts commenting on the cross-trait memes war and Little Pinks from several traditional and digital media. The authors believe that their study "contradicts the popularized narratives of the female-led youthful nationalism in China and instead demonstrates that Little Pink was largely an invented phenomenon-a label that then took on a life of its own during and especially in the aftermath of the cross-strait campaign"(Fang & Repnikova, 2017).

However, after the first author, Kecheng Fang, rephrased this paper in Chinese and published it in Chinese media, his findings were critized by many Chinese netizens. Many netizens stated that they never bulit a tie between gender identity and the lable "Little Pink". Instead, they thought the label was origned from the word "red", which is the symbol of Communism. Besides, according to their narratives, since the vast majority of Little Pinks are young and not party menbers(not red enough), they are labeled as "little" and "pink (light red)". Therefore, the word "Pink" here is not related to feminine color or identity. Additionally, some people also critized that the authors only read texts from a very limited number of forums and media so that they cannot be aware of mutiple origins, evolutions and current meanings of this label.

**Human Computation and Its Advantages**

The criticism from Chinese netizens implies the drawbaks of traditional method used in the paper. Since there are only two researchers and they want to closely read texts in digital or traditional outlets, they can only select a very limited number of outlets and selectively read some texts there. In order to deal with more outlets and texts for better understanding Little Pink, this paper can be refomulated as a human computation project, and the spilt-apply-combine stragety mentioned in *Bit by Bit* is a very proper method in this field.

1.  The authors can at first scrape numerious texts containing words "Little Pink" from main forums and media in China and split them into sentences.
2.  Workers can be recruited from micro-task labor markets with a very low cost. Given that Chinese workers cannot use Amazon Mechanical Turk and most users in AMT cannot read Chinese texts, the authors can select Chinese alternatives such as *Baiduzhongbao* and *Wenjuanxing* to recruit Chinese workers.
3.  When workers accept the task, they will required to rate several sentences in terms of gender, nationalism and rationality as well as their sentiments(positive, neutral or negative). For example, they will be asked which gender a sentence implies (predominantly male, tend to male, both, tend to female, predominantly female), how rational the idea in a sentence or a paragraph is(very irrelational, irrelational, both irrelational and rational, rational, very rational), and how strongly a sentence or a paragraph implicitly or explicitly refers to nationalism (Very Strongly, Strongly, Moderately, weakly, very weakly or no). Each sentence or paragraph will be rated by several workers.
4.  Besides, workers will also be asked about their perception about the lable "Little Pink": What elements are contained in this label? This is a multiple choice question and workers can select from nationalism, gender, rationality and so on. Through this question we can know the people's current perception about the label.
5.  Finally ratings can be combined and computed through statistical model. Furthermore, the authors can also rate some sentence or paragraph by themselves and then test the similarity between their ratings and workers' ratings.

This project design can improve the journal article by several ways. First, it can comprehensively analyze more texts instead of a limited number of texts from several outlets. Therefore, it is possible for us to explore multiple origins, evolution processes and current meanings of the label "Little Pink". Second, we can arrange ratings chronoligically. Under this circumstance, we can not only trace the evolution processes of the meanings of "Little Pink", but also find how many meanings existed in a certain time period. Third, the authors in the paper can save a lot of time becuase they need not to read thousands of texts by their own. Instead, their task is simply test how accurate workers' ratings are. Finally, the cost of the human computation project is relatively low especially when researchers recruit workers form Chinese micro-task labor markets due to the cheap labor in China.

### Part 3: InfluenzaNet project

#### 1. Compare and contrast the design, costs, and likely errors in InfluenzaNet, Google Flu Trends, and traditional influenza tracking systems.

**Design**

InfluenzaNet recruit participants from the general population and ask them to take questionnaire containning demographic and life style questions as well as following weekly questionnaires about a number of influenza-like-illness(ILI) symptoms (including non-symptom) that participants may have experienced since their last report during influenza season. Participants will receive weekly newsletter about influenza questionnaire by e-mail. Questions in questionnaire will be adjusted according to different situations. Researchers then reweighting their sample, excluding some invalid sample (those who only finish one or two questionnaires) and build a statistical model to compute the trend.

In Google Flu Trends Researchers design an automated method to select ILI-related search queries in Google. Then they regard the selected ILI-related query fraction as the explanatory variable and fit a linear model to weekly ILI percentages. The algorithm used in selecting search queries will be calibrated by CDC data.

Traditional influenza tracking system relies on sentinel networks of physicians. This method asks individual physicians or clinics/hospitals to report their patients' influenza-like-illness.

These three designs aim at three types of data. The first type is digital-enhanced survey data with patients' self-reported information. The second is digital observational data. The final one is traditional reported data with physicians' report. They have their own advantages and disadvantages. Traditional data contains least dirty information, but its sample size and population coverage are usually small. Besides, it takes a lot of time to be collected. Digital observational data in Google Flu Trends is the biggest and always-on, and it can predict current trend without any delay. However, it contains a lot of dirty information that may result in biases. Digital-enhanced data has medium sample size and medium data quality so that it has parts of advantages and disadvantages of other two types of data. Besides, it can also collect some distinct information such as whether people attend physician. Therefore, three designs are complementary rather than supplementary.

**Cost**

There is no doubt that **traditional influenza tracking system is the most expensive method** in terms of time, energy and money. Researchers have to cooperate and communicate with numerious physicians or clinics/hospitals and collect numerious reported data. It is a huge task for both researchers, physicians and sometimes patients. **Google Flu Trends might be the cheapest method.** It has existing data so that their work is simply tackling data. **InfluenzaNet is more expansive than Google Flu Trends but much cheaper than traditional method.** Compared with Google Flu Trends, it costs some money, energy and time to publicize this project, recruit participants, distribute weekly questionnaire and prepare the participant payment.

**Likely Errors**

The biggest problem in traditonal influenza tracking system is that only part of population who have influenza-like-illness will attend physicians. Furthermore, this proportion of this kind of people is unknown and it may vary with demographic or characteristics and may change over the course of epidemic. Therefore, it is difficult to obtain unbiased estimation.

InfluenzaNet can track many people who don't attend physicians, but it also has to deal with three kinds of likely errors. The first is derived from ILI definitions. For example, HPA definition is different from GIS and CDC definition and also brings different estimation. Therefore, selecting an unsuitable definition will bring errors. Second, ILI symptoms do not necessarily indicate influenza so that there must be some errors to estimating influenza through ILI. On the contrary, this is not a problem in traditional tracking system because physicians will give a relatively precise diagnosis. Third, this method may have response biases. Although researchers try to adjust demographic biases through weighting the sample, there are still unknown confounders. For example, people who have ILI symptoms are more likely to response while those who don't have would not report their non-symptoms and thus it is hard to know the denominator(those with symptoms plus those without them) for estimation.

As for Google Flu Trends that seldom relies on direct indicators (such as ILI symptoms), system shift, dependence on CDC data and lacking explanatory power/overfitting will bring likely errors. First, Google Search Engine is always changing in terms of new services, data-generating process and so on. Any change might alter users' searching habit and willings and thus produce different type of data. Therefore, estimation errors will occur when Google Search Engine changes but researchers haven't adjusted their algorithm. Second, the algorithm in this method have to be calibrated according to CDC data that is collected by traditional method. Therefore, as long as CDC data has its errors mentioned above, Google Flu Trends will also duplicate them. Finally, this method use a very indirect variable to predict flu trends and thus we don't know much about the direct or indirect causal relationship between flu trends and users' search habit. As long as some unkown causal mechanism change and the algorithm become overfitting, errors in this method might be unbelievably large. The typical example was that Google Flu Trends failed to predit 2013 flue peak since it used some seasonal terms unrelated to flu in its overfitting algorithm.

#### 2. Consider an unsettled time, such as the swine flu outbreak. Describe the possible errors in each system.

**Traditional Tracking System**

Assuming that many people do not hear the information about a new type of swine flu at the beginning of outbreak, most people might just take some medicine at home instead of seeing physicians when they have some ILI symptoms. In this case physicians can only know a very limited number of paitents and report them. Finally, the estimation will be much lower than the status quo. On the contrary, if more people see the physicians than the past flu periods but researchers build a stastical model derived from the previous experience, they are likely to overestimate the trend.

**InfluenzaNet**

Assuming that the symptoms of the swine flu are not fully understood by physicians and scientists and thus it does not have an accurate definition or is very difficult for people without medical background to diagnose, the estimation in this method might have many errors caused by definition and diagnosis biases. Besides, assuming that the treatment period of the swine flue is one to two weeks and thus many cured people are less likely to finish the thrid weekly questionnaire. Since researchers will exclude those who only finish less then two questionnaires, the trend will be underestimated.

**Google Flu Trends**

Actually, search queries does not necessarily correlated with the real flu trends. For example, if the swine flu has a high lethal rate that has caused a social panic, many people who don't have symptoms will search the information about it. In this case, overestimation occurs. Therefore, it is very likely to be overfitting in current algorithm and have no predictory power. Besides, it also depends on Google's system. For example, Google may provide more advertisement related to the lethal swine flu during this period. It might encourage people without symptoms to search swine flu and finally result in overestimation. Furthermore, Google Flu Trends will calibrate its algorithm according to CDC data. Therefore, when CDC data contains errors mentioned above, Google Flu Trends is the same.

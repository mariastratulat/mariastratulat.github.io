
## Finding The Best Market to Advertise In

```Note:
The aim of this project is to summarize the statistics skills learned with Dataquest.```

### Introduction
Let's assume that we are working for an e-learning company that offers courses on programming. Most of our courses are on web and mobile development, but we also cover many other domains, like data science and game development. We want to promote our product and we'd like to invest some money in advertisement. Our goal in this project is to find out the two best markets to advertise our product in.

### Understanding the Data

To avoid spending money on organizing a survey, we'll try to make use of existing data to determine whether we can reach any reliable result.

A good candidate for the dataset to use is the data from [freeCodeCamp's 2017 Coder Survey](https://www.freecodecamp.org/news/we-asked-20-000-people-who-they-are-and-how-theyre-learning-to-code-fff5d668969/), a free e-learning platform that offers courses on web development. Because they run a [popular Medium publication](https://www.freecodecamp.org/news/) (over 400,000 followers), their survey attracted new coders with varying interests, which is ideal for our analysis.

[Survey data](https://github.com/freeCodeCamp/2017-new-coder-survey)


```python
#import
import pandas as pd

pd.options.display.max_columns = 150 # to avoid truncated output 
```


```python
#read the data
coders_survey = pd.read_csv('2017-fCC-New-Coders-Survey-Data.csv')
```

    C:\Users\maria\Anaconda3\lib\site-packages\IPython\core\interactiveshell.py:2785: DtypeWarning: Columns (17,62) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)
    


```python
coders_survey.shape
```




    (18175, 136)




```python
coders_survey.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>AttendedBootcamp</th>
      <th>BootcampFinish</th>
      <th>BootcampLoanYesNo</th>
      <th>BootcampName</th>
      <th>BootcampRecommend</th>
      <th>ChildrenNumber</th>
      <th>CityPopulation</th>
      <th>CodeEventConferences</th>
      <th>CodeEventDjangoGirls</th>
      <th>CodeEventFCC</th>
      <th>CodeEventGameJam</th>
      <th>CodeEventGirlDev</th>
      <th>CodeEventHackathons</th>
      <th>CodeEventMeetup</th>
      <th>CodeEventNodeSchool</th>
      <th>CodeEventNone</th>
      <th>CodeEventOther</th>
      <th>CodeEventRailsBridge</th>
      <th>CodeEventRailsGirls</th>
      <th>CodeEventStartUpWknd</th>
      <th>CodeEventWkdBootcamps</th>
      <th>CodeEventWomenCode</th>
      <th>CodeEventWorkshops</th>
      <th>CommuteTime</th>
      <th>CountryCitizen</th>
      <th>CountryLive</th>
      <th>EmploymentField</th>
      <th>EmploymentFieldOther</th>
      <th>EmploymentStatus</th>
      <th>EmploymentStatusOther</th>
      <th>ExpectedEarning</th>
      <th>FinanciallySupporting</th>
      <th>FirstDevJob</th>
      <th>Gender</th>
      <th>GenderOther</th>
      <th>HasChildren</th>
      <th>HasDebt</th>
      <th>HasFinancialDependents</th>
      <th>HasHighSpdInternet</th>
      <th>HasHomeMortgage</th>
      <th>HasServedInMilitary</th>
      <th>HasStudentDebt</th>
      <th>HomeMortgageOwe</th>
      <th>HoursLearning</th>
      <th>ID.x</th>
      <th>ID.y</th>
      <th>Income</th>
      <th>IsEthnicMinority</th>
      <th>IsReceiveDisabilitiesBenefits</th>
      <th>IsSoftwareDev</th>
      <th>IsUnderEmployed</th>
      <th>JobApplyWhen</th>
      <th>JobInterestBackEnd</th>
      <th>JobInterestDataEngr</th>
      <th>JobInterestDataSci</th>
      <th>JobInterestDevOps</th>
      <th>JobInterestFrontEnd</th>
      <th>JobInterestFullStack</th>
      <th>JobInterestGameDev</th>
      <th>JobInterestInfoSec</th>
      <th>JobInterestMobile</th>
      <th>JobInterestOther</th>
      <th>JobInterestProjMngr</th>
      <th>JobInterestQAEngr</th>
      <th>JobInterestUX</th>
      <th>JobPref</th>
      <th>JobRelocateYesNo</th>
      <th>JobRoleInterest</th>
      <th>JobWherePref</th>
      <th>LanguageAtHome</th>
      <th>MaritalStatus</th>
      <th>MoneyForLearning</th>
      <th>MonthsProgramming</th>
      <th>NetworkID</th>
      <th>Part1EndTime</th>
      <th>Part1StartTime</th>
      <th>Part2EndTime</th>
      <th>Part2StartTime</th>
      <th>PodcastChangeLog</th>
      <th>PodcastCodeNewbie</th>
      <th>PodcastCodePen</th>
      <th>PodcastDevTea</th>
      <th>PodcastDotNET</th>
      <th>PodcastGiantRobots</th>
      <th>PodcastJSAir</th>
      <th>PodcastJSJabber</th>
      <th>PodcastNone</th>
      <th>PodcastOther</th>
      <th>PodcastProgThrowdown</th>
      <th>PodcastRubyRogues</th>
      <th>PodcastSEDaily</th>
      <th>PodcastSERadio</th>
      <th>PodcastShopTalk</th>
      <th>PodcastTalkPython</th>
      <th>PodcastTheWebAhead</th>
      <th>ResourceCodecademy</th>
      <th>ResourceCodeWars</th>
      <th>ResourceCoursera</th>
      <th>ResourceCSS</th>
      <th>ResourceEdX</th>
      <th>ResourceEgghead</th>
      <th>ResourceFCC</th>
      <th>ResourceHackerRank</th>
      <th>ResourceKA</th>
      <th>ResourceLynda</th>
      <th>ResourceMDN</th>
      <th>ResourceOdinProj</th>
      <th>ResourceOther</th>
      <th>ResourcePluralSight</th>
      <th>ResourceSkillcrush</th>
      <th>ResourceSO</th>
      <th>ResourceTreehouse</th>
      <th>ResourceUdacity</th>
      <th>ResourceUdemy</th>
      <th>ResourceW3S</th>
      <th>SchoolDegree</th>
      <th>SchoolMajor</th>
      <th>StudentDebtOwe</th>
      <th>YouTubeCodeCourse</th>
      <th>YouTubeCodingTrain</th>
      <th>YouTubeCodingTut360</th>
      <th>YouTubeComputerphile</th>
      <th>YouTubeDerekBanas</th>
      <th>YouTubeDevTips</th>
      <th>YouTubeEngineeredTruth</th>
      <th>YouTubeFCC</th>
      <th>YouTubeFunFunFunction</th>
      <th>YouTubeGoogleDev</th>
      <th>YouTubeLearnCode</th>
      <th>YouTubeLevelUpTuts</th>
      <th>YouTubeMIT</th>
      <th>YouTubeMozillaHacks</th>
      <th>YouTubeOther</th>
      <th>YouTubeSimplilearn</th>
      <th>YouTubeTheNewBoston</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>27.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>Canada</td>
      <td>Canada</td>
      <td>software development and IT</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>02d9465b21e8bd09374b0066fb2d5614</td>
      <td>eb78c1c3ac6cd9052aec557065070fbf</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>start your own business</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>150.0</td>
      <td>6.0</td>
      <td>6f1fbc6b2b</td>
      <td>2017-03-09 00:36:22</td>
      <td>2017-03-09 00:32:59</td>
      <td>2017-03-09 00:59:46</td>
      <td>2017-03-09 00:36:26</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>some college credit, no degree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>34.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>less than 100,000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>35000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>10.0</td>
      <td>5bfef9ecb211ec4f518cfc1d2a6f3e0c</td>
      <td>21db37adb60cdcafadfa7dca1b13b6b1</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within 7 to 12 months</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a nonprofit</td>
      <td>1.0</td>
      <td>Full-Stack Web Developer</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>single, never married</td>
      <td>80.0</td>
      <td>6.0</td>
      <td>f8f8be6910</td>
      <td>2017-03-09 00:37:07</td>
      <td>2017-03-09 00:33:26</td>
      <td>2017-03-09 00:38:59</td>
      <td>2017-03-09 00:37:10</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>some college credit, no degree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>software development and IT</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>70000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>25.0</td>
      <td>14f1863afa9c7de488050b82eb3edd96</td>
      <td>21ba173828fbe9e27ccebaf4d5166a55</td>
      <td>13000.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Within 7 to 12 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a medium-sized company</td>
      <td>1.0</td>
      <td>Front-End Web Developer, Back-End Web Develo...</td>
      <td>no preference</td>
      <td>Spanish</td>
      <td>single, never married</td>
      <td>1000.0</td>
      <td>5.0</td>
      <td>2ed189768e</td>
      <td>2017-03-09 00:37:58</td>
      <td>2017-03-09 00:33:53</td>
      <td>2017-03-09 00:40:14</td>
      <td>2017-03-09 00:38:02</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Codenewbie</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>high school diploma or equivalent (GED)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>26.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I work from home</td>
      <td>Brazil</td>
      <td>Brazil</td>
      <td>software development and IT</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>40000.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>40000.0</td>
      <td>14.0</td>
      <td>91756eb4dc280062a541c25a3d44cfb0</td>
      <td>3be37b558f02daae93a6da10f83f0c77</td>
      <td>24000.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>Within the next 6 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a medium-sized company</td>
      <td>NaN</td>
      <td>Front-End Web Developer, Full-Stack Web Deve...</td>
      <td>from home</td>
      <td>Portuguese</td>
      <td>married or domestic partnership</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>dbdc0664d1</td>
      <td>2017-03-09 00:40:13</td>
      <td>2017-03-09 00:37:45</td>
      <td>2017-03-09 00:42:26</td>
      <td>2017-03-09 00:40:18</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>some college credit, no degree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Portugal</td>
      <td>Portugal</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>140000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10.0</td>
      <td>aa3f061a1949a90b27bef7411ecd193f</td>
      <td>d7c56bbf2c7b62096be9db010e86d96d</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within 7 to 12 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>1.0</td>
      <td>Full-Stack Web Developer, Information Security...</td>
      <td>in an office with other developers</td>
      <td>Portuguese</td>
      <td>single, never married</td>
      <td>0.0</td>
      <td>24.0</td>
      <td>11b0f2d8a9</td>
      <td>2017-03-09 00:42:45</td>
      <td>2017-03-09 00:39:44</td>
      <td>2017-03-09 00:45:42</td>
      <td>2017-03-09 00:42:50</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Information Technology</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Most column names are self-explanatory, but we don't have clear documentation explaining each column name. However, we can find the initial survey questions in the `raw-data` folder of the [repository](https://github.com/freeCodeCamp/2017-new-coder-survey) which makes an easy job to infer what each column describes.

### Checking for Sample Representativity

For the analysis, we want to answer questions about a population of new coders that are interested in the subject we teach. We'd like to know:
- Where are the new coders located?
- What are the locations with the greatest number of coders?
- How much money new coders are willing to spend on learning?

First, let's clarify whether the sample of data is representative for our population of interest.


```python
# frequency table in percentage
coders_survey["JobRoleInterest"].value_counts(normalize=True) * 100
```




    Full-Stack Web Developer                                                                                                                                                                                                                 11.770595
      Front-End Web Developer                                                                                                                                                                                                                 6.435927
      Data Scientist                                                                                                                                                                                                                          2.173913
    Back-End Web Developer                                                                                                                                                                                                                    2.030892
      Mobile Developer                                                                                                                                                                                                                        1.673341
    Game Developer                                                                                                                                                                                                                            1.630435
    Information Security                                                                                                                                                                                                                      1.315789
    Full-Stack Web Developer,   Front-End Web Developer                                                                                                                                                                                       0.915332
      Front-End Web Developer, Full-Stack Web Developer                                                                                                                                                                                       0.800915
      Product Manager                                                                                                                                                                                                                         0.786613
    Data Engineer                                                                                                                                                                                                                             0.758009
      User Experience Designer                                                                                                                                                                                                                0.743707
      User Experience Designer,   Front-End Web Developer                                                                                                                                                                                     0.614989
      Front-End Web Developer, Back-End Web Developer, Full-Stack Web Developer                                                                                                                                                               0.557780
      DevOps / SysAdmin                                                                                                                                                                                                                       0.514874
    Back-End Web Developer,   Front-End Web Developer, Full-Stack Web Developer                                                                                                                                                               0.514874
    Back-End Web Developer, Full-Stack Web Developer,   Front-End Web Developer                                                                                                                                                               0.514874
    Full-Stack Web Developer,   Front-End Web Developer, Back-End Web Developer                                                                                                                                                               0.443364
      Front-End Web Developer, Full-Stack Web Developer, Back-End Web Developer                                                                                                                                                               0.429062
    Full-Stack Web Developer,   Mobile Developer                                                                                                                                                                                              0.414760
      Front-End Web Developer,   User Experience Designer                                                                                                                                                                                     0.414760
    Back-End Web Developer, Full-Stack Web Developer                                                                                                                                                                                          0.386156
    Full-Stack Web Developer, Back-End Web Developer                                                                                                                                                                                          0.371854
    Back-End Web Developer,   Front-End Web Developer                                                                                                                                                                                         0.286041
    Data Engineer,   Data Scientist                                                                                                                                                                                                           0.271739
    Full-Stack Web Developer, Back-End Web Developer,   Front-End Web Developer                                                                                                                                                               0.271739
      Front-End Web Developer,   Mobile Developer                                                                                                                                                                                             0.257437
    Full-Stack Web Developer,   Data Scientist                                                                                                                                                                                                0.243135
      Mobile Developer, Game Developer                                                                                                                                                                                                        0.228833
      Data Scientist, Data Engineer                                                                                                                                                                                                           0.228833
                                                                                                                                                                                                                                               ...    
    Game Developer,   DevOps / SysAdmin,   Front-End Web Developer, Full-Stack Web Developer, Back-End Web Developer                                                                                                                          0.014302
      Mobile Developer, Game Developer, Back-End Web Developer, Full-Stack Web Developer,   Front-End Web Developer,   User Experience Designer, User Interface Designer                                                                      0.014302
      Mobile Developer, Game Developer,   DevOps / SysAdmin, Information Security, Data Engineer                                                                                                                                              0.014302
      Data Scientist, Game Developer,   Quality Assurance Engineer                                                                                                                                                                            0.014302
      Data Scientist,   Front-End Web Developer, Full-Stack Web Developer, Back-End Web Developer                                                                                                                                             0.014302
    Game Developer,   Data Scientist                                                                                                                                                                                                          0.014302
      Front-End Web Developer,   Mobile Developer, Back-End Web Developer, Full-Stack Web Developer, Data Engineer                                                                                                                            0.014302
    Back-End Web Developer,   Mobile Developer,   Front-End Web Developer, Full-Stack Web Developer,   User Experience Designer                                                                                                               0.014302
    Full-Stack Web Developer, Information Security,   DevOps / SysAdmin,   Data Scientist                                                                                                                                                     0.014302
      Front-End Web Developer, Data Engineer, Back-End Web Developer,   Quality Assurance Engineer                                                                                                                                            0.014302
    Full-Stack Web Developer, Back-End Web Developer, Data Engineer, Information Security                                                                                                                                                     0.014302
      User Experience Designer, Full-Stack Web Developer,   Mobile Developer,   Front-End Web Developer, Back-End Web Developer                                                                                                               0.014302
    Information Security, Full-Stack Web Developer, Back-End Web Developer,   Front-End Web Developer, Data Engineer,   Data Scientist,   Mobile Developer,   Quality Assurance Engineer,   User Experience Designer,   DevOps / SysAdmin     0.014302
    Full-Stack Web Developer, Game Developer,   Mobile Developer, Back-End Web Developer,   Front-End Web Developer                                                                                                                           0.014302
      User Experience Designer, Information Security,   Mobile Developer,   Product Manager,   Quality Assurance Engineer                                                                                                                     0.014302
      Mobile Developer, Game Developer, Full-Stack Web Developer,   Front-End Web Developer, Back-End Web Developer,   User Experience Designer, Information Security                                                                         0.014302
    Full-Stack Web Developer, Back-End Web Developer,   Data Scientist,   Mobile Developer                                                                                                                                                    0.014302
    Full Stack Software Engineer                                                                                                                                                                                                              0.014302
    Full-Stack Web Developer,   Mobile Developer,   User Experience Designer,   Product Manager,   Front-End Web Developer                                                                                                                    0.014302
      Front-End Web Developer, Back-End Web Developer, Full-Stack Web Developer,   Mobile Developer, Data Engineer,   DevOps / SysAdmin                                                                                                       0.014302
    Back-End Web Developer,   Front-End Web Developer, Game Developer, Information Security, Full-Stack Web Developer                                                                                                                         0.014302
    Full-Stack Web Developer,   Mobile Developer, Data Engineer,   Front-End Web Developer                                                                                                                                                    0.014302
      Product Manager, Information Security,   Mobile Developer,   Front-End Web Developer,   Data Scientist,   DevOps / SysAdmin                                                                                                             0.014302
      Mobile Developer,   Front-End Web Developer, Full-Stack Web Developer, Back-End Web Developer, Game Developer                                                                                                                           0.014302
    Back-End Web Developer, Full-Stack Web Developer,   Data Scientist, Information Security                                                                                                                                                  0.014302
    Full-Stack Web Developer,   Front-End Web Developer,   DevOps / SysAdmin                                                                                                                                                                  0.014302
      DevOps / SysAdmin, Full-Stack Web Developer, Back-End Web Developer, Game Developer, Data Engineer                                                                                                                                      0.014302
    Data Engineer,   Data Scientist,   Product Manager, Back-End Web Developer,   Quality Assurance Engineer                                                                                                                                  0.014302
    Back-End Web Developer, Full-Stack Web Developer,   Mobile Developer,   DevOps / SysAdmin                                                                                                                                                 0.014302
    Full-Stack Web Developer,   Data Scientist,   DevOps / SysAdmin, Data Engineer                                                                                                                                                            0.014302
    Name: JobRoleInterest, Length: 3213, dtype: float64



Web development is very popular in the frequency table we generated. And to note that many coders are interested in more than one subject.

Let's find the percentage of coders interested in one subject only.


```python
interest_no_null = coders_survey["JobRoleInterest"].dropna()

interests_list = interest_no_null.str.split(",")
interests_num = interests_list.apply(lambda x: len(x))
interests_num.value_counts(normalize=True).sort_index() * 100
```




    1     31.650458
    2     10.883867
    3     15.889588
    4     15.217391
    5     12.042334
    6      6.721968
    7      3.861556
    8      1.759153
    9      0.986842
    10     0.471968
    11     0.185927
    12     0.300343
    13     0.028604
    Name: JobRoleInterest, dtype: float64



The frequency table above shows that only 31.6% of people chose only one programming niche of interest. 

The focus of our interest in web and mobile development. Let's find out how many people are interested in at least one of these two subjects.


```python
web_or_mobile = interest_no_null.str.contains("Web Developer|Mobile Developer")

web_or_mobile_num = web_or_mobile.value_counts(normalize=True) * 100
web_or_mobile_num
```




    True     86.241419
    False    13.758581
    Name: JobRoleInterest, dtype: float64




```python
%matplotlib inline
import matplotlib.pyplot as plt
plt.style.use('seaborn-deep')

web_or_mobile_num.plot.bar()
plt.title("Coders Interests in \nWeb or Mobile Development vs Other", fontsize=14)
plt.ylabel("Percentage")
plt.ylim([0,100])
plt.xticks([0,1],['Web or mobile \ndevelopment', 'Other'], rotation=0)
plt.box(False)
plt.grid(axis='y')
plt.show()
```


![png](output_14_0.png)


Now that we found out that the sample has the right categories of people for our purpose, 86% of people interested in web or mobile development, we can begin analyzing it. We start with finding coders' location and their density.

Because the data set provides information at the country level, we can think as of each country as an individual market. We can frame our goal as finding the two countries to advertise in.

One indicator of a good market is the number of potential customers -- the more potential customers in a market, the better. If out adds manage to convince 10% of the 5000 potential customers in market A to buy our product, then this is better than convincing 100% of the 30 potential customers in market B.

### New Coders - Locations and Densities


```python
coders_no_null = coders_survey[coders_survey['JobRoleInterest'].notnull()].copy()
coders_live_abs = coders_no_null['CountryLive'].value_counts()
coders_live_rel = coders_no_null['CountryLive'].value_counts(normalize=True) * 100

pd.DataFrame(data={"Absolute frequency" : coders_live_abs,
                  "Relative frequency" : coders_live_rel})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Absolute frequency</th>
      <th>Relative frequency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>United States of America</th>
      <td>3125</td>
      <td>45.700497</td>
    </tr>
    <tr>
      <th>India</th>
      <td>528</td>
      <td>7.721556</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>315</td>
      <td>4.606610</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>260</td>
      <td>3.802281</td>
    </tr>
    <tr>
      <th>Poland</th>
      <td>131</td>
      <td>1.915765</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>129</td>
      <td>1.886517</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>125</td>
      <td>1.828020</td>
    </tr>
    <tr>
      <th>Australia</th>
      <td>112</td>
      <td>1.637906</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>102</td>
      <td>1.491664</td>
    </tr>
    <tr>
      <th>Ukraine</th>
      <td>89</td>
      <td>1.301550</td>
    </tr>
    <tr>
      <th>Nigeria</th>
      <td>84</td>
      <td>1.228429</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>77</td>
      <td>1.126060</td>
    </tr>
    <tr>
      <th>France</th>
      <td>75</td>
      <td>1.096812</td>
    </tr>
    <tr>
      <th>Romania</th>
      <td>71</td>
      <td>1.038315</td>
    </tr>
    <tr>
      <th>Netherlands (Holland, Europe)</th>
      <td>65</td>
      <td>0.950570</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>62</td>
      <td>0.906698</td>
    </tr>
    <tr>
      <th>Serbia</th>
      <td>52</td>
      <td>0.760456</td>
    </tr>
    <tr>
      <th>Philippines</th>
      <td>52</td>
      <td>0.760456</td>
    </tr>
    <tr>
      <th>Greece</th>
      <td>46</td>
      <td>0.672711</td>
    </tr>
    <tr>
      <th>Ireland</th>
      <td>43</td>
      <td>0.628839</td>
    </tr>
    <tr>
      <th>South Africa</th>
      <td>39</td>
      <td>0.570342</td>
    </tr>
    <tr>
      <th>Mexico</th>
      <td>37</td>
      <td>0.541094</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>36</td>
      <td>0.526470</td>
    </tr>
    <tr>
      <th>Singapore</th>
      <td>34</td>
      <td>0.497221</td>
    </tr>
    <tr>
      <th>Hungary</th>
      <td>34</td>
      <td>0.497221</td>
    </tr>
    <tr>
      <th>New Zealand</th>
      <td>33</td>
      <td>0.482597</td>
    </tr>
    <tr>
      <th>Croatia</th>
      <td>32</td>
      <td>0.467973</td>
    </tr>
    <tr>
      <th>Argentina</th>
      <td>32</td>
      <td>0.467973</td>
    </tr>
    <tr>
      <th>Pakistan</th>
      <td>31</td>
      <td>0.453349</td>
    </tr>
    <tr>
      <th>Sweden</th>
      <td>31</td>
      <td>0.453349</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Botswana</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Angola</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Qatar</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Guadeloupe</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Guatemala</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Vanuatu</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Channel Islands</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Kyrgyzstan</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Rwanda</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Cameroon</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Myanmar</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Somalia</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Aruba</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Anguilla</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Gibraltar</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Bolivia</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Trinidad &amp; Tobago</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Yemen</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Samoa</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Mozambique</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Liberia</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Jordan</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Cuba</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Papua New Guinea</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Panama</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Sudan</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Gambia</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Nicaragua</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Nambia</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
    <tr>
      <th>Turkmenistan</th>
      <td>1</td>
      <td>0.014624</td>
    </tr>
  </tbody>
</table>
<p>137 rows × 2 columns</p>
</div>



The top two countries with interest in studying web or mobile development are USA and India with 45.7% and respectively 7.7%. The result for India is very close to the UK and Canada. Further exploration would be needed to see people from which country are willing to spend money on online learning.

### Spending Money for Learning

It seems like a good idea to narrow down our analysis to only four countries: the US, India, the UK, and Canada. Two reasons for this decision are:
- These are the countries having the highest absolute frequencies in our sample, which means we have a decent amount of data for each.
- Our courses are written in English, and English is an official language in all of these four countries. The more people that know English, the better our chances to target the right people with ads.


```python
coders_no_null["MonthsProgramming"].value_counts().sort_index()
```




    0.0      235
    1.0      767
    2.0      669
    3.0      637
    4.0      367
    5.0      279
    6.0      654
    7.0      124
    8.0      195
    9.0      102
    10.0     144
    11.0      39
    12.0     616
    13.0      36
    14.0      76
    15.0      70
    16.0      58
    17.0      20
    18.0     160
    19.0       7
    20.0      92
    21.0       9
    22.0       5
    23.0       4
    24.0     422
    25.0      12
    26.0      17
    27.0       8
    28.0      13
    29.0       6
            ... 
    73.0       1
    75.0       2
    80.0       3
    83.0       1
    84.0      11
    86.0       1
    89.0       1
    96.0       8
    100.0      8
    105.0      1
    108.0      2
    111.0      1
    113.0      1
    120.0     13
    124.0      1
    144.0      5
    156.0      2
    171.0      1
    180.0      1
    190.0      1
    198.0      1
    200.0      6
    240.0      3
    264.0      1
    300.0      1
    360.0      5
    370.0      1
    408.0      1
    480.0      2
    744.0      4
    Name: MonthsProgramming, Length: 91, dtype: int64



We have to divide the `MoneyForLearning` column to the `MonthsProgramming` column to create a new column that describes the amount of money a student had spend per month. To avoid dividing by 0, we'll replace all the 0 values with 1, as we assume that students just started learning.


```python
coders_no_null['MonthsProgramming'].replace(0, 1, inplace=True)

coders_no_null['MonthsProgramming'].value_counts().sort_index().head()
```




    1.0    1002
    2.0     669
    3.0     637
    4.0     367
    5.0     279
    Name: MonthsProgramming, dtype: int64




```python
coders_no_null['money_per_month'] = coders_no_null['MoneyForLearning'] / coders_no_null['MonthsProgramming']

coders_no_null['money_per_month'].isnull().sum()
```




    675



We want to keep only the rows that have the spending amount per month greater than zero.


```python
coders_no_null = coders_no_null[coders_no_null['money_per_month'].notnull()]
```

We want to group the remaining data by country and find the amount of money a student spends on average each month in the US, India, the UK, and Canada.


```python
coders_no_null = coders_no_null[coders_no_null['CountryLive'].notnull()]

coders_no_null['CountryLive'].value_counts().head()
```




    United States of America    2933
    India                        463
    United Kingdom               279
    Canada                       240
    Poland                       122
    Name: CountryLive, dtype: int64




```python
countries_mean = coders_no_null.groupby('CountryLive').mean()
countries_mean['money_per_month'][['United States of America', 'India',
                                 'United Kingdom', 'Canada']].sort_values(ascending=False)
```




    CountryLive
    United States of America    227.997996
    India                       135.100982
    Canada                      113.510961
    United Kingdom               45.534443
    Name: money_per_month, dtype: float64



The results for the UK and Canada are surprisingly low relative to the other values we see for India. If we consider a few social-economical metrics ([GDP per capita](https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(PPP)_per_capita#Lists_of_countries_and_dependencies)), we'd intuitively expect people in the UK and Canada to spend more on learning than people in India.

It might be we don't have enough representative data for the UK and Canada, or we have outliers, or it might be the results are correct.

### Dealing with Extreme Outliers


```python
countries_top_four = coders_no_null[coders_no_null['CountryLive'].str.contains('United States of America|India|United Kingdom|Canada')]

import seaborn as sns

sns.boxplot(x='CountryLive', y='money_per_month', data=countries_top_four)
plt.title('Money Spent Per Month Per Country', fontsize=14)
plt.ylabel('Money per month (in US dollars)')
plt.xlabel('Country')
plt.show()
```


![png](output_28_0.png)


Nothing looks wrong with the data, except for the US, which has two outliers. It seems like two students spend \$50000 and \$80000 a month. This is not impossible but it is unlikely to happen. Let's keep only the data with the amount up to \$20000  spent a month.


```python
coders = coders_no_null[coders_no_null['money_per_month'] < 20000]

#recompute the mean
countries_mean = coders.groupby('CountryLive').mean()
countries_mean['money_per_month'][['United States of America', 'India',
                                 'United Kingdom', 'Canada']].sort_values(ascending=False)
```




    CountryLive
    United States of America    183.800110
    India                       135.100982
    Canada                      113.510961
    United Kingdom               45.534443
    Name: money_per_month, dtype: float64




```python
countries_top_four = coders[coders_no_null['CountryLive'].str.contains('United States of America|India|United Kingdom|Canada')]

import seaborn as sns

sns.boxplot(x='CountryLive', y='money_per_month', data=countries_top_four)
plt.title('Money Spent Per Month Per Country', fontsize=14)
plt.ylabel('Money per month (in US dollars)')
plt.xlabel('Country')
plt.show()
```

    C:\Users\maria\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: UserWarning: Boolean Series key will be reindexed to match DataFrame index.
      """Entry point for launching an IPython kernel.
    


![png](output_31_1.png)


We find some outliers for India. Let's isolate those rows to figure out whether these big expenses are justified (maybe some bootcamps attended).


```python
india_outliers = countries_top_four[
    (countries_top_four['CountryLive'] == 'India') & 
    (countries_top_four['money_per_month'] >= 2500)]
india_outliers
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>AttendedBootcamp</th>
      <th>BootcampFinish</th>
      <th>BootcampLoanYesNo</th>
      <th>BootcampName</th>
      <th>BootcampRecommend</th>
      <th>ChildrenNumber</th>
      <th>CityPopulation</th>
      <th>CodeEventConferences</th>
      <th>CodeEventDjangoGirls</th>
      <th>CodeEventFCC</th>
      <th>CodeEventGameJam</th>
      <th>CodeEventGirlDev</th>
      <th>CodeEventHackathons</th>
      <th>CodeEventMeetup</th>
      <th>CodeEventNodeSchool</th>
      <th>CodeEventNone</th>
      <th>CodeEventOther</th>
      <th>CodeEventRailsBridge</th>
      <th>CodeEventRailsGirls</th>
      <th>CodeEventStartUpWknd</th>
      <th>CodeEventWkdBootcamps</th>
      <th>CodeEventWomenCode</th>
      <th>CodeEventWorkshops</th>
      <th>CommuteTime</th>
      <th>CountryCitizen</th>
      <th>CountryLive</th>
      <th>EmploymentField</th>
      <th>EmploymentFieldOther</th>
      <th>EmploymentStatus</th>
      <th>EmploymentStatusOther</th>
      <th>ExpectedEarning</th>
      <th>FinanciallySupporting</th>
      <th>FirstDevJob</th>
      <th>Gender</th>
      <th>GenderOther</th>
      <th>HasChildren</th>
      <th>HasDebt</th>
      <th>HasFinancialDependents</th>
      <th>HasHighSpdInternet</th>
      <th>HasHomeMortgage</th>
      <th>HasServedInMilitary</th>
      <th>HasStudentDebt</th>
      <th>HomeMortgageOwe</th>
      <th>HoursLearning</th>
      <th>ID.x</th>
      <th>ID.y</th>
      <th>Income</th>
      <th>IsEthnicMinority</th>
      <th>IsReceiveDisabilitiesBenefits</th>
      <th>IsSoftwareDev</th>
      <th>IsUnderEmployed</th>
      <th>JobApplyWhen</th>
      <th>JobInterestBackEnd</th>
      <th>JobInterestDataEngr</th>
      <th>JobInterestDataSci</th>
      <th>JobInterestDevOps</th>
      <th>JobInterestFrontEnd</th>
      <th>JobInterestFullStack</th>
      <th>JobInterestGameDev</th>
      <th>JobInterestInfoSec</th>
      <th>JobInterestMobile</th>
      <th>JobInterestOther</th>
      <th>JobInterestProjMngr</th>
      <th>JobInterestQAEngr</th>
      <th>JobInterestUX</th>
      <th>JobPref</th>
      <th>JobRelocateYesNo</th>
      <th>JobRoleInterest</th>
      <th>JobWherePref</th>
      <th>LanguageAtHome</th>
      <th>MaritalStatus</th>
      <th>MoneyForLearning</th>
      <th>MonthsProgramming</th>
      <th>NetworkID</th>
      <th>Part1EndTime</th>
      <th>Part1StartTime</th>
      <th>Part2EndTime</th>
      <th>Part2StartTime</th>
      <th>PodcastChangeLog</th>
      <th>PodcastCodeNewbie</th>
      <th>PodcastCodePen</th>
      <th>PodcastDevTea</th>
      <th>PodcastDotNET</th>
      <th>PodcastGiantRobots</th>
      <th>PodcastJSAir</th>
      <th>PodcastJSJabber</th>
      <th>PodcastNone</th>
      <th>PodcastOther</th>
      <th>PodcastProgThrowdown</th>
      <th>PodcastRubyRogues</th>
      <th>PodcastSEDaily</th>
      <th>PodcastSERadio</th>
      <th>PodcastShopTalk</th>
      <th>PodcastTalkPython</th>
      <th>PodcastTheWebAhead</th>
      <th>ResourceCodecademy</th>
      <th>ResourceCodeWars</th>
      <th>ResourceCoursera</th>
      <th>ResourceCSS</th>
      <th>ResourceEdX</th>
      <th>ResourceEgghead</th>
      <th>ResourceFCC</th>
      <th>ResourceHackerRank</th>
      <th>ResourceKA</th>
      <th>ResourceLynda</th>
      <th>ResourceMDN</th>
      <th>ResourceOdinProj</th>
      <th>ResourceOther</th>
      <th>ResourcePluralSight</th>
      <th>ResourceSkillcrush</th>
      <th>ResourceSO</th>
      <th>ResourceTreehouse</th>
      <th>ResourceUdacity</th>
      <th>ResourceUdemy</th>
      <th>ResourceW3S</th>
      <th>SchoolDegree</th>
      <th>SchoolMajor</th>
      <th>StudentDebtOwe</th>
      <th>YouTubeCodeCourse</th>
      <th>YouTubeCodingTrain</th>
      <th>YouTubeCodingTut360</th>
      <th>YouTubeComputerphile</th>
      <th>YouTubeDerekBanas</th>
      <th>YouTubeDevTips</th>
      <th>YouTubeEngineeredTruth</th>
      <th>YouTubeFCC</th>
      <th>YouTubeFunFunFunction</th>
      <th>YouTubeGoogleDev</th>
      <th>YouTubeLearnCode</th>
      <th>YouTubeLevelUpTuts</th>
      <th>YouTubeMIT</th>
      <th>YouTubeMozillaHacks</th>
      <th>YouTubeOther</th>
      <th>YouTubeSimplilearn</th>
      <th>YouTubeTheNewBoston</th>
      <th>money_per_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1728</th>
      <td>24.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>India</td>
      <td>India</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A stay-at-home parent or homemaker</td>
      <td>NaN</td>
      <td>70000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.0</td>
      <td>d964ec629fd6d85a5bf27f7339f4fa6d</td>
      <td>950a8cf9cef1ae6a15da470e572b1b7a</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>work for a startup</td>
      <td>1.0</td>
      <td>User Experience Designer,   Mobile Developer...</td>
      <td>in an office with other developers</td>
      <td>Bengali</td>
      <td>single, never married</td>
      <td>20000.0</td>
      <td>4.0</td>
      <td>38d312a990</td>
      <td>2017-03-10 10:22:34</td>
      <td>2017-03-10 10:17:42</td>
      <td>2017-03-10 10:24:38</td>
      <td>2017-03-10 10:22:40</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>bachelor's degree</td>
      <td>Computer Programming</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5000.000000</td>
    </tr>
    <tr>
      <th>1755</th>
      <td>20.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>India</td>
      <td>India</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working and not looking for work</td>
      <td>NaN</td>
      <td>100000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10.0</td>
      <td>811bf953ef546460f5436fcf2baa532d</td>
      <td>81e2a4cab0543e14746c4a20ffdae17c</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>I haven't decided</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>1.0</td>
      <td>Information Security, Full-Stack Web Developer...</td>
      <td>no preference</td>
      <td>Hindi</td>
      <td>single, never married</td>
      <td>50000.0</td>
      <td>15.0</td>
      <td>4611a76b60</td>
      <td>2017-03-10 10:48:31</td>
      <td>2017-03-10 10:42:29</td>
      <td>2017-03-10 10:51:37</td>
      <td>2017-03-10 10:48:38</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>bachelor's degree</td>
      <td>Computer Science</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3333.333333</td>
    </tr>
    <tr>
      <th>7989</th>
      <td>28.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>15 to 29 minutes</td>
      <td>India</td>
      <td>India</td>
      <td>software development and IT</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>500000.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>20.0</td>
      <td>a6a5597bbbc2c282386d6675641b744a</td>
      <td>da7bbb54a8b26a379707be56b6c51e65</td>
      <td>300000.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>more than 12 months from now</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>work for a multinational corporation</td>
      <td>1.0</td>
      <td>User Experience Designer, Back-End Web Devel...</td>
      <td>in an office with other developers</td>
      <td>Marathi</td>
      <td>married or domestic partnership</td>
      <td>5000.0</td>
      <td>1.0</td>
      <td>c47a447b5d</td>
      <td>2017-03-26 14:06:48</td>
      <td>2017-03-26 14:02:41</td>
      <td>2017-03-26 14:13:13</td>
      <td>2017-03-26 14:07:17</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not listened to anything yet.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Aerospace and Aeronautical Engineering</td>
      <td>2500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5000.000000</td>
    </tr>
    <tr>
      <th>8126</th>
      <td>22.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>India</td>
      <td>India</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>80000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>80.0</td>
      <td>69e8ab9126baee49f66e3577aea7fd3c</td>
      <td>9f08092e82f709e63847ba88841247c0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>I'm already applying</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a startup</td>
      <td>1.0</td>
      <td>Back-End Web Developer, Full-Stack Web Develop...</td>
      <td>in an office with other developers</td>
      <td>Malayalam</td>
      <td>single, never married</td>
      <td>5000.0</td>
      <td>1.0</td>
      <td>0d3d1762a4</td>
      <td>2017-03-27 07:10:17</td>
      <td>2017-03-27 07:05:23</td>
      <td>2017-03-27 07:12:21</td>
      <td>2017-03-27 07:10:22</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Electrical and Electronics Engineering</td>
      <td>10000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>5000.000000</td>
    </tr>
    <tr>
      <th>13398</th>
      <td>19.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>India</td>
      <td>India</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Unable to work</td>
      <td>NaN</td>
      <td>100000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.0</td>
      <td>b7fe7bc4edefc3a60eb48f977e4426e3</td>
      <td>80ff09859ac475b70ac19b7b7369e953</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>I haven't decided</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>1.0</td>
      <td>Mobile Developer</td>
      <td>no preference</td>
      <td>Hindi</td>
      <td>single, never married</td>
      <td>20000.0</td>
      <td>2.0</td>
      <td>51a6f9a1a7</td>
      <td>2017-04-01 00:31:25</td>
      <td>2017-04-01 00:28:17</td>
      <td>2017-04-01 00:33:44</td>
      <td>2017-04-01 00:31:32</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>bachelor's degree</td>
      <td>Computer Science</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10000.000000</td>
    </tr>
    <tr>
      <th>15587</th>
      <td>27.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>India</td>
      <td>India</td>
      <td>software development and IT</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>65000.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>36.0</td>
      <td>5a7394f24292cb82b72adb702886543a</td>
      <td>8bc7997217d4a57b22242471cc8d89ef</td>
      <td>60000.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>I haven't decided</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a startup</td>
      <td>NaN</td>
      <td>Full-Stack Web Developer,   Data Scientist</td>
      <td>from home</td>
      <td>Hindi</td>
      <td>single, never married</td>
      <td>100000.0</td>
      <td>24.0</td>
      <td>8af0c2b6da</td>
      <td>2017-04-03 09:43:53</td>
      <td>2017-04-03 09:39:38</td>
      <td>2017-04-03 09:54:39</td>
      <td>2017-04-03 09:43:57</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>bachelor's degree</td>
      <td>Communications</td>
      <td>25000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4166.666667</td>
    </tr>
  </tbody>
</table>
</div>




```python
india_outliers['EmploymentStatus'].value_counts()
```




    Employed for wages                      2
    Not working and not looking for work    1
    A stay-at-home parent or homemaker      1
    Not working but looking for work        1
    Unable to work                          1
    Name: EmploymentStatus, dtype: int64



It looks like neither of the participants attended a boot camp, and the employment status is "Unemployed" for most of them. It is not clear if the students spend the amount of money on learning or they misunderstood the question. We will remove the outliers.


```python
countries_top_four = countries_top_four.drop(india_outliers.index)
```


```python
import seaborn as sns

sns.boxplot(x='CountryLive', y='money_per_month', data=countries_top_four)
plt.title('Money Spent Per Month Per Country', fontsize=14)
plt.ylabel('Money per month (in US dollars)')
plt.xlabel('Country')
plt.show()
```


![png](output_37_0.png)


Let's isolate the outliers for US. 


```python
usa_outliers = countries_top_four[
    (countries_top_four['CountryLive'] == 'United States of America') & 
    (countries_top_four['money_per_month'] >= 6000)]
usa_outliers
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>AttendedBootcamp</th>
      <th>BootcampFinish</th>
      <th>BootcampLoanYesNo</th>
      <th>BootcampName</th>
      <th>BootcampRecommend</th>
      <th>ChildrenNumber</th>
      <th>CityPopulation</th>
      <th>CodeEventConferences</th>
      <th>CodeEventDjangoGirls</th>
      <th>CodeEventFCC</th>
      <th>CodeEventGameJam</th>
      <th>CodeEventGirlDev</th>
      <th>CodeEventHackathons</th>
      <th>CodeEventMeetup</th>
      <th>CodeEventNodeSchool</th>
      <th>CodeEventNone</th>
      <th>CodeEventOther</th>
      <th>CodeEventRailsBridge</th>
      <th>CodeEventRailsGirls</th>
      <th>CodeEventStartUpWknd</th>
      <th>CodeEventWkdBootcamps</th>
      <th>CodeEventWomenCode</th>
      <th>CodeEventWorkshops</th>
      <th>CommuteTime</th>
      <th>CountryCitizen</th>
      <th>CountryLive</th>
      <th>EmploymentField</th>
      <th>EmploymentFieldOther</th>
      <th>EmploymentStatus</th>
      <th>EmploymentStatusOther</th>
      <th>ExpectedEarning</th>
      <th>FinanciallySupporting</th>
      <th>FirstDevJob</th>
      <th>Gender</th>
      <th>GenderOther</th>
      <th>HasChildren</th>
      <th>HasDebt</th>
      <th>HasFinancialDependents</th>
      <th>HasHighSpdInternet</th>
      <th>HasHomeMortgage</th>
      <th>HasServedInMilitary</th>
      <th>HasStudentDebt</th>
      <th>HomeMortgageOwe</th>
      <th>HoursLearning</th>
      <th>ID.x</th>
      <th>ID.y</th>
      <th>Income</th>
      <th>IsEthnicMinority</th>
      <th>IsReceiveDisabilitiesBenefits</th>
      <th>IsSoftwareDev</th>
      <th>IsUnderEmployed</th>
      <th>JobApplyWhen</th>
      <th>JobInterestBackEnd</th>
      <th>JobInterestDataEngr</th>
      <th>JobInterestDataSci</th>
      <th>JobInterestDevOps</th>
      <th>JobInterestFrontEnd</th>
      <th>JobInterestFullStack</th>
      <th>JobInterestGameDev</th>
      <th>JobInterestInfoSec</th>
      <th>JobInterestMobile</th>
      <th>JobInterestOther</th>
      <th>JobInterestProjMngr</th>
      <th>JobInterestQAEngr</th>
      <th>JobInterestUX</th>
      <th>JobPref</th>
      <th>JobRelocateYesNo</th>
      <th>JobRoleInterest</th>
      <th>JobWherePref</th>
      <th>LanguageAtHome</th>
      <th>MaritalStatus</th>
      <th>MoneyForLearning</th>
      <th>MonthsProgramming</th>
      <th>NetworkID</th>
      <th>Part1EndTime</th>
      <th>Part1StartTime</th>
      <th>Part2EndTime</th>
      <th>Part2StartTime</th>
      <th>PodcastChangeLog</th>
      <th>PodcastCodeNewbie</th>
      <th>PodcastCodePen</th>
      <th>PodcastDevTea</th>
      <th>PodcastDotNET</th>
      <th>PodcastGiantRobots</th>
      <th>PodcastJSAir</th>
      <th>PodcastJSJabber</th>
      <th>PodcastNone</th>
      <th>PodcastOther</th>
      <th>PodcastProgThrowdown</th>
      <th>PodcastRubyRogues</th>
      <th>PodcastSEDaily</th>
      <th>PodcastSERadio</th>
      <th>PodcastShopTalk</th>
      <th>PodcastTalkPython</th>
      <th>PodcastTheWebAhead</th>
      <th>ResourceCodecademy</th>
      <th>ResourceCodeWars</th>
      <th>ResourceCoursera</th>
      <th>ResourceCSS</th>
      <th>ResourceEdX</th>
      <th>ResourceEgghead</th>
      <th>ResourceFCC</th>
      <th>ResourceHackerRank</th>
      <th>ResourceKA</th>
      <th>ResourceLynda</th>
      <th>ResourceMDN</th>
      <th>ResourceOdinProj</th>
      <th>ResourceOther</th>
      <th>ResourcePluralSight</th>
      <th>ResourceSkillcrush</th>
      <th>ResourceSO</th>
      <th>ResourceTreehouse</th>
      <th>ResourceUdacity</th>
      <th>ResourceUdemy</th>
      <th>ResourceW3S</th>
      <th>SchoolDegree</th>
      <th>SchoolMajor</th>
      <th>StudentDebtOwe</th>
      <th>YouTubeCodeCourse</th>
      <th>YouTubeCodingTrain</th>
      <th>YouTubeCodingTut360</th>
      <th>YouTubeComputerphile</th>
      <th>YouTubeDerekBanas</th>
      <th>YouTubeDevTips</th>
      <th>YouTubeEngineeredTruth</th>
      <th>YouTubeFCC</th>
      <th>YouTubeFunFunFunction</th>
      <th>YouTubeGoogleDev</th>
      <th>YouTubeLearnCode</th>
      <th>YouTubeLevelUpTuts</th>
      <th>YouTubeMIT</th>
      <th>YouTubeMozillaHacks</th>
      <th>YouTubeOther</th>
      <th>YouTubeSimplilearn</th>
      <th>YouTubeTheNewBoston</th>
      <th>money_per_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>718</th>
      <td>26.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>The Coding Boot Camp at UCLA Extension</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>architecture or physical engineering</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>50000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>35.0</td>
      <td>796ae14c2acdee36eebc250a252abdaf</td>
      <td>d9e44d73057fa5d322a071adc744bf07</td>
      <td>44500.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>Within the next 6 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>work for a startup</td>
      <td>1.0</td>
      <td>User Experience Designer, Full-Stack Web Dev...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>single, never married</td>
      <td>8000.0</td>
      <td>1.0</td>
      <td>50dab3f716</td>
      <td>2017-03-09 21:26:35</td>
      <td>2017-03-09 21:21:58</td>
      <td>2017-03-09 21:29:10</td>
      <td>2017-03-09 21:26:39</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Architecture</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8000.000000</td>
    </tr>
    <tr>
      <th>1222</th>
      <td>32.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>The Iron Yard</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working and not looking for work</td>
      <td>NaN</td>
      <td>50000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>50.0</td>
      <td>bfabebb4293ac002d26a1397d00c7443</td>
      <td>590f0be70e80f1daf5a23eb7f4a72a3d</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>work for a nonprofit</td>
      <td>1.0</td>
      <td>Front-End Web Developer,   Mobile Developer,...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>single, never married</td>
      <td>13000.0</td>
      <td>2.0</td>
      <td>e512c4bdd0</td>
      <td>2017-03-10 02:14:11</td>
      <td>2017-03-10 02:10:07</td>
      <td>2017-03-10 02:15:32</td>
      <td>2017-03-10 02:14:16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Anthropology</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6500.000000</td>
    </tr>
    <tr>
      <th>3184</th>
      <td>34.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>We Can Code IT</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Less than 15 minutes</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>software development and IT</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>60000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10.0</td>
      <td>5d4889491d9d25a255e57fd1c0022458</td>
      <td>585e8f8b9a838ef1abbe8c6f1891c048</td>
      <td>40000.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>I haven't decided</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>work for a medium-sized company</td>
      <td>0.0</td>
      <td>Quality Assurance Engineer,   DevOps / SysAd...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>single, never married</td>
      <td>9000.0</td>
      <td>1.0</td>
      <td>e7bebaabd4</td>
      <td>2017-03-11 23:34:16</td>
      <td>2017-03-11 23:31:17</td>
      <td>2017-03-11 23:36:02</td>
      <td>2017-03-11 23:34:21</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>some college credit, no degree</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9000.000000</td>
    </tr>
    <tr>
      <th>3930</th>
      <td>31.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working and not looking for work</td>
      <td>NaN</td>
      <td>100000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>50.0</td>
      <td>e1d790033545934fbe5bb5b60e368cd9</td>
      <td>7cf1e41682462c42ce48029abf77d43c</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a startup</td>
      <td>1.0</td>
      <td>DevOps / SysAdmin,   Front-End Web Developer...</td>
      <td>no preference</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>65000.0</td>
      <td>6.0</td>
      <td>75759e5a1c</td>
      <td>2017-03-13 10:06:46</td>
      <td>2017-03-13 09:56:13</td>
      <td>2017-03-13 10:10:00</td>
      <td>2017-03-13 10:06:50</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>reactivex.io/learnrx/ &amp; jafar husain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Biology</td>
      <td>40000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>various conf presentations</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10833.333333</td>
    </tr>
    <tr>
      <th>6805</th>
      <td>46.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Sabio.la</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>70000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>45.0</td>
      <td>69096aacf4245694303cf8f7ce68a63f</td>
      <td>4c56f82a348836e76dd90d18a3d5ed88</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>1.0</td>
      <td>Full-Stack Web Developer, Game Developer,   Pr...</td>
      <td>no preference</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>15000.0</td>
      <td>1.0</td>
      <td>53d13b58e9</td>
      <td>2017-03-21 20:13:08</td>
      <td>2017-03-21 20:10:25</td>
      <td>2017-03-21 20:14:36</td>
      <td>2017-03-21 20:13:11</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>bachelor's degree</td>
      <td>Business Administration and Management</td>
      <td>45000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15000.000000</td>
    </tr>
    <tr>
      <th>7198</th>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>education</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>55000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>4.0</td>
      <td>cb2754165344e6be79da8a4c76bf3917</td>
      <td>272219fbd28a3a7562cb1d778e482e1e</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>I'm already applying</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>0.0</td>
      <td>Full-Stack Web Developer, Back-End Web Developer</td>
      <td>no preference</td>
      <td>Spanish</td>
      <td>single, never married</td>
      <td>70000.0</td>
      <td>5.0</td>
      <td>439a4adaf6</td>
      <td>2017-03-23 01:37:46</td>
      <td>2017-03-23 01:35:01</td>
      <td>2017-03-23 01:39:37</td>
      <td>2017-03-23 01:37:49</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>professional degree (MBA, MD, JD, etc.)</td>
      <td>Computer Science</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>14000.000000</td>
    </tr>
    <tr>
      <th>7505</th>
      <td>26.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>Codeup</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>65000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>40.0</td>
      <td>657fb50800bcc99a07caf52387f67fbb</td>
      <td>ad1df4669883d8f628f0b5598a4c5c45</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a government</td>
      <td>1.0</td>
      <td>Mobile Developer, Full-Stack Web Developer, ...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>single, never married</td>
      <td>20000.0</td>
      <td>3.0</td>
      <td>96e254de36</td>
      <td>2017-03-24 03:26:09</td>
      <td>2017-03-24 03:23:02</td>
      <td>2017-03-24 03:27:47</td>
      <td>2017-03-24 03:26:14</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>bachelor's degree</td>
      <td>Economics</td>
      <td>20000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6666.666667</td>
    </tr>
    <tr>
      <th>9778</th>
      <td>33.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>Grand Circus</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>education</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>55000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>40.0</td>
      <td>7a62790f6ded15e26d5f429b8a4d1095</td>
      <td>98eeee1aa81ba70b2ab288bf4b63d703</td>
      <td>20000.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>Within the next 6 months</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>work for a medium-sized company</td>
      <td>NaN</td>
      <td>Full-Stack Web Developer, Data Engineer,   Qua...</td>
      <td>from home</td>
      <td>English</td>
      <td>single, never married</td>
      <td>8000.0</td>
      <td>1.0</td>
      <td>ea80a3b15e</td>
      <td>2017-04-05 19:48:12</td>
      <td>2017-04-05 19:40:19</td>
      <td>2017-04-05 19:49:44</td>
      <td>2017-04-05 19:49:03</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>master's degree (non-professional)</td>
      <td>Chemical Engineering</td>
      <td>45000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8000.000000</td>
    </tr>
    <tr>
      <th>16650</th>
      <td>29.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>400000.0</td>
      <td>40.0</td>
      <td>e1925d408c973b91cf3e9a9285238796</td>
      <td>7e9e3c31a3dc2cafe3a09269398c4de8</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>I'm already applying</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>1.0</td>
      <td>Product Manager, Data Engineer, Full-Stack W...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>200000.0</td>
      <td>12.0</td>
      <td>1a45f4a3ef</td>
      <td>2017-03-14 02:42:57</td>
      <td>2017-03-14 02:40:10</td>
      <td>2017-03-14 02:45:55</td>
      <td>2017-03-14 02:43:05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>associate's degree</td>
      <td>Computer Programming</td>
      <td>30000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>16666.666667</td>
    </tr>
    <tr>
      <th>16997</th>
      <td>27.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>health care</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>60000.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>female</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>12.0</td>
      <td>624914ce07c296c866c9e16a14dc01c7</td>
      <td>6384a1e576caf4b6b9339fe496a51f1f</td>
      <td>40000.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Within 7 to 12 months</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>work for a medium-sized company</td>
      <td>1.0</td>
      <td>Mobile Developer, Game Developer,   User Exp...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>single, never married</td>
      <td>12500.0</td>
      <td>1.0</td>
      <td>ad1a21217c</td>
      <td>2017-03-20 05:43:28</td>
      <td>2017-03-20 05:40:08</td>
      <td>2017-03-20 05:45:28</td>
      <td>2017-03-20 05:43:32</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>some college credit, no degree</td>
      <td>NaN</td>
      <td>12500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12500.000000</td>
    </tr>
    <tr>
      <th>17231</th>
      <td>50.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>less than 100,000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Kenya</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>40000.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>female</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>d4bc6ae775b20816fcd41048ef75417c</td>
      <td>606749cd07b124234ab6dff81b324c02</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a nonprofit</td>
      <td>0.0</td>
      <td>Front-End Web Developer</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>30000.0</td>
      <td>2.0</td>
      <td>38c1b478d0</td>
      <td>2017-03-24 18:48:23</td>
      <td>2017-03-24 18:46:01</td>
      <td>2017-03-24 18:51:20</td>
      <td>2017-03-24 18:48:27</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Computer Programming</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15000.000000</td>
    </tr>
  </tbody>
</table>
</div>



We will remove the rows with no boot camps attended.


```python
usa_no_bootcamp = countries_top_four[
    (countries_top_four['CountryLive'] == 'United States of America') &
    (countries_top_four['money_per_month'] >= 6000) &
    (countries_top_four['AttendedBootcamp'] == 0)]

countries_top_four = countries_top_four.drop(usa_no_bootcamp.index)

usa_no_bootcamp
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>AttendedBootcamp</th>
      <th>BootcampFinish</th>
      <th>BootcampLoanYesNo</th>
      <th>BootcampName</th>
      <th>BootcampRecommend</th>
      <th>ChildrenNumber</th>
      <th>CityPopulation</th>
      <th>CodeEventConferences</th>
      <th>CodeEventDjangoGirls</th>
      <th>CodeEventFCC</th>
      <th>CodeEventGameJam</th>
      <th>CodeEventGirlDev</th>
      <th>CodeEventHackathons</th>
      <th>CodeEventMeetup</th>
      <th>CodeEventNodeSchool</th>
      <th>CodeEventNone</th>
      <th>CodeEventOther</th>
      <th>CodeEventRailsBridge</th>
      <th>CodeEventRailsGirls</th>
      <th>CodeEventStartUpWknd</th>
      <th>CodeEventWkdBootcamps</th>
      <th>CodeEventWomenCode</th>
      <th>CodeEventWorkshops</th>
      <th>CommuteTime</th>
      <th>CountryCitizen</th>
      <th>CountryLive</th>
      <th>EmploymentField</th>
      <th>EmploymentFieldOther</th>
      <th>EmploymentStatus</th>
      <th>EmploymentStatusOther</th>
      <th>ExpectedEarning</th>
      <th>FinanciallySupporting</th>
      <th>FirstDevJob</th>
      <th>Gender</th>
      <th>GenderOther</th>
      <th>HasChildren</th>
      <th>HasDebt</th>
      <th>HasFinancialDependents</th>
      <th>HasHighSpdInternet</th>
      <th>HasHomeMortgage</th>
      <th>HasServedInMilitary</th>
      <th>HasStudentDebt</th>
      <th>HomeMortgageOwe</th>
      <th>HoursLearning</th>
      <th>ID.x</th>
      <th>ID.y</th>
      <th>Income</th>
      <th>IsEthnicMinority</th>
      <th>IsReceiveDisabilitiesBenefits</th>
      <th>IsSoftwareDev</th>
      <th>IsUnderEmployed</th>
      <th>JobApplyWhen</th>
      <th>JobInterestBackEnd</th>
      <th>JobInterestDataEngr</th>
      <th>JobInterestDataSci</th>
      <th>JobInterestDevOps</th>
      <th>JobInterestFrontEnd</th>
      <th>JobInterestFullStack</th>
      <th>JobInterestGameDev</th>
      <th>JobInterestInfoSec</th>
      <th>JobInterestMobile</th>
      <th>JobInterestOther</th>
      <th>JobInterestProjMngr</th>
      <th>JobInterestQAEngr</th>
      <th>JobInterestUX</th>
      <th>JobPref</th>
      <th>JobRelocateYesNo</th>
      <th>JobRoleInterest</th>
      <th>JobWherePref</th>
      <th>LanguageAtHome</th>
      <th>MaritalStatus</th>
      <th>MoneyForLearning</th>
      <th>MonthsProgramming</th>
      <th>NetworkID</th>
      <th>Part1EndTime</th>
      <th>Part1StartTime</th>
      <th>Part2EndTime</th>
      <th>Part2StartTime</th>
      <th>PodcastChangeLog</th>
      <th>PodcastCodeNewbie</th>
      <th>PodcastCodePen</th>
      <th>PodcastDevTea</th>
      <th>PodcastDotNET</th>
      <th>PodcastGiantRobots</th>
      <th>PodcastJSAir</th>
      <th>PodcastJSJabber</th>
      <th>PodcastNone</th>
      <th>PodcastOther</th>
      <th>PodcastProgThrowdown</th>
      <th>PodcastRubyRogues</th>
      <th>PodcastSEDaily</th>
      <th>PodcastSERadio</th>
      <th>PodcastShopTalk</th>
      <th>PodcastTalkPython</th>
      <th>PodcastTheWebAhead</th>
      <th>ResourceCodecademy</th>
      <th>ResourceCodeWars</th>
      <th>ResourceCoursera</th>
      <th>ResourceCSS</th>
      <th>ResourceEdX</th>
      <th>ResourceEgghead</th>
      <th>ResourceFCC</th>
      <th>ResourceHackerRank</th>
      <th>ResourceKA</th>
      <th>ResourceLynda</th>
      <th>ResourceMDN</th>
      <th>ResourceOdinProj</th>
      <th>ResourceOther</th>
      <th>ResourcePluralSight</th>
      <th>ResourceSkillcrush</th>
      <th>ResourceSO</th>
      <th>ResourceTreehouse</th>
      <th>ResourceUdacity</th>
      <th>ResourceUdemy</th>
      <th>ResourceW3S</th>
      <th>SchoolDegree</th>
      <th>SchoolMajor</th>
      <th>StudentDebtOwe</th>
      <th>YouTubeCodeCourse</th>
      <th>YouTubeCodingTrain</th>
      <th>YouTubeCodingTut360</th>
      <th>YouTubeComputerphile</th>
      <th>YouTubeDerekBanas</th>
      <th>YouTubeDevTips</th>
      <th>YouTubeEngineeredTruth</th>
      <th>YouTubeFCC</th>
      <th>YouTubeFunFunFunction</th>
      <th>YouTubeGoogleDev</th>
      <th>YouTubeLearnCode</th>
      <th>YouTubeLevelUpTuts</th>
      <th>YouTubeMIT</th>
      <th>YouTubeMozillaHacks</th>
      <th>YouTubeOther</th>
      <th>YouTubeSimplilearn</th>
      <th>YouTubeTheNewBoston</th>
      <th>money_per_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3930</th>
      <td>31.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>between 100,000 and 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working and not looking for work</td>
      <td>NaN</td>
      <td>100000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>50.0</td>
      <td>e1d790033545934fbe5bb5b60e368cd9</td>
      <td>7cf1e41682462c42ce48029abf77d43c</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a startup</td>
      <td>1.0</td>
      <td>DevOps / SysAdmin,   Front-End Web Developer...</td>
      <td>no preference</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>65000.0</td>
      <td>6.0</td>
      <td>75759e5a1c</td>
      <td>2017-03-13 10:06:46</td>
      <td>2017-03-13 09:56:13</td>
      <td>2017-03-13 10:10:00</td>
      <td>2017-03-13 10:06:50</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>reactivex.io/learnrx/ &amp; jafar husain</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Biology</td>
      <td>40000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>various conf presentations</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10833.333333</td>
    </tr>
    <tr>
      <th>7198</th>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>education</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>55000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>4.0</td>
      <td>cb2754165344e6be79da8a4c76bf3917</td>
      <td>272219fbd28a3a7562cb1d778e482e1e</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>I'm already applying</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>0.0</td>
      <td>Full-Stack Web Developer, Back-End Web Developer</td>
      <td>no preference</td>
      <td>Spanish</td>
      <td>single, never married</td>
      <td>70000.0</td>
      <td>5.0</td>
      <td>439a4adaf6</td>
      <td>2017-03-23 01:37:46</td>
      <td>2017-03-23 01:35:01</td>
      <td>2017-03-23 01:39:37</td>
      <td>2017-03-23 01:37:49</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>professional degree (MBA, MD, JD, etc.)</td>
      <td>Computer Science</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>14000.000000</td>
    </tr>
    <tr>
      <th>16650</th>
      <td>29.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>400000.0</td>
      <td>40.0</td>
      <td>e1925d408c973b91cf3e9a9285238796</td>
      <td>7e9e3c31a3dc2cafe3a09269398c4de8</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>I'm already applying</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a multinational corporation</td>
      <td>1.0</td>
      <td>Product Manager, Data Engineer, Full-Stack W...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>200000.0</td>
      <td>12.0</td>
      <td>1a45f4a3ef</td>
      <td>2017-03-14 02:42:57</td>
      <td>2017-03-14 02:40:10</td>
      <td>2017-03-14 02:45:55</td>
      <td>2017-03-14 02:43:05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>associate's degree</td>
      <td>Computer Programming</td>
      <td>30000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>16666.666667</td>
    </tr>
    <tr>
      <th>16997</th>
      <td>27.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>more than 1 million</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15 to 29 minutes</td>
      <td>United States of America</td>
      <td>United States of America</td>
      <td>health care</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>60000.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>female</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>12.0</td>
      <td>624914ce07c296c866c9e16a14dc01c7</td>
      <td>6384a1e576caf4b6b9339fe496a51f1f</td>
      <td>40000.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Within 7 to 12 months</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>work for a medium-sized company</td>
      <td>1.0</td>
      <td>Mobile Developer, Game Developer,   User Exp...</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>single, never married</td>
      <td>12500.0</td>
      <td>1.0</td>
      <td>ad1a21217c</td>
      <td>2017-03-20 05:43:28</td>
      <td>2017-03-20 05:40:08</td>
      <td>2017-03-20 05:45:28</td>
      <td>2017-03-20 05:43:32</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>some college credit, no degree</td>
      <td>NaN</td>
      <td>12500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12500.000000</td>
    </tr>
    <tr>
      <th>17231</th>
      <td>50.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>less than 100,000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Kenya</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not working but looking for work</td>
      <td>NaN</td>
      <td>40000.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>female</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>d4bc6ae775b20816fcd41048ef75417c</td>
      <td>606749cd07b124234ab6dff81b324c02</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>Within the next 6 months</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>work for a nonprofit</td>
      <td>0.0</td>
      <td>Front-End Web Developer</td>
      <td>in an office with other developers</td>
      <td>English</td>
      <td>married or domestic partnership</td>
      <td>30000.0</td>
      <td>2.0</td>
      <td>38c1b478d0</td>
      <td>2017-03-24 18:48:23</td>
      <td>2017-03-24 18:46:01</td>
      <td>2017-03-24 18:51:20</td>
      <td>2017-03-24 18:48:27</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>bachelor's degree</td>
      <td>Computer Programming</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15000.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
import seaborn as sns

sns.boxplot(x='CountryLive', y='money_per_month', data=countries_top_four)
plt.title('Money Spent Per Month Per Country', fontsize=14)
plt.ylabel('Money per month (in US dollars)')
plt.xlabel('Country')
plt.show()
```


![png](output_42_0.png)



```python
canada_outlier = countries_top_four[
    (countries_top_four['CountryLive'] == 'Canada') &
    (countries_top_four['money_per_month'] > 4000)
]
canada_outlier
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>AttendedBootcamp</th>
      <th>BootcampFinish</th>
      <th>BootcampLoanYesNo</th>
      <th>BootcampName</th>
      <th>BootcampRecommend</th>
      <th>ChildrenNumber</th>
      <th>CityPopulation</th>
      <th>CodeEventConferences</th>
      <th>CodeEventDjangoGirls</th>
      <th>CodeEventFCC</th>
      <th>CodeEventGameJam</th>
      <th>CodeEventGirlDev</th>
      <th>CodeEventHackathons</th>
      <th>CodeEventMeetup</th>
      <th>CodeEventNodeSchool</th>
      <th>CodeEventNone</th>
      <th>CodeEventOther</th>
      <th>CodeEventRailsBridge</th>
      <th>CodeEventRailsGirls</th>
      <th>CodeEventStartUpWknd</th>
      <th>CodeEventWkdBootcamps</th>
      <th>CodeEventWomenCode</th>
      <th>CodeEventWorkshops</th>
      <th>CommuteTime</th>
      <th>CountryCitizen</th>
      <th>CountryLive</th>
      <th>EmploymentField</th>
      <th>EmploymentFieldOther</th>
      <th>EmploymentStatus</th>
      <th>EmploymentStatusOther</th>
      <th>ExpectedEarning</th>
      <th>FinanciallySupporting</th>
      <th>FirstDevJob</th>
      <th>Gender</th>
      <th>GenderOther</th>
      <th>HasChildren</th>
      <th>HasDebt</th>
      <th>HasFinancialDependents</th>
      <th>HasHighSpdInternet</th>
      <th>HasHomeMortgage</th>
      <th>HasServedInMilitary</th>
      <th>HasStudentDebt</th>
      <th>HomeMortgageOwe</th>
      <th>HoursLearning</th>
      <th>ID.x</th>
      <th>ID.y</th>
      <th>Income</th>
      <th>IsEthnicMinority</th>
      <th>IsReceiveDisabilitiesBenefits</th>
      <th>IsSoftwareDev</th>
      <th>IsUnderEmployed</th>
      <th>JobApplyWhen</th>
      <th>JobInterestBackEnd</th>
      <th>JobInterestDataEngr</th>
      <th>JobInterestDataSci</th>
      <th>JobInterestDevOps</th>
      <th>JobInterestFrontEnd</th>
      <th>JobInterestFullStack</th>
      <th>JobInterestGameDev</th>
      <th>JobInterestInfoSec</th>
      <th>JobInterestMobile</th>
      <th>JobInterestOther</th>
      <th>JobInterestProjMngr</th>
      <th>JobInterestQAEngr</th>
      <th>JobInterestUX</th>
      <th>JobPref</th>
      <th>JobRelocateYesNo</th>
      <th>JobRoleInterest</th>
      <th>JobWherePref</th>
      <th>LanguageAtHome</th>
      <th>MaritalStatus</th>
      <th>MoneyForLearning</th>
      <th>MonthsProgramming</th>
      <th>NetworkID</th>
      <th>Part1EndTime</th>
      <th>Part1StartTime</th>
      <th>Part2EndTime</th>
      <th>Part2StartTime</th>
      <th>PodcastChangeLog</th>
      <th>PodcastCodeNewbie</th>
      <th>PodcastCodePen</th>
      <th>PodcastDevTea</th>
      <th>PodcastDotNET</th>
      <th>PodcastGiantRobots</th>
      <th>PodcastJSAir</th>
      <th>PodcastJSJabber</th>
      <th>PodcastNone</th>
      <th>PodcastOther</th>
      <th>PodcastProgThrowdown</th>
      <th>PodcastRubyRogues</th>
      <th>PodcastSEDaily</th>
      <th>PodcastSERadio</th>
      <th>PodcastShopTalk</th>
      <th>PodcastTalkPython</th>
      <th>PodcastTheWebAhead</th>
      <th>ResourceCodecademy</th>
      <th>ResourceCodeWars</th>
      <th>ResourceCoursera</th>
      <th>ResourceCSS</th>
      <th>ResourceEdX</th>
      <th>ResourceEgghead</th>
      <th>ResourceFCC</th>
      <th>ResourceHackerRank</th>
      <th>ResourceKA</th>
      <th>ResourceLynda</th>
      <th>ResourceMDN</th>
      <th>ResourceOdinProj</th>
      <th>ResourceOther</th>
      <th>ResourcePluralSight</th>
      <th>ResourceSkillcrush</th>
      <th>ResourceSO</th>
      <th>ResourceTreehouse</th>
      <th>ResourceUdacity</th>
      <th>ResourceUdemy</th>
      <th>ResourceW3S</th>
      <th>SchoolDegree</th>
      <th>SchoolMajor</th>
      <th>StudentDebtOwe</th>
      <th>YouTubeCodeCourse</th>
      <th>YouTubeCodingTrain</th>
      <th>YouTubeCodingTut360</th>
      <th>YouTubeComputerphile</th>
      <th>YouTubeDerekBanas</th>
      <th>YouTubeDevTips</th>
      <th>YouTubeEngineeredTruth</th>
      <th>YouTubeFCC</th>
      <th>YouTubeFunFunFunction</th>
      <th>YouTubeGoogleDev</th>
      <th>YouTubeLearnCode</th>
      <th>YouTubeLevelUpTuts</th>
      <th>YouTubeMIT</th>
      <th>YouTubeMozillaHacks</th>
      <th>YouTubeOther</th>
      <th>YouTubeSimplilearn</th>
      <th>YouTubeTheNewBoston</th>
      <th>money_per_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13659</th>
      <td>24.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Bloc.io</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>more than 1 million</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>30 to 44 minutes</td>
      <td>Canada</td>
      <td>Canada</td>
      <td>finance</td>
      <td>NaN</td>
      <td>Employed for wages</td>
      <td>NaN</td>
      <td>60000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>250000.0</td>
      <td>10.0</td>
      <td>739b584aef0541450c1f713b82025181</td>
      <td>28381a455ab25cc2a118d78af44d8749</td>
      <td>140000.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>I haven't decided</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>work for a multinational corporation</td>
      <td>NaN</td>
      <td>Mobile Developer, Full-Stack Web Developer, ...</td>
      <td>from home</td>
      <td>Yue (Cantonese) Chinese</td>
      <td>single, never married</td>
      <td>10000.0</td>
      <td>2.0</td>
      <td>41c26f2932</td>
      <td>2017-03-25 23:23:03</td>
      <td>2017-03-25 23:20:33</td>
      <td>2017-03-25 23:24:34</td>
      <td>2017-03-25 23:23:06</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>bachelor's degree</td>
      <td>Finance</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# recompute the mean for each country
countries_top_four.groupby('CountryLive').mean()['money_per_month'].sort_values(ascending=False)
```




    CountryLive
    United States of America    160.532509
    Canada                      113.510961
    India                        65.758763
    United Kingdom               45.534443
    Name: money_per_month, dtype: float64



### Choosing the Two Best Markets
Considering the results we've found so far, one country we should advertise in is the USA. Many new coders are living in the USA and they are willing to pay a good amount of money each month. 

We need to choose the best second country to invest in advertisement.

We sell a subscription for \&59 per month. Our analysis result shows that people from the US, Canada, and India are willing to spend, on average, more than 59 US dollars.


```python
countries_top_four['CountryLive'].value_counts(normalize=True) * 100
```




    United States of America    74.987186
    India                       11.711943
    United Kingdom               7.150179
    Canada                       6.150692
    Name: CountryLive, dtype: float64



Canada shows a higher potential to pay for learning, but we have more Indian students, and then India is a large population country. We could consider splitting the investment amount unequally between USA and India, or between the USA and Canada.

At this point would be better to send our investigation results to the marketing team and let them use their domain knowledge for the best decision.

### Conclusion
In this project, we analyzed survey data from new coders to find the best two markets to advertise in. The only solid conclusion we reached is that the US would be a good market for advertisement.

For the second-best market, it wasn't clear what to choose between India and Canada. We decided to send the results to the market team so they can use their domain knowledge to make the best decision. 

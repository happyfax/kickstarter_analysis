
# Kickstarter_Analysis

## **Project Overview:**  
This project analyzes how launch date and funding goals relate to outcomes for Kickstarter campaigns classified as Plays:Theater, the subcategory:Category with the largest number of outcomes.

## Purpose and Background:
The dataset presents a compilation of data regarding Goals, Pledged Donations, Outcomes, Dates Launched, Dates Ended, Project Duration, Staff Picks, Backers, Spotlight, Category, Subcategory, Percentage Funded, Average Donation, and Year of 4114 Kickstarter campaigns from 21 countries `AT AU BE CA CH DE DK ES FR GB HK IE IT LU MX NL NO NZ SE SG US` using `EUR AUD CAD CHF DKK GBP HKD MXN NOK NZD SEK SGD USD`.  Analaysis of related data reveals parameters for identifying which areas of Kickstarter campaigns are most and least effective in outcome and pledges given associated factors.  

## **Analysis and Challenges**

### Deliverable 1: Outcomes Based on Launch Date Chart
Column J = launched_at
Column I = deadline 

Column S: Date Created Conversion  
`=((((J2:J4115/60)/60)/24)+DATE(1970,1,1))`  
Column T: Date Ended Conversion  
```=(((((I2/60)/60)/24)+DATE(1970,1,1)))```  
*Columns S + T formatted to yyyy-mmm-dd to be legible to the =YEAR function*  
Column U: Year  
```=YEAR(S2:S4115)```  

> ***Challenges***  
Overcomplicated the Years category:  
Tried to translate the launch date number via   
=YEAR((((((J2/60)/60)/24)+DATE(1970,1,1))))+40150 and =((((K2/60)/60)/24)+DATE(1970,1,1))  
Tried to reference a character within an Excel formula after translating its output  
by outputting the result to a new cell, converting the cell, the "yyyy" within the output  
Discovered `=(((M4/60)/60)/24/25550) = 1/0/1900`  
Calculated the duration of the campaign using `=T2:T4115-S2:S4115` to find the 2mo|3mo mark have the most successes  

![Theater_Outcomes_vs_Launch](/rss/img/Theater_Outcomes_vs_Launch.png) 

### Deliverable 2: Outcomes Based on Goals

`=COUNTIFS('Kickstarter - Main'!$F:$F, "successful", 'Kickstarter - Main'!$D:$D,"<1000",'Kickstarter - Main'!$P:$P,"plays")`  
`=COUNTIFS('Kickstarter - Main'!$F:$F, "successful", 'Kickstarter - Main'!$D:$D,">=1000", 'Kickstarter - Main'!$D:$D,"<=4999",'Kickstarter - Main'!$P:$P,"plays")`  
*Added increments of 5000to9999, 10000to14999, 15000to19999, 20000to24999, 25000to29999, 30000to34999, 35000to39999, 40000to44999, 45000to49999, to>50000*    
`=COUNTIFS('Kickstarter - Main'!$F:$F, "successful", 'Kickstarter - Main'!$D:$D,">=50000", 'Kickstarter - Main'!$P:$P,"plays")`  

*same formula, criteria1 as "failed"*  
`=COUNTIFS('Kickstarter - Main'!$F:$F, "failed", 'Kickstarter - Main'!$D:$D,"<1000",'Kickstarter - Main'!$P:$P,"plays")`  

*criteria1 as "canceled"*  
`=COUNTIFS('Kickstarter - Main'!$F:$F,"canceled", 'Kickstarter - Main'!$D:$D,"<1000",'Kickstarter - Main'!$P:$P,"plays")`  

*B14:E14*  
B=#Successful  
C=#Failed  
D=#Canceled  
E=Total Projects  
`=SUM(B2:B13) =SUM(C2:C13) =SUM(D2:D13) =SUM(E2:E13)`

*F14:H14*  
F=%Successful  
G=%Failed  
H=%Canceled  
`=B2/E2 =C2/E2 =D2/E2`  

*Verified SUM B14:E14*    
`=COUNTIFS('Kickstarter - Main'!$F:$F,"successful",'Kickstarter - Main'!$P:$P,"plays")`  

> ***Possible Challenges***
Not declaring column values as absolute values ($)  
Linking between sheets  
Declaring top and bottom value of ranges separately  

![Outcomes_vs_Goals](/rss/img/Outcomes_vs_Goals.png)  

## **Results:**  

#### **Two conclusions that may be drawn by Theater Outcomes by Launch Date:**  
- [x] May was a good month for theater outcomes with a peak at 111 successful campaigns  
- [x] No one canceled their campaigns in October although the ratio of failing to succeeding campaigns was higher; successful and failed campaigns were equal on December.   
#### ***One conclusion that may be drawn by Outcomes Based on Goals:***  
- [x] The majority of campaigns (56%) are within the $1000 to $4999 Goal Funding range (with a standard deviation of 108 for Successful, 41 Failed, 148 total). The Goal funding range 45,000-49999 has the least number of campaigns; successes are inversely proportional to failures in relation to goal ranges.  
#### ***Dataset limitations:***
- [x] Limitations within this dataset include the range of data (up to 2017), constituencies/preferences/conditions of optimal cause for patrons to value, and the potential to map regional relations of backers to Kickstarter campaign locations, methods of asking for donations, or optimal incentivization, e.g. the consumer sciences of how fundraising initiatives are more likely to earn more money when asked for open donations rather than specific values.  The range of donations (highest-lowest distribution) amongst donors, to see if and where large donor interests pull the data set, and what is in common amongst their interests.  A possible addendum would be tags on genres that transcend the categories/subcategories, to be able to see if specific themes in the content of the work have any effect on patron interest, the number of collaborators in each project, the criteria for staff picks, if campaigns were relaunched, extent of outreach on campaign viewership in relation to pledged donations.  
#### **Other possible tables and/or graphs:**  
- [x] The pledged to average donation (displayed in the Patron Donation Distribution tab) displays how donation amounts are distributed to show the relation of funding to amount funded.  The resulting graph indicates that a larger amount of smaller average contributions on Kickstarter results in the highest total Pledged Donation Amount.  Within this set, the overall chart of successful campaigns filtered by staff picks appear to have similar distribution patterns, on which more successful campaigns (3842) that are not staff picks far outweigh campaigns that were failed but staff picks (66), which indicates that Staff Picks directly affect the success rate of a campaign (or the factors that make campaigns).   Different categories have different goal trends, and charting successful/failed/canceled campaign genre popularity within different countries would display which genres are prioritized or less incentivized in different areas.  Charting if various subcategories are more successful launched at different times, and if there are any trends that are similar across different Categories, and preferred funding ranges for different genres (or related possible factors such the success of specific musical subcategories per year in relation to billboard chart genre popularity, or leisure activities in different social contexts).  Comparing Kickstarter data to Patreon and other crowdfunding sources, although analyzing every microfactor of crowdfunding campaigns and patron characteristics as well as variables would reveal more information.  However, patronage and bourses function under entirely different factors than fields with fixed factors [^4].   
- [x] The results may also be supplemented by considering factors such as, the accessibility of the Kickstarter platform, regional needs on pandemic funding to creative industries, if specific categories have greater visibility and success for their campaigns due to social media influence or metrics.  If there is a relation of exposure, search engine metrics and spotlighted campaigns, it would be helpful to see how the data would change if all campaigns (both failed and successful) were given spotlights, over considerations as to if adding elements such as spotlight duration affects the earnings potential of a campaign.   Obvious stipulations need to be made that data does not necessarily indicate that theater is the highest absolute industry for Kickstarter campaigns, in relation to the proportional constituency actively involved in campaigns, or the patronage system of theater groups in need during the difficulties of the current extended x Wave in different countries international crisis situation.   
- [x] From an alternate perspective of pitching a Kickstarter campaign, the relation between viewership and patronage of different Categories with political affiliation would be relatively critical to advertise towards, the socological importance of affiliations as related to the way the brain processes identity, a relatively important way to market products and visual media given that advertising targeted to specific demographics are not artificially engineered and actually representative.  However, media that increasingly reaffirms a narrowing field of archetypes propagated by cultural isolationism and lack of diversity in largely homogenous communities risks becoming a "spiral of silence," which can stifle the freedom of dissent that is crucial to a healthily functioning democratic society [^1][^2][^3]  Stipulations need to be made that dataset is specific to those creating Kickstarter campaigns, and specific numbers do not necessarily indicate that theater is the highest fixed industry for Kickstarter campaigns in relation to the proportional constituency actively involved in campaigns, rather, can in the current context outside of the date field of the dataset, express the patronage system of theater groups and fields in need during the current crisis context. The content follows all appropriate necessary considerations etc.   
#### ***Addendum:***
- [x] The dataset's campaign name/description list relates to one of a large number of personal concepts towards working on implementing, in various community collaborations, a 1min Film Fest for many different local areas where a group of folks will distribute QR codes in the city recruiting submissions of one-minute stories or actions in any format (social media included) from local communities in NYC.  They can be arranged in either an order of the participants' choosing, or in a chronological order of submission.  Once all the participants have registered, they will have the freedom to choose their position in the video editing reel, as well as accompanying descriptions and title of project, and if desired, input and participation into the creative process.  I can program the framework of open entry and schedule.  Themes would be open choice can be assigned or randomly called if preferred.  If it ever becomes a recurrent event, it would be fun to play with the idea of shifting the submissions to reel a specific day of week (possibly even on different days of the week from a different time zone internationally) versions. Entrants will sign a form of artist release and affirming that their content follows basic guidelines of social awareness and receive a participant's certificat as well as rights to the project, safety protocols, and access to its formation. The length of the campaign will run two months tentatively.  The intention would be to perform outreach personally via nonprofit avenues, and to public housing.  There will be no locational tags (unless specifically requested) except in inception to target NYC/NYS. All related #initiatives attached.  Meetings on a bi-weekly basis and events on a monthly basis to connect, work, thank and appreciate participants in the project.  Eventually, to make or find a way to take the presentational pitch on the project, a tech rider, to administrations towards proposing being incorporated in BIPOC, Hispanic/Latinx, AAPI Film Festivals, to display it in a site specific professional setting with no artist name, or have a version to share with international local artist film festival organizers, as an experience.  Applications of appropriate strategies.  No referential concepts other than experience, observations, ideas, similar thinking, and similar events that I helped generate overseas. Can draft a website that can display the videos in a (due to personal programming limitations), a randomized array, list, or table; specific spots can be activated by the individual's choosing (e.g., if someone wants to push display their submission on the site from any location at the time of their choosing during a preliminary screening duration of the project, they can click on a web interface button.  All additional appropriate necessary considerations.  I have no expectations as to the outcome.  

[1] https://www.apa.org/monitor/2019/11/cover-politics  
[2] https://reports.weforum.org/human-implications-of-digital-media-2016/downsides-and-risks/  
[3] https://nautil.us/blog/-collective-intelligence-will-end-identity_based-politics  
[4] https://www.bloomberg.com/news/features/2018-05-03/the-gambler-who-cracked-the-horse-racing-code  
[5] Permutations of Awesome()  
[8] SituationsoftheFistSymbol.com
[7] If I don't make money, at least I'll make SmallChanges.com  
[6] Conceptual DigitalPillowFight (a href="www") Dedicated to the Original Mass Pillow Fight held in Seoul  
[10] https://expmag.com/2021/10/the-key-to-a-kinder-gentler-internet-capybaras/ !?  
[**♡**]        

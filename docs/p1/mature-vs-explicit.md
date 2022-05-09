# Using tags and word patterns to understand how the community understands mature vs explicit-rated fics

## Sections
1. [Motivation of analysis](#motivation-of-analysis)<br>
2. [Methods used and possible applications](#methods-used-and-possible-applications)<br>
3. [Findings](#findings)

## Motivation of analysis
There are [five possible author-given ratings for fanfiction on AO3](https://archiveofourown.org/faq/tutorial-posting-a-work-on-ao3?language_id=en#pwtrating)- <br>
- General Audiences: The content is unlikely to be disturbing to anyone, and is suitable for all ages. <br>
- Teen And Up Audiences: The content may be inappropriate for audiences under 13. <br>
- Mature: The content contains adult themes (sex, violence, etc) that aren't as graphic as explicit-rated content.<br>
- Explicit: The content contains explicit adult themes, such as porn, graphic violence, etc.<br>
- Not Rated - no rating was given by the author, but is treated like Mature and Explicit content in search functions, etc. <br>
<br>

What differentiates mature from explicit fics? Teen from mature? General audiences from teen? On the surface these seem like very trivial questions. However, I would like to emphasise that these are <b>author-given ratings</b>, there is no central authority board of fanfiction governors that assigns every fic a rating (like movies - they do that for movies, right?). <b> In other words, given this general set of guidelines, thousands of independent authors will have to self-assess their own work and decide on their own an appropriate rating for it. Arguably, if we see some clear patterning of differences between ratings, I would say we are observing pretty interesting behaviour; many independent actors coalescing together in general agreement of what an explicit fic typically stands for, what a mature fic stands for, and so on</b>.

## Methods used and possible applications
The first thing that comes to mind would definitely be to just build a n-grams model that classifies fics into their respective ratings, and then to examine the most important features for each class/rating. However, I was also interested in attempting to verify my findings over different types of analyses that cut across the dataset in different ways. Thus I sought to use more descriptive methods closer to the ones I've learned previously when studying statistics for psychology.

### 1. Kruskal-Wallis test between unigrams of fics from different ratings
<b>How it was applied to this dataset</b>: This analysis was chosen on the basis of [this paper](https://users.ics.aalto.fi/lijffijt/articles/lijffijt2015a.pdf). The Kruskal-Wallis test is a (loosely put) non-parametric equivalent of the well-known ANOVA. I kept 9916 unigrams that appeared in at least 250 fics and counted the number of times each unigram appeared in each fic. This count is standardised by the fic's word count. I then applied the Kruskal-Wallis test with the Holm-Bonferroni correction for multiple comparisons (9916 comparisons). This was followed by post-hoc Dunn tests with another Holm-Bonferroni correction (6 comparisons) to identify exactly where the differences in unigram usage lay between ratings.<br>
<br>
<b>Potential applications to other data</b>: This is a very general sort of analysis that can be applied to any text corpora. I have used it time and again as a first-step analysis to sieve out any interesting differences in word usage between certain user groups, communities, etc. 

### 2. Structural topic modeling (STM) with ratings as a covariate
<b>How it was applied to this dataset</b>: [STM is a topic modeling algorithm](https://www.structuraltopicmodel.com). However, unlike vanilla Latent Dirichlet Allocation, it can incorporate document-level covariates about each document into the modeling. The relationship between these covariates and topic prevalence and/or topic content/vocabulary can then be explored, with uncertainty estimates calculated. I used STM to build on the first analysis, as it compares between ratings at a topic-level instead of just at the word-level. This means I can derive an idea about the common topics/themes written about in my dataset, then check how the covariate (assigned rating) affects topic prevalence.<br>
<br>
<b>Potential applications to other data</b>: This again is a broadly applicable sort of analysis. It was actually built for [social science research](https://scholar.princeton.edu/files/bstewart/files/stmnips2013.pdf). I hence believe it would be immensely useful (way more so than the way I used it here) for any human-generated text data that comes with any user attributes.

### 3. Correspondence analysis (CA) between freeform tags and ratings
<b>How it was applied to this dataset</b>: CA explores the relationships between two sets of categorical variables (in a contingency table). In freeform tags of their fics, authors can freely write whatever they want, making it a good summary source of the contents of the fic. I used the AO3 metadata dump for this analysis, as that dataset comes with AO3's internal standardisation of common freeform tags (which isn't available information for my scrape). I narrowed it down to fics involving just Harry Potter/Draco Malfoy for a faster run-time, but we will see in Findings that even this specific selection appears to back up the findings from my scraped dataset in the earlier two analyses.<br>
<br>
<b>Potential applications to other data</b>: Yet again, this is another very general sort of analysis. It can be applied to any contingency table, so I think it would just be a matter of structuring/thinking about the given data as such. For example, the age bands of users as one variable, and their usage of certain sorts of content as another.

## Findings
In the original blogposts about each of these analyses, I made comparison between the ratings (dropping non-rated for the first two analyses). Here I will just focus on the differences observed between mature- and explicit-rated fics, since that was the question that first drove this line of analysis.

### Main finding tl;dr
Mature fics appear to focus relatively more on themes like crime, injury, and other serious themes like mental health. Explicit fics typically focus very strongly on smut/sex. This observation (1) holds across all three types of analyses, and (2) is possibly generalisable across fandoms - at the very least, it holds both in my scraped dataset of the Detroit: Become Human fandom, and the much more narrow dataset of Harry Potter/Draco Malfoy fanfics. Of course, this is not to say that explicit fics do not discuss serious themes at all. They simply trend as a group to focus much more on explicit sex, and the mature fics trend (more weakly, as we'll see) as a group to be addressing topics like crime and mental health.

### Findings per analysis
<b>Click on the images below to access the interactive versions of them.</b><br>

#### 1. Kruskal-Wallis test between unigrams of fics from different ratings.
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/05_kw/mature_n1.html">
    <img src="https://raw.githubusercontent.com/dru-r/portfolio/main/docs/p1/imgs/m-vs-e-kw.JPG" title="Click for interactive version" alt="Click for interactive version"/></a>
<br>
This visualisation shows the top-200 words significantly different between mature and explicit fics, where mature fics had the top mean rank (i.e., words were generally most used by mature fics). They are arranged based on H-statistic (which can be converted to an effect size to assess practical significance). The unigrams run from smallest to largest H-statistic (largest at the bottom).<br>
<br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/05_kw/explicit_n1.html">
    <img src="https://raw.githubusercontent.com/dru-r/portfolio/main/docs/p1/imgs/m-vs-e-kw2.JPG" title="Click for interactive version" alt="Click for interactive version"/></a>
<br>
This visualisation is read similarly to the previous one, except this one shows the top-200 words significantly different between mature and explicit fics, <b>where explicit fics had the top mean rank</b>.<br>
<br>
We see that mature fics focus significantly much more on violent-sounding unigrams (e.g., blood, pain, dead) than explicit fics. We notice as well that mature fics actually use female pronouns the most, generally, across all ratings, and explicit fics the least. This can perhaps be explained by the popularity of M/M fics in the fandom. Explicit fics focus on sex-related unigrams. We also note that the H-statistic (and thus eventual effect size) for these sex-related unigrams is much higher than the violent unigrams found in the mature-first chart. This means that sex is much more strongly characteristic of explicit fics, than crime/violence is for mature fics, though statistical significance holds for both analyses.

#### 2. Structural topic modeling (STM) with ratings as a covariate
<small> no interactive visualisation available here </small><br>
![image](https://dru-r.github.io/ao3-dbh-analysis/visuals/07_stm/mature-explicit.jpg)<br>
<br>
The image presents all 30 topics found by running STM in a topic prevalence comparison between the mature and explicit ratings. Lines around each dot represent the confidence interval. Dots further along the right are topics more characteristic of explicit fics, dots further along the left are topics more characteristic of mature fics. Dots lying in the middle are not significantly related to either topic. <br>
<br>
We see the smut topic as extremely characteristic of explicit fics. And we see the same conclusion as the unigram analysis, except now at the topic-level, for mature fics. Mature fics are more characterised by topics relating to android errors, crime cases, and injury, amongst others. We note again the same trend we saw in the unigram analysis; smut is very characteristic of explicit fics, to a degree that is much greater than crime/guns, etc. are for mature fics.

#### 3. Correspondence analysis (CA) between freeform tags and ratings
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/drarry/02_CA_freeform/asymmetricbiplot.html">
    <img src="https://dru-r.github.io/ao3-dbh-analysis/visuals/drarry/02_CA_freeform/asymmetricbiplot.png" title="Click for interactive version" alt="Click for interactive version"/></a>
<br>
This visualisation shows a 2D asymmetric biplot of CA conducted between Harry Potter/Draco Malfoy freeform tags and the five ratings. Based on the relative positions of the ratings, the first dimension (component 0) appears to capture the explicit vs general audience rating divide. This dimension also captures the majority of the variance (71.46%) in the data. However, the first dimension does not appear to represent mature fics well at all (it is very close to x=0). The second dimension (component 1) represents mature fics better; the arrow of the mature rating is at an extremely acute angle towards the y-axis. Explicit and mature fics are definitely not the same.<br>
<br>
Looking at tags that lie at an acute angle to the ratings of interest (mature/explicit; these represent tags strongly associated to the specific rating), we can see the same difference in association patterns that we saw in the unigram and STM analyses. Many sex-related tags lie at an acute angle to the explicit rating. On the other hand, we see tags like 'Detectives', 'Past Abuse', 'Past Torture', lying at an acute angle to the mature rating. 

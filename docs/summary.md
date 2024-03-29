## side-project summaries

### Main side-project: Analysis of fanfiction from archiveofourown.org (AO3)
<b>Background</b>: I've worked plenty with social media data. Online communities congregate around other mediums too, however. Fanfiction is one such medium, with a long history acting as one of the pillars for many fandoms. Reader/viewer perceptions of characters are described and shaped via these narratives, some ideas catch a spark and spread and grow into full-fledged tropes.<br><br>
Having been a contributer to various fandoms - in fanfiction and fanart - for many years, fandom in its form of fanfiction was the side-project I dreamt of doing when I first learned to work with code. It started as a way to practise the simplest Python, then basic analyses, and has now become a dataset that I revisit again and again whenever I want to try a method I've just read about.<br><br>
<b>Dataset</b>: This is a self-scraped dataset of 16,211 Detroit: Become Human (D:BH) AO3 fanfiction stories with public metadata and their 486,907 comments. This dataset is a complete snapshot of all the D:BH fanfiction available on AO3 in June 2020 (when the scrape was done).<br>
I also make reference to analyses done on the [data dump provided by AO3 in March 2021](https://archiveofourown.org/admin_posts/18804).<br>
#### Content
I highlight and tie together some analyses I've done before in write-ups below. You may also view the analyses in their entirety on [this project's Github page](https://dru-r.github.io/ao3-dbh-analysis/) and [its Tumblr](https://program-800.tumblr.com).
1. [Details of the scrape process](/p1/ao3-dbh-scrape.md)<br>
2. [Using tags and word patterns to understand how the community understands mature vs explicit-rated fics](/p1/mature-vs-explicit.md)<br>
3. [Making use of tags to understand characterisation and tropes](/p1/tag-usage.md)<br>
4. [Understanding characters via dialogue and actions - WIP](/p1/dialog-actions.md)<br>

### Other side-projects
#### 1. Analysis of FFXIV-related subreddits
<b>Background</b>:  While fanfiction is my core interest, it does lack the high interactivity between commenters often seen in typical online communities on social media. Reddit’s comment tree structure makes it amenable to such explorations. The shorter text (unlike fanfiction’s long-form) also makes it more amenable as a quicker testbed for new text analysis methods I come across. <br><br>
<b>Dataset</b>: This dataset was retrieved via Pushshift API. It consists of posts and comments from the r/FFXIV, r/ShitpostXIV, and r/ffxivdiscussion subs, running from just before the release on Endwalker on 7 December 2021 to sometime in 20 May 2022. Specifically, there are 46547 posts and 1504706 comments from r/FFXIV, 6781 posts and 141204 comments from r/ShitpostXIV, and 1234 posts and 97270 comments from r/ffxivdiscussion. <br>
At the time of the pull, I noted a few shards from Pushshift were down (e.g., 20 out of 24), so there may be missing parts in the overall dataset.<br>
#### Content
I’ve not posted this set of analyses elsewhere, so I will keep the details contained within each page.
1. [Application of BERTopic to posts](/p2/bertopic.md)<br>

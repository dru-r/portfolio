# Making use of tags to understand characterisation and tropes

## Sections
1. [Motivation of analysis](#motivation-of-analysis)<br>
2. [Methods used and possible applications](#methods-used-and-possible-applications)<br>
3. [Findings](#findings)

## Motivation of analysis
The similiarities and divergences of canon (source material) and fanon (fan) representations of characters are something that have always deeply intrigued me, and was one of the reasons that sparked this overall project. <b>Can we aggregate and quantify how characters have been represented in fandom?</b> If we can, that opens the path to thinking about questions like - why are certain qualities ascribed more to some characters than others? What are some qualities that hold constant from canon, and which are more prone to adaptation in fandom? Do (and how do) fanon representations evolve over time?<br>
<br>
These questions may appear frivolous and limited to fandom on the surface, but I believe they are related to a broader understanding of human perceptions of personality and appearance and the potential influence of narratives on such. And while we speak about fictional characters here, people are also all - in a sense - characters in their own narratives and others' narratives.<br>
<br>
The second question I had was - <b>can we identify tropes automatically given a large enough dataset</b>? From my layman POV, tropes appear to be ideas that caught on in the fandom and became some form of reoccurring theme in a subset of fics. Famous tropes include Alpha/Beta/Omega dynamics; an example of a fandom-specific trope is Draco Malfoy being a Veela. Again, this idea of trope-finding seems almost inane. But it is immensely interesting to think about what ideas get popularised within a community, and eventually to how these ideas got popularised and evolved over time as common sub-narratives.<br>
<br>

## Methods used and possible applications
Definitely, the best way to handle this is to just get to the actual fan material of the written fanfiction narrative. However, fanfiction formatting is typically finicky, the grammar sometimes irregular, and processing a sometimes book-length document can't be done and tested that easily. <b>I hence chose to do this analysis with just freeform tags*, but am currently actively working on recreating this with the actual fic narratives</b>.<br>
<small>*freeform tags on AO3 are tags that authors can freely write. they are often phrases (e.g., 'Good Harry Potter'), meaning they leave valuable information about authors' perceptions of the characters as well, but more easily parsed than long fic documents</small>

### 1. Dependency parsing to retrieve character descriptions from freeform tags
<b>How it was applied to this dataset</b>: I came up with a set of heuristics and wrote them out in a function that relied on Stanford CoreNLP's dependency parser for tagging. This function handled: <br>

1. (noun)(character-name) - e.g., <b>police cop</b> Connor <br>
2. (adverbs, if any)(adjective/past participle verb)(character-name) - e.g., <b>(very) sad</b> Connor<br>
3. (character-name) is/being (adjective) - e.g., Connor is <b>awkward</b>. This portion also checks for any adverbs, adjectives, past participle verbs, nouns, and negations that may have modified the adjectives - e.g., Connor is <b>low</b> on <b>battery</b>.<br>
4. (character-name) is/being (noun) - e.g., Connor is a <b>BAMF</b>. This portion also checks for any adverbs, adjectives, past participle verbs, nouns, and negations that may have modified the nouns - e.g., Connor is an <b>angry boi</b>.<br>
<br>

With the descriptions retrieved, I manually sorted synonyms together (e.g., adorable bun, very adorable, into adorable). The data dump by AO3 may have circumvented some of this as it came with information on how certain similar tags were standardised manually by site volunteers. However, this data dump came after I did this analysis.<br>
<br>
<b>Potential applications to other data</b>: I think this can be an analysis done for any topic/individual of discussion and provides a first step into asking more questions about how the subject of interest is perceived. A possible way to automate the grouping of extracted descriptions would perhaps be clustering embeddings; word vectors, pre-trained BERT embeddings, or the like. 

### 2. Network analysis via community detection to identify tropes from freeform tags
<b>How it was applied to this dataset</b>: I used Harry Potter/Draco Malfoy fanfiction freeform tags, provided in the AO3 data dump, for this analysis. I made use of the provided standardisation information to standardise common freeform tags (e.g., 'Dracy Malfoy' was converted to the main 'Draco Malfoy' tag). I created networks with the freeform tags as nodes; one network per rating. Edges between nodes meant that they had appeared together in a fic - these edges were weighted by the number of fics that used both. I applied a disparity filter to keep statistically significant edges before running the Louvain algorithm and keeping the partition with the highest modularity. The idea was that tropes should appear as 'communities'/clusters of tags.<br>
<br>
<b>Potential applications to other data</b>: This can be applied pretty broadly; e.g., clustering hashtags using a similar co-occurrence network to find hashtag groups. Taking a network analysis perspective on this problem also means that other analyses can also be done; other things I'm looking at including a dynamic analysis to see how paths formed between tags over time, and using the network structure as one piece of information amongst others in creating representations of fics (e.g., with GraphSAGE).

## Findings
I would like to highlight again that these findings are based only on <b>author-provided freeform tags</b>. Freeform tags are not mandatory and definitely, many qualities/attributes are written/performed in narrative instead of explicitly written in the tags section. Nevertheless, I do believe the findings are a good first step into understanding characterisation and tropes in these two fandoms.

### Main finding tl;dr
For characterisation, the four examined Detroit: Become Human (D:BH) characters (Connor RK800, RK900, Hank Anderson, Gavin Reed) appear to have qualities grounded in their canon personalities. At the same time, some qualities have become more exaggerated, perhaps reflective of the fandom's overall preference for a certain portrayal of the character (e.g., the RK800 Connor's fanon personality more strongly reflecting his softer canon game route personality, than his calculating/machine game route personality). We also see new qualities that are not stated in canon, but appear derivative from what canon could possibly imply. <br>
<br> 
For tropes, we observe semantically coherent clusters for the most part. There also appear to be some slightly specific clusters per rating (mental health makes a reappearance in the mature network; if you've read the [previous analysis](https://dru-r.github.io/portfolio/p1/mature-vs-explicit.html). However, many clusters are small (some even with just two tags). Modularity is also not high for most of the networks, indicating that there was not very dense subclustering. This highlights the limitations of relying just on tags, as not all authors will choose to tag every trope and sub-plot in their work for various reasons (e.g., not wanting to spoil too much for the potential reader).

### Findings per analysis
<b>Click on the images below to access the larger versions of them. Those with interactive versions will be indicated.</b><br>

#### 1. Dependency parsing to retrieve character descriptions from freeform tags
Words are sized by their frequency in the tag corpus. Results may not make complete sense if you are unfamiliar with D:BH, but not to worry - note too as well the dominance and coherence of certain qualities of each fanon representation.<br>
<br>
<b>Connor (RK800)</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/08_charatags/connor_wc.png">
    <img src="https://raw.githubusercontent.com/dru-r/ao3-dbh-analysis/master/docs/visuals/08_charatags/connor_wc.png" title="Click for larger" alt="Click for larger"/></a>
<br>
<br>
<b>RK900</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/08_charatags/nines_wc.png">
    <img src="https://raw.githubusercontent.com/dru-r/ao3-dbh-analysis/master/docs/visuals/08_charatags/nines_wc.png" title="Click for larger" alt="Click for larger"/></a>
<br>
Note the contrast between RK900 and their predecessor, Connor (RK800). <br>
<br>
<b>Hank Anderson</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/08_charatags/hank_wc.png">
    <img src="https://raw.githubusercontent.com/dru-r/ao3-dbh-analysis/master/docs/visuals/08_charatags/hank_wc.png" title="Click for larger" alt="Click for larger"/></a>
<br>
<br>
<b>Gavin Reed</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/08_charatags/gavin_wc.png">
    <img src="https://raw.githubusercontent.com/dru-r/ao3-dbh-analysis/master/docs/visuals/08_charatags/gavin_wc.png" title="Click for larger" alt="Click for larger"/></a>
<br>
<small><b>[You can read a more detailed write-up of this whole analysis here](https://dru-r.github.io/ao3-dbh-analysis/dbh-charadescripts.html)</small></b>

#### 2. Network analysis via community detection to identify tropes from freeform tags
Click on any of the full networks for each rating below to access an interactive version. The interactive version shows the top 5 co-occurring tags to any tag which you click in the network. For clarity, I've also provided a link to the summary table of the clusters in each rating network. The summary table contains example tags, a link to an interactive version of said cluster, and my comments on the possible trope/theme (from my understanding as a fandom consumer/creator).<br>
<br>
<b>Explicit tag network</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/drarry/01_tagnetworks/explicit/full_explicit.html">
    <img src="https://raw.githubusercontent.com/dru-r/portfolio/main/docs/p1/imgs/exp-network.JPG" title="Click for interactive version" alt="Click for interactive version"/></a><br>
List of [clusters in explicit network](https://dru-r.github.io/ao3-dbh-analysis/drarry-tropesfromtags.html#explicit-tag-network)<br>
Note the several clusters dedicated to explicit mentions of sex.<br>
<br>
<b>Mature tag network</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/drarry/01_tagnetworks/mature/full_mature.html">
    <img src="https://raw.githubusercontent.com/dru-r/portfolio/main/docs/p1/imgs/mature-network.JPG" title="Click for interactive version" alt="Click for interactive version"/></a><br>
List of [clusters in mature network](https://dru-r.github.io/ao3-dbh-analysis/drarry-tropesfromtags.html#mature-tag-network)<br>
Note the mental health cluster.<br>
<br>
<b>Teen and Up tag network</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/drarry/01_tagnetworks/teen/full_teen.html">
    <img src="https://raw.githubusercontent.com/dru-r/portfolio/main/docs/p1/imgs/teen-network.JPG" title="Click for interactive version" alt="Click for interactive version"/></a><br>
List of [clusters in teen and up network](https://dru-r.github.io/ao3-dbh-analysis/drarry-tropesfromtags.html#teen-tag-network)<br>
Note the 'softening' in themes.<br>
<br>
<b>General Audiences tag network</b><br>
<a href="https://dru-r.github.io/ao3-dbh-analysis/visuals/drarry/01_tagnetworks/gen/full_gen.html">
    <img src="https://raw.githubusercontent.com/dru-r/portfolio/main/docs/p1/imgs/ga-network.JPG" title="Click for interactive version" alt="Click for interactive version"/></a><br>
List of [clusters in general audiences network](https://dru-r.github.io/ao3-dbh-analysis/drarry-tropesfromtags.html#gen-tag-network)<br>
The themes are soft and very reminsicent of fluff fics.

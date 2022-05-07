# Details of the scrape process

Large social media sites like Twitter and Reddit typically have some form of easy-to-use API to collect data from. Archiveofourown.org (AO3) doesn't have one. Thankfully, [scraping isn't against its TOS](https://archiveofourown.org/tos_faq). To collect my dataset, I relied on the requests and bs4 libraries (and respectful delay times between each request). I selected the Detroit: Become Human fandom due to my familairity with the fandom, and its smaller relative size (so easier testing, etc.) compared to long-running fandoms like Harry Potter.<br>
<br>
![image](/imgs/ao3dbh-may2022capture.JPG)
<br>
One of the things we note immediately is that every fanfiction is behind another hyperlink. So we'd have to load into every one of those links to get the story. And that's not the only thing we'd have to account for in the scrape. From trial-and-error, I realised a scrape function had to handle several things:<br>
<br>
1. A list of all the links to all the stories in the specified fandom.<br>
2. Many stories are chaptered, so the links should be appended with the field to view the full work on one page.<br>
3. Comments can be paginated as well, but there's no field to view all comments on one page. The function has to be able to 'flip' through comment pages to collect all the comments. <br>
4. Comments have a tree structure (like Reddit) - information on parents should be preserved.<br>
<br>
With a lot of soup wrangling, I was able to retrieve just about all the public information on each fanfiction. <br><br>
For each fanfiction, I retrieved:<br>
1. Story ID <br>
2. Story title <br>
3. Actual story text <br>
4. Summary <br>
5. Author <br>
6. Chapter count <br>
7. Published and updated dates <br>
8. Word count <br>
9. Rating <br>
10. Warnings <br>
11. Categories (e.g., M/M, F/F)<br>
12. Relationship tags <br>
13. Character tags <br>
14. Fandom tags <br>
15. Freeform tags <br>
16. Hit count, kudo count, bookmark count, comment count <br>
17. List of users who left kudos and count of guests who left kudos <br>
<br>
For each comment for each fanfiction, I managed to retrieve:<br>
1. Comment ID <br>
2. Comment author <br>
3. Chapter the comment was left on <br>
4. Comment time and timezone <br>
5. Actual comment text <br>
6. Comment parent ID <br>

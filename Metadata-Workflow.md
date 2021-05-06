### Goals

We want to be able to accomplish multiple goals with this metadata project:
1. Expose the metadata for the articles we publish in a standards-compliant way so that we can improve their visibility in scholarly databases and search engines.
2. Prepare our metadata in anticipation of potentially indexing our articles with a DOI registrar in the future.
3. Attach metadata to articles we publish with a minimum of additional work and/or presumption of technical expertise. The imperatives are to manage everything within the GUI of WordPress, and where possible to ingest information that we're already using/creating elsewhere in the process of publishing articles.

### Workflow
#### Generating Metadata in the WordPress CMS
1. When you create a new article in WordPress (Posts-\>Add New), you will now see a new menu directly underneath the Title section of the editor: "Bibliographic Metadata." This section has been generated using the [Advanced Custom Fields](https://www.advancedcustomfields.com) plugin (Admin users will now see an option in the sidebar menu to control its parameters, but you should not need to edit this.) Contained within this menu are a series of inputs that we will use to create the required metadata:
- Journal Title
- Volume
- Issue
- Publication Date
- Language
- Publisher
- Full-text URL
- ISSN
- Keywords
![](Screen%20Shot%202021-04-28%20at%205.21.38%20PM.png)
2. You will note that some fields are formatted differently: some are pre-populated (Journal Title, Language, Publisher, ISSN, Keywords); others are drop-down menus (Volume, Issue); some require you to choose an option (Publication Date, Full-text URL); and others are text boxes (Author). The process here is fairly self-explanatory, but a few notes:
- You shouldn't ever need to change the fields for Journal Title, Publisher, or ISSN. (Provided the article is written in English, the same goes for Language.) 
- I'm working on automating this wherever possible; already you'll see that Keywords is populated with whatever tags you assign to the article elsewhere in the Post Editor.
- I've labeled the choices in the Volume menu to reflect both the number and year of each volume. That's not possible with the Issue menu, considering our irregular publication history, so please be attentive there to which issue you assign the article to.
- A note on URL: when you create a new post in WordPress, it isn't assigned a permalink until its initial publication to the web. I've chosen to make Full-text URL a link selection box, rather than a text field, to ensure that there aren't any typos in transposing URLs into the box. But this means that in order for a new article's link to show up in the box, you'll need to first publish it to the website, then come back to the Bibliographic Metadata menu, choose the (new) link, and update the post.
- Author names should be inputted as Last Name, Given Name (eg. Kredell, Brendan).

### Metadata Outputs
Once all this metadata has been input into WordPress, publish the article to the web as usual. Readers of the site won't notice any of this information; it's stored alongside the articles themselves, but we're not presenting it visually anywhere on the site. Rather, this information is collected in two places, each to serve different tasks for us: the HTML header tags of each article (for Google Scholar), and an XML feed of each issue's contents (for indexing purposes).

#### Google Scholar
The primary impediment to achieving visibility in Google Scholar results is that we have not been publishing articles in a way that is machine-readable. Our metadata has been optimized for social sharing – it complies with the format Facebook and Twitter expect - but it does not "read" to a parser like that used by Google Scholar. To solve that problem, I've edited the way our site handles metadata so that this information now displays in the site headers (the data that browsers load but that isn't displayed to the reader). Specifically, we've aligned our metadata to comply with the Highwire Press [tag schema](https://www.monperrus.net/martin/accurate+bibliographic+metadata+and+google+scholar), following a recommendation from [Google Scholar](https://scholar.google.com/intl/en/scholar/inclusion.html#indexing) about maximizing site compliance. As an example, that means that each article on our site will include in its header a section that looks something like this:  
		<meta name="citation_title" content="Another Metadata Post"/>
	    <meta name="citation_author" content="Brendan Kredell"/>
	    <meta name="citation_journal_title" content="Mediapolis: A Journal of Cities and Culture"/>
	    <meta name="citation_volume" content="6"/>
	    <meta name="citation_issue" content="5"/>
	    <meta name="citation_publication_date" content="2021/04/23"/>
	    <meta name="citation_issn" content="2767-8148"/>
	    <meta name="citation_language" content="eng"/>
	    <meta name="citation_publisher" content="Mediapolis: A Journal of Cities and Culture"/>
	    <meta name="citation_fulltext_html_url" content="https://www.mediapolisjournal.com/test/?p=8308"/>
Once we've implemented this system, we should be able to request that Google Scholar parse our site, and if everything works as expected, we would then begin to see *Mediapolis* articles appear in Google search results.

#### Database Indexing
Separately from Google Scholar, the issue of database visibility and digital object identifiers (DOI) are intertwined. Indices like Crossref and Directory of Open Access Journals (DOAJ) are major sources for search engines and databases, so having our articles indexed by those services should provide a significant impact on article visibility. The workflow would look something like this:
- We publish a new issue, and output a specially formatted file (in XML) that displays the bibliographic information for each record (article) in that issue.
- We upload that XML file to a DOI registrar (like [Crossref](https://www.crossref.org)), who validates the information and issues a unique DOI for each article. (We would likely also upload this XML file to the DOAJ index, following a similar process.)
- We display DOI information alongside the record of each article on the site.

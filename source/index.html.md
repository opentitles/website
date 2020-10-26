---
title: OpenTitles

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/opentitles' rel='noopener' target="_blank">OpenTitles on Github</a>

includes:
  - errors

search: false

code_clipboard: true
---

# Introduction

OpenTitles is a browser addon that tracks changes to over forty news sites, such as nos.nl, nytimes.com and theguardian.com. This addon adds a button to the headlines on these sites, which when clicked, will show all recent changes to the title of this article. Additionally, OpenTitles is available as an API and as a daily database dump that may be used for research purposes.

<p align="center">
  <a href="https://chrome.google.com/webstore/detail/opentitles/ipcpballelfolmocdhfjijgmbljachog" rel="noopener" target="_blank"><img height="50" style="margin-right: 1.5em;" src="images/chrome.png" alt="Download on Chrome Webstore"></a><a href="https://addons.mozilla.org/en-GB/firefox/addon/opentitles/" rel="noopener" target="_blank"><img height="50" src="images/firefox.png" alt="Download for Firefox"></a>
</p>

_OpenTitles is made by [Floris de Bijl](https://twitter.com/fdebijl)_

# Technical Overview

OpenTitles relies on RSS feeds and persistent ID's in order to keep track of articles. Every few minutes a scraper will pull all the RSS feeds for every site and compare the titles in the RSS feed to the titles in the database.

While titles and URL's may change, the ID will generally persist between changes to an article. We can therefore use the ID in the RSS feed to match an article to an ID in the database.

This approach has a few limitations, most notably the refresh rate and retention of the RSS feeds. Some RSS feeds are generated on demand, which is the best-case scenario for OpenTitles. In the worst cases the feed is only refreshed
every hour, so changes made to titles in that time may not be picked up by the scraper. 

Furthermore, RSS feeds usually only contain a few dozen articles, so sites with a high throughput might have an article on the RSS feeds for a few hours at most. Any changes made to the title after that can't be tracked, as the scraper relies on the RSS feed for indexing new titles.

A more robust version of OpenTitles would still use the RSS feed for indexing articles, but manually visit those articles for a set period of time to check for new titles. This is vastly more complex than the current approach and my time is very limited, so a rewrite using this technique is not on the roadmap at this point.

The source code for OpenTitles is available on <a href="https://github.com/opentitles" rel="noopener" target="_blank">Github</a>. The project is split into five repositories: this website, the scraper, the API server, the definition and the client (i.e. the browser addon).

All components are made with Typescript, with the exception of this website. 

# Database Dump

Every 24 hours (Central European Time) a new database dump is generated using mongoexport and made available through <a href="https://dump.opentitles.info/" rel="noopener" target="_blank">https://dump.opentitles.info/</a>. This data is free to use for any purpose.

# API

_To be expanded_

The entry point for the API is
<a href="https://api.opentitles.info/v2/country" rel="noopener" target="_blank">https://api.opentitles.info/v2/country</a>

The path to an article is as follows
`https://api.opentitles.info/v2/country/%country%/org/%org/article/%articleId%`

For example: <a href="https://api.opentitles.info/v2/country/nl/org/NOS/article/2353584" rel="noopener" target="_blank">https://api.opentitles.info/v2/country/nl/org/NOS/article/2353584</a>
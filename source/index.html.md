---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://twitter.com/fdebijl' rel='noopener'>Floris on Twitter</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

OpenTitles is a browser addon that tracks changes to over forty news sites, such as nos.nl, nytimes.com and theguardian.com. This addon adds a button to the headlines on these sites, which when clicked, will show all recent changes to the title of this article.

Additionally, OpenTitles is available as an API and as a daily database dump that may be used for research purposes.

# Technical Overview

OpenTitles relies on RSS feeds and persistent ID's in order to keep track of articles. Every few minutes a scraper will pull all the RSS feeds for every site and compare the titles in the RSS feed to the titles in the database.

While titles and URL's may change, the ID will generally persist between changes to an article. We can therefore use the ID in the RSS feed to match an article to an ID in the database.

This approach has a few limitations, most notably the refresh rate and retention of the RSS feeds. Some RSS feeds are generated on demand, which is the best-case scenario for OpenTitles. In the worst cases the feed is only refreshed
every hour, so changes made to titles in that time may not be picked up by the scraper. 

Furthermore, RSS feeds usually only contain a few dozen articles, so sites with a high throughput might have an article on the RSS feeds for a few hours at most. Any changes made to the title after that can't be tracked, as the scraper relies on the RSS feed for indexing new titles.

A more robust version of OpenTitles would still use the RSS feed for indexing articles, but manually visit those articles for a set period of time to check for new titles. This is vastly more complex than the current approach and my time is very limited, so a rewrite using this technique is not on the roadmap at this point.

The source code for OpenTitles is available on Github. The project is split into five repositories: this website, the scraper, the API server, the definition and the client (i.e. the browser addon).

All components are made with Typescript, with the exception of this website. 

# Database Dump

Every 24 hours (Central European Time) a new database dump is generated using mongoexport and made available through https://dump.opentitles.info/. 

# API

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


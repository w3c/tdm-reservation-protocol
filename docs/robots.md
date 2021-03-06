# robots for non techies

## robots.txt 

A Web crawler  (a.k.a bot)  is a software application that systematically browses the [World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web), typically for the purpose of [Web indexing](https://en.wikipedia.org/wiki/Web_indexing). A robots.txt file is a small file that can be placed at the root of any Web site. Such robots.txt file tells Web crawlers which pages or files of the Web server the crawler can or can't request on this Web site.

When a search engine crawls a Website, it requests by default every single file of the site, by browsing the directories it has access to and following every link it finds into Web pages. And if the site has lots of pages, it will take the crawler a while to crawl them; for the sake of efficiency, a crawler has therefore a crawl budget, i.e the number of URLs the crawler can afford to process in a session.

Because of this, a robots.txt file tries to maximize the crawl budget of search engines by telling them to not crawl the parts of a site that aren’t displayed to the public. It is important to recognize that robots.txt is not a mechanism for keeping files out of reach from a crawler, but rather a mechanism for helping crawlers being more efficient. 

**robots.txt is not meant to protect or block sensitive data.**

A robots.txt file is placed at the top level path of the service (i.e.root of a web server). The URL of the file is therefore something like: 

```
http://www.example.com/robots.txt
```

If no file is found at this location, a web crawler will consider that every file present on the web site can be parsed and indexed. 

The expressivity of robots.txt is very limited, with only three “words”:

- *User-Agent* identifies a Web crawler (e.g. Googlebot) to which the following instructions apply; The asterisk ‘*’ is a wildcard and means “all crawlers”;
- *Disallow* specifies a path representing a set of files that should not be crawled. ‘*’ can be used as a wildcard;
- *Allow* specifies a path representing a set of files that can be crawled even though its parent page or older may be disallowed. ‘*’ can be used as a wildcard.

robots.txt may include several User-Agent directives, each followed by one or more Disallow and Allow instructions.

Each Disallow or Allow instruction contains the path of Web resources impacted by the instruction. Jockers like '*' and '?' are allowed to minimize verbosity.

In the following example, any user agent ('*') should follow the rule that disallows exploring the top level path ('/'), and therefore every file and directory at this location, meaning the whole web site.

```
User-agent: *
Disallow: /
```

In the following example, exploring the content of the '/public/covers' directory and any file with a .pdf extension is disallowed ('$' marks the end of a match pattern).

```
User-agent: *
Disallow: /public/covers
Disallow: /*.pdf$
```

robots.txt has been so far loosely specified, but there is an effort undergoing to [make it an Internet Standard(https://tools.ietf.org/html/draft-koster-rep-00)] via the IETF standardization body. 

## robots meta directives 

Whereas robots.txt file directives give bots suggestions for how to crawl files on a website robots meta directives provide more firm instructions on how to process the content of a Web page (or other kind of file) after the file has been crawled. If these directives are discovered by bots, their parameters serve as strong suggestions for crawler indexation behavior. 

There are two types of robots meta directives: those that are part of a Web page (necessarily in HTML) and those a web server sends back (as an X-Robots-Tag HTTP header) to the crawler when the Web resource (any file: image, audio, video etc.) is fetched. 

The author of a Web page can easily add a meta directive to the header of any HTML page. Its syntax is of the type:

``` html
<meta name=”robots” content=”noindex, nofollow”>
```

An equivalent formulation using an HTTP response header would be:

``` http
HTTP/1.1 200 OK
Date: Tue, 25 May 2010 21:42:43 GMT
(…)
X-Robots-Tag: noindex, nofollow
(…)
````

A list of <meta> names maintained by the W3C in the document https://wiki.whatwg.org/wiki/MetaExtensions. This document contains the "robots" entry and lists a small series of possible values, which could be completed by Mike Smith (W3C) at the request of the publishing industry.

To add X-Robots-Tag headers to a site's HTTP responses, a technician must modify the configuration files of the Web server software. This solution is therefore much more flexible (any kind of file) but more complex to set up (a technician must act). 

The most frequent instructions are:

- *noindex* which means “do not index this file”;
- *nofollow* which means “do not follow the hyperlinks you may find in this Web page”, i.e. “do not crawl the files hyperlinked from this page”.

But other instructions have also been defined over time, like: 

- *noimageindex* which means “do not index the images found in this Web page”. 
- *noarchive* which means “do not show a cached link to this page on a search engine result page”.
- *nosnippet* which means “do not show a snippet of this page on a search engine result page”.
- *notranslate* which means “do not offer this page’s translation on a search engine result page”.

This set of instructions is not properly standardized and different search engines accept different meta-tag parameters for the “robots” meta-tag. For instance Google specifies [here(https://developers.google.com/search/reference/robots_meta_tag)] the vocabulary it understands.
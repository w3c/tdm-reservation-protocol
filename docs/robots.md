# robots for non techies

## Web crawlers and SEO

A Web crawler (a.k.a bot)  is a software application that systematically browses the [World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web), typically for the purpose of [Web indexing](https://en.wikipedia.org/wiki/Web_indexing). A robots.txt file is a small file that is placed at the root of any Web site. This robots.txt file tells Web crawlers which pages or files of the Web server the crawler can or can't fetch on this Web site. It is purely indicative, and does not block a crawler to fetch data from the Web server. Good citizens follow the rules set in robots.txt, bad citizens don't. 

If robots.txt is not a blocking mechanism, then what is its practical use? 

When a search engine crawls a Website, it requests every single file of the site by default, by browsing the directories it has access to and following every link it finds into Web pages. And if the site has lots of pages, it will take a while to the crawler for fetching them all; for the sake of efficiency, a crawler has therefore a crawl budget, i.e the number of URLs the crawler can afford to process in a session.

Because of this, the SEO (Search Engine Optimization) manager of a web site tries to optimize the crawl budget of search engines. It may be by telling bots to not crawl parts of a site that are not displayed to the user, by limiting the number of hyperlinks crawlers should follow from a web page, or other techniques known only to SEO wizards.

Webmasters can also use robots.txt to ask bots (any, or specific ones) to avoid crawling their Web server because such load is cumbersome for them. But as we said before, only good citizens will follow this request.  

## robots.txt 

The Robots Exclusion Protocol was initially defined in 1996. It is an IETF Internet Standard since September 2022 under the name [RFC 9309](ttps://datatracker.ietf.org/doc/html/rfc9309). 

A robots.txt file is placed at the top level path of the service (i.e.root of a web server). The URL of the file is therefore something like: 

```
http://www.example.com/robots.txt
```

If no file is found at this location, a web crawler will consider that every file present on the web site can be fetched, parsed and indexed. 

The expressivity of robots.txt is very limited, with only three “words”:

- *User-Agent* identifies a specific Web crawler (e.g. Googlebot) to which the following instructions apply; The asterisk ‘*’ is a wildcard and means “all crawlers”;
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


## Robots meta directives 

Whereas robots.txt file directives give bots suggestions for how to crawl files on a website robots meta directives provide more firm instructions on how to process the content of a Web page (or other kind of file) after the file has been crawled. If these directives are discovered by bots, their parameters serve as strong suggestions for crawler indexation behavior. 

There is no Internet Standard for Robots meta directives. 

There are two types of robots meta directives: those that are part of a Web page (necessarily in HTML) and those a web server sends back (as an X-Robots-Tag HTTP header) to the crawler when the Web resource (any file: image, audio, video etc.) is fetched. 

The author of a Web page can easily add a meta directive to the header of any HTML page. Its syntax is of the type:

``` html
<meta name="robots" content="noindex, nofollow">
```

An equivalent formulation using an HTTP response header would be:

``` http
HTTP/1.1 200 OK
Date: Tue, 25 May 2010 21:42:43 GMT
( … )
X-Robots-Tag: noindex, nofollow
( … )
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

This set of instructions is not properly standardized and different search engines accept different meta-tag parameters for the “robots” meta-tag. For instance Google specifies [here](https://developers.google.com/search/reference/robots_meta_tag) the vocabulary it understands.

## Conclusion

robots.txt and robots meta directives give indications to search engines, essentially for SEO purposes. These techniques have not been created to protect sensitive data from a specific usage (like TDM).

Using robots.txt for managing TDM opt-out would require a webmaster to enter every single user agent (i.e. bot name) he wants to stop from mining the site, whatever the mining purpose is (including indexing for web search). There may be already thousands of TDM and IA robots in the wild, and some of them do not even use a bot-specific user agent. Using robots.txt for opting-out from TDM/AI crawlers is therefore impossible today. This could change if robots.txt evolves and supports the expression of an opt-out (here Disallow) relative to certain purposes like "mining for training TDM and AI solutions". 

Robots meta directives  already suport a notion of purpose: "nosnippet" and "notranslate" are examples of such purpose. It would therefore be easier to use robots meta directives for supporting a "notdm" directive conforming to the CDSM Article 4. A "noai" directive has already been proposed, but it is not clearly aligned with the TDM opt-out we can legally declare, and it does not directly resolve our need for a Policy property (as a URL). 

This is why the TDMRep Community Group decided to get inspiration from robots.txt and robots meta directives, which have proven simple to implement, but using a different syntax. A syntax which is cleary different from the technique used for web indexing control, and allows the addition of a useful Policy feature. 

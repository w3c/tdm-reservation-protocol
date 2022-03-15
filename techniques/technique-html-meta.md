# Technique based on html meta tags

## Status of this document

This is a best practices document, its aims is to help implementors handling this technique and it may evolve over time.

The related section of the specification is [TDM Metadata in HTML Content](https://w3c.github.io/tdm-reservation-protocol/spec/#sec-tdm-html-meta). 


## Use of meta tags

In html, metadata are defined using the repeatable and empty <meta> element, child of <head>. The meta element supports three main attributes: **name**, **content** and **scheme** (the http-equiv attribute is out of scope in our case).  

## Implementing the proposal

This solution is only relevant for html (or xhtml) documents and does not apply to any other type of Web resource.
  
The protection offered by this solution only applies to the html (or xhtml) content: it does not apply to the Web resources referenced from such html content, e.g. images (via and <img> tag) or audiovisual content (via an <audio> <video> or <object> tag). 

Meta elements can easily be integrated in html document at the time they are produced. No configuration is needed on the Web server which will serve these documents.

This solution cannot associate particular rights to different fragments of html content (this may be added to a next version of the specification). 

## Relationship with other initiatives

html meta tags are found in the context of [robots meta directives]()https://github.com/w3c/tdm-reservation-protocol/blob/main/docs/robots.md#robots-meta-directives.

html meta tags are also found in the context of the [Article Sharing Framework](https://github.com/w3c/tdm-reservation-protocol/blob/main/docs/initiatives.md#article-sharing-framework-stm-association). Look especially at the [NISO ALI Best practices](https://groups.niso.org/apps/group_public/download.php/14226/rp-22-2015_ALI.pdf) in section 4. 

# Proposal based on html meta tags

## Status of this document

This is a working document. It serves as a support for discussions of the TDMRep CG.

This document is by no way an outcome of the work of the TDMRep CG and does not adopt the style of W3C CG Notes.

We’ll reuse here the TDM-a and TDM-b properties as defined in [Proposal based on http headers](/proposals/proposal-http-headers.md).

## Use of meta tags

In html, metadata are defined using the repeatable and empty <meta> element, child of <head>. The meta element supports three main attributes: **name**, **content** and **scheme** (the http-equiv attribute is out of scope in our case).  

This specification defines two metadata properties of html content: “TDM-a” and “TDM-b”. The values of these properties are set in the content attribute, the scheme attribute is not used. 

In the following example, an html document is associated with a TDM license:

``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="TDM-a" content="2">
  <meta name="TDM-b" content="https://example.com/licences/licence-a">
  <title>Page title</title>
</head>
<body>
  ...
  <!-- body content -->
  ...
</body>
</html>
```

## Implementing the proposal

This solution is only relevant for html (or xhtml) documents. It does not apply to any other type of Web resource.

Meta elements can easily be integrated in html document at the time they are produced. No configuration is needed on the Web server which will serve these documents.

This solution cannot associated particular rights to different fragments of html content (this is not a requirement we has agreed on but it is an open issue under discussion). 

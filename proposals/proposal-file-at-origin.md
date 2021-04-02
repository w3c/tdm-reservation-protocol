# Proposal based on a file hosted on the origin server

## Status of this document

This is a working document. It serves as a support for discussions of the TDMRep CG.
This document is by no way an outcome of the work of the TDMRep CG and does not adopt the style of W3C CG Notes.
No bikeshedding: choosing property names will come last; in this document, properties are prefixed by "TDM-" followed by a letter, starting at 'a'.

## Specification of the TDMRep.json file 

Let’s imagine a Web server hosting several sets of files, driven by different TDM policies; each set of files being located on the server using a regular expression. 

This specification defines TDMRep.json as as JSON file which contains an array of objects; each object contains three properties: 

- location: a pattern locating the set of files hosted on the server and driven by the sibling TDM-a and TDM-b values.
- TDM-a (*)
- TDM-b (*)

(*) We use here the property names and values already used in the [Proposal based on http headers](./proposal-http-headers.md).

A URL ready for matching is obtained by the concatenation of the protocol and domain name of the TDMRep JSON file URL with the path expressed in the location property.

Note 1: the name “TDMRep.json” is a placeholder, here also we’ll avoid bikeshedding in the first phase of discussion. 

Note 2: JSON is chosen because unmarshalling it is obvious in every language, and especially built-in in Javascript. Unmarshalling alternative formats like yaml or xml is not so immediate. Using JSON-LD makes no sense in our case, as no RDF model will be extracted from this structure. 

## Use of regular expressions

There are many variants of regular expressions. In order to be simplify the work of TDM Agents, this specification is using [Javascript RegExps](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions), Javascript being supposed to be used for developing most TDM Agents. 

Note: nginx is using another variant for expressing locations, a variant called [PCRE](https://www.pcre.org), for Perl compatible Regular Expressions. 

Note: the group may want to restrict the RegExp language to the simplest, e.G. ‘*’ and ‘?’ jokers. Or it may decide to reuse the specification and wording of the [robots.txt draft-koster-rep-00](https://tools.ietf.org/html/draft-koster-rep-00#section-2.2.2).

## Use of the .well-known directory

TDPRep.json is stored in the .well-known directory, located at the root of the origin server. 

Here is a quick introduction of [RFC-5785](https://tools.ietf.org/html/rfc5785):

It is increasingly common for Web-based protocols to require the discovery of policy or other information about a host (“site-wide metadata”) before making a request.
[…]
When this happens, it is common to designate a “well-known location” for such data, so that it can be easily located.
[…]
To address this, this memo defines a path prefix in HTTP(S) URIs for these “well-known locations”, “/.well-known/".

## Implementing the proposal

Let’s imagine that a Web server is hosting three groups of files. The rightsholder of the first group of files (PDF documents) wants to express that TDM rights are reserved on this content. The rightsholder of the two other groups of files wants to express that TDM rights are tied to a license for the second group (html pages) and TDM rights are not reserved for the third (JPEG images).

In this example, the first group is a set of files stored in /directory-a; the second group is stored in /directory-b/html and the third group in /directory-b/other. 

TDMRep.json is therefore structured as: 

```json
[
  {
  "location": "/directory-a",
  "TDM-a": 1
  },
  {
  "location": "/directory-b/html",
  "TDM-a": 2,
  "TDM-b":"https://example.com/tdm-licenses/license-a"
  },
  {
  "location": "/directory-b/other/*.jpg",
  "TDM-a": 0
  }
]
```

Note:  in this example, if non-JPEG files are also located in “/directory-b/images”, they are driven by the TDM exception of the DSM. 

## Solution vs requirements

### Specify how a rightsholder can declare the reservation of TDM Rights on each individual Web resource he controls.

Yes. By locating content driven by specific TDM rights in specific locations, rightsholders can easily associate locations on their servers with well defined TDM rights.

### Specify how a rightsholder can indicate the location of human readable information indicating how to apply for a TDM License.

Yes. If the value of TDM-b resolves to an html page, human-readable information is available. It is up to the rightsholder to indicate clearly in this page how to apply to a TDM license.

### Specify how a rightsholder can indicate the location of a TDM Licence associated with each individual Web resource he controls.

Yes. If the value of TDM-b resolves to a resource in the format selected for TDM licenses, machine-readable information is available.

### Specify a machine-readable format for TDM Licenses.

This requirement will be treated in due course.

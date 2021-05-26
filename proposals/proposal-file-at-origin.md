# Proposal based on a wll known file hosted on the origin server

## Status of this document

This is a working document. It serves as a support for discussions of the TDMRep CG.

This document is by no way an outcome of the work of the TDMRep CG and does not adopt the style of W3C CG Notes.

We’ll reuse here the TDM-a and TDM-b properties as defined in [Proposal based on http headers](/proposals/proposal-http-headers.md).

## Specification of the TDMRep.json file 

Let’s imagine a Web server hosting several sets of files, driven by different TDM policies. 

This specification defines TDMRep.json as as JSON file which contains an array of objects; each object represents a rule and contains three properties: 

- location: a pattern matching the path of a set of files hosted on the server, associated with the sibling TDM properties.
- TDM-a
- TDM-b

Note 1: the name “TDMRep.json” is a placeholder, here also we’ll avoid bikeshedding in this phase of the discussion. 

Note 2: JSON is chosen because unmarshalling it is obvious in every language, and especially built-in in Javascript. Unmarshalling alternative formats like yaml or xml is not so immediate. Using JSON-LD is an option, but no RDF model will be extracted from this structure. 

Note 3: the following specification has been extracted from  [robots.txt draft-koster-rep-00 2.2.2](https://tools.ietf.org/html/draft-koster-rep-00#section-2.2.2).

To evaluate if the URL of a Web resource is subject to a given rule, a TDM Agent MUST match the paths against the URL.  The matching SHOULD be case sensitive.  The most specific match found MUST be used.  The most specific match is the first in sequence.

If a percent-encoded US-ASCII character is encountered in the URI, it MUST be unencoded prior to comparison, unless it is a reserved character in the URI as defined by RFC3986 or the character is outside the unreserved character range.  The match evaluates positively if and only if the end of the path from the rule is reached before a difference in octets is encountered.

## Use of regular expressions

There are many variants of regular expressions. In order to simplify the work of TDM Agents, this specification is re-using the specification and wording of the [robots.txt draft-koster-rep-00 2.2.3](https://tools.ietf.org/html/draft-koster-rep-00#section-2.2.3).

> TDM Agents MUST allow the following special characters:

| Character | Description | Example |
| -------- | -------- | -------- |
| "#"       | Designates an end of line comment. | "TDM-b: / # comment at the end |
| "$"       | Designates the end of the match pattern. A URI MUST end with a $. | "TDM-b: /this/path/exactly$" |
| "*"       | Designates 0 or more instances of any character | "TDM-b: /this/*/end" |

If TDM Agents match special characters verbatim in the URI, they MUST use "%" encoding.  For example:

| Pattern       | URI |
| -------- | -------- |
| /path/foo-%24 | https://www.example.com/path/foo-$ |

Note 1: [Javascript RegExps](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) was a possible alternative, Javascript being supposed to be used for developing most TDM Agents. 

Note 2: nginx is using another variant for expressing locations on which specific rules apply, a variant called [PCRE](https://www.pcre.org) for Perl compatible Regular Expressions. 

## Use of the .well-known directory

TDMRep.json is stored in the .well-known directory, located at the root of the origin server. 

Here is a quick introduction of [RFC-5785](https://tools.ietf.org/html/rfc5785):

It is increasingly common for Web-based protocols to require the discovery of policy or other information about a host (“site-wide metadata”) before making a request.<br>
[…]<br>
When this happens, it is common to designate a “well-known location” for such data, so that it can be easily located.<br>
[…]<br>
To address this, this memo defines a path prefix in HTTP(S) URIs for these “well-known locations”, “/.well-known/".

## Example

Let’s imagine that a Web server is hosting three groups of files. The rightsholder of the first group of files (PDF documents) wants to express that TDM rights are reserved on this content. The rightsholder of the two other groups of files wants to express that TDM rights are tied to a license for the second group (html pages) and TDM rights are not reserved for the third (JPEG images).

In this example, the first group is a set of files stored in /directory-a; the second group is stored in /directory-b/html and the third group in /directory-b/images. 

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
  "location": "/directory-b/images/*.jpg",
  "TDM-a": 0
  }
]
```

Note: in this example, if non-JPEG files are also located in “/directory-b/images”, they are by default driven by the TDM exception of the DSM. 

## Implementing the proposal

This solution applies to any type of Web resource. 

It does not require a specific configuration of the Web server, only write access to the /.well-known directory. 


## Solution vs requirements

### Specify how a rightsholder can declare the reservation of TDM Rights on each individual Web resource he controls.

Yes. By locating content driven by specific TDM rights in specific locations, rightsholders can easily associate locations on their servers with well defined TDM rights.

### Specify how a rightsholder can indicate the location of human readable information indicating how to apply for a TDM License.

Yes. If the value of TDM-b resolves to an html page, human-readable information is available. It is up to the rightsholder to indicate clearly in this page how to apply to a TDM license.

### Specify how a rightsholder can indicate the location of a TDM Licence associated with each individual Web resource he controls.

Yes. If the value of TDM-b resolves to a resource in the format selected for TDM licenses, machine-readable information is available.

### Specify a machine-readable format for TDM Licenses.

This requirement will be treated in due course.

# Technique based on a well known file hosted on the origin server

## Status of this document

This is a best practices document, its aims is to help implementors handling this technique and it may evolve over time.

The related section of the specification is [TDM File on the Origin Server](https://w3c.github.io/tdm-reservation-protocol/spec/#sec-tdm-file). 

## Use of the .well-known directory

tdmrep.json is stored in the .well-known directory, located at the root of the origin server. 

Here is a quick introduction of [RFC-5785](https://tools.ietf.org/html/rfc5785):

It is increasingly common for Web-based protocols to require the discovery of policy or other information about a host (“site-wide metadata”) before making a request.<br>
[…]<br>
When this happens, it is common to designate a “well-known location” for such data, so that it can be easily located.<br>
[…]<br>
To address this, this memo defines a path prefix in HTTP(S) URIs for these “well-known locations”, “/.well-known/".

## Implementing the proposal

This solution applies to any type of Web resource. 

It does not require a specific configuration of the Web server, only write access to the /.well-known directory.
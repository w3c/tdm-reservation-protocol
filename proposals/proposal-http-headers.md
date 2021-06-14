# Proposal based on http headers

## Status of this document

This is a working document. It serves as a support for discussions of the TDMRep CG.

This document is by no way an outcome of the work of the TDMRep CG and does not adopt the style of W3C CG Notes. 

No bikeshedding: choosing property names will come last; in this document, properties are prefixed by "TDM-" followed by a letter, starting at 'a'. 

## Determining the choice of a rightsholder

This is done using two properties:

### TDM-a

TDM-a is a integer which can take the following values. 

value | meaning | reference use-case
----- | ------- | ------------------
unset | no declaration              | use-case 1
0     | TDM rights are not reserved | use-case 2
1     | TDM rights are reserved     | use-case 3
2     | TDM rights are reserved but a TDM license can be acquired  | use-case 4

Other values are considered protocol errors. In such a case the TDM Actor MUST consider that the value of TDM-a is `unset`.

### TDM-b

If the value of TDM-a is `2`, the absence of TDM-b is considered a protocol error. In such a case the TDM Actor MUST consider that the value of TDM-a is `1`. 

TDM-b is a URL. 

If the Web resource located at this URL is a Web page (i.e. its content-type is `text/html`), this resource is considered human readable. If it has the content-type of the license format defined by the protocol, this resource is considered machine-readable. 

Other content-types are considered protocol errors. In such a case the TDM Actor MUST consider that the value of TDM-a is `1`. 

## Use of http headers

Let's imagine that a TDM Agent fetches a Web resource using: 

``` http
GET /path/page.html HTTP/1.1
Host: http://example.com 
```

The message returned by the Web server to the TDM Agent may have the following header:

``` http
HTTP/1.1 200 OK
Server: Apache
Last-Modified: Tue, 12 Feb 2019 17:47:55 GMT
Content-Type: text/html
Content-Length: 35026
TDM-a: 2
TDM-b: https://example.com/policies/policy-a
```

The TDM Agent can then fetch the resource corresponding to the policy. 

``` http
GET /policies/policy-a HTTP/1.1
Host: http://example.com 
```

The message returned by the Web server to the TDM Agent may indicate that the information is human readable: 

``` http
HTTP/1.1 200 OK
Server: Apache
Last-Modified: Tue, 12 Feb 2019 17:47:56 GMT
Content-Type: text/html
Content-Length: 1456
```

Or it may indicate that the information is machine-readable (here we suppose that the content-type associated with the chosen license format is application/ld+json):

``` http
HTTP/1.1 200 OK
Server: Apache
Last-Modified: Tue, 12 Feb 2019 17:47:56 GMT
Content-Type: application/ld+json
Content-Length: 1245
```

## Implementing the proposal

HTTP headers can easily be integrated by web servers like Apache (using mod_headers), reverse-proxies like nginx, or directly in the source code driving the behavior of a web server (e.g. using Golang). This is made particularly easy if the resources associated with given TDM properties are placed in specific locations. 

In Apache for instance, setting TDM-a to 0 for all resources contained in the directory "/path" is obtained via the directive: 

```
<Directory "/path">
  Header set TDM-a "0"
</Directory>
```

In nginx, the equivalent is obtained via the directive: 

```
location /path {
  add_header TDM-a 0;
}
```

## Solution vs requirements

### Specify how a rightsholder can declare the reservation of TDM Rights on each individual Web resource he controls.

Yes. http headers are set on individual web resources and technicians mastering web servers or reverse proxies can easily control the relationships between resources and TDMRep values. 

### Specify how a rightsholder can indicate the location of human readable information indicating how to apply for a TDM License.

Yes. If the content-type of TDM-b corresponds to an html page, human-readable information is avalable. It is up to the rightsholder to indicate clearly in this page how to apply to a TDM license 

### Specify how a rightsholder can indicate the location of a TDM Licence associated with each individual Web resource he controls.

Yes. In this case the content-type of TDM-b corresponds to the format selected for TDM licenses.

### Specify a machine-readable format for TDM Licenses. 

This requirement will be treated in due course. 




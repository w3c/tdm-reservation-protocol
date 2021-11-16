# Technique based on http headers

## Status of this document

This is a best practices document, its aims is to help implementors handling this technique and it may evolve over time.

The related section of the specification is [TDM Header Field in HTTP Responses](https://w3c.github.io/tdm-reservation-protocol/spec/#sec-tdm-header). 

## Implementing the technique

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


# Vocabulary and requirements for a technical solution

## Definitions:

- **Rightsholder**: person or organization that owns the legal rights to something, in our case Web Resources. (Wiktionary)
- **TDM Actor**: organization practicing TDM (on Web resources in our case).
- **TDM Agent**: software crawling web content for TDM purposes. 
- **TDM License**: description of the terms and conditions by which a TDM actor can process a given Web resource.  
- **TDM Rights**: rights to process a Web resource via TDM techniques, for a certain purpose (e.g commercial / non-commercial).  
- **URL**: Uniform Resource Locator, also named Web address (Wikipedia)
- **Web resource**: identifiable thing available on the Web, e.g. HTML formatted text, an image, audio or video file. Web resources are located using URLs.
- **Web page**: Web resource formatted in HTML. 

## High level requirements: 

To ensure that all users without discrimination will be able to reserve their rights, the solution shall:

1. Rely on open standards and be interoperable.
1. Rely on tools and formats widely supported by web crawlers.
1. Be easy to implement, with no economic or technical barriers.

As noted above, TDM and content indexing for search and discovery have different usage purposes. Therefore a prerequisite for any technical solutions that may be explored is that such solution shall enable rightsholders to reserve TDM rights without affecting access to other services such as content indexing and listing by search engines, nor affect content ranking in search pages results. 

**The solution shall:**

1. Specify how a rightsholder can declare TDM rights on a Web page he controls.
1. Specify how a rightsholder can declare TDM rights on each individual Web resource he controls, when such Web resources are present in a Web page.
1. Specify how the rightsholder can indicate whether a licence for TDM rights is available (in case TDM rights are reserved).
1. Specify how a TDM actor can apply for a TDM license.
1. Specify a machine-readable format for TDM licenses. 

**Although it should not over-complexify the solution, it should still:**

1. Allow the rightsholder to specify whether i) all TDM rights (other than for scientific research purposes) are reserved or ii) only TDM rights for commercial purposes are reserved  
1. Specify how a rightsholder can indicate that TDM rights are reserved on random Web resources he controls (e.g. images and video files which may be found by crawlers outside of Web pages).
# Past and existing initiatives

This list of initiatives has to be considered as a sort of toolbox, from which ideas may be extracted for building the final recommended technical solution.  

## ACAP

Automated Content Access Protocol ("ACAP"; http://the-acap.org) was proposed in 2007 by a set of organisations from the publishing industry (led by the World Association of Newspapers, European Publishers Council and International Publishers Association) for communicating machine-readable copyright terms and conditions associated with online content. 

The goal of the initiative was to communicate precise permission information to search engines, like disallowing the presentation of a snippet of text or limiting its size, disallowing the presentation of page as a thumbnail, limiting the part of a text that can be indexed ...   

ACAP 1.0 was implemented as an extension of the Robots Exclusion Protocol (robots.txt and robots meta directives).

Major search engines (Google, Yahoo, Microsoft) and content aggregators were active during the specification of ACAP but all declined to adopt the solution once released. Only Exalead (France) implemented the spec. 

The maintenance of ACAP was moved to the [IPTC](https://iptc.org) in 2011; the IPTC renamed the ACAP 2.0 standard to RightsML, to align its branding to the existing xxxML standards of this standardization organisation.

## RightsML

[RightsML](https://iptc.org/standards/rightsml/) is a standard maintained by the IPTC (International Press & Telecommunication Council); it is a profile of ODRL 2, the framework for digital rights hosted by the W3C, which identifies features most usefully employed in news syndication and defines additional vocabulary for expressing the usage permissions and constraints that are particular to the news industry. The first version was released in 2012, and [RightsML v2.0](https://iptc.org/std/RightsML/2.0/RightsML_2.0-specification.html) was released in 2018, based on ODRL 2.2. 

RightsML enables a wide range of usage policies to be expressed in news exchange formats. A news agency may for instance indicate to a newspaper, in a machine readable way, rights relative to a syndicated news item previously expressed as text of the form “UK out; archive out; for use in North America only; may not be archived”. Detailed rights can also be expressed about each component of a multimedia news publication.

The IPTC invites publishers and their partners to signal if terms are missing, which could lead to new versions of the standard.

Unlike ACAP, RightsML is a standard focusing on business workflows (e.g. news agency to newspapers and news websites, you can [watch this BBC news presentation](https://www.youtube.com/watch?v=rr9HO7Adesw) for a use case). There is no evidence of a use of RighstML for conveying rights and restrictions to Web crawlers of any kind. 

## RightFind® XML for Mining Solution (Copyright Clearance Center)

The Copyright Clearance Center (CCC) has developed [RightFind](http://www.copyright.com/publishers/rightfind-xml-for-mining-solution/) XML for Mining  in partnership with dozens of leading STM publishers (including Oxford University Press and Springer Nature, as well as Wiley, BMJ, the Royal Society of Chemistry, Taylor & Francis, SAGE, Cambridge University Press, American Diabetes Association, American Society for Nutrition, and Future Medicine).

All articles from this corpus are authorized for mining and commercial use; they are provided in XML format, easier to mine than PDF and this corpus is searcheable in full-text mode from the platform. Subscribed content plus paid copies of unsubscribed content can be downloaded. 

## Assert your rights in online content (EPC / Copyright Hub)

The European Publishers Council (EPC) has developed a standard for [asserting rights in online content](http://www.copyrighthub.org/assert-your-rights-in-online-content/) in collaboration with the Copyright Hub (UK).

The proposed solution is split in three parts:
- A standardized JSON-LD structure to be added to Web pages: this structure identifies the rightsholder and links the content to an online license;
- License information hosted by the Copyright Hub in ODRL 2.0 format (as JSON-LD), which details the terms and conditions associated with the use of source content;
- An optional visual eCopyright symbol that can be added to each Web page (or component of a Web page) to indicate the presence of reservation of TDM rights.  

Using a proper semantic structuration of a Web page, individual media files referred to from HTML 5 content may be associated with their own license. 

The ODRL message returned typically allows indexing and then makes a further statement as to whether TDM is disallowed or can be licensed ( note that the Hub is able to express far more complex rights and permissions statements in ODRL than simply these - giving future extensibility). 

A small yearly fee is requested to the publishers by the Copyright Hub for the support of the infrastructure needed to generate, host and return the ODRL response.

This solution covers the use case where the content on which the TDM reservation is applied is a Web page; it does not cover the case of Web resources like media files when not “discovered” via Web Pages. EPC believes that this does not limit the interest of their approach.

Note that the Hub does not mandate how the Hub connectivity between asset and licence information is implemented. This is because that relates to how metadata is presented which may well change over time and is certainly different for different media, but they can and do suggest ways in which it can be done. The Hub can be used in many ways and the current EPC recommendation is one of these ways.

## Article Sharing Framework (STM Association)

The STM Association - the global voice of scholarly publishing -  has developed the Article Sharing Framework ([video](https://drive.google.com/file/d/1jVn9Qcz8fi612EpgEygedIZrSUNKhQim/view?usp=sharing)) allowing online content sharing platforms for an easy identification of articles and the associated sharing permissions. It is a response to the raise of Scholarly Collaboration Networks and the release of the EU Copyright Article 17. By using this framework, online platforms can check their compliance with rightsholder’s content sharing policies at the point of content upload and determine in real-time if the uploading of the content is permissible. 

To enable this framework, rightsholders have to embed metadata tags in the content in machine-actionable form: this includes at least the DOI (Digital Object Identifier) and version of the resource, plus the URIs of the associated sharing policies. PDF articles, for instance, will embed in their XMP metadata a DOI, as well as Access and License Indicators (cf Notes). There is a limited set of possible sharing policies and corresponding situations (currently 46); each online platform can therefore easily decide in which situation the content can or cannot be processed. 

The registry of machine-readable sharing policies defined by the Article Sharing Framework is stored in Crossref, a cross-industry metadata database. 

Notes:
- The work on the Article Sharing Framework has been managed by STM’s Standard and Technology Executive Committee, [STEC](https://www.stm-assoc.org/standards-technology/executive-committee-stec/).
- The STM Association maintains a [page on TDM](https://www.stm-assoc.org/policy-advocacy/text-data-mining-tdm/).
- Access and License Indicators (ALI) are defined in the [NISO ALI Schema](https://www.niso.org/schemas/ali/1.0). 

## Crossref TDM service 

Crossref provides a [TDM service](https://www.crossref.org/education/retrieve-metadata/rest-api/text-and-data-mining-for-members/) for its members, which allows them to associate with a registered DOI the link to the related TDM license (in machine readable format).

This service has been developed for the STM sector and relies on the DOI standard and Crossref infrastructure. Within the Crossref platform, each article is identified by a DOI and can be linked to the full-text of the article. However, given a DOI, it is not necessary that  a processing platform knows that Crossref is the service  to be queried in order to get licensing information about this article: the DOI infrastructure provides a common service for all DOIs deposited in any DOI Registration Agency, called DOI content negotiation, that allows to retrieve DOI records in multiple formats. If the DOI record includes the full text links for TDM and the link to the licence, these can be returned as part of the metadata, or, as in the case of Crossref, in the link header in the content negotiated response; both options are possible and can be implemented by any DOI Registration Agency..  

Note: Crossref also provides a TDM click-through service which allows Crossref members to post additional TDM terms and conditions and for researchers to access, review and accept these terms. However, due to a lack of use, Crossref has decided ([blog article](https://www.crossref.org/blog/evolving-our-support-for-text-and-data-mining/)) to close it by the end of 2020.

## ARDITO

The EU funded project ARDITO (Access to Rights Data via Identification Technology Optimisation, https://www.ardito-project.eu/) developed tools designed to facilitate access to rights and licensing information from the point of discovery of creative content (books and e-books, images and audio-visual) in a digital environment.

ARDITO tools allows to link rights and licenses information to standard persistent identifiers (DOI, ISBN) or to the digital content itself (e-books and e-book fragments, images, video) by means of watermarks, fingerprinting and content recognition technologies. Rights information are then made available to users (either in human or machine-readable format) in a digital environment through web resolution technologies. Here’s a [demo](https://www.ardito-project.eu/tools-in-action).

The ARDITO website provides details on the tools that partners developed for [Images](https://www.ardito-project.eu/images-tools), [Publishing](https://www.ardito-project.eu/publishing-tools), [e-Book Publishing](https://www.ardito-project.eu/e-book-publishing), [Video](https://www.ardito-project.eu/video-tools). The Copyright Hub provided enhanced back-end infrastructure and front-end tools for content users (browser plug-in and e-Copyright symbol).

No specific service for TDM rights declaration has been piloted so far, however, in principle, it could be possible to extend the rights information scheme used by ARDITO tools for these purpose and to enable rightsholders to specify whether TDM rights are reserved and links to the TDM licenses available.

For example the [ARDI](https://www.ardito-project.eu/publishing-tools) service provides persistent and web resolvable identification of rights and copyright declarations (Digital Rightsholder Statement) using the DOI system for identification and an interoperable standard format to express and communicate rights declarations that can be extended to accommodate also indication of TDM reservation and link to TDM policy or license.

## Do Not Track

Do Not Track (DNT) was a proposed HTTP header field, designed to allow internet users to opt-out of tracking by websites—which includes the collection of data regarding a user's activity across multiple distinct contexts, and the retention, use, or sharing of data derived from that activity outside the context in which it occurred.

The Do Not Track header was originally proposed in 2009. It was implemented by Firefox, then later Internet Explorer, Safari, Opera and Chrome. Efforts to standardize Do Not Track by the W3C in the Tracking Protection WG reached only the Note stage and ended in January 2019 due to insufficient deployment and support (by trackers).

The DNT header accepted three values: 1 in case the user does not want to be tracked (opt out), 0 in case the user consents to being tracked (opt in), or null (no header sent) if the user has not expressed a preference. 

DNT was not widely adopted by the industry, with companies citing the lack of legal mandates for its use, as well as unclear standards and guidelines for how websites are to interpret the header.

In 2020, a coalition of US-based internet companies announced Global Privacy Control header that spiritually succeeds Do Not Track header. The creators hope that this new header will meet the definition of "user-enabled global privacy controls" defined by California law and European GDPR. In this case, the new header would be automatically strengthened by existing laws and companies would be required to honor it.

### DNT References

- [Wikipedia article](https://www.ardito-project.eu/publishing-tools)
- [How the tragic death of Do Not Track ruined the web for everyone](https://www.fastcompany.com/90308068/how-the-tragic-death-of-do-not-track-ruined-the-web-for-everyone), Fast Company article, 2019
- [W3C DNT spec](https://www.w3.org/TR/tracking-dnt/) (2019), which is a great model for the spec we may soon write. 
- [Tracking Protection WG page](https://www.w3.org/2011/tracking-protection/), chair was Matthias Schunter (Intel).
- [Global Privacy Control](https://globalprivacycontrol.org/) home page. Note the use of the /.well-known directory.

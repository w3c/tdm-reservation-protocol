
# Text and Data Mining Reservation Protocol Community Group

## The Community Group

The goal of this [Community Group](https://www.w3.org/community/tdmrep/) is to facilitate TDM in Europe and elsewhere, by specifying a simple and practical machine-readable solution, capable of expressing the reservation of TDM rights.

Read more details is the [CG Charter](charter.md).  

In order to [join the group](https://www.w3.org/community/tdmrep/join), you will need a (free) [W3C account](https://www.w3.org/accounts/request). Please note, however, that [W3C Membership](https://www.w3.org/community/about/faq/#is-w3c-membership-required-to-participate-in-a-community-or-business-group) is _not_ required to join a Community Group.

If you are new to Github, an interesting read is [I.Herman's introduction on the subject](https://iherman.github.io/misc-notes/docs/BasicGitHubContributionIntro). 

## Introduction

In addition to their significance in the context of scientific research, Text and Data Mining techniques (TDM) are widely used both by private and public entities to analyse large amounts of data (including copyright protected content like text, images, video etc.) in different areas of life and for various purposes, including for government services, complex business decisions and the development of new applications or technologies.

In a digital environment, TDM usage of copyright protected works can be subject to different terms and conditions, depending on the legal framework. In generic terms, an act of reproduction is required before TDM can be applied on content accessible on the Web; international laws stipulate that such act of reproduction is subject to authorization by rightsholders. So far, analyzing and processing the terms and conditions of a website, contacting rightsholders, seeking for permission and concluding licensing agreements require time and resources.  

In such context, a machine-readable solution which streamlines the communication of TDM rights and licenses available for online copyrighted content is necessary to facilitate the development of TDM applications and reduce the risks of legal uncertainty for TDM actors. Such a solution, that shall rely on a consensus by rightsholders and TDM actors, will optimize the capacity of TDM actors to lawfully access and process useful content at large scale.

The European Directive on Copyright and related rights in the Digital Single Market or [EU Directive 2019/790](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32019L0790&from=EN), better known as the "CDSM Directive", introduces two exceptions or limitations to the rights of rightsholders on lawfully accessible content, for reproductions and extractions for the purposes of TDM:

- In its Article 3, a mandatory exception for research organisations and cultural heritage institutions which carry out TDM for the purposes of scientific research.
- In its Article 4, an exception for any organisation willing to carry out TDM  for any purpose other than scientific research, including commercial purposes, which applies if the use of content for TDM has not been expressly reserved by their rights holders in an appropriate manner, such as machine-readable means. 

The European AI Act, i.e. [EU Directive 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), states that the copyright exceptions and limitations introduced in  Articles 3 and 4 of the CDSM apply to general-purpose AI models, and in particular large generative AI models. Any provider placing a general-purpose AI model on the Union market should comply with this obligation, regardless of the jurisdiction in which the copyright-relevant acts underpinning the training of those general-purpose AI models take place. Outside of the EU, advocating fair use or a similar rule is legally uncertain, as these actions are judged on a case-per-case basis.

The “opt-out” mechanism introduced by the CDMS Directive is therefore a real opportunity for TDM/AI actors and publishers across countries to define a machine-readable technique able to express not only whether mining rights on specific content are reserved or not, but also how rightsholders can be contacted and which licenses are available, if any. This is a tremendous help for TDM/AI actors from all countries looking for legal certainty.

## Documents

### Specification and guidelines

- [Specification (current version)](https://www.w3.org/2022/tdmrep/)
- [Draft Specification (upcoming version)](spec/index.html)
- [Technique based on http headers](techniques/technique-http-headers.md)
- [Technique based on a well known file hosted on the origin server](techniques/technique-file-at-origin.md)
- [Technique based on html meta tags](techniques/technique-html-meta.md)
- [Dealing with TDM Policies](techniques/tdm-policies.md)

### Adopters

- [TDMRep Adopters](docs/adopters.md)

### Useful notes

- [TDM: what does it mean in practice?](docs/tdm-meaning.md)
- [Vocabulary used during the project](docs/vocabulary.md)
- [Goals and Requirements for a technical solution](docs/requirements.md)
- [Use cases](docs/use-cases.md)

### Appendix

- [Useful extracts of the European CDSM and AI Directives](docs/eu-act-extracts.md)
- [Past and existing initiatives](docs/initiatives.md)
- [Robots.txt for non techies](docs/robots.md)
- [Github project](https://github.com/w3c/tdm-reservation-protocol)

### Illustration of the three approved techniques 

On the left, the choice of the rightsholder is conveyed as a property (or two) set in the http headers associated with the fetching of the resource. On the center, it is conveyed as a property set in a well known file hosted on the origin server. On the right it is conveyed as a property set in the html metadata of the resource itself. 

![tdmrep techniques](https://www.edrlab.org/public/tdmrep/tdmrep1.png)



# Proposal for Policies as ODRL 2.2 structures

Policies are machine-readable structures referenced from the TDM-b property defined in the specification, in case the value of TDM-a is "2". They provide ways for TDM Actors to contact content rightsholder and may offer details about available TDM licenses. Thus, they facilitate the acquisition of TDM licenses from rightsholders by TDM Actors. 

The format of policies defined in this specification is a profile of the Open Digital Rights Language 2.2, a W3C recommandation. 

## TDMRep Profile of ODRL

### Additional Action defined by this profile

This profile defines the following Action: 

*Definition*: analyse, via automated analytical technique, text and data in digital form in order to generate information which includes but is not limited to patterns, trends and correlations.

*Label*: Text & Data Mine

*Identifier*: https://edrlab.org/tdmrep/odrl-profile/tdmine

*Included in*: http://www.w3.org/ns/odrl/2/use

Notes: 
- A explanatory page will be set on the profile URL, as part of the EDRLab webpage. 
- About ODRL Policy Offers, see https://www.w3.org/TR/odrl-model/#policy-offer
- The definition of the `tdmine` action is copied from the EU Copyright Directive itself. 

### Requirements of a Policy belonging to this profile

- A Policy MUST have a `profile` property and the value of this property MUST be `https://edrlab.org/tdmrep/odrl-profile`
- A Policy MUST be of subclass `Offer`.
- A Policy MUST contain one `permission` property and no `prohibition` nor `obligation` property. 
- Every `action` property in a Policy MUST have `tdmine` as value.

## Identification of a Policy

As an ODRL structure, a Policy MUST have one `uid` property value (of type IRI [rfc3987]) to identify the Policy.

Note:
- Policy https://www.w3.org/TR/odrl-model/#policy

## Identification and contact info for the rightholder

As a member of the subclass `Offer`, a Policy MUST have one `assigner` property value, of type Party. 
The 

A Party MUST have a `uid` property. To describe more details about the Party, ODRL recommended to use W3C vCard Ontology [vcard-rdf] or FOAF Vocabulary [foaf]. 

For the sake of interoperability, this profile imposes the use of a limited number of vCard properties: "fn", "nickname", "hasEmail", "hasAddress", "hasTelephone", "hasURL".

In particular, `hasURL` designates a URL to reach in order to acquire a license. 

Notes:
- Offer https://www.w3.org/TR/odrl-model/#policy-offer
- Party https://www.w3.org/TR/odrl-model/#party 

## Identification of the target resource in a Permission

ODRL 2 specifies that a Permission MUST have one `target` property value, of type Asset or AssetCollection. 
Such value may be expressed as a JSON object or as a URI (i.e. the identifier of an Asset). 

A Policy is shared by multiple resources, therefore in this profile, the `target` property identifies "a collection of resources" via a URL which makes sense to the content provider. 

Note: The target value is not used by TDM Agents. Accessing such URL may end with an http error (403 in many cases): this is not a processing error. 

## Rules allowed in this profile

An ORDL Policy MUST have at least one property value of type Rule. Subtypes of Rules are Permission, Prohibition and Duty. 

The Policies defined here do not replace the TDMRep property TDM-a / TDM-b set via different means (http, file, html), but rather complement them. An important question is therefore: should we repeat in the Policy the permission / prohibition to mine already expressed via the TDM-a property? 

In this draft, the editor proposes to only express permission (yes / yes if), the logic being that if TDM-a expresses a prohibition (no tdm), the Policy will never be fetched by the TDM Actor. Expressing in ODRL Policies what is already expressed with a different format (in e.g. http headers or a "file on the origin server") could lead to many ambiguities for implementers.

Note: looking at the similarities between the structure we obtain here and the [Proposal based on a file hosted on the origin server](./proposal-file-at-origin.md)), we could decide to merge both ... In such a case, the `target` URL must point to the folder containing every resource associated with this Policy and pattern matching must be allowed: a slight departure from the RDF purity of ODRL. Or the `target` must become an AssetCOllection object with a `source` property, pure but more verbose. 

## Constraints on the type of usage

ODRL 2 specifies that a Permission may have one `constraint` property value of type Constraint. 

This profile uses one value from the ODRL Vocabulary for the `leftOperand`:

- `purpose` creates a constrain on a usage of the mined content.

This profile defines two corresponding values for the `rightOperand`:

- `research` designates research purposes.
- `commercial` designates any non-research purposes.

Using these values, a rightsholder can constraint TDM usage to research purposes only. 

Notes:
- Purpose: https://www.w3.org/TR/odrl-vocab/#term-purpose

## Constraints on geographical areas

This profile uses one value from the ODRL Vocabulary for the `leftOperand`:

- `spatial` creates a constrain on a geographical location of the TDM Agent.

This profile uses one value from the ODRL Vocabulary for the `operator`:

- `isPartOf` indicates that a given value is contained by the right operand of the constraint.

This profile defines the possible values of each item of the `rightOperand`, expressed as an array:

- `urn:iso:3166:` followed by a 3 letter code designates an iso3166 3 letter country code.

Notes:
- Geospacial Named Area: https://www.w3.org/TR/odrl-vocab/#term-spatial
- Expressing the code as a full URI avoids declaring aliases in the @context part of the structure when used (which is tricky JSON-LD stuff as we want to use the odrl contect directly).
- Using only iso3166 alpha3 provides better interoperability results; the alpha3 list is more complete than the alpha2. 
- The urn form was found in https://www.hl7.org/fhir/iso3166.html and simplified from there. It's a pity that there is not proper standard form for that. 
- Enabling the expression of "allowed here, denied there", "allowed everywhere but" ... would add a lot to the complexity. 

## Payment Duties

ODRL 2 specifies that a Permission may have one `duty` property value of type Duty. 

This profile defines one value for the `action` property of the `duty` property:

- `compensate` is a request for payment for mining the content.

Notes:
- A future extension could allow rightsholders to detail the amount (& currency) they are expecting. 

## Examples

### Example 1

In this example, the rightsholder expresses detailed contact information using the W3C vCard Ontology. 
He agrees that TDM Actors from any country can mine its research papers:

```json
{
  "@context": "http://www.w3.org/ns/odrl.jsonld",
  "@type": "Offer",
  "uid": "https://provider.com/policy/1",
  "profile": "https://edrlab.org/tdmrep/odrl-profile",
  "assigner": {
    "uid": "https://provider.com",
    "vcard:fn": "Provider",
    "vcard:nickname": "PRV",
    "vcard:hasEmail": "mailto:contact@provider.com",
    "vcard:hasAddress": {
      "vcard:country-name": "Belgium",
      "vcard:locality": "WonderCity",
      "vcard:postal-code": "5555",
      "vcard:street-address": "111 Lake Drive"
    },
    "vcard:hasTelephone": "tel:+61755555555",
    "vcard:hasURL": "https://provider.com/tdm/licensing.html" 
  },
  "permission": [{
    "target": "https://provider.com/research-papers",
    "action": "tdmine"
    }
  ]
}
```

### Example 2

In this example, the rightsholder agrees that TDM Actors from any country can mine its content only if they are mining for research purpose:

```json
{
  "@context": "http://www.w3.org/ns/odrl.jsonld",
  "@type": "Offer",
  "uid": "https://provider.com/policy/1",
  "profile": "https://edrlab.org/tdmrep/odrl-profile",
  "assigner": {
    "uid": "https://provider.com",
    "vcard:fn": "Provider",
    "vcard:hasEmail": "mailto:contact@provider.com"
  },
  "permission": [{
      "target": "https://provider.com/research-papers",
      "action": "tdmine",
      "constraint": [{
        "leftOperand": "usage",
        "operator": "eq",
        "rightOperand": "research"
        }
      ]
    }
  ]
}
```

### Example 3

In this example, the rightsholder agrees that TDM Actors from any country can mine its content only if they are ready to pay a fee:

```json
{
  "@context": "http://www.w3.org/ns/odrl.jsonld",
  "@type": "Offer",
  "uid": "https://provider.com/policy/1",
  "profile": "https://edrlab.org/tdmrep/odrl-profile",
  "assigner": {
    "uid": "https://provider.com",
    "vcard:fn": "Provider",
    "vcard:hasEmail": "mailto:contact@provider.com"
  },
  "permission": [{
      "target": "https://provider.com/research-papers",
      "action": "tdmine",
      "duty": [{
        "action": "compensate"
        }
      ]
    }
  ]
}
```
### Example 4

In this example, the rightsholder agrees that TDM Actors from Canada and Brazil only can mine his content:

```json
{
  "@context": "http://www.w3.org/ns/odrl.jsonld",
  "@type": "Offer",
  "uid": "https://provider.com/policy/1",
  "profile": "https://edrlab.org/tdmrep/odrl-profile",
  "assigner": {
    "uid": "https://provider.com",
    "vcard:fn": "Provider",
    "vcard:hasEmail": "mailto:contact@provider.com"
  },
  "permission": [{
      "target": "https://provider.com/research-papers",
      "action": "tdmine",
      "constraint": [{
        "leftOperand": "spatial",
        "operator": "isPartOf",
        "rightOperand": ["iso3166-3:can", "iso3166-3:bra"]
        }
      ]
    }
  ]
}
```

## References

- [ODRL Information Model 2.2](https://www.w3.org/TR/odrl-model)
- [ODRL VOcabulary & Expression 2.2](https://www.w3.org/TR/odrl-vocab/)
- [vCard rdf](https://www.w3.org/TR/vcard-rdf/)
- [IPTC external controlled vocabularies](https://cvx.iptc.org/)







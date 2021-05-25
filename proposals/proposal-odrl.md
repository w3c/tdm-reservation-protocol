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
- The definition of the datamine action is copied from the EU Copyright Directive itself. 

### Requirements of a Policy belonging to this profile

- A Policy MUST have a `profile` property and the value of this property MUST be `https://edrlab.org/tdmrep/odrl-profile`
- A Policy MUST be of subclass `Offer`.
- All `action` properties in a Policy MUST have a `tdmine` value.

## Identification of a Policy

As an ODRL structure, a Policy MUST have one `uid` property value (of type IRI [rfc3987]) to identify the Policy.

Note:
- Reference https://www.w3.org/TR/odrl-model/#policy

## Identification and contact info for the rightholder

As a member of the subclass `Offer`, a Policy MUST have one `assigner` property value, of type Party. 
The 

A Party MUST have a `uid` property. To describe more details about the Party, ODRL recommended to use W3C vCard Ontology [vcard-rdf] or FOAF Vocabulary [foaf]. This profile recommends the use of a limited number of vCard properties: "fn", "nickname", "hasEmail", "hasAddress", "hasTelephone".

This profile defines a new property called `licensing` which designates a URL to reach in order to acquire a license. 

Examples are given below.

Notes:
- Reference for Offer https://www.w3.org/TR/odrl-model/#policy-offer
- Reference for Party https://www.w3.org/TR/odrl-model/#party 
- Reference for vCard rdf https://www.w3.org/TR/vcard-rdf/

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

## Constraints on the type of usage expressed in a Permission

ODRL 2 specifies that a Permission may have one `constraint` property value of type Constraint. 

This profile defines one value for the `leftOperand`:

- `usage` constrains on a usage of the mined content.

This profile defines one value for the `rightOperand`:

- `research` designates research purposes.
- `commercial` designates any non-research purposes.

Using these values, a rightsholder can constraint TDM usage to research purposes only. 

Examples are given below.

## Payment Duties

ODRL 2 specifies that a Permission may have one `duty` property value of type Duty. 

This profile defines one value for the `action` property of the `duty` property:

- `compensate` is a request for payment for mining the content.

Examples are given below.

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
    "fn": "Provider",
    "nickname": "PRV",
    "hasEmail": "mailto:contact@provider.com",
    "hasAddress": {
      "country-name": "Belgium",
      "locality": "WonderCity",
      "postal-code": "5555",
      "street-address": "111 Lake Drive"
    },
    "hasTelephone": "tel:+61755555555",
    "licensing": "https://provider.com/tdm/licensing.html" 
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
    "fn": "Provider",
    "hasEmail": "mailto:contact@provider.com"
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
    "fn": "Provider",
    "hasEmail": "mailto:contact@provider.com"
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






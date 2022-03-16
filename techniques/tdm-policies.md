# Dealing with TDM Policies

## Status of this document

This is a best practices document, its aims is to help implementors handling with TDM Policies and it may evolve over time.

The related section of the specification is [Expressing a TDM Policy](https://w3c.github.io/tdm-reservation-protocol/spec/#sec-policy). 

## How TDM miners should identify the content they want to mine?

An issue TDM Actors are facing is that when scrapping a server, TDM Agents will retrieve large series of resources for which TDM Rights are reserved and a TDM Policy is set. 

If the policy states that consent must be obtained, it would be illogical to send an email for each and every resource the TDM Actor is willing to mine. The good thing is that TDM Policies have a URL which is a first mean to de-duplicate such requests, and a `permission` / `target` property as a second mean to achieve optimal de-duplication (several Policy URLs could reference the same target). 

Reminder: the mandatory `target` of a `permission` is a URI identifying the collection of resources involved in the policy.

TDM Agents will use the value of this `target` property in their messages to publishers, to identify a collection of resources they wish to mine. This identifier shall therefore properly identify a specific collection of resources and be well know from their publisher.

The process a TDM Agent follows can be:

* Check every resource for TDM properties
* For each resource having TDM Rights reserved and a TDM Policy set
  * retrieve the TDM Policy if its URL is not already in the cache, and cache the URL and the content of the TDM Policy (at least `permission` / `target`).
* Group the resources by `permission` / `target`.
* For each group, send an email to a publisher stating the desire to "mine the collection of resources identified by the following target value: 'https://provider.com/research-papers' ".

Note: The `target` value is not necessarily dereferencable. Accessing this URL may end with an http error (403 in many cases): this is not a processing error.


## Possible extensions

### Constraints on geographical areas

A permission MAY be completed with a geographical constraint. 

This profile uses one value from the ODRL Vocabulary for the `leftOperand`:

- `spatial` creates a constraint on a geographical location of the TDM Agent.

This profile uses one value from the ODRL Vocabulary for the `operator`:

- `isPartOf` indicates that a given value is contained by the right operand of the constraint.

This profile defines the possible values of each item of the `rightOperand`, expressed as an array:

- `urn:iso:3166:` followed by a 3 letter code designates an iso3166 3 letter country code.

Notes:
- Geospatial Named Area: https://www.w3.org/TR/odrl-vocab/#term-spatial
- Expressing the code as a full URI avoids declaring aliases in the @context part of the structure when used (which is tricky JSON-LD stuff as we want to use the odrl contect directly).
- Using only iso3166 alpha3 provides better interoperability results; the alpha3 list is more complete than the alpha2. 
- The urn form was found in https://www.hl7.org/fhir/iso3166.html and simplified from there. It's a pity that there is not proper standard form for that. 
- Enabling the expression of "allowed here, denied there", "allowed everywhere but" ... would add a lot to the complexity. 


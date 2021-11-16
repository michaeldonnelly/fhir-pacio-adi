
This section defines additional requirements and guidance relevant to this guide as a whole. The conformance verbs - **SHALL**, **SHOULD**, **MAY** - used in this guide are defined in [FHIR Conformance Rules](http://hl7.org/fhir/R4/conformance-rules.html).


### Claiming Conformance to a PACIO ADI Profile
To claim conformance to a profile in this guide, servers **SHALL**:

- Be able to populate all profile data elements that have a minimum cardinality >= 1 and/or flagged as Must Support as defined by that profile’s StructureDefinition.
- Conform to the [PACIO ADI Capability Statement](CapabilityStatement-padi.html) expectations for that profile’s type.
<!-- TODO note about what profiles must be supported?-->

### Must Support
The following rules apply to all PACIO ADI Profile elements marked as Must Support. Must Support on any profile data element **SHALL** be interpreted as follows:


#### Data Source System Requirements

- Data Sources Systems **SHALL** be capable of populating all data elements as part of the query results as specified by the [PACIO ADI Capability Statement](CapabilityStatement-padi.html).

#### Data Consumer System Requirements

- Data Consumer Systems **SHALL** be capable of displaying the data elements for human use.
- Data Consumer Systems **SHOULD** be capable of storing the data elements for other uses (such record keeping of data used for clinical use).
- Data Consumer Systems **SHALL** be capable of processing resource instances containing the data element without generating an error or causing the application to fail.
- Data Consumer Systems **SHALL** interpret missing data elements within resources instances as not being present on the Data Sources system’s or as being withheld for privacy or business reasons.
- Data Consumer Systems **SHALL** be able to process resource instances containing data elements asserting missing information. Data Consumer Systems are not required to process assertions of missing data. Assertion of missing information may be expressed using an appropriate value set code (such as nullFlavor) where available or using a dataAbsentReason extension.

Profiles used by this guide, but defined in other implementation guides inherit the definition of Must Support from their respective guides.

### Must Support of CodeableConcept Text Elements

The area of advance directive interoperability is relatively new and codes capturing the concepts related to advance directives are not well established or well known. This implementation guide provides several codes for expressing this information but specifies extensible bindings to use other code systems where necessary. These code systems may also not be well-known. 
Additionally, there are not widely accepted universal or national for standards for capturing this information. Different scopes of use and jurisdictions capture and organize this information in different ways. As such, it is important for data sources to capture this information as it is presented and for data consumer systems to be able to present it the same way to users. 

To that end, several `CodeableConcept` `text` data elements are marked as Must Support. 

Per the FHIR Standard for [Using Text in CodeableConcept](https://www.hl7.org/fhir/datatypes.html#CodeableConcept): 
> The `text` is the representation of the concept as entered or chosen by the user, and which most closely represents the intended meaning of the user or concept. Very often the `text` is the same as a `display` of one of the codings. One or more of the codings may be flagged as the user selected code - the code or concept that the user selected directly.

In some cases a code may not exist for a particular concept, in such cases, it is possible to provide a free text only representation of the concept in the `CodeableConcept` `text` element without any 'coding' elements present.

For example, using text only, the `Goal.category` element would be:

    "valueCodeableConcept": {
        "text": "Free text concept description"
    }

### Must Support of Resource Text Elements

Because advance directive interoperability is relatively new and there are not any widely accepted universal or national for standards for capturing this information, advance directives may be represented in many different ways. It is important that this information be communicated as it is meant and that it is received and viewable in that same manner. 

To address this need, most of the profiles in this implementation guide require the resource instance's `text` element (cardinality `1..1`).

The `text` element of a resource is a [Narrative](http://hl7.org/fhir/R4/narrative.html#Narrative) data type. The `status` element of this data type indicates whether the text is generated by a system based on the structured data in the resource or if it contains additional information. The `status` element is required. 

For the purposes of this implementation guide, it is expected that most implementations will have resource instances that have additional data in the `text` than is captured in the structured data. When that is the case, the narrative `text.status` **SHALL** be `additional`.

### Document Bundles and Constituent Resources

<!--[TODO]--> 
This guide requires the interoperability of Advance Directive Information through the use of wholly contained documents as part of its use case. While it is required that this data be made interoperable as a collection of Advance Directive Information in document Bundles, systems may decide to make use of the constituent resources as separate resources for additional uses and purposes, such as use in support of Clinical Decision Support 

### Advance Directive Native FHIR Document Structure Requirements

DocumentReference, Binary, Bundle

### Document Digital Signatures

### Replacing Documents


### Deprecating Documents

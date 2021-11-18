
This section provides additional guidance on the relationship between the associated profiles and the structure of the advance directive document.

### Profile & Resource relationships

Advance directive documents may take several forms including scanned PDF documents, CDA documents and native FHIR documents. This guide defines interoperability to support any number of types, though focuses on native FHIR documents.

All documents, regardless of format is saved in the Binary resource and is available through the Binary endpoint. FHIR native documents **SHALL** be Bundle resources with `type` = `document` and encoded as a Binary resource. Documents that are communicated **SHALL** have at least one DocumentReference resource that references the Binary though the `DocumentReference.content.attachment.url`.

The DocumentReference is the resource that is used for "indexing" of documents and can be used for searching and finding documents with specific attributes such as type of document, subject, or dates.

<img src="./ADI_profile_resource_relationships.png" alt="Profile & Resource relationships"  style="width: 100%; float: none; align: middle;"/>

Digital signatures are defined as optional in this guide. If supported, the digital signature will be a captured in a Binary resource that is referenced by an additional DocumentReference resource.

### Document Structure

ADI FHIR native documents are instances of the Bundle resource with the `type` = `document`. The document should have all content contained within the Bundle with no external references except for the references to external documents in the [DocumentationObservation](StructureDefinition-PADI-DocumentationObservation.html).focus. FHIR Bundle documents consist or multiple entry resources within it, with the first entry being a Composition resource. The Composition resource acts as the header and organizational construct. It contains information about the document such as the category of document, dates, and references to the various participants of the document, as well as document sections used to categorize or organize the contains entries.

The Advance Directive Interoperability document defines 7 sections:
1. Healthcare Agent - Healthcare agents, healthcare agent advisors, and consent regarding their roles, powers, and limitations
2. Quality of Life (Care Experience Preferences) - Quality of Life related personal care experiences, personal goals, and priorities
3. End of Life/Emergency Intervention Preferences (Under Certain Health Conditions) - Preference CarePlans that contain the persons goals to be considered active under specific situations or conditions
4. Goals, Preferences, and Priorities Upon Death - Goals, preferences, and priorities a person has at the time of or soon after there death
5. Additional Documentation - Observations regarding the existence of other advance directive related information
6. Witness & Notary - References and information regarding witnesses and notary
7. Administrative Information - Administrative information associated with this personal advance care plan

<img src="./ADI_DocumentStructure.png" alt="Advance Directive Document Structure"  style="width: 100%; float: none; align: middle;"/>

#### Clause Extension
Advance directives documents often have additional information or clauses related to specific areas of the document. This may include things like additional information about the conditions under which a healthcare agent has been selected, whether a healthcare agent has been notified of or accepted their role as such, or other information that provides context to the data otherwise expressed in the sections or entries of a document. To support this information this guide has defined a [Clause extension] to all of the Composition sections and various profiles and elements.
# CBS event using MHD

To store a case-based surveillance event we send a **FHIR transaction bundle** to Hearth containing 3 things and some extras:

  1. **The document manifest** - describes the purpose of the document and it's context (links to patient, practitioner etc)
  2. **The document reference** (referenced by the document mainfest) - describes where to find the document, the `content.attachment.url` property will reference the binary reference below
  3. **The the Binary resource** (referenced by the document reference)
  4. **Any other resources** that are referenced in the bundle link patient

The binary resource will contain a base64 encoded version of something similar to a subset of [fhir-document.json](fhir-document.json) depending on the events we are sending. It also contains references to related resources from the document manifest like patient and practitioner.

Hearth can process FHIR transactions and will store the individual resources. It can also notice FHIR documents being stored in binary resources if the correct FHIR content-type is used and it will break those resources out and store them individually as well.

# Fast Healthcare Interoperability Resources (FHIR)

## Introduction
FHIR is a standard for interoperability with the main function to provide the exchange of healthcare data between stakeholders involved in the healthcare scene, such as patients, doctors, caregivers, and researchers. It consists of two parts: a content model in the form of resources and a specification for the exchange of information provided under the RESTful API as well as Messaging and Documents.

## Setup with OpenEMR
### Prerequisites
FHIR is a standard. This means that there are many software out there providing each of their own implementations to the standard, including the free and open-source OpenEMR.

By using OpenEMR, one needs to understand that OpenEMR needs to be installed first. One also needs to enable the Standard FHIR service (or the `/fhir/` endpoints in OpenEMR menu.

One is able to access the settings under Administration -> Globals -> Connectors -> "Enable OpenEMR Standard FHIR REST API".

## Features
### Multisite support
FHIR with OpenEMR supports multisite. When multisite is enabled, the access path will be on `apis/default/fhir/patient` if using the `default` option, otherwise the access path will be on `apis/alternate/fhir/patient`.

### Authorization
OpenEMR uses OIDC-compliant authorization for API. SSL is required and setting baseurl at Administration -> Globals -> Connectors -> 'Site Address (required for OAuth2 and FHIR)' is required. [This document](https://github.com/openemr/openemr/blob/master/API_README.md#authorization) lists out more details about authorization with OpenEMR and FHIR.

## External sources
- [Support for FHIR API by OpenEMR](https://github.com/openemr/openemr/blob/master/FHIR_README.md)
- [The FHIR standard](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=491)

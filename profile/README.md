# MOSIP Modules Overview

The **Modular Open Source Identity Platform (MOSIP)** is an open-source, modular platform designed to help governments and organizations build secure, scalable, and customizable digital identity systems. Below is an overview of MOSIP’s key modules, their purposes, functionalities, key features, and links to their respective GitHub repositories. All modules are licensed under the Mozilla Public License 2.0 and hosted on GitHub.

## 1. Pre-Registration Module
### Purpose
Facilitates online appointment booking and data collection while managing crowds at registration centers by allowing users to pre-fill and validate demographic information before their visit.

### Functionality
- Enables residents to enter demographic details (e.g., name, address) and schedule appointments via a web portal or mobile app.
- Reduces congestion at registration centers and improves data accuracy.
- Supports integration with external systems for validation (e.g., civil registries).

### Key Features
- User-friendly interface for data entry.
- Appointment scheduling and notifications.
- Data pre-verification to minimize errors during registration.

### GitHub Repository
[mosip/pre-registration](https://github.com/mosip/pre-registration)

## 2. Registration Client Module
### Purpose
Captures demographic and biometric data at registration centers using an offline-first thick client that operates offline or partially online, collects evidence for demographic data, and interacts with the Pre-Registration Module to fetch pre-filled data.

### Functionality
- Collects data such as fingerprints, iris scans, facial images, and demographic details.
- Operates on offline-capable devices to support remote areas with limited connectivity.
- Securely packages data for transmission to the backend.

### Key Features
- Supports multiple biometric devices adhering to MOSIP’s standards.
- Performs local deduplication to identify duplicate registrations.
- Offers configurable workflows to meet country-specific requirements.

### GitHub Repository
[mosip/registration-client](https://github.com/mosip/registration-client) (Desktop Client)  
[mosip/android-registration-client](https://github.com/mosip/android-registration-client) (Android Client, a tablet-based portable version designed for mobility and accessibility in remote areas)

## 3. Registration Processor Module
### Purpose
Processes and validates information collected by the Registration Client, including PII, operator, introducer, evidence, biometrics, and other trust elements. Designed as an Apache Camel workflow with Vert.x-based stages grouped under Docker, it interacts with ABIS and a deduplication engine to deduplicate data, receiving input from the Registration Client and outputting to the ID Repository, print, and notification systems.

### Functionality
- Conducts quality checks on biometric and demographic data.
- Performs deduplication using ABIS (Automated Biometric Identification System) to prevent duplicate identities.
- Routes data through configurable workflows (e.g., manual adjudication for flagged cases).

### Key Features
- Scales to handle millions of registrations.
- Supports parallel processing for efficiency.
- Integrates with external systems for additional verification (e.g., civil registries).

### GitHub Repository
[mosip/registration](https://github.com/mosip/registration)

## 4. ID Repository Module
### Purpose
Securely stores and manages processed identity information, assigns a Unique Identification Number (UIN) or token to each resident, and is responsible for extraction, credential creation, and issuance of digital or physical credentials for internal and resident usage.

### Functionality
- Serves as the central database for demographic and biometric data.
- Assigns a Unique Identification Number (UIN) or token to each resident.
- Ensures data encryption and access control to protect privacy.
- Creates identity credentials such as ID cards, digital IDs, or QR codes.
- Supports secure delivery of credentials (e.g., via mobile apps or physical cards).
- Integrates with printing and issuance partners.

### Key Features
- Employs zero-knowledge architecture (data is encrypted; even administrators cannot access it without authorization).
- Supports data sovereignty (data remains within the country’s borders).
- Scales for large populations.
- Provides customizable credential formats (e.g., smart cards, digital wallets).
- Incorporates secure encryption and anti-counterfeiting measures.
- Supports offline verification for credentials.

### GitHub Repository
[mosip/id-repository](https://github.com/mosip/id-repository)

## 5. Authentication Module
### Purpose
Verifies identities for access to services through APIs as an independent module, also known as IDA, separate from the Registration Processor and ID Repository. Supports multiple instances for a single ID Repository and provides authentication using OTP, biometric, demographic, and cryptographic key methods.

### Functionality
- Supports multiple authentication methods: biometric (fingerprint, iris, face), demographic, OTP, and token-based.
- Integrates with relying parties (e.g., banks, government agencies) via APIs.
- Handles authentication requests in real-time or offline (e.g., via QR codes).

### Key Features
- Adheres to standards like OAuth 2.0 and OpenID Connect.
- Offers configurable authentication policies (e.g., single-factor or multi-factor).
- Scales to handle high transaction volumes.

### GitHub Repository
[mosip/id-authentication](https://github.com/mosip/id-authentication)

## 6. Resident Services Module
### Purpose
Provides self-service tools utilized by residents through an online portal. The Resident Portal is a web-based user interface application that offers services related to the residents' Unique Identification Number (UIN), allowing residents to perform various operations related to their UIN or Virtual ID (VID) and raise any concerns they may have.

### Functionality
- Provides a portal or app for residents to update demographic details, request replacement credentials, or revoke access.
- Supports self-service features like address updates or lost ID reporting.
- Enables consent management for data sharing with third parties.

### Key Features
- Offers a user-friendly interface for non-technical users.
- Supports multiple languages for accessibility.
- Maintains audit trails for all resident-initiated actions.

### GitHub Repository
[mosip/resident-ui](https://github.com/mosip/resident-ui) (Resident Portal user interface)  
[mosip/resident-services](https://github.com/mosip/resident-services) (Backend services for the Resident Portal)

## 7. Partner Management Module
### Purpose
Provides a single portal to manage the growing ecosystem of partners, including biometric device providers, printers, and authentication partners, essential for a digital ID system as the partner ecosystem expands post-MOSIP deployment.

### Functionality
- Onboards and certifies technology partners (e.g., biometric device providers, ABIS vendors).
- Ensures compliance with MOSIP’s standards and APIs.
- Monitors partner performance and security.

### Key Features
- Promotes a vendor-neutral ecosystem to avoid lock-in.
- Provides API-driven integration for seamless interoperability.
- Maintains a marketplace for certified partners.

### GitHub Repository
[mosip/partner-management-services](https://github.com/mosip/partner-management-services) (Backend services for partner management)  
[mosip/partner-management-portal](https://github.com/mosip/partner-management-portal) (Partner Management Portal UI)

## 8. Administration Module
### Purpose
Helps in setting up all master data and field-related operations and management, such as zone mapping, and provides a user interface to upload packets in case of a faulty machine in the field.

### Functionality
- Configures system parameters and master data.
- Manages user roles and access controls for operators.
- Supports the zone mapping and center management.

### Key Features
- Supports configuration of master data and system parameters, including zone mapping.
- Provides a user-friendly interface for packet uploads from faulty field machines.
- Enables secure management of user roles and access controls.

### GitHub Repository
[mosip/admin-services](https://github.com/mosip/admin-services) (Backend services for administration)  
[mosip/admin-ui](https://github.com/mosip/admin-ui) (Administration user interface)

## 9. Analytics and Reporting Module
### Purpose
An optional module used to generate reports from anonymous profiles, with built-in access to vital data to support continuous reporting and monitoring of registrations and authentications.

### Functionality
- Tracks registration progress, authentication success rates, and system uptime.
- Provides anonymized analytics for policy decisions (e.g., coverage in rural areas).
- Supports compliance reporting for regulators.

### Key Features
- Offers customizable reports for different stakeholders.
- Integrates with external analytics tools.
- Ensures privacy-preserving data aggregation.

### GitHub Repository
[mosip/reporting](https://github.com/mosip/reporting)

## Additional Notes
- **Interoperability**: Each module integrates with external systems (e.g., civil registries, OpenG2P) via standardized APIs.
- **Customization**: Modules can be adapted to meet legal, cultural, and technical requirements.
- **Open Source**: All code is available on GitHub under the Mozilla Public License 2.0.
- **Scalability**: Designed for populations of millions, with cloud-native and on-premise deployment options.
- **Configuration**: Module configurations are stored in the [mosip/mosip-config](https://github.com/mosip/mosip-config) repository.
- **Infrastructure**: Deployment scripts and Kubernetes configurations are available in [mosip/mosip-infra](https://github.com/mosip/mosip-infra).

## Getting Started
To explore MOSIP’s source code, fork the relevant repositories and refer to the [MOSIP Documentation](https://docs.mosip.io) for setup guides. For contribution guidelines, see the [Contributor Guide](https://docs.mosip.io/1.2.0/community/code-contributions).

## License
All core MOSIP modules are licensed under the [Mozilla Public License 2.0](https://www.mozilla.org/en-US/MPL/2.0/).
All reference MOSIP modules are licensed under the [MIT License](https://mit-license.org/).
Please look at the individual repostories for the correct license.

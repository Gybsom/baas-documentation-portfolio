## Release Notes

### **Version 2.0.0 - September 29, 2025**

We are excited to announce the release of BaaS Platform v2.0.0. This major update introduces powerful new payment capabilities to enhance your application.

#### 🚀 New Features

* **Boleto Payments:** You can now offer your users the ability to pay boletos directly from their accounts. The new `/boletos` endpoints allow you to validate boleto information and process payments securely.
* **Pix Transfers:** We have integrated with Brazil's instant payment network. The new `/pix` endpoints enable you to create and manage instant transfers using Pix keys, providing a faster and more convenient payment experience.

#### 🔧 Fixes

* Improved the performance of the account balance retrieval endpoint.
* Fixed a bug where transaction history was not correctly displaying timestamps in UTC.

#### ⚠️ Breaking Changes

* The authentication endpoint `POST /auth/login` now returns a structured object `{"token": "your_jwt_token"}` instead of a plain text token. Please update your integration to handle the new response format.

---

### **Version 1.0.0 - March 15, 2025**

Welcome to the BaaS Platform! We are thrilled to announce our official public launch. Our mission is to provide developers with a simple, robust, and secure platform to embed financial services into any application.

Version 1.0.0 marks our foundational release, providing the core building blocks for digital banking experiences.

#### ✨ Core Features at Launch

* **Accounts API (`/accounts`):** A full suite of endpoints to programmatically create and manage user accounts. Includes functionalities for opening, closing, and retrieving account details.
* **Balance and Statements (`/accounts/{id}/balance`, `/accounts/{id}/statement`):** Secure endpoints to instantly check account balances and retrieve detailed transaction histories.
* **Internal P2P Transfers (`/transfers`):** Enable seamless peer-to-peer money transfers between accounts within the BaaS ecosystem.
* **Secure Authentication:** Robust, token-based authentication (`Bearer Token`) to ensure all API communications are secure.

#### Developer Experience

* **Sandbox Environment:** A fully-featured sandbox is available from day one, allowing you to test your integration thoroughly before going into production.
* **Comprehensive Documentation:** We launch with a commitment to clear and complete documentation, covering guides, detailed API references, and tutorials to help you get started quickly.

We are incredibly excited to see what you will build with the BaaS Platform. Thank you for being with us from the very beginning!
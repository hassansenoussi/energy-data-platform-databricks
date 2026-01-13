# 4. Data Governance and Security

## 4.1 Governance Objectives
The governance framework ensures that data is:
- secure and protected
- accessible only to authorized users
- reliable and traceable
- compliant with regulatory requirements

Governance is treated as a core component of the platform, not as an afterthought.

---

## 4.2 Data Sensitivity and Classification
Data handled by the platform is classified into categories:

- **Public Data**  
  Aggregated and anonymized datasets used for analytics.

- **Internal Data**  
  Operational and reference data with no direct personal identifiers.

- **Sensitive Data**  
  Customer-related data that may fall under GDPR regulations.

This classification drives access control and protection mechanisms.

---

## 4.3 Access Control and Roles
Access to the platform follows the principle of least privilege.

Defined roles include:
- **Platform Admin**: infrastructure and security management
- **Data Engineer**: pipeline development and maintenance
- **Data Analyst**: access to Gold datasets only
- **Data Scientist**: access to curated datasets for ML use cases

Raw (Bronze) data access is restricted to technical roles only.

---

## 4.4 Data Protection Mechanisms
The following mechanisms are implemented:
- anonymization of customer identifiers
- masking of sensitive attributes
- encryption at rest and in transit
- audit logs for data access

Sensitive fields are never exposed directly to BI users.

---

## 4.5 Regulatory Considerations (GDPR)
The platform design considers GDPR principles:
- data minimization
- purpose limitation
- traceability of data usage
- ability to remove or anonymize personal data

All datasets used in this project are simulated and non-identifying.

---

## 4.6 Data Lineage and Traceability
Data lineage is ensured through:
- Medallion Architecture separation
- versioned Delta Lake tables
- reproducible pipelines
- documented transformations

This enables auditability and simplifies issue investigation.

---

## 4.7 Governance Limitations
Known governance limitations:
- simplified role model
- no automated data catalog integration
- manual review of access policies

These limitations are acceptable for a proof-of-concept platform and can be extended later.

# 5. Costs, Risks and Limitations

## 5.1 Cost Considerations
Databricks costs are primarily driven by compute usage rather than storage.

Main cost drivers include:
- size and type of Databricks clusters
- job execution frequency
- inefficient Spark transformations
- idle compute resources

Cost optimization strategies:
- use of autoscaling clusters
- separation of development and production environments
- termination of inactive clusters
- optimized data partitioning and caching strategies

Cost control is considered a design requirement, not an operational afterthought.

---

## 5.2 Technical Risks

### Data Volume and Performance
Risk:
- inefficient handling of large time-series datasets may lead to performance degradation

Mitigation:
- partitioning by date
- use of Delta Lake optimizations
- query performance monitoring

---

### Data Quality Issues
Risk:
- inconsistent or incomplete source data affecting analytics reliability

Mitigation:
- data validation rules in Silver layer
- data quality checks before Gold exposure
- logging and alerting mechanisms

---

### Platform Complexity
Risk:
- Databricks learning curve for new users

Mitigation:
- standardized notebooks
- clear documentation
- limited technology scope

---

## 5.3 Security and Compliance Risks
Risk:
- unauthorized access to sensitive data

Mitigation:
- role-based access control
- data masking and anonymization
- audit logging

---

## 5.4 Project Limitations
The following limitations are acknowledged:
- batch-oriented ingestion only
- simplified data sources
- no real-time streaming implementation
- no automated CI/CD pipeline

These limitations are acceptable for a proof-of-concept and learning-oriented project.

---

## 5.5 Future Improvements
Potential future enhancements include:
- introduction of real-time streaming ingestion
- advanced anomaly detection models
- integration with a data catalog
- implementation of CI/CD pipelines
- advanced cost monitoring and optimization

---

## 5.6 Risk Acceptance
All identified risks and limitations are documented and accepted as part of the project scope, with clear mitigation strategies defined.

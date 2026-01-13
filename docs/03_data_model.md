# 3. Data Model and Analytical Design

## 3.1 Modeling Approach
The data model is designed to support analytical workloads rather than transactional operations.

Key principles:
- simplicity and clarity
- separation between reference data and fact data
- explicit handling of time-series data
- alignment with the Medallion Architecture

The model evolves progressively from raw ingestion (Bronze) to business-ready datasets (Gold).

---

## 3.2 Core Business Entities

### Customer
Represents an energy customer (individual or company).

Key attributes:
- customer_id
- customer_type (B2C, B2B)
- region
- anonymized identifiers (when applicable)

---

### Contract
Represents the contractual relationship between a customer and the energy provider.

Key attributes:
- contract_id
- customer_id
- contract_type
- start_date
- end_date

A customer may have multiple contracts over time.

---

### Meter
Represents a physical or logical energy meter.

Key attributes:
- meter_id
- contract_id
- meter_type
- installation_date

Each contract may be associated with one or more meters.

---

### Energy Consumption
Represents measured energy consumption values.

Key attributes:
- meter_id
- timestamp
- consumption_value (kWh)
- measurement_quality_flag

This entity is the primary time-series dataset of the platform.

---

### Energy Price
Represents energy pricing information.

Key attributes:
- price_date
- energy_type
- unit_price

---

## 3.3 Logical Data Model
The logical relationships between entities are as follows:

Customer → Contract → Meter → Energy Consumption  
Energy Price → Energy Consumption (via date alignment)

This structure enables:
- customer-level consumption analysis
- contract-based reporting
- time-based aggregations
- cost estimation use cases

---

## 3.4 Medallion Layer Mapping

### Bronze Layer
- raw_customer
- raw_contract
- raw_meter
- raw_consumption
- raw_energy_price

Characteristics:
- minimal transformations
- original schema preserved
- ingestion metadata added

---

### Silver Layer
- dim_customer
- dim_contract
- dim_meter
- fact_energy_consumption
- dim_energy_price

Characteristics:
- cleaned and standardized schemas
- enforced data types
- deduplication and validation
- referential consistency

---

### Gold Layer
- gold_daily_consumption_by_customer
- gold_consumption_anomalies
- gold_energy_cost_summary

Characteristics:
- aggregated datasets
- business-oriented metrics
- optimized for BI and analytics

---

## 3.5 Time-Series Considerations
Energy consumption data is handled as a high-volume time-series dataset.

Design considerations:
- partitioning by date
- efficient filtering on time ranges
- support for rolling window aggregations
- late-arriving data handling

---

## 3.6 Data Quality Rules (High-Level)
Examples of enforced rules:
- consumption_value ≥ 0
- mandatory foreign keys in Silver layer
- uniqueness constraints on reference entities
- timestamp consistency checks

Data quality rules are applied progressively from Silver to Gold layers.

---

## 3.7 Model Limitations
Known limitations of the current model:
- batch-oriented processing only
- simplified pricing logic
- no real-time meter calibration logic

These limitations are accepted to keep the model understandable and extensible.

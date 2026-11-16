

\# Day 2 – MES Architecture \& ISA-95 Information Flow



\## 1. Learning Objectives



\- Understand typical industrial MES architecture.

\- Understand how ERP, MES, SCADA, PLC and databases interact.

\- Understand ISA-95 Levels 0–4.

\- Trace production-order information from SAP to MES.

\- Understand production confirmation from MES to SAP.

\- Understand industrial communication protocols.



\## 2. Typical MES Architecture



\### Level 4 – Enterprise

\- SAP ERP

\- Production orders

\- BOM and routing

\- Material master

\- Inventory management



\### Level 3 – Manufacturing Operations

\- Sepasoft MES

\- Work order management

\- Production scheduling

\- Production dispatch

\- Production tracking

\- Quality management

\- OEE and downtime



\### Level 2 – Supervisory Control

\- Ignition SCADA

\- Perspective and Vision

\- Alarms and trends

\- Operator interfaces

\- Machine monitoring



\### Level 1 – Control

\- Siemens PLC

\- Sensors and actuators

\- Machine sequences

\- Interlocks



\### Level 0 – Physical Process

\- Motors

\- Conveyors

\- CNC machines

\- Manufacturing equipment



\## 3. Production Order Example – PO-1001



| Parameter | Value |

|---|---|

| Production order | PO-1001 |

| Material | Automotive Component A |

| Order quantity | 1,000 |

| Production line | ProductionLine01 |

| Equipment | Machine01 |

| Scheduled quantity | 100 |



\## 4. SAP to MES Information Flow



SAP creates and releases the production order.



Typical information:

\- Production order number

\- Material number

\- Order quantity

\- Plant

\- BOM

\- Routing

\- Planned start and end dates

\- Production version



MES receives and validates the order.



Typical validations:

\- Material exists.

\- Equipment is valid.

\- Routing is available.

\- Required master data exists.

\- Duplicate production orders are prevented.



\## 5. MES to Shop-Floor Information Flow



MES provides production context:

\- Active work order

\- Material

\- Target quantity

\- Equipment assignment

\- Operation details

\- Production parameters or recipes

\- Operator instructions



Ignition displays the relevant production information.



PLC executes machine sequences and controls physical equipment.



\## 6. Shop Floor to MES to SAP



Example production result:



| Parameter | Quantity |

|---|---:|

| Total produced | 100 |

| Good quantity | 97 |

| Rejected quantity | 3 |



MES associates production results with the work order, operation and equipment.



MES sends relevant production confirmation to SAP.



SAP processes the confirmation according to configured business rules.



\## 7. Communication Technologies



| Technology | Purpose |

|---|---|

| OPC UA | Industrial data exchange |

| MQTT | Publish/subscribe messaging |

| REST API | Application integration |

| IDoc | SAP business document exchange |

| JDBC | Database connectivity |

| SQL | Database queries and manipulation |



\## 8. Architecture Failure Scenarios



\### SAP Unavailable

\- Continue permitted existing production execution.

\- Maintain locally available production-order data.

\- Queue outbound confirmations.

\- Retry delivery after recovery.

\- Reconcile MES and SAP records.



\### MES Database Unavailable

\- Detect database connectivity failure.

\- Protect production data.

\- Follow designed recovery procedures.

\- Reconcile missing or failed transactions.



\### PLC Communication Lost

\- Detect communication failure.

\- Identify bad-quality or stale values.

\- Display communication status.

\- Reconcile missed production counts.



\### Duplicate Production Orders

\- Use stable external order identifiers.

\- Implement idempotent processing.

\- Prevent duplicate order creation.

\- Maintain integration logs.



\### Incorrect Production Confirmations

\- Validate order identity and status.

\- Validate production quantities.

\- Validate good and rejected quantities.

\- Prevent duplicate confirmations.

\- Track SAP acknowledgements.



\## 9. Key Architecture Principles



1\. ERP manages business planning.

2\. MES manages manufacturing execution.

3\. SCADA provides supervisory monitoring and control.

4\. PLC manages real-time machine control.

5\. Production data must be associated with the correct order and equipment.

6\. Integration must handle retries, duplicates and failures.

7\. Production data must be validated and reconciled.



\## 10. Day 2 Self-Assessment



1\. Why should a production order go to MES instead of directly to the PLC?

2\. What is the difference between OPC UA and REST API?

3\. What information should Ignition receive for an active production order?

4\. Which system records production results and sends confirmation to SAP?

5\. What should happen if MES–SAP communication is lost?



\## Next Lesson



Day 3 – Building a Machine01 MES Operator Application using Ignition Perspective and Sepasoft.




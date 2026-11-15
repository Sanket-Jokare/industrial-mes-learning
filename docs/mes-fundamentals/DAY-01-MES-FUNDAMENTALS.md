# Day 1 -- MES Fundamentals

## Learning objectives

By the end of this lesson, you should be able to:

1.  Explain what a Manufacturing Execution System (MES) does.
2.  Distinguish the responsibilities of ERP, MES, SCADA and PLC.
3.  Explain the five ISA-95 functional levels.
4.  Describe how a production order flows from SAP to MES and the shop
    floor.
5.  Explain why MES sends production confirmation back to SAP.

------------------------------------------------------------------------

## 1. What is MES?

A **Manufacturing Execution System (MES)** manages, monitors, tracks and
coordinates manufacturing operations on the shop floor.

It connects business-level production planning with the actual execution
of production.

Typical MES responsibilities include:

-   Managing and dispatching production orders.
-   Detailed production scheduling.
-   Tracking actual production quantities.
-   Tracking material usage and production progress.
-   Recording quality results and rejects.
-   Recording equipment states and downtime.
-   Calculating production performance metrics such as OEE.
-   Maintaining production history and traceability.
-   Sending production confirmations to ERP systems.

### Simple example

Suppose SAP releases an order to manufacture 1,000 automotive
components.

MES receives the order, validates the production requirements, schedules
the work, assigns it to suitable equipment, tracks production and
records the actual results.

MES can then send the production confirmation to SAP.

**Key idea:** MES manages and records the manufacturing execution
process. It does not replace the PLC's real-time machine control logic.

------------------------------------------------------------------------

## 2. ERP vs MES vs SCADA vs PLC

These systems work together, but each has a different primary
responsibility.

  -----------------------------------------------------------------------
  System                  Main responsibility     Example activities
  ----------------------- ----------------------- -----------------------
  ERP                     Business planning and   Production orders,
                          resource management     procurement, inventory
                                                  and finance

  MES                     Manufacturing           Scheduling,
                          operations management   dispatching, production
                                                  tracking, quality and
                                                  downtime

  SCADA                   Supervisory monitoring  HMI screens, alarms,
                          and control             trends and supervisory
                                                  commands

  PLC                     Real-time machine       Reading sensors,
                          control                 controlling actuators,
                                                  sequences and
                                                  interlocks
  -----------------------------------------------------------------------

### Remember it this way

-   **ERP:** What does the business need to produce?
-   **MES:** How should manufacturing execute and track that
    requirement?
-   **SCADA:** What is happening on the shop floor?
-   **PLC:** How does the machine operate?

### Practical example

A production order is released for 1,000 components.

1.  SAP ERP creates and releases the production order.
2.  MES schedules and dispatches the work to production equipment.
3.  SCADA displays machine status, process values and alarms.
4.  The PLC executes the machine sequence and controls sensors and
    actuators.
5.  MES collects production information and associates it with the
    relevant order and equipment.

**Important distinction:** SCADA commonly operates at ISA-95 Level 2,
while MES commonly operates at Level 3. Actual system boundaries can
vary by implementation and function.

------------------------------------------------------------------------

## 3. ISA-95 and its functional levels

**ISA-95**, also known as **IEC 62264**, is a standard for integrating
enterprise systems with manufacturing and control systems.

It provides common models and terminology to help define how information
and activities relate across business and manufacturing systems.

### ISA-95 levels

  -----------------------------------------------------------------------
  Level             Name              Typical           Examples
                                      responsibility    
  ----------------- ----------------- ----------------- -----------------
  0                 Physical process  The actual        Machining,
                                      physical          mixing, assembly
                                      manufacturing     
                                      process           

  1                 Sensing and       Detecting process Sensors,
                    manipulation      conditions and    transmitters,
                                      manipulating the  actuators
                                      process           

  2                 Monitoring and    Monitoring and    PLC, DCS, HMI,
                    supervisory       supervising       SCADA functions
                    control           physical          
                                      processes         

  3                 Manufacturing     Managing          MES, production
                    Operations        manufacturing     operations,
                    Management (MOM)  operations        quality
                                                        operations

  4                 Business planning Business planning ERP, SAP
                    and logistics     and logistics     
  -----------------------------------------------------------------------

### Level 2 vs Level 3

**Level 2 -- Supervisory control**

Focus: What is happening on the machine or process?

Examples:

-   Monitoring machine parameters.
-   Displaying alarms and trends.
-   Providing operator interfaces.
-   Performing supervisory control.

**Level 3 -- Manufacturing operations management**

Focus: How is production being executed?

Examples:

-   Managing production orders.
-   Scheduling and dispatching operations.
-   Tracking production quantities.
-   Managing quality and downtime.
-   Maintaining production traceability.
-   Calculating OEE.

### Example: Machine fault

Suppose Machine01 stops because of a motor fault.

-   Level 2 detects the fault and displays the alarm to the operator.
-   Level 3 records the downtime and associates it with the equipment
    and production context, according to the configured MES design.

**Important:** ISA-95 levels describe functions and activities. They are
not rigid boundaries that every software product must follow.

------------------------------------------------------------------------

## 4. SAP-to-MES production order flow

Consider this example:

  Field                    Example
  ------------------------ ------------------------
  Production order         PO-1001
  Material                 Automotive Component A
  Order quantity           1,000
  Plant                    Training Plant
  Production destination   Production Line 01

### Step 1 -- SAP creates the production order

SAP creates a production order containing information such as:

-   Production order number.
-   Material number and description.
-   Order quantity.
-   Plant.
-   Planned start and end dates.
-   Bill of Materials (BOM).
-   Routing.
-   Production version or other relevant planning information.

### Step 2 -- SAP releases the production order

When the order is released, SAP makes it available for execution
according to the integration design.

Possible integration approaches include:

-   IDoc.
-   BAPI or RFC.
-   REST API.
-   SAP Integration Suite or other middleware.

The actual interface depends on the architecture selected for the
project.

### Step 3 -- MES receives and validates the order

MES receives the production order and maps it to its own work-order or
production-order representation.

Typical validations include:

-   Is the material known to MES?
-   Is the equipment or work center valid?
-   Are the required operations available?
-   Is the order already present?
-   Are the production requirements complete?

### Step 4 -- MES schedules and dispatches production

MES determines how the order should be executed based on the configured
scheduling rules and available resources.

For example, MES may schedule the first 100 components on Machine01.

### Step 5 -- Shop-floor execution

The operator interacts with the manufacturing application, for example
through an Ignition Perspective screen.

The PLC controls the machine. Shop-floor data may be communicated
through OPC UA, MQTT or another configured interface.

MES associates the collected information with the relevant production
context, such as:

-   Work order.
-   Operation.
-   Equipment.
-   Production run.
-   Material.

### Step 6 -- MES records production results

MES may record:

-   Total produced quantity.
-   Good quantity.
-   Rejected quantity.
-   Downtime.
-   Production duration.
-   Quality results.
-   Material consumption, where configured.

### Step 7 -- MES sends production confirmation to SAP

MES sends relevant production results back to SAP.

SAP can use these confirmations to update production-order progress,
yield, scrap and other relevant records.

Inventory postings, goods movements and order-status updates depend on
the configured SAP integration and business process.

------------------------------------------------------------------------

## 5. BOM vs Routing

These two concepts are essential when understanding production orders.

### Bill of Materials (BOM)

A BOM defines **what materials and components are required** to
manufacture a product.

Example:

  Component         Required quantity
  --------------- -------------------
  Metal housing                     1
  Fastener                          4
  Seal                              1

### Routing

Routing defines **which manufacturing operations must be performed and
in what sequence**.

Example:

1.  Cutting.
2.  Machining.
3.  Drilling.
4.  Inspection.
5.  Packing.

**Remember:**

-   BOM = What materials are needed?
-   Routing = What operations are required, and in what sequence?

------------------------------------------------------------------------

## 6. Key terminology

  -----------------------------------------------------------------------
  Term                                Meaning
  ----------------------------------- -----------------------------------
  Production order                    An instruction to manufacture a
                                      specified quantity of a material

  Work order                          An MES representation of production
                                      work; exact terminology varies by
                                      system

  Material                            The product or component being
                                      manufactured or consumed

  BOM                                 List of required materials and
                                      quantities

  Routing                             Sequence of manufacturing
                                      operations

  Work center                         A production resource or group of
                                      resources used for operations

  Production schedule                 Plan for when and where production
                                      should occur

  Dispatch                            Making work available to a resource
                                      for execution

  Production confirmation             Report of actual production results
                                      to the ERP system

  OEE                                 Overall Equipment Effectiveness, a
                                      measure based on availability,
                                      performance and quality
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 7. End-to-end architecture at a glance

``` text
                 LEVEL 4 – BUSINESS
                    SAP ERP
                       |
             Production order released
                       |
                       v
             LEVEL 3 – OPERATIONS
                 Sepasoft MES
          Validate / Schedule / Dispatch
                       |
             Production instructions
                       |
                       v
              LEVEL 2 – SUPERVISION
                Ignition SCADA
              HMI / Alarms / Trends
                       |
               OPC UA / MQTT
                       |
                       v
                LEVEL 1 – CONTROL
                    PLC
             Logic / Sequences / Interlocks
                       |
                       v
                LEVEL 0 – PROCESS
              Sensors / Motors / Machines

        Production data and confirmations flow
             back through the MES to SAP
```

This is a simplified conceptual architecture. A real deployment may have
additional gateways, databases, integration services and direct
communication paths.

------------------------------------------------------------------------

## 8. Day 1 recap

1.  MES connects business production planning with manufacturing
    execution.
2.  ERP plans business resources and production requirements.
3.  MES manages manufacturing operations and production tracking.
4.  SCADA provides supervisory monitoring and control.
5.  PLCs execute real-time machine control.
6.  ISA-95 provides a framework for understanding enterprise-to-control
    integration.
7.  BOM defines required materials; routing defines required operations.
8.  SAP sends production-order information to MES.
9.  MES tracks execution and sends production confirmation to SAP.

------------------------------------------------------------------------

## 9. Self-assessment

Try answering these questions without referring to the notes.

1.  What is the primary responsibility of MES?
2.  SAP releases a production order for 1,000 components. Which system
    decides how production is executed on Machine01?
3.  What is the difference between Level 2 and Level 3 in ISA-95?
4.  What information should SAP send to MES when releasing a production
    order? List at least five fields.
5.  Why does SAP need production confirmation from MES?

### Practical thinking exercise

For production order PO-1001, imagine that MES schedules 100 components
on Machine01.

Explain:

-   What information does MES need before scheduling?
-   What does the PLC control?
-   What information should MES record during execution?
-   What should MES report back to SAP?

------------------------------------------------------------------------

## Suggested next lesson

**Day 2 -- MES architecture and ISA-95 information flow**

We will trace the information flow from SAP to Sepasoft MES, Ignition,
PLC and back to SAP, using PO-1001 as the running example.

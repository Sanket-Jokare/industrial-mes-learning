# Day 3 – MES Operator Application

## 1. Learning Objective

Build an understanding of how a manufacturing operator interacts with an MES application built using Ignition Perspective and Sepasoft MES.

The focus of this session:
- Understand the MES Work Order Table.
- Understand the role of Equipment Manager.
- Review Machine01 production counter configuration.
- Understand the difference between PLC cumulative counters and MES work-order production quantities.
- Identify the unresolved production-count discrepancy.

## 2. Environment

| Item | Configuration |
|---|---|
| Ignition | 8.3.7 |
| Sepasoft Production | 4.8.3.3 |
| Sepasoft OEE Downtime | 4.8.3.3 |
| Perspective | Available |
| Project | Machine01_MES_Operator |
| View | ProductionDashboard |
| License | Trial |

The `ProductionDashboard` view was created, and its root Flex Container was configured.

## 3. MES Work Order Table

### Purpose

The MES Work Order Table displays work orders managed by Sepasoft MES.

An operator or supervisor can use it to view work orders and, depending on permissions and configuration, add or edit work orders.

It retrieves work-order information from the MES system rather than requiring the developer to manually populate the table.

### Properties observed

The following properties were visible in the component configuration:

- `creationBeginDate`
- `creationEndDate`
- `closedBeginDate`
- `closedEndDate`
- `equipmentPathFilter`
- `materialNameFilter`
- `workOrderNameFilter`
- `showClosedWorkOrder`
- `enableAdd`
- `enableEdit`
- `enableExport`
- `selectedRow`
- `sortingEnabled`
- `searchEnabled`
- `tableColumns`
- `data`

The `data` property contains the table's returned data. It should not be manually populated for this exercise.

### Work order retrieval

Initially, the table displayed no data.

After broadening the date range and applying the work-order name filter `PO-1001`, the work order appeared.

Observed work order:

| Field | Observed value |
|---|---|
| Work Order | PO-1001 |
| Material | Automotive Component A |
| Order Quantity | 1,000 |
| Scheduled Quantity | 100 |
| Actual Quantity | Approximately 171,680–174,164 across observations |

The Edit Work Order dialog was opened to inspect the order. The order quantity, material, creation date, and closed status were reviewed. No changes were saved.

**Important:** The displayed Actual Quantity is unexpectedly high compared with the order quantity. Its source and calculation have not yet been established.

## 4. Equipment Hierarchy

The following equipment hierarchy was created in Sepasoft Equipment Manager:

```text
New Enterprise
└── TrainingPlant
    └── MachiningArea
        └── ProductionLine01
            ├── Machine01
            ├── Machine02
            └── Machine03
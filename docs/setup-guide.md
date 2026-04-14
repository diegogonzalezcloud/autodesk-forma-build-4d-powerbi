# Step-by-Step Setup Guide

This guide explains how to configure the Power BI templates using Autodesk Forma Build data.

---

## 0. Prerequisites in Autodesk Forma Build

### 1. Load BIM Model

* Upload a model:

  * IFC **or**
  * RVT

---

### 2. Create Assets from Model

* Generate assets from model elements
* Ensure mapping of an ID field:

| Model Type | Field                |
| ---------- | -------------------- |
| IFC        | `IfcElement.Tag`     |
| RVT        | `Original System Id` |

👉 Map this ID to:

```
Assets → Barcode
```

---

### 3. Create Schedule

* Create a construction schedule
* Define activities

---

### 4. Link Assets to Schedule

* Assign assets to activities
* This enables 4D simulation

---

### 5. Run Data Connector Extraction

Go to:

```
Insight → Data Connector
```

* Run extraction including:

  * Assets
  * Relationships
  * Schedule

* Download the ZIP

* Extract it locally

---

## 1. Open Power BI Template

Open one of the templates:

```
/templates/PowerBI_IFC_Template.pbix
```

or

```
/templates/PowerBI_RVT_Template.pbix
```

---

## 2. Load Data Connector Data (CSV)

1. Open **Transform Data**
2. Locate parameter:

```
SourceFolder
```

3. Update it with your extraction path:

Example:

```
C:\autodesk_data_extract
```

4. Apply changes

---

## 3. Connect Data Exchange (3D Model)

### Create Data Exchange

* From Forma or ACC
* Select the desired 3D view
* Create Data Exchange
* Copy the URL

---

### Connect in Power BI

1. Go to:

```
Home → Get Data
```

2. Search:

```
Autodesk Data Connector
```

3. Select:

```
Data Exchange
```

4. Paste the URL
5. Load the model

---

## 4. Prepare Data (Important)

Go to **Table View → Edit Query**

### Select correct ID column:

| Model Type | Column               |
| ---------- | -------------------- |
| IFC        | `IfcElement.Tag`     |
| RVT        | `Original System Id` |

### Ensure:

* Data type = Whole Number (if numeric)
* Remove:

  * Null values
  * Duplicates

Apply changes.

---

## 5. Update Model Relationships

Go to **Model View**

1. Locate existing relationship (example dataset)
2. Replace with your Data Exchange table

### Configure:

* Relationship:

  * Model ID ↔ Assets Barcode
* Cross filter:

  ```
  Both
  ```
* Active:

  ```
  Yes
  ```

---

## 6. Configure Data Exchange Viewer

In Power BI visual:

Set fields:

* Viewer → `your-model.viewer`
* ExternalElementId_1 → `ExternalElementId`
* ExternalElementId_2 → `ExternalElementId`

---

## 7. Validate Dashboard

Check:

* 3D model loads correctly
* Schedule filters work
* Gantt chart displays data
* Assets interact with model

---

## ⚠️ Common Issues

### Model not visible

* Wrong Data Exchange selected
* Missing viewer fields

---

### No relationship between model and assets

* ID mismatch
* Wrong data type
* Null values

---

### Multiple schedules appearing

* Filter correct schedule in Power BI

---

## 🔄 Updating Data

Each time data changes in Forma:

1. Re-run Data Connector extraction
2. Replace CSV folder
3. Refresh Power BI

---

## ✅ Final Result

You should have:

* 3D model visualization
* Time-based construction simulation
* Fully interactive dashboard

---

## 🎯 Tip

Start with the template closest to your workflow:

* IFC → more flexible
* RVT → simpler mapping

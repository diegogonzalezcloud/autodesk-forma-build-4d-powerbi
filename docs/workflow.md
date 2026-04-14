# Workflow Explanation

This document explains how Autodesk Forma Build data is connected with Power BI to enable a **4D construction workflow**.

---

## 🧩 Data Sources

The workflow is based on two main data pipelines:

### 1. Data Connector (Tabular Data)

Provides structured data from Autodesk Forma Build:

* Assets
* Relationships
* Schedule (activities, dependencies, resources)

**Format:**

* CSV files (downloaded as ZIP)

---

### 2. Data Exchange (3D Model Data)

Provides BIM model data:

* Geometry (for visualization)
* Element properties
* Identifiers for mapping

**Source:**

* RVT or IFC model

---

## 🔗 Integration Logic

The workflow connects three key domains:

| Domain   | Source        |
| -------- | ------------- |
| 3D Model | Data Exchange |
| Assets   | Forma Build   |
| Schedule | Forma Build   |

These are unified in Power BI.

---

## 🔑 Key Concept: ID Mapping

The entire workflow depends on matching IDs between datasets.

### Mapping structure:

| Element         | Field                |
| --------------- | -------------------- |
| BIM Model (IFC) | `IfcElement.Tag`     |
| BIM Model (RVT) | `Original System Id` |
| Assets          | `Barcode`            |

👉 This mapping allows linking:

* Model elements ↔ Assets
* Assets ↔ Schedule activities

---

## 🧠 Data Flow

1. Upload BIM model (IFC or RVT) to Forma
2. Generate **Assets from model elements**
3. Map model IDs to Asset attributes
4. Create **Schedule (planning)**
5. Link Assets to Schedule activities
6. Run **Data Connector extraction**
7. Create **Data Exchange** from BIM model
8. Connect everything in Power BI

---

## 📊 Output in Power BI

The final dashboard combines:

* 3D model visualization (Data Exchange viewer)
* Time-based simulation (Schedule)
* Asset filtering and categorization
* Gantt chart visualization

---

## 🎯 Result

A unified system that enables:

> **4D simulation (3D + time) driven by real construction data**

---

## ⚠️ Important Considerations

* ID mapping must be consistent
* Data types must match (numeric vs text)
* Null or duplicate IDs will break relationships
* Each update in Forma requires:

  * New Data Connector extraction
  * Refresh in Power BI

---

## 🔄 IFC vs RVT Differences

| Aspect             | IFC              | RVT                  |
| ------------------ | ---------------- | -------------------- |
| ID Field           | `IfcElement.Tag` | `Original System Id` |
| Source             | IFC export       | Native Revit         |
| Mapping complexity | Medium           | Lower                |

Both workflows are fully supported using the provided templates.

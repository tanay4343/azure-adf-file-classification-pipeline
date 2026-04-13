# 🚀 Azure Data Factory – Dynamic File Routing Pipeline

## 📌 Project Overview

This project demonstrates a real-world **Azure Data Factory (ADF)** pipeline that automatically processes files from a source container and organizes them into destination folders based on file extensions.

The pipeline supports multiple file types such as:

* CSV
* XLSX
* PDF
* TXT
* DOC

---

## 🎯 Objective

* Read multiple files from Azure Data Lake Storage (ADLS)
* Identify file extensions dynamically
* Create folders automatically based on extension
* Store files in corresponding folders
* Automate execution using triggers

---

## 🏗️ Architecture

### 🔄 Flow Diagram

flowchart TD
    A[Source ADLS Container] --> B[Get Metadata Activity]
    B --> C[childItems (List of Files)]
    C --> D[ForEach Loop]
    D --> E[Copy Activity]
    E --> F[Dynamic Expression Logic]
    F --> G[Destination ADLS Container]
    G --> H[csv/]
    G --> I[pdf/]
    G --> J[xlsx/]
    G --> K[txt/]

---

## ⚙️ Technologies Used

* Azure Data Factory (ADF)
* Azure Data Lake Storage Gen2 (ADLS)
* Dynamic Expressions (ADF)
* Schedule Trigger

---

## 🔧 Pipeline Components

### 1. Get Metadata Activity

* Fetches list of files using `childItems`
* Output: Array of file objects

### 2. ForEach Activity

* Iterates through each file dynamically

### 3. Copy Activity

* Copies file from source to destination
* Uses dynamic dataset parameters

---

## 🧠 Key Concepts Used

### 🔹 Metadata Handling

* `childItems` to retrieve all files in folder

### 🔹 Dynamic Expressions

#### Extract File Extension

```adf
@toLower(last(split(item().name, '.')))
```

#### File Name

```adf
@item().name
```

---

## 📂 Folder Structure (Output)

```
destination/
 ├── csv/
 │    ├── file1.csv
 ├── pdf/
 │    ├── file2.pdf
 ├── xlsx/
 │    ├── file3.xlsx
```

---

## 🔁 Trigger Configuration

* Type: **Schedule Trigger**
* Frequency: Every 5 minutes
* Used due to Azure Student subscription limitations (Event Grid not available)

---

## ⚠️ Challenges Faced

* Folder vs File dataset confusion
* Metadata configuration issues
* Dynamic parameter passing errors
* Event Grid limitations in student subscription

---

## ✅ Solutions Implemented

* Used parameterized datasets
* Implemented `Get Metadata + ForEach` pattern
* Used dynamic expressions for routing
* Switched to Schedule Trigger

---

## 🚀 Features

* Fully dynamic pipeline
* Handles multiple file formats
* Auto folder creation
* Scalable and reusable design

---

## 📈 Future Improvements

* Add duplicate file handling
* Move processed files to archive folder
* Implement logging and monitoring
* Switch to Event-based trigger (production setup)

---

## 🧑‍💻 Author

**Tanay Chourasiya**

---

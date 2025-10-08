# PL/SQL: ORACLE DATABASE

**Name:** IRAGENA SHEMA Cedrick  
**ID:** 24766  
**Date:** 08/10/2025  

---

## 📘 Overview

This report outlines the steps taken to complete the **Oracle Pluggable Database (PDB)** assignment which involved the creation, management, and deletion of PDBs using **SQL*Plus** and **Oracle Enterprise Manager (OEM)**.  

The tasks were executed successfully, including troubleshooting errors during configuration. Screenshots were captured as evidence of each step.

---

## 🧩 Task 1: Create a New Pluggable Database (PDB)

**Objective:**  
Create a PDB with the format:  
> FirstTwoLettersOfFirstName_pdb_StudentID  

**Database Created:** `ce_pdb_24766`  
**Admin Username:** `cedrick_plsqlauca_24766`  
**Password:** `shemac`  
**File Location:** Custom path provided using `FILE_NAME_CONVERT`

### 🧱 SQL Steps

```sql
CREATE PLUGGABLE DATABASE ce_pdb_24766
ADMIN USER cedrick_plsqlauca_24766 IDENTIFIED BY shemac
ROLES = (DBA)
FILE_NAME_CONVERT = ('...pdbseed\', '...ce_pdb_24766\');

ALTER PLUGGABLE DATABASE ce_pdb_24766 OPEN;
ALTER PLUGGABLE DATABASE ce_pdb_24766 SAVE STATE;
```

✅ **Result:**  
The database was successfully created, opened, and saved in a persistent open state.

---

Screenshot:

![Screenshot](screenshots/9.png)


<br><br><br><br>


## 🗑️ Task 2: Create and Delete a PDB

**Objective:**  
Create and delete a second PDB following the naming format:  
> FirstTwoLettersOfFirstName_to_delete_pdb_StudentID

**Database Created:** `ce_to_delete_pdb_24766`  
**Admin Username:** `cedrick_delete`  
**Password:** `shemac`

### 🧱 SQL Steps

```sql
CREATE PLUGGABLE DATABASE ce_to_delete_pdb_24766
ADMIN USER cedrick_delete IDENTIFIED BY shemac
ROLES = (DBA)
FILE_NAME_CONVERT = ('...pdbseed\', '...ce_to_delete_pdb_24766\');

-- Attempted to close before deletion (error encountered)

DROP PLUGGABLE DATABASE ce_to_delete_pdb_24766 INCLUDING DATAFILES;
```

### ⚠️ Issue Encountered

**Error Message:**
```
ORA-65020: pluggable database CE_TO_DELETE_PDB_24766 already closed
```

**Resolution:**  
This occurred when attempting to close a PDB that was already in a closed state.  
It was resolved by **directly issuing the DROP command** without closing again.

✅ **Status:**  
Created and deleted successfully after resolving the close issue.

---
Screenshot: Pluggable database created

![Screenshot](screenshots/9.png)


<br><br><br><br>

Screenshot: Pluggable database droped

![Screenshot](screenshots/9.png)


<br><br><br><br>



## 🖥️ Task 3: Oracle Enterprise Manager (OEM)

**Objective:**  
Configure and access Oracle Enterprise Manager (OEM) and verify the dashboard.

### 🧾 Steps Taken

1. Verified HTTPS port:
   ```sql
   SELECT DBMS_XDB_CONFIG.GETHTTPSPORT FROM DUAL;
   ```

2. Attempted to set ports 5500 and 5501:
   ```sql
   EXEC DBMS_XDB_CONFIG.SETHTTPSPORT(5500);
   ```
   ❌ **Error 1:** `ORA-12542: TNS:address already in use`  
   ❌ **Error 2:** `ORA-44718: Port conflict in XDB Configuration file`

3. Resolved conflict by changing to **port 5505**:
   ```sql
   EXEC DBMS_XDB_CONFIG.SETHTTPSPORT(5505);
   ```

✅ **Status:**  
OEM configured and accessible on **port 5505**.

---

Screenshot:

![Screenshot](screenshots/9.png)


<br><br><br><br>


## ⚙️ Issues Encountered and Solutions

| **Issue** | **Error Message** | **Solution** |
|------------|------------------|---------------|
| Trying to close a PDB already closed | `ORA-65020` | Skipped the close step and directly dropped the PDB |
| Port conflict when setting HTTPS port | `ORA-12542`, `ORA-44718` | Changed to an unused port (**5505**), which worked successfully |

---

## ✅ Conclusion

All tasks were successfully completed:

- ✅ A new PDB (**ce_pdb_24766**) was created and configured correctly.  
- ✅ A second PDB (**ce_to_delete_pdb_24766**) was created and deleted as required.  
- ✅ Oracle Enterprise Manager was configured successfully after resolving port conflicts.

---

**End of Report**

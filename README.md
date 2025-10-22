# Streamlining Ticket Assignment for Efficient Support Operations

## 📘 Project Overview
This project aims to implement an **automated ticket routing system** in **ServiceNow** for **ABC Corporation**.  
The main goal is to improve operational efficiency by automatically assigning support tickets to the appropriate teams, reducing delays, and improving customer satisfaction.

---

## 🧭 Objectives
- Automate ticket routing to the correct support group.
- Reduce manual errors and time delays.
- Improve issue resolution speed.
- Optimize resource utilization and boost customer satisfaction.

---

## 🧑‍💻 Step-by-Step Implementation

### 1️⃣ Create Users
**Path:**  
`All → System Security → Users → New`

**Steps:**
- Click **New** and fill in the required user details.
- Click **Submit** to save.
- Repeat the process to create another user.

> 💬 *Comment:* Creating users helps define who can interact with the system. Each user can later be assigned to groups and roles.  

![Create Users Screenshot](1%20User%201.png) 
![Create Users Screenshot](./images/2%20User%202.png) 

> 📸 *Comment for photo:* Screenshot showing user creation form in ServiceNow with user details filled.

---

### 2️⃣ Create Groups
**Path:**  
`All → System Security → Groups → New`

**Steps:**
- Click **New** and enter group details.
- Click **Submit** to create the group.
- Repeat to create an additional group.

> 💬 *Comment:* Groups represent departments or teams such as “Certificates” or “Platform” — they’re key for automatic ticket routing.  

![Create Groups Screenshot](./images/3%20Certificates%20Group%201.png)  
![Create Groups Screenshot](./images/4%20Platform%20Group%202.png)
> 📸 *Comment for photo:* Screenshot of group form showing "Certificates" group being created.

---

### 3️⃣ Create Roles
**Path:**  
`All → System Security → Roles → New`

**Steps:**
- Click **New** to create a new role.
- Fill in details and click **Submit**.
- Repeat for additional roles.

> 💬 *Comment:* Roles control **permissions and access** to ServiceNow modules and tables.  

![Create Groups Screenshot](./images/5%20Certification_role.png)
![Create Groups Screenshot](./images/6%20Platform_role.png)
> 📸 *Comment for photo:* Screenshot of role creation showing “Platform_Role”.

---

### 4️⃣ Create a Table
**Path:**  
`All → System Definition → Tables → New`

**Steps:**
- Label: `Operations Related`
- Check ✅ `Create module` and `Create mobile module`
- Menu Name: `Operations related`
- Add relevant table columns.
- Click **Submit**.

**Add Choices for Issue Field:**
- unable to login to platform  
- 404 error  
- regarding certificates  
- regarding user expired  

> 💬 *Comment:* The table stores all operational issues and their related ticket data, forming the foundation for the automation process.

![Create Groups Screenshot](./images/7%20Operations%20Related%20Table.png)

> 📸 *Comment for photo:* Screenshot showing “Operations Related” table structure with issue field choices.

---

### 5️⃣ Assign Roles & Users to Certificate Group
**Path:**  
`All → System Security → Groups → Certificates`

**Steps:**
- Edit **Group Members** and add `Katherine Pierce`.
- Under **Roles**, assign `Certification_Role`.

> 💬 *Comment:* This links users and roles to the Certificates group so that only authorized users handle certificate-related issues.  

---

### 6️⃣ Assign Roles & Users to Platform Group
**Path:**  
`All → System Security → Groups → Platform`

**Steps:**
- Edit **Group Members** and add `Manne Niranjan`.
- Under **Roles**, assign `Platform_Role`.

> 💬 *Comment:* Assigning users ensures that specific platform-related tickets go directly to the right support person or team.  

---

### 7️⃣ Assign Role to Table
**Path:**  
`All → System Definition → Tables → Operations Related → Application Access`

**Steps:**
- Click **u_operations_related (read)** → elevate to `security_admin`.
- Add both `Platform_Role` and `Certification_Role` under “Requires Role”.
- Repeat for **write** access.

> 💬 *Comment:* Defining read/write access ensures that only authorized teams can view or modify specific ticket data.  


---

### 8️⃣ Create Access Control List (ACL)
**Path:**  
`All → System Security → Access Control (ACL) → New`

**Steps:**
- Create new ACL.
- Under “Requires Role,” add `admin`.
- Repeat to create 4 ACLs for related fields.

> 💬 *Comment:* ACLs strengthen **security** by controlling which roles can access or modify specific fields.  

![Create ACL Screenshot](./images/8%20ACLs%204.png)  
> 📸 *Comment for photo:* Screenshot showing ACL configuration window with admin role applied.

---

### 9️⃣ Create Flow – Assign Operations Ticket to Certificates Group
**Path:**  
`All → Process Automation → Flow Designer → New Flow`

**Flow Properties:**
- **Name:** Regarding Certificate  
- **Application:** Global  
- **Run As:** System User  

**Trigger:**  
- Table: Operations Related  
- Condition: `issue is Regarding Certificates`

**Action:**  
- Update Record → Field: `Assigned to group` = `Certificates`  

> 💬 *Comment:* This flow ensures that all certificate-related issues are instantly routed to the Certificate team.  

![Certificate Flow Screenshot](./images/9%20Regarding%20Certification%20Flow.png)  
> 📸 *Comment for photo:* Screenshot of Flow Designer showing “Regarding Certificate” flow logic.

---

### 🔟 Create Flow – Assign Operations Ticket to Platform Group
**Path:**  
`All → Process Automation → Flow Designer → New Flow`

**Flow Properties:**
- **Name:** Regarding Platform  
- **Application:** Global  
- **Run As:** System User  

**Trigger:**  
- Table: Operations Related  
- Conditions:  
  - issue is “Unable to login to platform”  
  - issue is “404 Error”  
  - issue is “Regarding User Expired”

**Action:**  
- Update Record → Field: `Assigned to group` = `Platform`  

> 💬 *Comment:* This flow automatically routes platform-related tickets to the Platform team for faster resolution.  

![Platform Flow Screenshot](./images/10%20Regarding%20Platform%20Flow.png)  
> 📸 *Comment for photo:* Screenshot of Flow Designer showing “Regarding Platform” flow configuration.

---

## ✅ Conclusion
The implementation of the **automated ticket routing system** in **ServiceNow** at **ABC Corporation** successfully streamlined the ticket management process.  
By automating group assignments using Flows, the system reduces manual effort, minimizes response delays, and improves overall operational efficiency and customer satisfaction.

![Create Groups Screenshot](./images/11%20Conclusion.png)

> 💬 *Final Comment:* This automation showcases ServiceNow’s potential in workflow orchestration and intelligent support operations.

---

## 📂 Folder Structure Example



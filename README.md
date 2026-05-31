# 🏥 GDPR Hospital Information System

A role-based hospital records system built around **GDPR data-protection rights** from the ground up. Manages patients, examinations, prescriptions and medical records, with separate workspaces for administrators, doctors, nurses and patients.

🔗 **Live demo:** https://pmf-ris.onrender.com/Bolnica/

> ⚠️ Hosted on a free tier — the first request after a period of inactivity may take ~50 seconds while the server wakes up. The interface is in Serbian.

---

## 🔑 Demo Credentials

| Role | Username | Password |
|------|----------|----------|
| Admin | `admin` | `admin` |
| Nurse | `sestra1` | `MvCvnSkw` |
| Doctor | `markpetrovic` | `RFWsjkhQ` |
| Patient | `jovanapopovic213` | `KjstpGvE` |

Useful demo values:
- Existing patient ID number (JMBG): `2209985714225`
- A valid JMBG for creating a **new** patient: `0912976801350`

> These are shared demo accounts on public sample data. Please don't store anything real!

---

## 📸 Screenshots

<table>
  <tr>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/andrej1011/pmf-ris/portfolio-deployment/docs/login.png" alt="Login" width="280"/><br/>
      <sub><b>Login</b></sub>
    </td>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/andrej1011/pmf-ris/portfolio-deployment/docs/doctor.png" alt="Doctor — examination" width="280"/><br/>
      <sub><b>Doctor's dashboard</b></sub>
    </td>
   <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/andrej1011/pmf-ris/portfolio-deployment/docs/report.png" alt="PDF report" width="280"/><br/>
      <sub><b>PDF report</b></sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/andrej1011/pmf-ris/portfolio-deployment/docs/past-exams.png" alt="Past examinations" width="280"/><br/>
      <sub><b>Past examinations</b></sub>
    </td>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/andrej1011/pmf-ris/portfolio-deployment/docs/recepti.png" alt="Prescriptions" width="280"/><br/>
      <sub><b>Patient's Prescriptions</b></sub>
    </td>
    <td align="center" width="33%">
      <img src="https://raw.githubusercontent.com/andrej1011/pmf-ris/portfolio-deployment/docs/gdpr.png" alt="GDPR requests" width="280"/><br/>
      <sub><b>GDPR requests</b></sub>
    </td>
  </tr>
</table>

---

## 📚 Academic Background

This project was built for **Razvoj Informacionog Softvera** (*Information System Development*), a course at the **Faculty of Sciences (Prirodno-matematički fakultet) at the University of Novi Sad** during my Bachelor studies.

The goal was to design and implement a complete information system, with a strong focus on **GDPR data-protection requirements** applied to sensitive medical data.

### Branches
- **`main`** — the original course project as submitted.
- **`portfolio-deployment`** — the same app adapted for cloud hosting (containerized with Docker, deployed on **Render** with a **TiDB Cloud** MySQL database) so it can run live as a portfolio piece.

---

## Features

- **GDPR data rights** — patients can request data access, correction, portability (export) and erasure through a built-in consent & request workflow that an administrator reviews and approves.
- **Role-based access control** — four roles (Admin, Doctor, Nurse, Patient), each with its own scoped dashboard and permissions.
- **Audit trail** — every sensitive action is logged with user, timestamp and IP address.
- **Reporting** — examination reports, GDPR data exports and monthly statistics generated as PDF via JasperReports.
- **Scheduling** — nurses book examinations; doctors manage their schedule, requests and completed visits.

---

## 🎬 Demo Walkthrough

A full end-to-end scenario that touches every role and the GDPR flow:

**Admin & Nurse — setup**
1. Log in as **admin** → create a medical nurse.
2. Log in as the **nurse** → register a new patient → schedule an examination.

**Doctor — clinical work**

3. Log in as **doctor** → review requests and upcoming examinations.
4. Perform the examination, view past examinations, and print the report (PDF).

**Patient — records & GDPR rights**

5. Log in as the **patient** → view reports and prescriptions.
6. Submit GDPR requests: data correction, portability, PDF export, and erasure.

**Admin — GDPR approval**

7. Log in as **admin** → approve the correction / portability / export requests.
8. Patient logs back in → sees the changes and generates the exported PDF.

**Admin — erasure & reporting**

9. Admin deletes the patient → that patient can no longer log in (right to erasure).
10. Admin generates the monthly statistics report.



## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Java 21 |
| Framework | Spring Boot 4, Spring Security 7 |
| Persistence | Hibernate 7 / Spring Data JPA, MySQL |
| Views | JSP + JSTL, Bootstrap |
| Reports | JasperReports |

---

## 📁 Project Structure

```
pmf_ris/
├── BolnicaJPA/      # JPA entities (model)
├── BolnicaWeb/      # Spring Boot app: controllers, services, security, JSP views
```

---
## 🚀 Running Locally (Docker)

The project is a Maven multi-module app (`BolnicaJPA` + `BolnicaWeb`) packaged as a WAR and served by Tomcat in Docker.

```bash
# 1. Build the image
docker build -t bolnica .

# 2. Run it (point it at your own MySQL database)
docker run -p 8080:8080 \
  -e SPRING_DATASOURCE_URL="jdbc:mysql://<host>:<port>/<db>?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC" \
  -e MYSQLUSER="<user>" \
  -e MYSQLPASSWORD="<password>" \
  bolnica
```

Then open **http://localhost:8080/Bolnica/**

You'll need a MySQL database with the schema imported (see `sql/`). Table names are case-sensitive on Linux MySQL, so keep them exactly as in the dump.

---

## 📝 Notes

This is a faculty project demonstrating a GDPR-aware information system. The data is fictional and for demonstration purposes only.

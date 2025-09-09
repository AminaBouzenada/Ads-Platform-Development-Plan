# Ads-Platform-Development-Plan
# 📌 Project Roadmap

This roadmap outlines the step-by-step plan to complete the Ads Platform with **Supabase** (backend/auth), **Chargily Pay** (payments), and **Vercel/Netlify** (deployment).  

---

## Week 1 – Backend + Core Features

### **Day 1 – Setup & Cleanup**
- Configure `.env` with Supabase + Chargily sandbox API keys.  
- Verify Supabase project is online.  
- Clean project structure (remove mock data after testing).  

### **Day 2 – Authentication**
- Implement Supabase auth (login/register).  
- Add user roles:  
  - **Admin** → dashboard, campaign approvals, user management  
  - **Advertiser** → create campaigns, make payments  
  - **Viewer** → limited dashboard access  

### **Day 3 – Route Protection**
- Protect pages with role-based access control.  
- Redirect unauthorized users (e.g., Advertiser trying to access `AdminDashboard`).  

### **Day 4 – Database Schema**
Create Supabase tables:  
- **users** → id, email, role, profile info  
- **campaigns** → id, advertiserId, name, objective, audience, budget, creative, status  
- **payments** → id, campaignId, userId, amount, status (pending/paid/failed), transactionRef  

### **Day 5 – Campaign Builder Integration**
- Connect **CampaignBuilder** steps to DB.  
- When advertiser completes all steps, insert into `campaigns` with status = `Draft`.  

### **Day 6 – Admin Management**
- Admin can view **Pending campaigns**.  
- Admin can approve/reject campaigns.  
- Campaign lifecycle: `Draft → Pending Payment → Pending Approval → Accepted/Rejected → Running/Ended`.  

### **Day 7 – CRUD Operations & Testing**
- Advertiser: **Edit/Delete campaigns** before approval.  
- Admin: **Manage users (suspend/delete)**.  
- Replace all mock data with live Supabase queries.  
- Test full flow (**create → approve → cancel**).  

---

## Week 2 – Payments, Analytics & Deployment

### **Day 8 – Dashboard Analytics**
- Connect dashboard charts to real DB data.  
- Show:  
  - Total campaigns  
  - Campaigns by status  
  - Budget distribution  

### **Day 9 – Notifications**
- Add **toast notifications** (success/error).  
- Trigger notifications on:  
  - Campaign creation  
  - Payment confirmation  
  - Campaign approval/rejection  

### **Day 10 – UI Enhancements**
- Add validation to campaign forms.  
- Polish **Sidebar navigation + dashboards**.  
- Improve campaign steps UX.  

### **Day 11 – Chargily Payment Integration**
- Integrate **Chargily Pay API**:  
  - At `BudgetStep`, generate a payment link.  
  - Store transaction in `payments` table with status = `pending`.  
  - Redirect advertiser to Chargily checkout (CCP / EDAHABIA).  

### **Day 12 – Payment Confirmation (Webhook)**
- Set up **Chargily webhook** (via Supabase Edge Function or small backend).  
- On payment success → update `payments.status = paid`.  
- Campaign moves automatically from `Pending Payment` → `Pending Approval`.  

### **Day 13 – Deployment**
- Deploy frontend on **Vercel/Netlify**.  
- Connect to **Supabase production project**.  
- Add **Chargily production keys**.  
- Test end-to-end: **Create campaign → Pay → Admin approval → Running**.  

### **Day 14 – Final QA & Documentation**
- Test all user roles:  
  - **Advertiser**: register, create campaign, pay, track status.  
  - **Admin**: approve/reject, manage users.  
  - **Viewer**: see limited dashboard.  
- Write **README** with setup, `.env` variables, and payment config.  
- Clean code & finalize project.  

---

## ✅ Final Platform Includes
- **Authentication & Roles (Supabase)**  
- **Campaign Builder (multi-step wizard)**  
- **Campaign Lifecycle Management (Draft → Payment → Approval → Running/Ended)**  
- **Admin Dashboard with User & Campaign Management**  
- **Analytics Dashboard (charts + metrics)**  
- **Chargily Payments (CCP & EDAHABIA)**  
- **Deployment & Documentation**  

# AWS Budgets 
## Hands-On Guide to Cost Management

Efficient cost management in AWS starts with enabling IAM billing access and setting up budget alerts.  
This guide walks you through both — step-by-step and simplified for practical understanding.

---

## 1. Prerequisites: Enabling IAM User Billing Access

For IAM users to **view and manage Billing and Cost Management data**,  
the **Root Account** must explicitly enable IAM billing access.

###  Quick Hands-On (Root Account Required)

1. Log in to the **AWS Management Console** using the **Root Account**.  
2. Open the **Account Settings** page  
   → Click the dropdown in the top-right corner (your account name).  
3. Scroll to **IAM User and Role Access to Billing Information**.  
4. Select the checkbox to **Activate IAM access to the billing console**.  

**✅ Result:**  
IAM users can now be granted permissions to view the Billing section using IAM policies.

---

###  Clarifying IAM User Access

IAM billing access is controlled by **two layers**:

| Layer | Description |
|--------|-------------|
| **Root Account Setting** | Must be manually enabled (steps above). Without it, *no IAM user*, even with `AdministratorAccess`, can view billing data. |
| **IAM Policy** | Once access is enabled, attach a policy that grants billing permissions — e.g. `ViewBilling` or `ViewOnlyAccess`. |

**Important Note:**  
The `AdministratorAccess` policy **does not** automatically include billing permissions.  
This design ensures **financial data remains protected** unless intentionally shared by the root user.

---

## 2. Setting Up Budget Alerts with Templates

AWS Budgets helps you **monitor and control costs** by setting alerts for cost or usage thresholds.

---

###  Hands-On: Zero Spend Budget (Prevention)

A **Zero Spend Budget** ensures you don’t accidentally incur charges — perfect for learners or sandbox accounts.

**Steps:**
1. Open the **AWS Budgets** service in the console.  
2. Click **Create budget**.  
3. Under **Set up budget**, choose **Use a template (simplified)**.  
4. Select **Zero spend budget**.  
5. Configure:
   - **Budget Name:** `Zero_Spend_Alert`
   - **Alert Recipient:** your email address  
6. Click **Create**.

**Concept Simplified:**  
This budget sets a threshold at **$0.01** and alerts you if any cost is forecasted,  
acting as an *“unexpected cost” alarm* for free-tier or training environments.

---

###  Hands-On: Monthly Cost Budget (Threshold)

Track your **monthly AWS spending** and receive alerts before reaching your limit.

**Steps:**
1. Navigate to **AWS Budgets** in the console.  
2. Click **Create budget**.  
3. Under **Set up budget**, choose **Use a template (simplified)**.  
4. Select **Monthly cost budget**.  
5. Configure:
   - **Budget Name:** `Monthly_Max_200`
   - **Monthly Budget Amount:** `$200`
   - **Alert Threshold:** `85%`
   - **Alert Recipient:** your email  
6. Click **Create**.

**Concept Simplified:**  
This budget monitors your **Actual** and **Forecasted Costs** against a set dollar limit.  
Setting an 85% alert gives you **early warning** to manage rising costs before hitting your cap.

---

###  Summary

| Concept | Purpose |
|----------|----------|
| **Enable IAM Billing Access** | Allows IAM users to view billing data securely. |
| **Zero Spend Budget** | Prevents unintentional charges in test or training accounts. |
| **Monthly Cost Budget** | Tracks monthly spending and alerts before overspending. |

---

## Next Step:
Use **AWS Cost Explorer** to analyze trends

**Important Note:**  AWS Budgets and Cost Explorer work together for full cost visibility


###  Visual Overview — AWS Budgets + Cost Explorer Workflow
```mermaid
flowchart TD
    A[Root Account] --> B[Enable IAM Billing Access];
    B --> C[IAM User / Role];
    C --> D[AWS Budgets];
    C --> E[AWS Cost Explorer];
    D --> F[Budget Alerts (Email / SNS)];
    E --> G[Cost Trends & Analysis];
    D --> H[Prevent Overspending];
    E --> H;
    H --> I[Full Cost Visibility & Control];

    %% Custom Styling for Color Coding
    style A fill:#f9f9f9,stroke:#333,stroke-width:1px
    style D fill:#f4faff,stroke:#0073bb,stroke-width:1px
    style E fill:#f4faff,stroke:#0073bb,stroke-width:1px
    style F fill:#fff3cd,stroke:#ffcc00,stroke-width:1px
    style G fill:#e9f7ef,stroke:#28a745,stroke-width:1px
    style H fill:#fdf6ec,stroke:#ff9800,stroke-width:1px
    style I fill:#dff0d8,stroke:#3c763d,stroke-width:1px```

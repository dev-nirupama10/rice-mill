# A CRM APPLICATION FOR WHOLESALE RICEMILL

1. **Overview**     

   The Rice Mill CRM Application is designed to streamline daily rice tracking, sales, and type reporting, sending daily reports to owners. Leveraging CRM, it enhances customer experiences, optimizes operations. This user-friendly application addresses the specific needs of a rice mill.

2. **Features**

- **Daily Rice Tracking**: Monitor the amount of rice processed each day.
- **Sales Reporting**: Track how much rice is sold daily.
- **Rice Type Reporting**: Record and report the types of rice sold.
- **Daily Reports**: Send comprehensive daily reports to owners.
- **Roll-Up Summaries**: Summarize data from child objects to parent objects.
- **Cross-Object Formula Fields**: Calculate and display data from multiple objects on a single record.
- **Validation Rules**: Ensure data quality and consistency.

3. Objects Created

### Rice Mill

- **Fields**: `rice price/kg` (Number, Length: 5)
- **Roll-Up Summary**:
  - Field Label: `rice distributed to shops`
  - Summarized Object: `rice details`
  - Roll-Up Type: `sum`
  - Field to Aggregate: `rice distributed`

### Consumer

- **Fields**:
  - `First Name` (Text)
  - `Last Name` (Text)
  - `Phone Number` (Phone)
  - `Email` (Email)
  - `Rice Taken by Shops` (Number, Length: 5)
  - `Rice Type` (Picklist: Basmati, Normal Rice)
  - `Mode of Payment` (Picklist: Credit Card, Debit Card, Net Banking, UPI, Cash)
- **Cross-Object Formula Fields**:
  - **Amount Paid**:
    - Field Label: `Amount Paid`
    - Formula Return Type: `Number`
    - Formula: `rice_taken_by_shops__c * rice_mill_name__r.rice_price_kg__c`
  - **Consumer Name**:
    - Field Label: `Consumer Name`
    - Formula Return Type: `TEXT`
    - Formula: `First_Name__c + ' ' + Last_Name__c`
- **Validation Rules**:
  - **Phone Number or Email Blank**:
    - Rule Name: `Phonenumberoremailblankrule`
    - Formula: `OR(ISBLANK(phone_number__c), ISBLANK(email__c))`
    - Error Message: "Please fill in your phone number."

### Supplier

- **Fields**: Standard fields as needed
- **Roll-Up Summary**:
  - Field Label: `sum of rice distributed`
  - Summarized Object: `rice details`
  - Roll-Up Type: `sum`
  - Field to Aggregate: `rice distributed`

### Rice Details

- **Fields**:
  - `rice distributed` (Number, Length: 5)
  - Master-Detail relationships with `Supplier` and `Rice Mill`

4. Page Layouts

- **Personal Details**
- **Rice Details**
- **Receipt Details**

5. Tabs

- Create tabs for the following objects:
  - Supplier
  - Rice Mill
  - Consumer
  - Rice Details

6. Lightning App

- Create a Lightning App and add these navigation items:
  - Supplier
  - Rice Mill
  - Consumer
  - Rice Details

7. Relationships

- **Master-Detail Relationship**: Between Consumer and Rice Mill

8. Reports

- **Range of Amount per Day**
  - **Fields**: `Consumer Name`, `Rice Type`, `Rice Price/kg`, `Mode of Payments`, `Amount Paid`
  - **Group By**: `Rice Taken by Shops`

10. Profiles and Roles

### Profiles

- **Owner**
- **Employer**
- **Worker**

### Roles

- **Owner**: Reports to CEO
- **Employer**: Reports to Owner
- **Worker**: Reports to Employer

11. Users

- **Owner User**:
  - First Name: `Vicky`
  - Last Name: `Y`
  - Role: `Owner`
  - Profile: `Owner`
- **Employer User**:
  - First Name: `Ram`
  - Last Name: `Ram`
  - Role: `Employer`
  - Profile: `Employer`
- **Worker User**:
  - First Name: `Ragu`
  - Last Name: `Raj`
  - Role: `Worker`
  - Profile: `Worker`

12. Sharing Settings

- **Default Internal Access**: Public Read-Only for Rice Mill and Supplier

13. Dashboards

### Create Dashboard Folder

1. **Dashboard Folder**: `amount data dashboard`

### Create Dashboard

1. **Dashboard Name**: Your chosen name
2. **Components**:
   - **Vertical Bar Chart**:
     - X-axis: `rice taken by shops`
     - Y-axis: `sum of amount`
     - Component theme: `dark`
   - **Donut Chart**:
     - Sort by: `sum of amount`
     - Title: `range of amount per day`
     - Component theme: `dark`

## Daily Reports

- **Subscription**: Set up to send daily email notifications of the rice mill report to the owner.

## Conclusion

The Rice Mill CRM Application is an efficient tool designed to optimize the operations of a rice mill factory.

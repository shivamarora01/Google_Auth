# Google Authentication Setup

## Steps to Obtain Client ID & Client Secret

### Step 1: Open the Google Developer Console
Open [Google Developer Console](https://console.developers.google.com/) and you will be directed to this page:

![Step 1](https://drive.google.com/uc?export=view&id=1u71-OriOL1XNGPDlRBPLIUOJUzHDhHVv)

### Step 2: Access Projects Dropdown
Click on the **dropdown of Projects**:

![Step 2](https://drive.google.com/uc?export=view&id=1goWq-VO_jgRhYrMsk9aTZrimcSTNGfzx)

### Step 3: Create a New Project
Tap on **New Project** as shown below:

![Step 3](https://drive.google.com/uc?export=view&id=1Pic7uCu4uSVDX5ZlKA81L4ZP5BixtWIM)

### Step 4: Add Project Name
Create a **New Project** by adding a Project name:

![Step 4](https://drive.google.com/uc?export=view&id=1TnoHVS6waMv29dP9l78pNzWy-G6v18md)

### Step 5: Select Your Project
You will be directed to the dashboard. Go to the projects dropdown and select your project:

![Step 5](https://drive.google.com/uc?export=view&id=1c9hn4qLy9kEr2Hu9aqgVRz-RcA3vBM5e)

### Step 6: Navigate to Credentials
Click on the **Credentials** option and then click on the **create credentials** button in the credentials page:

![Step 6](https://drive.google.com/uc?export=view&id=1LQ5ZNAML6N2TWvOn0Yax0DCENc66DIt0)

### Step 7: Create OAuth Client ID
Click on **OAuth Client ID** and then click on the **create credentials** button in the credentials page:

![Step 7](https://drive.google.com/uc?export=view&id=1KNPBw_gk01oaL6113P_zet0otlC4LMRy)

### Step 8: Configure Consent Screen
Click on the **Consent screen** button:

![Step 8](https://drive.google.com/uc?export=view&id=1Ckfxc5N7LzKT5rywXMQ5_pAWmrH4HOLT)

### Step 9: Set User Type and Create App Registration
Select the User Type **External** and complete the app registration:

![Step 9](https://drive.google.com/uc?export=view&id=1aSDd_3Da7oCX-kZrCS_2phr4y4-uCqUR)

### Step 10: Add App Information
Add the **App information name** and **user mail**:

![Step 10](https://drive.google.com/uc?export=view&id=1K3GKLjgXdc4wLgNMTcwlvp6N6jTo9jZ7)

![Step 10](https://drive.google.com/uc?export=view&id=1XjTG7cxfuoE4-3-ZoIKQFcyqWXkUH5NW)

### Step 11: Save and Continue
Click **SAVE AND CONTINUE** for the next scope and test users:

![Step 11](https://drive.google.com/uc?export=view&id=1G7Yqy7X-7CJACX-BefciVC-zEtzxVF7t)

![Step 11](https://drive.google.com/uc?export=view&id=1obpi2DMigkPEjhSBs5Yg_CUKm9samFBF)

### Step 12: Create OAuth Client ID Again
Click on the **Credentials** option and then click on the **create credentials** button again in the credentials page:

![Step 12](https://drive.google.com/uc?export=view&id=1LQ5ZNAML6N2TWvOn0Yax0DCENc66DIt0)

### Step 13: Create OAuth Client ID Again
Click on **OAuth Client ID** and then tap on the **create credentials** button in the credentials page:

![Step 13](https://drive.google.com/uc?export=view&id=1KNPBw_gk01oaL6113P_zet0otlC4LMRy)

### Step 14: Configure Web Application
Choose the application type as **Web application** and add the redirect URI: `http://localhost:3000/auth/google/callback`. Adjust the port number according to your setup.

![Step 14](https://drive.google.com/uc?export=view&id=1sqAYCgxSqToRNYcrZUe9P3-q_OL-Rgpa)

![Step 14](https://drive.google.com/uc?export=view&id=1k_11fB0EPRonmz7cOZb4NJyVKsS8I0Uj)

### Step 15: Copy OAuth Keys
Copy and paste the keys into your project where needed:

![Step 15](https://drive.google.com/uc?export=view&id=1ppTtjqfYvtnUsJljaocHKVOuboctCPb9)


## Setting Up Node.js Application

### Step 1: Open VSCode and Setup Node.js
Set up Node.js environment in your preferred code editor.

### Reference Files:
- [Google Login Link](https://drive.google.com/file/d/1Hpt-hGoZZmgte9-V541v9_1blj-qC92l/view?usp=sharing)

### Directory Structure:
![Directory Structure](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.018.png)

### Step 2: Install Required Packages
Install necessary packages in your terminal:


```bash
echo "SESSION_SECRET=\"YOUR_SESSION_SECRET_HERE\"" > .env
echo "CLIENT_ID=\"YOUR_CLIENT_ID_HERE\"" >> .env
echo "CLIENT_SECRET=\"YOUR_CLIENT_SECRET_HERE\"" >> .env
```

```bash
npm i express dotenv ejs express-session passport passport-google-oauth2


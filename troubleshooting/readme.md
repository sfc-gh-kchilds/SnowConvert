# Troubleshooting & FAQ

Below are common issues encountered during the SnowConvert HOL and their resolutions.

---

## "Failed to prepare code processor for SqlServer" Error

**Symptoms:** Conversion fails immediately with the message "Failed to prepare code processor for SqlServer."

**Cause:** The `~/.config/Snowflake Inc` directory may have incorrect ownership (e.g., owned by `root` instead of your user account). This can happen if SnowConvert or another Snowflake tool was run with elevated privileges at some point.

**Solution:**
```bash
sudo mkdir -p ~/.config/Snowflake\ Inc
sudo chown -R $(whoami) ~/.config/Snowflake\ Inc/
```
Restart SnowConvert after running these commands and try the conversion again.

---

## Cannot Connect to the SQL Server Source Database

**Symptoms:** Connection test fails or times out when entering SQL Server credentials.

**Cause:** Two common issues:
1. You are not on a full-tunnel VPN. The lab SQL Server is only reachable through the RTF VPN.
2. You accidentally entered your **Snowflake** account URL instead of the **SQL Server** URL.

**Solution:**
- Connect to one of the **RTF labeled VPN gateways** (full tunnel). With RTF you will still be able to reach your Snowflake demo account.
- Verify you are using the correct SQL Server connection details:
  - Server URL: `snowconvert-datamigration.database.windows.net`
  - Port: `1433`
  - Database: `AdventureWorks`
  - Username: `demo_user`
  - Password: `Secure12345!ForDem0`

---

## PAT Authentication Does Not Work

**Symptoms:** Snowflake connection fails or the PAT token appears truncated when using Personal Access Token authentication.

**Cause:** PAT authentication is not reliably supported in SnowConvert AI at this time.

**Solution:** Use **Standard** authentication (username and password) for your Snowflake connection. Do not use PAT.

---

## "Convert with AI" Button Does Not Work

**Symptoms:** Clicking "Convert with AI" produces no result or an error.

**Cause:** This feature is not functional in the current version of SnowConvert AI.

**Solution:** Use the **"Convert code and ETL/BI projects"** option instead. This performs the same conversion successfully.

---

## AI Verification Requires a Warehouse

**Symptoms:** When navigating to AI Verification, you are prompted for a warehouse or the verification fails.

**Cause:** Your Snowflake connection in SnowConvert may not have a warehouse specified.

**Solution:** Go to your Snowflake connection settings in SnowConvert and ensure a warehouse (e.g., `MEDIUM`) is selected before running AI Verification.

---

## Sign-In: Choose Your Personal Demo Account

**Symptoms:** AI Verification or deployment behaves unexpectedly, or objects are created in the wrong account.

**Cause:** At the Snowflake sign-in prompt, you may have selected the wrong account (e.g., SNOWHOUSE instead of your personal demo account).

**Solution:** When prompted to sign in to Snowflake, always select your **personal demo account** (e.g., `sfsenorthamerica-demo83`), not SNOWHOUSE or any shared account.

---

## DatabaseLog Table Error During Data Migration

**Symptoms:** An error appears for the DatabaseLog table during the data migration step.

**Cause:** The DatabaseLog table contains XML data types that may not migrate cleanly.

**Solution:** This error can be safely ignored. All other tables will migrate successfully.

---

## DV10 Data Validation Error

**Symptoms:** A DV10 error appears if you attempt to use the data validation feature.

**Cause:** The data validation feature is still in development.

**Solution:** This is a known issue and can be ignored for this lab. Data validation is not required to complete the lab successfully.

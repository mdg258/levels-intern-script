### README for **Levels.fyi Internship Data Scraper**

---

#### **Overview**

This JavaScript code is designed to scrape internship data from the [levels.fyi internship page](https://www.levels.fyi/internships) and download the extracted data as a CSV file. It gathers company names, locations, monthly rates, application statuses, and links for easy analysis or storage.

---

#### **Steps to Use**

1. **Navigate to the Correct URL**:
   - Open your browser and go to **[https://www.levels.fyi/internships](https://www.levels.fyi/internships)**.

2. **Open the Browser Console**:
   - Right-click anywhere on the page and select **Inspect**.
   - Go to the **Console** tab in the Developer Tools window.

3. **Paste the Code**:
   - Copy the entire JavaScript code provided below.
   - Paste the code into the **Console** and press **Enter**.

4. **Download the CSV**:
   - The script will automatically scrape the data from the internships table.
   - A CSV file named `internships.csv` will be generated and automatically downloaded.

---

#### **How the Code Works**

1. **Scrapes Data**:
   - The script uses XPath expressions to select elements from the internships table on the page.
   - It extracts the following data for each internship:
     - **Company Name**: Extracted from the first column.
     - **Location**: Extracted from the first column, under the company name.
     - **Monthly Rate**: Extracted from the second column.
     - **Status**: Whether the position is open for applications or not, found in the fourth column.
     - **Application Links**: Links to apply for the internships, also found in the fourth column.

2. **Generates CSV**:
   - The extracted data is formatted into CSV format with the columns:
     - `Company Name`, `Location`, `Monthly Rate`, `Status`, and `Link`.
   - Each field is enclosed in double quotes to handle potential commas in the data.

3. **Downloads the CSV**:
   - The generated CSV is automatically downloaded to your computer as `internships.csv`.

---

#### **Troubleshooting**

- If the data is not scraped correctly or the CSV does not download:
  - Ensure that you are on the correct page (`https://www.levels.fyi/internships/`).
  - Make sure that the internships table is visible and loaded before running the code.

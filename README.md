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

#### **The Code**

```javascript
// Company Names
const nameXpath = "//*[@id='internships-table']/tbody/tr/td[1]/div/div[2]/h6";
const nameSnapshot = document.evaluate(nameXpath, document, null, XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
const names = [];
for (let i = 0; i < nameSnapshot.snapshotLength; i++) {
    names.push(nameSnapshot.snapshotItem(i).textContent.trim());
}

// Locations
const locationXpath = "//*[@id='internships-table']/tbody/tr/td[1]/div/div[2]/p";
const locationSnapshot = document.evaluate(locationXpath, document, null, XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
const locations = [];
for (let i = 0; i < locationSnapshot.snapshotLength; i++) {
    locations.push(locationSnapshot.snapshotItem(i).textContent.trim());
}

// Monthly Rates
const monthlyRateXpath = "//*[@id='internships-table']/tbody/tr/td[2]/div[1]/div/p[1]";
const monthlyRateSnapshot = document.evaluate(monthlyRateXpath, document, null, XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
const monthlyRates = [];
for (let i = 0; i < monthlyRateSnapshot.snapshotLength; i++) {
    monthlyRates.push(monthlyRateSnapshot.snapshotItem(i).textContent.trim());
}

// Open or Not Open
const statusXpath = "//*[@id='internships-table']/tbody/tr/td[4]/p/a";
const statusSnapshot = document.evaluate(statusXpath, document, null, XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
const statuses = [];
for (let i = 0; i < statusSnapshot.snapshotLength; i++) {
    statuses.push(statusSnapshot.snapshotItem(i).textContent.trim());
}

// Application Links
const linkXpath = "//*[@id='internships-table']/tbody/tr/td[4]/p/a";
const linkSnapshot = document.evaluate(linkXpath, document, null, XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
const links = [];
for (let i = 0; i < linkSnapshot.snapshotLength; i++) {
    links.push(linkSnapshot.snapshotItem(i).href);
}

// Generate CSV content with each field enclosed in quotes to handle commas
let csvContent = `"Company Name","Location","Monthly Rate","Status","Link"\n`;
for (let i = 0; i < names.length; i++) {
    csvContent += `"${names[i]}","${locations[i]}","${monthlyRates[i]}","${statuses[i]}","${links[i]}"\n`;
}

// Download the CSV
const blob = new Blob([csvContent], { type: 'text/csv' });
const link = document.createElement('a');
link.href = URL.createObjectURL(blob);
link.download = 'internships.csv';  // Name of the file
document.body.appendChild(link);
link.click();
document.body.removeChild(link);
```

---

#### **Troubleshooting**

- If the data is not scraped correctly or the CSV does not download:
  - Ensure that you are on the correct page (`https://www.levels.fyi/internships/`).
  - Make sure that the internships table is visible and loaded before running the code.

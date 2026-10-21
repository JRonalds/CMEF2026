# CMEF 2026 Mission Control — GitHub Pages + Google Sheets

Responsive Thai-language app for the CMEF Beijing 22–23 October trip. Includes Dashboard, detailed planner, hall explorer, supplier CRM, medical discovery checklists, export and a shared team overview.

## 1. Publish on GitHub Pages
1. Create a **public** GitHub repository, e.g. `cmef-mission-control`.
2. Upload `index.html`, `assets/`, and optionally `README.md`. **Do not upload confidential information.**
3. Go to **Settings → Pages → Build and deployment → Deploy from a branch → main / (root) → Save**.
4. Wait for the site link: `https://YOUR-USERNAME.github.io/cmef-mission-control/`.
5. Open that URL on Safari, then Share → Add to Home Screen.

## 2. Create Google Sheets database
1. Create a new Google Sheet named `CMEF 2026 Team Data`.
2. Copy its ID from `https://docs.google.com/spreadsheets/d/THIS_ID/edit`.
3. In the sheet, choose **Extensions → Apps Script**.
4. Paste the contents of `apps-script/Code.gs` into `Code.gs`.
5. In Apps Script choose **Project Settings → Script Properties → Add script property**.
6. Set name `SPREADSHEET_ID` and value to the Sheet ID, then save.
7. Choose **Deploy → New deployment → Web app**. Set **Execute as: Me** and **Who has access: Anyone**, then Deploy and authorize.
8. Copy the Web App URL ending in `/exec`.
9. On the GitHub Pages app open **☁️ Team Sync**, choose a user (`Business`, `น้องคนที่ 1`, or `น้องคนที่ 2`), paste the Web App URL, click **บันทึกการตั้งค่า** then **ส่งข้อมูลของฉัน**.
10. Click **ดูข้อมูลทีมล่าสุด**. Each user can repeat these steps on their own phone. Share the same Apps Script URL privately among the three participants.

## Data and sync behavior
- Local device data remains in the browser's `localStorage`.
- Changes send a snapshot for the **selected user only**; the three users' records do not overwrite each other.
- The Team Dashboard reads three separate snapshots from Sheets. The regular Dashboard/Planner/CRM remains device-local; it does **not** merge teammates' individual supplier records into a shared CRM.
- Sending uses an opaque cross-origin request. It cannot confirm success from the response alone; click **ดูข้อมูลทีมล่าสุด** and verify the updated timestamp.
- Changing devices will not automatically restore local data. Export JSON regularly.
- Offline use is limited to an already loaded page and local storage; this is not a full offline PWA.

## IMPORTANT SECURITY NOTICE
This starter setup intentionally has **no authentication or authorization**. Public GitHub Pages JavaScript and a publicly reachable Apps Script endpoint are unsuitable for confidential information. Anyone with the Apps Script URL may potentially read or alter records. Do **not** enter personal details, medical records, customer details, confidential quotations, passwords, private phone numbers, or business secrets. For private production use, replace this backend with Firebase Authentication + Firestore security rules or a properly authenticated API.

## Troubleshooting
- If buttons don't work on iPhone, **open the GitHub Pages HTTPS URL in Safari**, not the HTML file in the iOS Files preview.
- If data does not appear, confirm deployment URL ends `/exec`, Script Properties contains the correct Sheet ID, and Web App access is `Anyone`.
- If you edit `Code.gs`, deploy a **new version** via **Deploy → Manage deployments → Edit → New version**.
- GitHub Pages changes may take a few minutes to appear. Reload Safari.

# Portfolio update guide

## What is in this folder
- `index.html` - your upgraded portfolio (all old projects kept, new ones added)
- `n8n-portfolio-form-workflow.json` - ready-to-import n8n workflow for the forms

## Step 1: Set up the n8n workflow (about 10 minutes)
1. Open your n8n. Click **Workflows > Add workflow > the three dots > Import from file**.
2. Choose `n8n-portfolio-form-workflow.json`.
3. Open the **Email Me** node: replace `YOUR_EMAIL_HERE` with the email where you want alerts. Pick your Gmail credential.
4. Open the **Auto-reply to Visitor** node: pick the same Gmail credential.
5. Open the **Save to Google Sheet** node: pick your Google Sheets credential, then choose your spreadsheet and sheet. Give the sheet these column headings in row 1: `Submitted At, Type, Name, Email, Service, Preferred Date, Preferred Time, Timezone, Message`.
6. Open the **Portfolio Webhook** node and copy the **Production URL** (not the Test URL).
7. Turn the workflow **Active** (switch at the top right).

## Step 2: Connect the website
1. Open `index.html` and search for `PASTE_YOUR_N8N_WEBHOOK_URL_HERE`.
2. Replace it with your Production URL, keeping the quotation marks.
3. Save.

Until you do this, the forms keep sending to your old Google Sheet script, so nothing breaks.

## Step 3: Test
Fill in both forms on your site (message and request a call). You should get an email alert, the visitor gets an auto-reply, and a new row appears in your sheet.

## Step 4: Push to GitHub
1. Replace the old `index.html` in your repo with this one (upload on github.com, or `git add index.html`, `git commit -m "Upgrade portfolio"`, `git push`).
2. Wait 1 to 2 minutes, then refresh your live site.

## Adding links to the new projects later
Each new project shows "Client delivery". To link one to a demo or Drive folder, find its `<span class="wnote">` line and replace it with:
`<a class="warrow" href="YOUR_LINK" target="_blank" rel="noopener">View details →</a>`

## Good to know
- If n8n is ever down, the form automatically falls back to the Google Sheet script, so the lead is not lost.
- The hidden "company" field catches spam bots.
- If a webhook test fails with a browser error, check that the webhook node option "Allowed Origins" is set to `*` (it is in the import).

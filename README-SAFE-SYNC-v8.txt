# Happy Home Quiz App — Safe Sync v8

## What changed
- Bulk question imports are uploaded to Google Apps Script in smaller sequential batches (40 questions per batch).
- The app reads the cloud database after upload and verifies that every imported question ID exists before clearing the pending-sync queue.
- If verification fails, the local changes remain queued for retry and the UI reports that cloud sync was not verified.
- After successful verification, the app pulls the merged cloud database so the importing device receives other teachers' records.
- Existing merge-by-ID Apps Script backend is retained.
- Service worker cache changed from v7 to v8.

## Deploy
1. In the existing GitHub repository, replace `index.html` and `sw.js` with these files.
2. Do not replace `Code.gs` if the Safe Sync v7 Apps Script code is already deployed. The existing backend supports `SYNC_TABLE` batches.
3. Commit the two files and wait for GitHub Pages deployment to succeed.
4. On each device, close the app and reopen it, then hard refresh (Ctrl+F5 on desktop).
5. Test with a small import first, then a larger Excel/CSV import.
6. Confirm the imported questions appear on another device and in the Google Sheets `QUESTIONS` tab.

## Important
- The app still uses `no-cors` for POST because Apps Script web-app POST responses can be opaque in browsers. It now verifies by making a separate GET request.
- If verification fails, do not clear browser data or delete the pending queue. The app retains it for retry.
- Test the live Apps Script deployment and actual school data before relying on the feature.

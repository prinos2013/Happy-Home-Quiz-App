# Happy Home Quiz App — Submission Management and Empty Template Update

This package builds on the previously corrected CSV/Excel answer-key importer.

## New changes

- Teachers can delete an individual student submission only when it belongs to one of their assigned classes.
- Teachers can select multiple visible submissions and delete them together. The bulk action rechecks the assigned-class permissions before removing anything.
- Administrators can view and delete submissions from all classes, individually or in bulk.
- Deletions are saved to the app's ATTEMPTS table and passed through the existing `SYNC_TABLE` cloud-sync path. When offline, the existing pending-sync mechanism queues the table update for the next connection.
- The downloadable import template now contains only the column headings. No sample classes, subjects, questions, options, answer keys, or timer values are prefilled.
- The service-worker cache name has been increased to v5 so deployed devices fetch the updated app files.

## Empty CSV template columns

`Class,Subject,Question,OptionA,OptionB,OptionC,OptionD,CorrectAnswer,TimerMinutes`

Teachers and administrators fill in their own rows beneath these headings. For `CorrectAnswer`, either the A/B/C/D key or the full text of the matching option is accepted by the corrected importer.

## Updating GitHub Pages

1. Extract this ZIP.
2. Replace the repository-root `index.html`, `sw.js`, and `manifest.json` with the files in this package.
3. Upload/replace `logo.png`, `icon-192.png`, and `icon-512.png` in the repository root.
4. Commit the changes and wait for GitHub Pages to deploy.
5. Open the website in a browser and refresh it. If an installed PWA still shows the old screen, close and reopen it after the service worker updates.

## Notes on submission deletion

The app deletes records from its stored `ATTEMPTS` table and syncs that updated table using the existing cloud-sync endpoint. The separate append-only Google Sheets history created by the `APPEND_RESULT` action is controlled by the Google Apps Script; this package does not modify that script or guarantee removal of already-appended sheet rows.

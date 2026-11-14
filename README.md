# Happy Home Quiz App — CSV Answer-Key Fix

This package contains the corrected GitHub Pages application.

## What was wrong
The supplied `HappyHome_Quiz_Template_11_Populated.csv` contains complete answer text in the `CorrectAnswer` column (not only A/B/C/D). Some question/option cells also contain commas inside CSV quotes. The old importer split every row at every comma and extracted the first A-D character it found in answer text, which could save the wrong answer key.

## What is fixed
- CSV parsing now respects quoted commas and quoted cells.
- Correct-answer text is matched against Option A, B, C, or D and stored as the corresponding letter.
- Scoring resolves letter, numeric, and full-option-text keys defensively.
- Re-importing a question set replaces old records with matching class, subject, and question text. This prevents old incorrectly imported duplicates from continuing to appear in student quizzes.
- The service-worker cache was increased to v4 so deployed clients can move off the older cached app.

## GitHub Pages update
1. Extract this ZIP.
2. Upload/replace all files in the repository root: `index.html`, `sw.js`, `manifest.json`, `logo.png`, `icon-192.png`, and `icon-512.png`.
3. Commit the changes and wait for the GitHub Pages deployment to finish.
4. Open the deployed site in a normal browser tab, not only the installed app, and refresh it once.
5. Sign in to the Teacher Portal and upload the same populated CSV again. The importer now replaces matching old question records instead of adding duplicate copies.
6. Ask a student to open a fresh quiz and answer a few questions whose correct options are known.

The current importer's spreadsheet support uses SheetJS from its CDN for `.xlsx`/`.xls`; CSV import works directly in the browser.

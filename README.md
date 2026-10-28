# Team 5103 documentation Apps Script

`AppScript.js` is the backend for the documentation site. It keeps public reads, including Kade's explicit `?full=true` Pi feed, but only exports pages linked from the public table of contents.

Writes require a verified Firebase Google user with the current `editor: true` custom claim. They are validated, written as literal Sheet values, and protected against overlapping or stale saves.

Before deploying, add these Apps Script project properties:

- `FIREBASE_WEB_API_KEY`
- `FIREBASE_PROJECT_ID`

Enable the Advanced Sheets service, set editor claims with your existing Firebase Admin tooling, then deploy `AppScript.js` as the existing web app so its `/exec` URL stays the same. Anonymous invocation remains enabled for public reads; write authorization happens inside `doPost`.

After deployment, check one public read, one editor save, one anonymous rejection, and one stale-version rejection. Then remove and rotate the old Sheet-stored passwords.

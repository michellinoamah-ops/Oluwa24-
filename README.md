# Oluwa Memorial Senior Secondary School • Class of 2014

## Open in VS Code

Extract the ZIP, then open the folder containing this README in VS Code. Use Live Server on dist/index.html, or run `python -m http.server 8080 --directory dist` and open http://localhost:8080. JavaScript modules and private-code lookup require HTTP on localhost or HTTPS on a hosted domain. There is no npm build step.

## Activate the live register

The site already contains the supplied web configuration for Firebase project **oluwa-24**. Use the project owner's Firebase Console for this one-time setup.

1. In Build → Firestore Database, create the default Cloud Firestore database if it does not exist. Use production mode.
2. In Firestore → Rules, publish the rules from firestore.rules. If this project serves another application, merge these collection rules with its existing rules and remove any broad rule that grants overlapping public access. Alternatively, from this directory use `firebase deploy --only firestore:rules --project oluwa-24` after Firebase CLI sign-in.
3. In Authentication → Sign-in method, enable Email/Password. In Users, add the treasurer's email and a strong password. Copy that user's UID.
4. In Firestore → Data, create collection **admins**, add a document whose ID exactly equals that UID, and add a string field named **label** with value **Treasurer**. The existence of this document grants access. Remove it to revoke access. Only the project owner should manage this collection in the console.
5. Under Authentication → Settings → Authorized domains, include the host used for deployment and localhost if needed for testing. If you restrict the web API key by HTTP referrer, include your deployed website there too.
6. Open Administrator sign-in from the footer. Add a member with the agreed first dues month and monthly amount, choose **Copy sign-in details**, and send the registered name and code privately to that member. The five-digit code and private member link are saved in the administrator-only memberAccess collection. Retrieve them any time under Member codes. For a previously registered member, Show or assign code issues new details while preserving the existing payment history and long-code access. Send the private link as well as the registered name and code.

Cloud Firestore is the only database. Firebase Authentication identifies administrators. Website assets, including the film, are ordinary static files. No Storage rules, Cloud Functions, service account JSON or composite indexes are required.

## Payment register

Enter the actual receipt date, amount and category. For monthly dues select the month the payment covers. Split receipts covering multiple months into one entry for each month. A wedding or child dedication entry takes the event name. Open Payment listings and search by name, month or event, or filter by category. Edit corrects an entry. Delete shows the member, amount, date and month or event for confirmation. A confirmed deletion removes the entry from the statement and report. Admin sessions last for the browser session. Select a category and choose Download category PDF to export every payment in that category. Download all payments exports the complete register. The reports cover payments received. The welfare schedule on the association page lists support payable by the union. Exports contain members' names and should be kept by the office.

## Membership policy used in this edition

- The administrator chooses the first chargeable month. Newly registered members pay ₦1,000 per month. Existing members retain their recorded rates. Monetary values are held as integer kobo.
- Months fall due at the end of the calendar month in Lagos. The current month can be paid early and is excluded from arrears. Partial payments accumulate for their assigned month. A surplus for one month stays assigned to that month.
- Any recorded positive monthly-dues payment establishes participation. No monthly-dues payments produces “You are not a member”. Weddings and child dedications do not affect this calculation.
- One underpaid completed month gives a one-month warning. Two or more underpaid completed months give an arrears warning listing every affected month and the combined shortfall, including nonconsecutive months.
- A missing or mistyped name/code produces “No matching record”.

## Deploy to Vercel from GitHub

Import this repository in Vercel under Add New → Project. Keep the Root Directory at the repository root and use the Other preset. The tracked vercel.json selects dist as the public output. Leave the install and build commands unset. The site needs no environment variables to build. After deployment add the Vercel hostname to Firebase Authentication's authorized domains. Publish firestore.rules separately in project oluwa-24. Changes pushed to the connected production branch deploy through Vercel.

## Media

The original association seal is dist/media/Oluwa-2014-Seal.png. The homepage loads a Wikimedia campus photograph with the local seal as its fallback. The uploaded film and poster are hosted inside dist/media. The school history and photograph source are linked on the credits page.

## Verify the live setup

Sign in as the approved administrator, enter a member and their first payment, and check that the name and code show the correct amount in a separate browser session. Check one wedding or child dedication entry and download the PDF. Use Firebase Rules Playground to verify that an unauthenticated write to members or payments is denied and a list request on members is denied.

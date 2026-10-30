# Privacy and local-first behavior

Local editing, search and recovery work without a TextRay account. The working library is on your Mac; Save writes a regular file to a location you choose.

| Action | Data boundary |
| --- | --- |
| Edit, search, create a View, inspect history | Local text and metadata. No AI or analytics service receives the working text. |
| Enable iCloud | Retained text and associated organization/history records sync through Apple CloudKit in your private iCloud database. |
| Activate or recover a license | The license service receives the required code, purchase email or random installation/device proof. It does not receive document text, filenames, paths or searches. |
| Buy TextRay | Stripe Managed Payments handles checkout, tax and payment details. Burrito’s Labs does not receive full card details. |
| Manually check for updates | The release server receives ordinary connection data, including IP address and app version. Automatic checks and system profiling are off by default. |
| Run a custom command | A program you choose runs with your account’s permissions and may access files or the network. |
| Open an external link or contact support | Your browser or email application handles that action. Diagnostics are not uploaded automatically. |

The application includes no analytics SDK or automatic diagnostic upload. Optional cloud sync is separate from local recovery, licensing and update checks. It should not be described as “no cloud” or as a guarantee that no network request ever occurs.

Markdown preview renders locally, with raw HTML and unsolicited network resources disabled. Local images and relative document links follow explicit access rules; this does not turn arbitrary Markdown into trusted executable content.

Closing work is different from deleting it. History retention and explicit deletion can remove retained revisions. Keep independent backups of important text. Uninstalling or updating the app does not remove its library.

This technical summary accompanies the full privacy information available in **Support & Policies** in the app. Contact [hello@burritoslabs.com](mailto:hello@burritoslabs.com) with privacy questions. Apple and payment providers also have their own policies.

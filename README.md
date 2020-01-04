# Exporting Protonmail On Linux

Because Protonmail has no [official import/export](https://protonmail.com/support/knowledge-base/export-import-emails/) tool for Linux I put down this modest repository. It serves as a simple example on how you can incrementally export (backup) all your email from Protonmail's servers to a local Maildir archive. 

This archive can be grepped (searched) because it is a bunch of good old resilient plaintext files. Because Maildir is a fairly standard format it can also be imported into mail clients like Thunderbird or be used when migrating away from Protonmail.

## Why would you export all your mail?

Email still has an import purpose for me personally. It is my archive of invoices, business arrangements and the rarest of memes. I would hate to not have access to them. I can imagine several situations where this could happen.

- Protonmail erroneously locks you out of your account.
- You want to do a full-text search of your mails (which Protonmail [does not support](https://protonmail.com/support/knowledge-base/search/)).
- You think it is generally bad practice to keep important data under the control of a single party.
- You want to migrate between providers or accounts.
- You want to get that feeling of nostalgia 20 years down the road, long after the internet ceases to exist. /s

## Where should I store my archive?

That really depends on your threat vectors. You could for example store and update the archive in an encrypted container (LUKS? Veracrypt?) which you regularly backup offsite. Think about how long you want to keep your archive and who you need to protect it from.

## Running an export

### Requirements:
- Probably any distro (Or anything that run offlineimap)
- [Offlineimap](https://github.com/OfflineIMAP/offlineimap) (I used v.7.2.3)
- Protonmail Bridge

### Procedure:
1. Install Protonmail Bridge (I usually get the url to the latest deb file for Ubuntu/Debian from [this](https://protonmail.com/download/beta/PKGBUILD)).
2. Run the Bridge and log in.
3. Clone and `cd` into this repository (in a encrypted container if you want).
4. Edit offlineimaprc and change at least the username (You can find it in the Bridge)
5. Run the export using `offlineimap -c offlineimaprc`
6. Offlineimap will ask for your Bridge password and start the sync.

Depending on the amount of emails in your account this can take few hours. Offlineimap uses a cache/metadata directory to track remote changes. This means you only download new emails when you run this command at a later date, something the official tool currently does not support.

## The future
I personally hope Protonmail releases both an open source version of the Bridge and Import/Export tool in the future that runs (or can be ported to) Windows, Linux and MacOS. Other than that: Keep up the great work Protonmail.

Furthermore: A heartfelt thanks to everyone in the Offlineimap project for powering my email archival needs all these years.

# Feature Catalogue — Later (unscheduled)

These 6 features (124–129) are worth building but have no release yet. Each is a candidate for any version once user feedback shows demand; until then they stay out of scope. Promote one by moving it to a release file and updating its version in `docs/planning/features.csv`.

## Unscheduled features

### 124. Dependency chains (download B after A)

**Queue and scheduling · Later · Pro**

**What it is:** Users can make one download wait for another to finish first, or build a chain of steps, for example: download a file, then download its matching subtitles, then run a script. Useful when one file only makes sense after another.

**User story:** As Sam, I want a download to start only after another finishes, so that multi-part jobs run in the right order without me watching them.

**Scenario:** Sam queues a large dataset and its smaller index file, and sets the index to start only after the dataset completes and passes its checksum, because his processing script needs both in that order.

**Acceptance criteria:**

- Any download can be set to wait for one or more other downloads to finish.
- A chain can require success: if an earlier download fails, the later ones pause with an explanation.
- Dependencies are shown visually in the queue.
- Circular dependencies (A waits for B, B waits for A) are prevented with a clear message.

### 125. Speed tests and diagnostics

**Network intelligence · Later · Free**

**What it is:** A built-in tool that checks the user's connection and explains why downloads might be slow: whether it's their internet, Wi-Fi, a VPN, a proxy, or the website's server.

**User story:** As Maya, I want the app to tell me why a download is slow, so that I know whether to fix my Wi-Fi or just wait.

**Scenario:** A download crawls at 200 KB/s. Maya clicks "Why is this slow?" The app tests her connection (50 Mbps, fine) and the server (limited to 200 KB/s per user), and explains that the website itself is the bottleneck.

**Acceptance criteria:**

- Measures the user's overall connection speed and delay, and the speed of the server for a given download.
- Explains the likely cause in plain language: connection, Wi-Fi signal, VPN or proxy, or server limits.
- Suggests a fix where possible (for example, more connections, a different mirror, or turning off a VPN).
- A diagnostics report can be copied for support or bug reports, with personal details removed.

### 126. Watch folders

**Automation · Later · Pro**

**What it is:** The app watches a chosen folder. When a file with download links (a text file of links, a .torrent or a .metalink) is dropped into it, the app queues those downloads automatically. Other programs or synced folders can feed downloads to the app this way.

**User story:** As Sam, I want to drop link files into a folder and have them downloaded, so that other tools and scripts can hand work to the app without using its API.

**Scenario:** Sam points a watch folder at a directory in his cloud storage. From his work computer he saves a text file of links into that folder; at home, the app sees it, queues the links, and moves the text file to a "processed" folder.

**Acceptance criteria:**

- Users can add one or more watch folders, each with its own queue and settings.
- Recognises .txt files of links, .torrent, .metalink and .url files.
- Processed files are moved to a subfolder or deleted, as chosen.
- Files with no valid links are left in place, with a note in the log.

### 127. Storage analytics and cleanup suggestions

**Library management · Later · Pro**

**What it is:** A view showing what's using storage in the user's download folders (by type, site, age and size), with suggestions for freeing space, such as old installers, duplicates, watched videos and leftover partial files.

**User story:** As Diego, I want to see what's filling my downloads drive and what's safe to delete, so that I can free space quickly before a big project.

**Scenario:** Diego's drive is nearly full. The storage view shows 180 GB of old installers and archives, 60 GB of watched reference videos older than a year, and 12 GB of abandoned partial downloads. He reviews the suggestions and frees 230 GB in a few clicks.

**Acceptance criteria:**

- Shows storage use by type, source site, age and size, in a clear chart.
- Suggests cleanup categories: old installers, archives already extracted, duplicates (feature 49), watched media, partial downloads.
- Every suggestion is reviewed before anything is deleted; nothing is deleted automatically.
- Deleted files go to the system bin.

### 128. Share links to downloaded files

**Sharing and collaboration · Later · Pro**

**What it is:** Users can create a private link to a file on their engine and send it to someone else, who can download it straight from the user's engine through the encrypted relay, without uploading it to a third-party service first.

**User story:** As Diego, I want to send a client a link to a large file on my studio engine, so that I don't have to upload it to a file-sharing service first.

**Scenario:** Diego right-clicks a 9 GB edit and creates a share link that expires in 7 days with a password. He sends it to his client, who downloads it straight from the studio engine.

**Acceptance criteria:**

- Share links can be created for files and folders.
- Options: expiry date, password, download limit, and revoke at any time.
- Downloads through a share link are encrypted and resumable.
- The owner sees when and how many times each link was used.
- Respects central policies (feature 118) in business workspaces.

### 129. Password-protected or locked folders

**Security and privacy · Later · Pro**

**What it is:** Users can lock particular folders or collections in the app behind a password or the computer's fingerprint or face login, and optionally encrypt the files in them, so other people using the computer can't open them through the app.

**User story:** As Priya, I want to lock a folder of confidential work documents, so that nobody else using my laptop can open them through the app.

**Scenario:** Priya locks her "Client contracts" collection with Touch ID. When her colleague borrows the laptop and opens the app, the collection shows only a lock icon.

**Acceptance criteria:**

- Folders and collections can be locked with a password or system biometric login (Windows Hello, Touch ID).
- Optional encryption of the locked files on disk, using a standard, well-reviewed method.
- Locked items are hidden from search, history and thumbnails until unlocked.
- Items lock again automatically after a chosen time or when the app closes.
- Clear warning that a forgotten password with encryption on means the files can't be recovered.

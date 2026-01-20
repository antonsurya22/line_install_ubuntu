# line_install_ubuntu
Way to install Line on Ubuntu 22.04 using Chromium Browser Extension


# LINE on Ubuntu 22.04 (Chromium Method)

LINE does not officially support Linux.  
This guide shows how to run LINE on **Ubuntu 22.04** using **Chromium + LINE Chrome extension**, and make it behave like a normal desktop app (Dash & Dock).

---

##  Requirements

- Ubuntu **22.04**
- Chromium browser
- Internet connection

---

## 1 Install Chromium

```bash
sudo apt update
sudo apt install chromium
````

> On Ubuntu 22.04, Chromium is installed as a **Snap package**.

Verify installation:

```bash
which chromium
```

Expected output:

```text
/snap/bin/chromium
```

---

## 2 Install LINE Chrome Extension

1. Open **Chromium**
2. Go to **Chrome Web Store**
3. Search for **LINE**
4. Install the **official LINE extension**
5. Open LINE and **log in successfully**

> Make sure LINE works normally before continuing.

---

## 3 Get LINE Extension ID

1. Open in Chromium:

```
chrome://extensions
```

2. Enable **Developer mode** (top right)
3. Find **LINE**
4. Copy the **Extension ID**

Example:

```
ophjlpahpchlmihnnnihgmmeilfjmjjc
```

---

## 4 Create LINE Desktop Launcher

Create a `.desktop` file:

```bash
nano ~/.local/share/applications/line.desktop
```

Paste the following **(replace `EXTENSION_ID`)**:

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=LINE
Comment=LINE Messenger (Chromium)
Exec=/snap/bin/chromium --profile-directory=Default --app="chrome-extension://EXTENSION_ID/index.html"
Icon=chromium
Terminal=false
Categories=Network;Chat;InstantMessaging;
StartupWMClass=chromium
```

### Example

```ini
Exec=/snap/bin/chromium --profile-directory=Default --app="chrome-extension://ophjlpahpchlmihnnnihgmmeilfjmjjc/index.html"
```

Save and exit:

* `Ctrl + O` → Enter
* `Ctrl + X`

---

## 5 Make Launcher Executable

```bash
chmod +x ~/.local/share/applications/line.desktop
update-desktop-database ~/.local/share/applications
```

Log out and log back in (recommended).

---

## 6 Pin LINE to Dock

1. Press **Super** key
2. Search **LINE**
3. Right-click → **Pin to Dash**

LINE now behaves like a normal desktop app.

---

## Optional: Separate Chromium Profile (Recommended)

To isolate LINE from your normal browser profile:

```bash
mkdir -p ~/.config/chromium-line
```

Edit launcher:

```bash
nano ~/.local/share/applications/line.desktop
```

Replace `Exec=` with:

```ini
Exec=/snap/bin/chromium --user-data-dir=/home/YOUR_USERNAME/.config/chromium-line --app="chrome-extension://EXTENSION_ID/index.html"
```

---

## Optional: Custom LINE Icon

1. Download a LINE icon (PNG)
2. Move it to:

```bash
~/.icons/line.png
```

3. Edit launcher:

```ini
Icon=/home/YOUR_USERNAME/.icons/line.png
```

---

## Test Command (Debug)

```bash
/snap/bin/chromium --profile-directory=Default --app="chrome-extension://EXTENSION_ID/index.html"
```

If this command works, the launcher will also work.

---

## Notes

* Not officially supported by LINE
* Uses Chromium Snap package
* Notifications depend on Chromium settings
* Tested on **Ubuntu 22.04 (GNOME)**

---

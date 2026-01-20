

## Requirements

- Ubuntu **22.04**
- Chromium browser (Snap)
- Internet connection

---

## 1 Install Chromium

```bash
sudo apt update
sudo apt install chromium
````

> On Ubuntu 22.04, Chromium is installed as a **Snap package**.

Verify:

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

2. Enable **Developer mode**
3. Find **LINE**
4. Copy the **Extension ID**

Example:

```
ophjlpahpchlmihnnnihgmmeilfjmjjc
```

---

## 4 Create LINE Desktop Launcher

Create the application launcher:

```bash
nano ~/.local/share/applications/line.desktop
```

Paste the following
(**replace `EXTENSION_ID` with your own**):

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=LINE
Comment=LINE Messenger (Chromium)
Exec=/snap/bin/chromium --class=LINE --profile-directory=Default --app="chrome-extension://EXTENSION_ID/index.html"
Icon=/home/YOUR_USERNAME/.icons/LINE.png
Terminal=false
Categories=Network;Chat;InstantMessaging;
StartupWMClass=LINE
```

### Example

```ini
Exec=/snap/bin/chromium --class=LINE --profile-directory=Default --app="chrome-extension://ophjlpahpchlmihnnnihgmmeilfjmjjc/index.html"
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

---

## 6 Restart Session (Important)

* Close all Chromium / LINE windows
* **Log out and log back in** (or reboot)

---

## 7 Pin LINE to Dock

1. Press **Super**
2. Search **LINE**
3. Right-click → **Pin to Dash**
4. Launch LINE from the Dock

 
 LINE now behaves like a native app:


## Optional: Custom LINE Icon

1. Download a LINE icon (PNG)
2. Create icons directory:

```bash
mkdir -p ~/.icons
```

3. Move icon:

```bash
mv LINE.png ~/.icons/LINE.png
```

4. Make sure launcher uses:

```ini
Icon=/home/YOUR_USERNAME/.icons/LINE.png
```

---

## Debug: Check Window Class

```bash
xprop | grep WM_CLASS
```

Click the LINE window.
Expected output:

```text
WM_CLASS(STRING) = "LINE", "LINE"
```

---

## Notes

* Not officially supported by LINE
* Uses Chromium Snap package
* Notifications depend on Chromium settings
* Tested on **Ubuntu 22.04 (GNOME)**

---


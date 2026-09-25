ShotPeak

A Windows-only, system-tray–resident screenshot and annotation tool built with **C# / WPF** on **.NET 8**.

ShotPeak stays quietly in the system tray. Press a global hotkey, drag a rectangle over the primary screen to crop, and annotate the selection in a normal resizable editor window — then save it as PNG/JPG or copy it to the clipboard. Pressing `ESC` or the close button never exits the app; it keeps running in the tray for the next capture. The only true exit is the tray menu **Exit**.

* * *

## ✨ Features

### Capture

* **Global hotkey** (default `Shift+Win+K`) opens a borderless, maximized, always-on-top fullscreen overlay of the **primary screen**.
* **Left-drag** a rectangle to select a crop region; the area outside your selection is dimmed.
* A live **size readout** (`W × H`) follows the selection.
* Release the mouse to close the overlay and open the crop in a normal, resizable editor window.

### Scrolling capture (long screenshot)

* **Global scrolling-capture hotkey** (default `Ctrl+Shift+L`) or tray menu → **Scrolling Capture** opens a fullscreen overlay with a **crosshair cursor**.
* **Left-drag** to select the content region to capture vertically (outside area dimmed, live size readout). On release a small progress panel appears at the bottom-right of the primary screen.
* **You** then scroll the content under the selected region yourself (mouse wheel or scrollbar) — the tool **continuously samples that fixed region** and stitches every newly exposed bottom strip into a growing image (empty/identical frames are skipped, and each seam is row-verified before it is appended, so the result contains **no duplicated or misplaced content**).
* Press **Enter** (or **Done** on the progress panel) to finish — the stitched long image opens in the editor for annotation/saving. Press **ESC** anytime to cancel.
* Total stitched height is capped at **20000 px**.

### Annotation toolbar (draggable)

The toolbar floats at the top-left and can be **dragged with the mouse** (drag on empty space; buttons and combo boxes remain clickable).

| Icon | Tool | Description |
| --- | --- | --- |
| ▭   | Rectangle | Drag to draw a rectangle frame |
| ◯   | Circle | Drag to draw an ellipse frame |
| ╱   | Line | Straight line (no arrowhead) |
| 〰   | Free Line | Freehand stroke using the current color/width |
| ↗   | Arrow | Line segment with an arrowhead |
| T   | Text | Type text onto the image |
| ▦   | Mosaic | Blur/pixelate a region (adjustable block size) |
| 🖊  | Crayon | Wide, translucent freehand brush — always uses the settings color/width, **independent** of the active editor style |
| ①   | Circle Number | Auto-incrementing numbered circle (1, 2, 3, …) with centered bold text |

### Style options

* **Color** — Red, Yellow, Green, Blue, White, Black
* **Line width** — 1, 3, 5, 8
* **Solid / Dashed** toggle
* **Mosaic block size** — 4, 8, 16, 32 (shown only when the Mosaic tool is active)

### Actions

* **Undo** (↩) — reverts the most recent action, one step per press
* **Redo** (↪) — re-applies the most recently undone action, one step per press
* **Copy** — copies the annotated result to the clipboard
* **Save** — saves as **PNG** or **JPG** (JPEG quality 95)
* **OCR** — runs Windows local OCR (`Windows.Media.Ocr`, fully offline) on the raw crop and copies the recognized text to the clipboard, then closes the editor. Requires MSIX package identity — see the OCR note below.
* **Close** — closes the editor; the app remains resident in the tray

### Settings (tray menu → Settings)

* **Capture hotkey** — choose any combination of `Ctrl` / `Alt` / `Shift` / `Win` plus a key (`A–Z`, `0–9`, or `F1–F12`). Applied immediately and persisted.
* **Crayon color** (translucent) and **crayon line width**.

### System tray

* Icon shows **"ShotPeak - Screenshot Tool"**.
* Right-click menu: **Capture** (shows current hotkey) · **Pick Color** (shows current hotkey) · **Settings** · **About** · **Launch at Startup** · **Exit**.
* **Launch at Startup** — a checkable toggle that registers/removes the `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` entry so the app starts automatically with Windows. Its text (On/Off) always reflects the current state.
* Double-click the icon to start a capture.

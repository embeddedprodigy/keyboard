# ErgoDash Rev1 Custom Keymap: myergodash

This repository contains the custom `myergodash` split mechanical keyboard profile. It uses a modern hybrid workflow: designing the baseline matrix visually via the online QMK Configurator tool, converting it locally using `json2c`, and embedding low-level C programming overrides for custom tap-hold timing thresholds.

---

## 🛠️ Step-by-Step Flashing & Deployment Pipeline

Follow this explicit sequence whenever you want to update or re-flash the layout configuration keys on your ErgoDash hardware.

### 🌐 Step 1: Design Layout in QMK Configurator
1. Open your web browser and navigate to the official **[QMK Configurator Website](https://qmk.fm)**.
2. Select the correct keyboard target hardware profile configuration template from the primary dropdown input field: **`omkbd/ergodash/rev1`**.
3. Arrange your structural matrix layout blocks visually across your layout layers exactly how you want them configured.

### 💾 Step 2: Download Your JSON Data Configuration File
1. Once your layout map design is complete, locate the right sidebar utility options panel layout.
2. Click the **Download Keymap JSON** button.
3. This saves a file named **`ergodash.json`** directly into your computer's local Windows `Downloads` folder.

### 💻 Step 3: Initialize Environment inside QMK MSYS
1. Fire up your local **QMK MSYS terminal tool application**.
2. Ensure you are sitting in your core firmware root workspace directory:
   ```bash
   cd qmk_firmware/
   ```
3. *Note: If this is the absolute first time you are initializing this profile setup on your machine, run the template generation script to set up your directory path workspace automatically:*
   ```bash
   qmk new-keymap -kb omkbd/ergodash/rev1 -km myergodash
   ```

### 🔧 Step 4: Convert and Parse JSON Code Layout Array
Run the compiler configuration parser tool to convert your web-generated visual layout array (`ergodash.json`) directly into a clean C source code file (`keymap.c`), automatically overwriting the default directory template file:
```bash
qmk json2c -o keyboards/omkbd/ergodash/rev1/keymaps/myergodash/keymap.c ~/Downloads/ergodash.json
```

### ⚡ Step 5: Direct Compile and Deployment Flash Execution
Execute the live build sequence script pipeline to compile the firmware and prepare your local environment listener for a live hardware transfer:
```bash
qmk flash -kb omkbd/ergodash/rev1 -km myergodash
```

### 💡 Step 6: Connect and Reset Hardware Bootloader
1. The script terminal prompt text scroll will halt and display a repeating listener tracking message:
   ```text
   Checking for bootloader...
   Please reset your keyboard's controller now...
   ```
2. Press the **physical hardware RESET button** located directly on your ErgoDash PCB board module circuitry (or quickly double-tap it depending on your controller board pin trace design).
3. The local program interface catches the initialization prompt signal and instantly builds your keys down directly onto your microcontroller chip.

---

## ⚙️ Advanced Layout Code Modifications

Because you are using local source files, you can override default QMK parameters to handle complex hardware rules that visual web configurators cannot natively process.

### 1. Customizing the Hold/Tap Long-Press Time (`config.h`)
If your Mod-Tap dual-function keys (like Shift or GUI keys on hold) are triggering too fast or too slow during normal typing rolls, you can configure their timing adjustments directly within this directory folder workspace.

1. In the same folder where this `readme.md` file lives (`keyboards/omkbd/ergodash/rev1/keymaps/myergodash/`), create a new blank text file named exactly **`config.h`**.
2. Open `config.h` using a text editor and paste the following baseline configuration settings text blocks directly into it:

```c
#pragma once

// Adjusts how long a key must be held down to count as a long-press (in milliseconds).
// The standard QMK default is 200. Increase it to 275 for cleaner typing rolling cuts.
#define TAPPING_TERM 275

// Optional: Prevents accidental modifier triggers during fast typing rolls
#define TAPPING_FORCE_HOLD
```

---

## 📋 Environment Profiles & Custom Target References

To verify your QMK target compilation environment or manage alternative layouts on your machine, you can run diagnostic tracking queries directly from your terminal.

### 1. Listing Available Keyboards
If you are switching hardware types or working across different layout architectures, you can verify all available keyboard profiles compiled within your local system registry metadata:
```bash
qmk list-keyboards
```
To quickly isolate and find your specific configurations from the full index, filter the query using a grep pipeline:
```bash
qmk list-keyboards | grep ergodash
```

### 2. Listing Available Keymaps
To see a full list of all custom and stock keymaps configured for the ErgoDash Rev1 hardware inside your repository setup, execute this path query:
```bash
qmk list-keymaps -kb omkbd/ergodash/rev1
```
*(Your custom `myergodash` directory profile should appear cleanly inside this printed list output).*

### 3. Creating a New Keymap
To scaffold a fresh keymap folder with template source files (see Step 3 above), run:
```bash
qmk new-keymap -kb omkbd/ergodash/rev1 -km <keymap-name>
```
For example:
```bash
qmk new-keymap -kb omkbd/ergodash/rev1 -km myergodash
```
This creates a new directory at `keyboards/omkbd/ergodash/rev1/keymaps/<keymap-name>/` populated with a template you can then overwrite via `qmk json2c`.

### 4. Querying the Default Keyboard & Keymap
QMK remembers your most recently used target as a saved default, letting you omit the `-kb` / `-km` flags on later commands. To check what is currently stored:
```bash
qmk config                      # shows ALL saved QMK settings in one view
qmk config user.keyboard        # shows the current default keyboard
qmk config user.keymap          # shows the current default keymap
```
If no default has been set yet, the output will be empty.

### 5. Setting the Default Keyboard & Keymap
Persist your target so `qmk compile` / `qmk flash` run without needing explicit flags:
```bash
qmk config user.keyboard=omkbd/ergodash/rev1
qmk config user.keymap=myergodash
```
After running these, the following works with no `-kb` / `-km` arguments:
```bash
qmk flash -km myergodash        # or simply: qmk flash
```

---

## 🗑️ Code Maintenance Notes
* **File Cleanup:** If the template code includes obsolete hardware rules like `#define AUDIO_PIN C6` but your build lacks a physical piezo buzzer speaker element, comment out or delete that line to prevent signal pin trace conflicts with your ErgoDash rev1 LED lighting matrix routes.


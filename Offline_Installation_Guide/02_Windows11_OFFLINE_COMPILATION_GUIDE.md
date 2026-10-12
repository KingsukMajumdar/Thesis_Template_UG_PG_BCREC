# ⚙️ Windows 11 (64-bit): Offline Compilation Guide: Thesis_Template_UG_PG_BCREC

A step-by-step setup guide for compiling this thesis template on your own Windows 11 (64-bit) laptop or desktop, without depending on Overleaf's free-tier compile queue and without purchasing an Overleaf plan.

Every step in the main part of this guide uses mouse and menus only (GUI). Users who prefer the terminal will find all PowerShell commands collected in **Appendix A** at the end.

With Regards
Kingsuk Majumdar, PhD(EE)

---

## 📋 Why compile on your own PC

Overleaf's free plan throttles compile time and queues long documents. A thesis with many chapters, MATLAB-highlighted listings, and multiple algorithm floats crosses that limit fast, and the paid plan is not affordable for every student. A local TeX installation is free, removes the queue entirely, and compiles in seconds once cached.

---

## 🧩 What this template actually needs

`thesis.cls` pulls in roughly 40 packages on top of the base `book` class. Three deserve special attention because a generic "install LaTeX" tutorial will not mention them:

1. **`fourier`**: needs the Adobe Utopia / Type 1 font set, not part of a minimal TeX install.
2. **`algorithm2e` (with `algcompatible`) loaded alongside `algorithmicx`/`algpseudocode`/`algorithm`**: two competing algorithm-typesetting families in the same class file. Both are present because different chapters historically used different syntax. Keep this in mind if you ever see a `\algorithmic already defined`-type error; see the Troubleshooting table.
3. **`mcode.sty`**: the MATLAB code-highlighting package by Florian Knorn. It is **not distributed through MiKTeX, TeX Live or CTAN**; it ships inside this template's repository itself. If it is missing from your working folder, no package manager will fix it. Section 2.6 explains how to add it.

---

## 🗺️ Road map (GUI route)

| Step | What you do | Section |
|---|---|---|
| 1 | Create a working folder `C:\Thesis` | 2.0 |
| 2 | Download the template from GitHub | 2.1 |
| 3 | Unzip it | 2.2 |
| 4 | Install MiKTeX (recommended) or TeX Live | 2.3, 2.4 |
| 5 | Install an editor: TeXworks, TeXstudio or VS Code | 2.5 |
| 6 | Check `mcode.sty` | 2.6 |
| 7 | Compile and get `main.pdf` | 2.7 |
| 8 | Fix problems, if any | 2.8, 2.9 |

---

## 🪟 2. Windows 11 (64-bit): GUI route

### 📁 2.0 Create a working folder

1. Open **File Explorer** (`Win + E`).
2. Click **This PC** → **Local Disk (C:)**.
3. Click **New** → **Folder** on the top toolbar. Name it `Thesis`.

You now have `C:\Thesis`. Keep the entire thesis inside this folder.

**Turn on file extensions** (needed later to spot `.sty`, `.cls`, `.bib` files):

1. In File Explorer, click **View** → **Show** → tick **File name extensions**.

> ⚠️ **Important:**
> 1. **Avoid OneDrive folders.** On Windows 11, `Documents` and `Desktop` are often synced to OneDrive (a cloud icon appears beside them). OneDrive locks `.aux`, `.log` and `.pdf` files during sync, and compilation then fails with `I can't write on file` or `Permission denied`. `C:\Thesis` sits outside OneDrive.
> 2. **Avoid spaces and special characters** in folder names (e.g. `My Thesis (final)`). Use `My_Thesis` instead.
> 3. **Keep the path short.** Deeply nested folders can cross the old 260-character Windows path limit.

---

### 📥 2.1 Downloading the repository

Repository link:

```text
https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC
```

Choose any one of the two options below.

**Option A: Download ZIP (simplest)**

1. Open the repository link in any browser (Edge, Firefox, Chrome).
2. Click the green **`<> Code`** button.
3. Click **Download ZIP**.
4. The file lands in your **Downloads** folder as `Thesis_Template_UG_PG_BCREC-main.zip`.

**Option B: GitHub Desktop (free, open source; easy updates later)**

Use this option if you want to receive later improvements of the template with one click.

1. Download and install **GitHub Desktop** from its official site (`desktop.github.com`). Signing in to a GitHub account is optional for cloning a public repository.
2. Open GitHub Desktop → **File** → **Clone repository...**
3. Click the **URL** tab and paste the repository link.
4. Set **Local path** to `C:\Thesis\Thesis_Template_UG_PG_BCREC`.
5. Click **Clone**.

To fetch later updates of the template: open GitHub Desktop → click **Fetch origin** → then **Pull origin** (if updates exist).

> 💡 **Tip:** Keep the cloned folder as a clean reference copy. Write your own thesis in a separate copy: in File Explorer, right-click `Thesis_Template_UG_PG_BCREC` → **Copy**, then right-click inside `C:\Thesis` → **Paste**, and rename the copy to `My_Thesis`. A later **Pull origin** then never clashes with your chapters.

---

### 🗜️ 2.2 Unzipping the repository

Skip this step if you used GitHub Desktop (Option B).

1. Open your **Downloads** folder in File Explorer.
2. Right-click `Thesis_Template_UG_PG_BCREC-main.zip` → **Extract All...**
3. In the box **"Files will be extracted to this folder"**, click **Browse...** and select `C:\Thesis`.
4. Click **Extract**.

You now have `C:\Thesis\Thesis_Template_UG_PG_BCREC-main\`. Optionally right-click it → **Rename** → `My_Thesis`.

> ⚠️ **Important:** If you accept Explorer's suggested destination, Windows creates a nested folder: `Thesis_Template_UG_PG_BCREC-main\Thesis_Template_UG_PG_BCREC-main\`. Changing the destination to `C:\Thesis` (step 3) avoids it.
>
> Do **not** work directly inside the ZIP file by double-clicking it. Windows only shows a preview; LaTeX cannot compile from there.

**Check the key files**

Open the extracted folder. These four files must sit **together in the same folder**:

| File | Role |
|---|---|
| `main.tex` | The master file you compile |
| `thesis.cls` | The thesis class (page layout, title page, headings) |
| `mcode.sty` | MATLAB code highlighting |
| `references.bib` | Bibliography database |

If you see them inside one more sub-folder, open that sub-folder and work from there.

---

### 📦 2.3 Choose a TeX distribution

A TeX distribution is the engine that turns `.tex` files into a PDF. Two free, open-source options exist for Windows. **Install only one of them.**

| Point | MiKTeX (recommended) | TeX Live |
|---|---|---|
| Download size at start | Small (a few hundred MB) | Large (around 8 GB for full) |
| Install time | Around 10 minutes | 1 to 3 hours |
| Missing packages | Downloaded automatically on first compile (internet needed) | Already installed with the full scheme |
| GUI manager | MiKTeX Console | TeX Live Manager |
| Comes with an editor | ✅ TeXworks | ✅ TeXworks |
| Best for | Personal laptops with internet | Lab PCs without reliable internet |

Since your PC has internet, **MiKTeX is the easier choice**. It downloads only what this template uses, and only once. After the first successful compile, later compiles work even without internet.

> ⚠️ **Install only one distribution.** MiKTeX and TeX Live together on the same PC fight over which `pdflatex` runs. If one is already installed and you want the other, first remove the old one: **Settings** → **Apps** → **Installed apps** → find it → **⋯** → **Uninstall**.

---

### 🔵 2.4 Installing the TeX distribution

#### 2.4.1 MiKTeX (recommended)

**Step 1: Download**

1. Open the official MiKTeX download page (`miktex.org/download`) in the browser.
2. Under **Windows**, click **Download** for the installer (64-bit). The file name looks like `basic-miktex-<version>-x64.exe`.

**Step 2: Run the installer**

1. Double-click the downloaded file. If Windows SmartScreen warns, click **More info** → **Run anyway**.
2. **Copying Conditions:** tick **I accept the MiKTeX copying conditions** → **Next**.
3. **Shared Installation:** choose **Install MiKTeX only for me** (recommended, no admin rights needed) → **Next**.
4. **Installation Directory:** keep the default → **Next**.
5. **Settings:**
   - **Preferred paper:** choose **A4**.
   - **Install missing packages on-the-fly:** choose **Yes**.
   - Click **Next**.
6. **Review** → **Start**. Wait until it finishes.
7. On the last page, tick **Check for updates now** → **Close**.

**Step 3: Update MiKTeX (do not skip)**

1. Open **Start** → type `MiKTeX Console` → open it.
2. If asked, choose **Stay in user mode**.
3. Click **Updates** (left panel) → **Check for updates** → **Update now**. Wait, then close and reopen MiKTeX Console.

**Step 4: Confirm the automatic package setting**

1. In MiKTeX Console, click **Settings** (left panel) → **General** tab.
2. Under **"You can choose whether missing packages are to be installed on-the-fly"**, select **Always install missing packages on-the-fly**.

> ⚠️ Without this setting, MiKTeX opens a pop-up for every missing package. Some editors (VS Code in particular) compile in the background, the pop-up never appears, and the build simply fails.

**Step 5: Pre-install the key packages (optional, saves time on first compile)**

1. In MiKTeX Console, click **Packages** (left panel).
2. Type a package name in the search box, select it in the list, and click the **+** button.
3. Repeat for: `fourier`, `algorithm2e`, `algorithmicx`, `algorithms`, `siunitx`, `ieeetran`, `tabu`.

If you skip this step, MiKTeX fetches these automatically during the first compile. The first compile then takes a few extra minutes; that is normal.

#### 2.4.2 TeX Live (alternative, for PCs without reliable internet)

1. Open this link in the browser. It downloads `install-tl-windows.exe`:

    ```text
    https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe
    ```

2. Right-click `install-tl-windows.exe` → **Run as administrator**. If SmartScreen warns, click **More info** → **Run anyway**.
3. Choose **Install** → **Next**.
4. Click **Advanced** to see all options.
5. **Scheme:** keep **full scheme** (recommended for this template).
6. **Installation root:** keep the default `C:\texlive\<year>`.
7. Tick **Install for all users** and **Add to PATH**.
8. Click **Install**. Keep the laptop on charger and switch off sleep until it finishes.
9. Restart Windows once after installation.

TeX Live installs **TeX Live Manager** (Start → type `TeX Live Manager`) for later package updates, and **TeXworks** as an editor.

---

### ✍️ 2.5 Installing an editor

An editor is where you write and compile. Choose any one.

| Editor | Cost | Best for | Install |
|---|---|---|---|
| **TeXworks** | Free, open source | Absolute beginners; already installed with MiKTeX/TeX Live | Nothing to install |
| **TeXstudio** | Free, open source | Most students; menus, spell check, auto-complete, PDF preview | Separate installer |
| **VS Code + LaTeX Workshop** | Free, open source | Users who also write Python/MATLAB code in VS Code | Separate installer |

**TeXworks:** Start → type `TeXworks` → open. Nothing more to do.

**TeXstudio:**

1. Open the official TeXstudio site (`texstudio.org`) → **Download** → choose the **Windows** installer (64-bit).
2. Run the installer → **Next** → **Install** → **Finish**.
3. Open TeXstudio. It detects MiKTeX or TeX Live automatically.

**VS Code + LaTeX Workshop:**

1. Install **Visual Studio Code** from its official site (`code.visualstudio.com`).
2. Open VS Code → click the **Extensions** icon on the left bar (four squares) → search `LaTeX Workshop` (by James Yu) → **Install**.

**Recommended PDF viewer: SumatraPDF (free, open source)**

Adobe Acrobat Reader **locks** `main.pdf` while it is open, so the next compile fails with `I can't write on file 'main.pdf'`. SumatraPDF refreshes the PDF automatically instead. Download it from its official site (`sumatrapdfreader.org`) and install. TeXworks, TeXstudio and VS Code also have their own built-in PDF preview, so an external viewer is optional.

---

### 📁 2.6 Adding `mcode.sty` and other local style files

`mcode.sty` is not available through MiKTeX Console or TeX Live Manager. `thesis.cls` loads it with the options `[framed,numbered,autolinebreaks,useliterate]`, so the TeX engine must find it by itself. The engine looks for a `.sty` file in this order:

1. The current folder (the folder holding `main.tex`)
2. The personal TeX folder (`C:\Users\<username>\texmf`)
3. The TeX installation itself

Choose any one of the three methods below.

**Method 1: Keep it in the project folder (default, recommended)**

The repository already places `mcode.sty` beside `main.tex`. Open the project folder in File Explorer and confirm that `mcode.sty` is visible.

If the file is missing:

1. Open the repository link in the browser.
2. Click on `mcode.sty` in the file list.
3. Click the **Download raw file** icon (top right of the file view).
4. In **Downloads**, right-click `mcode.sty` → **Cut**, then open your project folder (where `main.tex` sits) → right-click → **Paste**.

> 📌 **Note:** Some browsers save the file as `mcode.sty.txt`. With **File name extensions** turned on (Section 2.0), you will see it. Right-click → **Rename** → remove `.txt` → press **Enter** → click **Yes** on the warning.

**Method 2: Install once in the personal TeX folder (all your projects)**

Useful when you maintain several theses or reports with MATLAB listings. Install it once, and every project on your account finds it.

1. Open File Explorer → go to `C:\Users\<your_username>`.
2. Create these folders one inside the other: `texmf` → `tex` → `latex` → `mcode`.
   Final path: `C:\Users\<your_username>\texmf\tex\latex\mcode`
3. Copy `mcode.sty` into the `mcode` folder.

*For MiKTeX:* MiKTeX does not search this folder by default. Register it once:

1. Open **MiKTeX Console** → **Settings** → **Directories** tab.
2. Click **+** → select `C:\Users\<your_username>\texmf` → **Select Folder**.
3. Click **Tasks** (top menu) → **Refresh file name database**.

*For TeX Live:* `C:\Users\<your_username>\texmf` is searched automatically. If the file is still not found, open **TeX Live Manager** → **Actions** → **Regenerate filename database**.

**Method 3: Install for all users (lab or shared PCs)**

*MiKTeX:*

1. Open **Start** → type `MiKTeX Console` → right-click → **Run as administrator**, then choose **Switch to administrator mode** if asked.
2. Create a folder such as `C:\texmf-local\tex\latex\mcode` and copy `mcode.sty` into it.
3. **Settings** → **Directories** → **+** → add `C:\texmf-local`.
4. **Tasks** → **Refresh file name database**.

*TeX Live:*

1. Copy `mcode.sty` into `C:\texlive\texmf-local\tex\latex\mcode\` (create the `tex\latex\mcode` folders if needed).
2. Open **TeX Live Manager** as administrator → **Actions** → **Regenerate filename database**.

**The same rule applies to other local files**

Any `.sty`, `.cls` or `.bst` file that is not available through the package manager follows the same three methods. For Method 2, use the matching folder:

| File type | Folder inside `C:\Users\<your_username>\texmf` |
|---|---|
| `.sty` (style package) | `tex\latex\<name>\` |
| `.cls` (document class) | `tex\latex\<name>\` |
| `.bst` (bibliography style) | `bibtex\bst\<name>\` |
| `.bib` (shared reference database) | `bibtex\bib\<name>\` |

After copying, refresh the file name database as described above.

> ⚠️ **Important:**
> 1. Keep `thesis.cls` in the project folder. It is specific to this template and you may edit it (margins, title page, headers). A copy elsewhere gets silently overridden by the project-folder copy, which causes confusion during debugging.
> 2. If two copies of `mcode.sty` exist (project folder and personal folder), the project-folder copy wins. Keep only one copy to avoid version mismatch.
> 3. Do not substitute `matlab-prettifier`. It is a different package with a different command set, and the options used in `thesis.cls` are specific to Knorn's `mcode`.
> 4. `mcode.sty` is BSD-licensed (credited in `README.md` and `LICENSE`). Keep its licence header intact when copying it anywhere.

---

### ⚡ 2.7 Compiling the thesis (GUI)

**Golden rule:** always compile **`main.tex`**, never a chapter file. Chapter files are pulled in by `main.tex`.

A thesis with a bibliography needs four passes: **pdfLaTeX → BibTeX → pdfLaTeX → pdfLaTeX**. The first pass collects citations, BibTeX builds the reference list, and the last two passes fix the citation numbers, table of contents, and cross-references. Each editor below handles this in its own way.

> 📌 **First compile with MiKTeX:** a pop-up titled **"Package Installation"** may appear for each missing package. Untick **"Always show this dialog before installing packages"** and click **Install**. With the setting from Section 2.4.1 (Step 4), this happens silently. The first compile may take 3 to 10 minutes; later compiles take seconds.

#### 2.7.1 TeXworks

1. Open TeXworks → **File** → **Open** → select `main.tex` in your project folder.
2. In the toolbar at the top left, open the drop-down beside the green ▶ **Typeset** button and choose **pdfLaTeX+MakeIndex+BibTeX**.
3. Click the green ▶ **Typeset** button (or press `Ctrl + T`).
4. The PDF opens in a second window. Click ▶ once more if the references or table of contents still show `??`.

If **pdfLaTeX+MakeIndex+BibTeX** is not in the list (some TeX Live versions), do it manually: choose **pdfLaTeX** → ▶, then **BibTeX** → ▶, then **pdfLaTeX** → ▶ twice.

> 💡 If you open a chapter file in TeXworks and press ▶, it fails. Always switch back to the `main.tex` window before typesetting.

#### 2.7.2 TeXstudio

**One-time setup:**

1. **Options** → **Configure TeXstudio...** → **Build** (left list).
2. **Default Compiler:** `PdfLaTeX`.
3. **Default Bibliography Tool:** `BibTeX`.
4. **PDF Viewer:** `Internal PDF Viewer (embedded)` (recommended).
5. Click **OK**.

**Every time:**

1. **File** → **Open** → `main.tex`.
2. **Options** → **Root Document** → **Set Current Document As Explicit Root Document**.
   Now TeXstudio compiles `main.tex` even while you edit a chapter file.
3. Click **Tools** → **Compile** (pdfLaTeX pass).
4. Click **Tools** → **Bibliography** (BibTeX pass).
5. Click **Tools** → **Compile** twice more.
6. Click **Tools** → **View** to see the PDF.

After the first full build, the green double-arrow **Build & View** button on the toolbar is usually enough for small edits. Repeat steps 3 to 5 whenever you add a new citation.

The shortcut key for each action is shown beside its name in the **Tools** menu.

#### 2.7.3 VS Code + LaTeX Workshop

**One-time setup (create the settings file):**

1. Open VS Code → **File** → **Open Folder...** → select your project folder (the one holding `main.tex`).
2. In the **Explorer** panel on the left, click the **New Folder** icon → name it `.vscode`.
3. Right-click `.vscode` → **New File** → name it `settings.json`.
4. Paste the following text into `settings.json` and save (`Ctrl + S`):

```json
{
  "latex-workshop.latex.outDir": "%DIR%/OUTPUT",
  "latex-workshop.latex.recipes": [
    {
      "name": "pdflatex -> bibtex -> pdflatex*2",
      "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
    }
  ],
  "latex-workshop.latex.tools": [
    {
      "name": "pdflatex",
      "command": "pdflatex",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-output-directory=%DIR%/OUTPUT",
        "%DOC%"
      ]
    },
    {
      "name": "bibtex",
      "command": "bibtex",
      "args": ["%DIR%/OUTPUT/%DOCFILE%"]
    }
  ]
}
```

This is the same file as in the Linux guide, so one repository works on both OS. It keeps all generated files inside an `OUTPUT` folder.

**Every time:**

1. Open `main.tex` from the Explorer panel.
2. Click the **TeX** icon on the left bar → **Build LaTeX project** → **Recipe: pdflatex -> bibtex -> pdflatex\*2**.
3. Click **View LaTeX PDF** → **View in VS Code tab** to see the result.

#### 2.7.4 Where is my PDF?

| Editor | Location of `main.pdf` |
|---|---|
| TeXworks | Beside `main.tex` in the project folder |
| TeXstudio | Beside `main.tex` in the project folder |
| VS Code (with the settings above) | Inside the `OUTPUT` folder |

TeXworks and TeXstudio leave helper files (`.aux`, `.log`, `.toc`, `.bbl` and others) beside `main.tex`. That is normal. To clear them: TeXworks → **File** → **Remove Aux Files...**; TeXstudio → **Tools** → **Clean Auxiliary Files...**

---

### 🛠️ 2.8 Troubleshooting

Read the error in the editor's **Messages / Log** pane (TeXworks: bottom panel; TeXstudio: **Messages** and **Log** tabs; VS Code: **Problems** tab). The table below covers the common ones.

| Symptom | Likely cause | Fix (GUI) |
|---|---|---|
| Editor says `pdflatex` not found, or TeXstudio shows "Could not start the command" | TeX distribution not installed, or installed after the editor was opened | Close the editor and reopen it; if still failing, restart Windows. In TeXstudio, check **Options → Configure TeXstudio → Commands** |
| `I can't write on file 'main.pdf'` | PDF open in Adobe Reader, or OneDrive syncing the folder | Close the PDF; use the built-in preview or SumatraPDF (Section 2.5); move the project out of OneDrive (Section 2.0) |
| `Permission denied` on `.aux` / `.log` files | OneDrive or antivirus scanning the folder | Work from `C:\Thesis`; if antivirus still interferes, ask your IT team to exclude `C:\Thesis` from real-time scanning |
| `File 'mcode.sty' not found` | File missing, in the wrong folder, or saved as `mcode.sty.txt` | Follow Section 2.6; do not swap in `matlab-prettifier` |
| `File 'thesis.cls' not found` | Compiling from the wrong folder, a nested folder after Extract All, or straight from inside the ZIP | Open `main.tex` from the folder that holds all four key files (Section 2.2) |
| `File 'fourier.sty' not found` (or any other `.sty`) | Package not installed yet | MiKTeX: **MiKTeX Console → Packages** → search the name → **+**. TeX Live: **TeX Live Manager** → search → **Install** |
| MiKTeX build stops without a clear error in VS Code | Package pop-up blocked in background mode | Set **Always install missing packages on-the-fly** (Section 2.4.1, Step 4) |
| References show `[?]` and table of contents is empty | BibTeX pass or final pdfLaTeX passes not run | Run the full sequence: pdfLaTeX → BibTeX → pdfLaTeX → pdfLaTeX (Section 2.7) |
| `I found no \citation commands` (from BibTeX) | BibTeX run before the first pdfLaTeX pass | Run pdfLaTeX first, then BibTeX. `main.tex` already has `\nocite{*}`, so every entry in `references.bib` appears regardless of in-text citations |
| `I couldn't open style file IEEEtran.bst` | `ieeetran` package not installed | Install `ieeetran` through MiKTeX Console or TeX Live Manager |
| `Command \algorithmic already defined` or similar algorithm-package clash | `algorithm2e` and `algorithmicx`/`algpseudocode`/`algorithm` loaded together (thesis.cls lines 89-94) | This is a known combination in the class file. If your TeX build errors on it, open `thesis.cls` in the editor and temporarily comment out (put `%` at the start of the line) either the `algorithm2e`+`algcompatible` pair or the `algorithm`/`algorithmicx`/`algpseudocode` trio, matching whichever algorithm syntax your chapters actually use |
| Figures with `.eps` fail | EPS conversion helper missing | Open the figure in any image tool and save it as `.pdf` or `.png` (recommended for pdfLaTeX) |
| `tabu`/`longtabu`-related errors after an update | `tabu` is unmaintained upstream (last release 2019) and occasionally breaks with newer `xcolor`/`caption` releases | Usually cosmetic; if a build actually fails, rebuild the offending table with `tabularx` + `booktabs` instead of `tabu`/`Longtabu` |
| Strange errors after many edits | Stale helper files from an earlier failed run | Clean auxiliary files (Section 2.7.4) and compile again from the start |
| First compile is very slow | MiKTeX downloading packages | Normal, only once. Keep the internet on and wait |

---

### 🔍 2.9 Worked example: a required file is missing (GUI)

**Case A: `! LaTeX Error: File 'siunitx.sty' not found.`**

*MiKTeX:*

1. Open **MiKTeX Console** → **Packages**.
2. Type `siunitx` in the search box.
3. Select it → click **+** → wait for the install to finish.
4. Recompile `main.tex`.

*TeX Live:*

1. Open **TeX Live Manager** (as administrator).
2. Click **Load default repository** (if the package list is empty).
3. Search `siunitx` → select it → **Install marked**.
4. Recompile `main.tex`.

*Manual fallback (institute firewall blocks the package manager):*

1. On any PC with open internet, download `siunitx.tds.zip` from the CTAN page of `siunitx` (`ctan.org/pkg/siunitx`). Copy it to your PC by pen drive if needed.
2. Right-click `siunitx.tds.zip` → **Extract All...** → set the destination to `C:\Users\<your_username>\texmf` → **Extract**.
3. MiKTeX: register this folder once (Section 2.6, Method 2) and click **Tasks → Refresh file name database**. TeX Live: **TeX Live Manager → Actions → Regenerate filename database**.
4. Recompile `main.tex`.

`.tds.zip` files on CTAN are pre-arranged in the folder layout TeX expects, so extracting one straight into the personal `texmf` folder works for effectively any missing package, not just `siunitx`.

**Case B: `! I couldn't open style file IEEEtran.bst` (from BibTeX)**

1. Install the package `ieeetran` through MiKTeX Console or TeX Live Manager, exactly as in Case A.
2. *Manual fallback:* download `IEEEtran.bst` alone from the CTAN page of `ieeetran` (`ctan.org/pkg/ieeetran`), and copy it either beside `main.tex` (simplest) or into `C:\Users\<your_username>\texmf\bibtex\bst\local\` followed by a file name database refresh.
3. Run the full sequence again: pdfLaTeX → BibTeX → pdfLaTeX → pdfLaTeX. BibTeX needs a fresh `.aux` file from the first pdfLaTeX pass.

---
---

## 💻 Appendix A: Command-line instructions (optional, for advanced users)

Everything in Sections 2.0 to 2.9 can also be done from the terminal. Open **Windows Terminal** with **PowerShell** (right-click **Start** → **Terminal**). Commands marked **(Admin)** need **Terminal (Admin)**.

> 📌 **PowerShell notes:**
> 1. Type `curl.exe`, not `curl`. Plain `curl` may map to `Invoke-WebRequest` with different options.
> 2. Type `where.exe`, not `where`. Plain `where` is an alias of `Where-Object`.
> 3. After installing any program, close and reopen the Terminal so the new `PATH` loads.

### A.1 Working folder (Section 2.0)

```powershell
New-Item -ItemType Directory -Force -Path "C:\Thesis"
```

### A.2 Download with git (Section 2.1)

```powershell
winget install --id Git.Git -e

cd C:\Thesis
git clone https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC.git
cd Thesis_Template_UG_PG_BCREC

# Later updates
git pull

# Separate working copy for your own thesis
Copy-Item -Recurse C:\Thesis\Thesis_Template_UG_PG_BCREC C:\Thesis\My_Thesis
```

### A.3 Download the ZIP (Section 2.1)

```powershell
Invoke-WebRequest `
  -Uri "https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC/archive/refs/heads/main.zip" `
  -OutFile "$env:USERPROFILE\Downloads\Thesis_Template_UG_PG_BCREC-main.zip"

# or
curl.exe -L -o "$env:USERPROFILE\Downloads\Thesis_Template_UG_PG_BCREC-main.zip" `
  https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC/archive/refs/heads/main.zip
```

If the default branch of the repository is `master` instead of `main`, replace `main` with `master` in the URL and in the file name.

### A.4 Unzip and check the key files (Section 2.2)

```powershell
Expand-Archive `
  -Path "$env:USERPROFILE\Downloads\Thesis_Template_UG_PG_BCREC-main.zip" `
  -DestinationPath "C:\Thesis" -Force

Rename-Item C:\Thesis\Thesis_Template_UG_PG_BCREC-main My_Thesis
cd C:\Thesis\My_Thesis

Get-ChildItem -Path C:\Thesis -Recurse -Depth 3 -Filter main.tex | Select-Object FullName
Get-ChildItem main.tex, thesis.cls, mcode.sty, references.bib
```

### A.5 Install software with winget (Sections 2.4 and 2.5)

```powershell
winget install --id MiKTeX.MiKTeX -e                   # MiKTeX
winget install --id Microsoft.VisualStudioCode -e      # VS Code
winget install --id SumatraPDF.SumatraPDF -e           # PDF viewer
winget install --id 7zip.7zip -e                       # 7-Zip (optional)
winget install --id StrawberryPerl.StrawberryPerl -e   # Perl, needed by latexmk under MiKTeX

# Confirm exact IDs before installing these two
winget search texstudio
winget search ghostscript
winget install --id <id_shown_by_search> -e

# LaTeX Workshop extension for VS Code
code --install-extension James-Yu.latex-workshop
```

### A.6 MiKTeX package commands (Section 2.4.1)

```powershell
miktex packages update
miktex packages install fourier
miktex packages install algorithm2e
miktex packages install algorithmicx
miktex packages install algorithms
miktex packages install siunitx
miktex packages install ieeetran
miktex packages install tabu
miktex packages install latexmk
```

### A.7 TeX Live installer and targeted install (Section 2.4.2)

```powershell
Invoke-WebRequest `
  -Uri "https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe" `
  -OutFile "$env:USERPROFILE\Downloads\install-tl-windows.exe"
```

If you chose the **medium scheme** instead of full, add the collections this template needs **(Admin)**:

```powershell
tlmgr update --self
tlmgr install `
  collection-latexextra `
  collection-fontsextra `
  collection-fontsrecommended `
  collection-mathscience `
  collection-bibtexextra `
  collection-publishers `
  collection-pstricks `
  collection-plaingeneric `
  collection-binextra `
  latexmk
```

| TeX Live collection | Provides (relevant to this template) |
|---|---|
| `collection-latexextra` | `mathtools`, `siunitx`, `adjustbox`, `changepage`, `enumitem`, `tabu`, `soul`, `ragged2e` |
| `collection-fontsextra` | `fourier` (Utopia-based Type 1 fonts) |
| `collection-fontsrecommended` | Base fonts, `textcomp` |
| `collection-mathscience` | `algorithm2e`, `algorithmicx`, `algpseudocode`, `algorithm` |
| `collection-bibtexextra` | `natbib` extras, additional `.bst` styles |
| `collection-publishers` | `IEEEtran.bst` |
| `collection-pstricks` | `pstricks` family |
| `collection-plaingeneric` | Low-level generic macros several packages depend on |
| `collection-binextra` | `latexmk`, `epstopdf` and helper programs |

### A.8 `mcode.sty` commands (Section 2.6)

**Method 1, recover a missing file:**

```powershell
git checkout -- mcode.sty                                            # git clone only
Get-ChildItem -Path C:\Thesis -Recurse -Filter mcode.sty | Select-Object FullName
Copy-Item "<path_printed_above>" .\
Move-Item "$env:USERPROFILE\Downloads\mcode.sty" C:\Thesis\My_Thesis\
```

**Method 2, personal folder:**

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\texmf\tex\latex\mcode"
Copy-Item .\mcode.sty "$env:USERPROFILE\texmf\tex\latex\mcode\"

texhash "$env:USERPROFILE\texmf"           # TeX Live
initexmf --update-fndb                     # MiKTeX (after registering the folder in MiKTeX Console)

kpsewhich -var-value TEXMFHOME             # TeX Live: shows the personal folder
cd $env:USERPROFILE
kpsewhich mcode.sty                        # verify from outside the project folder
```

**Method 3, all users (Admin):**

```powershell
# TeX Live
$LOCAL = kpsewhich -var-value TEXMFLOCAL
New-Item -ItemType Directory -Force -Path "$LOCAL\tex\latex\mcode"
Copy-Item .\mcode.sty "$LOCAL\tex\latex\mcode\"
mktexlsr "$LOCAL"

# MiKTeX
initexmf --admin --update-fndb

kpsewhich mcode.sty
```

### A.9 Verify the install

```powershell
where.exe pdflatex          # must print ONE path only
pdflatex --version
bibtex --version
latexmk --version
kpsewhich fourier.sty
kpsewhich algorithm2e.sty
kpsewhich siunitx.sty
kpsewhich IEEEtran.bst
```

Two paths from `where.exe pdflatex` mean two distributions are installed (Section 2.3). An empty `kpsewhich` line means that package is missing; with MiKTeX, it may simply not be downloaded yet.

### A.10 Compile from the terminal (Section 2.7)

**PowerShell:**

```powershell
cd C:\Thesis\My_Thesis
New-Item -ItemType Directory -Force -Path OUTPUT | Out-Null
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
Move-Item main.pdf OUTPUT\ -Force
Get-ChildItem -Path *.aux, *.bbl, *.blg, *.log, *.toc, *.lof, *.lot -ErrorAction SilentlyContinue |
  Move-Item -Destination OUTPUT\ -Force
```

**Command Prompt (`cmd.exe`):**

```bat
cd /d C:\Thesis\My_Thesis
if not exist OUTPUT mkdir OUTPUT
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
move /Y main.pdf OUTPUT\
for %f in (*.aux *.bbl *.blg *.log *.toc *.lof *.lot) do move /Y "%f" OUTPUT\ >nul
```

**latexmk** (automatically re-runs pdflatex/bibtex only as many times as needed; MiKTeX needs Strawberry Perl from A.5):

```powershell
latexmk -pdf -output-directory=OUTPUT main.tex       # single build
latexmk -pdf -pvc -output-directory=OUTPUT main.tex  # rebuild on every save; Ctrl+C stops
```

### A.11 Worked example commands (Section 2.9)

**Case A, `siunitx.sty` missing:**

```powershell
kpsewhich siunitx.sty                     # empty result confirms it is missing

tlmgr install siunitx                     # TeX Live (Admin)
miktex packages install siunitx           # MiKTeX

# Manual fallback
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\texmf"
Invoke-WebRequest `
  -Uri "https://mirrors.ctan.org/install/macros/latex/contrib/siunitx.tds.zip" `
  -OutFile "$env:USERPROFILE\Downloads\siunitx.tds.zip"
Expand-Archive -Path "$env:USERPROFILE\Downloads\siunitx.tds.zip" `
  -DestinationPath "$env:USERPROFILE\texmf" -Force
texhash "$env:USERPROFILE\texmf"          # TeX Live
initexmf --update-fndb                    # MiKTeX
kpsewhich siunitx.sty
```

**Case B, `IEEEtran.bst` missing:**

```powershell
kpsewhich IEEEtran.bst

tlmgr install ieeetran                    # TeX Live (Admin)
miktex packages install ieeetran          # MiKTeX

# Manual fallback
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\texmf\bibtex\bst\local"
Invoke-WebRequest `
  -Uri "https://mirrors.ctan.org/macros/latex/contrib/IEEEtran/bibtex/IEEEtran.bst" `
  -OutFile "$env:USERPROFILE\texmf\bibtex\bst\local\IEEEtran.bst"
texhash "$env:USERPROFILE\texmf"          # TeX Live
initexmf --update-fndb                    # MiKTeX
kpsewhich IEEEtran.bst

# Rerun the full sequence
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

---

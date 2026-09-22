# ⚙️ Linux OS: Offline Compilation Guide: Thesis_Template_UG_PG_BCREC

A step-by-step, OS-wise setup guide for compiling this thesis template locally, without depending on Overleaf's free-tier compile queue.

With Regards
Kingsuk Majumdar, PhD(EE)

---

## 📋 Why go offline

Overleaf's free plan throttles compile time and queues long documents. A thesis with many chapters, MATLAB-highlighted listings, and multiple algorithm floats crosses that limit fast. A local TeX Live install removes the queue entirely and compiles in seconds once cached.

---

## 🧩 What this template actually needs

`thesis.cls` pulls in roughly 40 packages on top of the base `book` class. Three deserve special attention because a generic "install LaTeX" tutorial will not mention them:

1. **`fourier`** — needs the Adobe Utopia / Type 1 font set, not part of a minimal TeX install.
2. **`algorithm2e` (with `algcompatible`) loaded alongside `algorithmicx`/`algpseudocode`/`algorithm`** — two competing algorithm-typesetting families in the same class file. Both are present because different chapters historically used different syntax. Keep this in mind if you ever see a `\algorithmic already defined`-type error; see the Troubleshooting table.
3. **`mcode.sty`** — the MATLAB code-highlighting package by Florian Knorn. It is **not distributed through TeX Live or CTAN**; it ships inside this template's repository itself. If it is missing from your working folder, no distro package will fix it.

---

## 🐧 1. Linux

### 📦 Prerequisites checklist (all distros)

| Requirement | Purpose |
|---|---|
| TeX Live (2023 or newer) | Core engine + packages |
| `pdflatex` binary | Compiler specified in `main.tex` |
| `bibtex` binary | Bibliography engine (`\bibliographystyle{IEEEtran}`) |
| Ghostscript | Needed by `epstopdf` if any figure is `.eps` |
| Perl | Required by several TeX Live helper scripts |
| `latexmk` (recommended, not mandatory) | Automates the pdflatex → bibtex → pdflatex → pdflatex loop |
| `mcode.sty` present in the project root | Already included in the repo; verify it is not missing after a fresh clone/download |

---

### 🟠 1.1 Ubuntu / Debian-based (apt)

**Fastest route (recommended for a first-time setup):**

```bash
sudo apt update
sudo apt install texlive-full latexmk ghostscript
```

`texlive-full` is large (around 5-7 GB) but removes essentially all "package not found" errors for a document this feature-rich. If disk space is tight, use the targeted install instead.

**Targeted install (smaller footprint):**

```bash
sudo apt update
sudo apt install \
  texlive-latex-base \
  texlive-latex-recommended \
  texlive-latex-extra \
  texlive-fonts-recommended \
  texlive-fonts-extra \
  texlive-science \
  texlive-bibtex-extra \
  texlive-publishers \
  texlive-pstricks \
  texlive-plain-generic \
  latexmk \
  ghostscript \
  perl
```

| Distro package | Provides (relevant to this template) |
|---|---|
| `texlive-latex-base` | Core LaTeX, `book` class |
| `texlive-latex-recommended` | `setspace`, `titlesec`, `array`, `tools` bundle |
| `texlive-latex-extra` | `mathtools`, `siunitx`, `adjustbox`, `changepage`, `enumitem`, `tabu`, `soul`, `ragged2e` |
| `texlive-fonts-extra` | `fourier` (Utopia-based Type 1 fonts) |
| `texlive-fonts-recommended` | Base fonts, `textcomp` |
| `texlive-science` | `algorithm2e`, `algorithmicx`, `algpseudocode`, `algorithm` |
| `texlive-bibtex-extra` | `natbib` extras, additional `.bst` styles |
| `texlive-publishers` | `IEEEtran.bst` (used by `\bibliographystyle{IEEEtran}`) |
| `texlive-pstricks` | `pstricks` family, pulled in transitively by some figure packages |
| `texlive-plain-generic` | Low-level generic macros several packages depend on |

---

### 🔵 1.2 Fedora (dnf)

**Fastest route:**

```bash
sudo dnf install texlive-scheme-full latexmk ghostscript
```

**Targeted install:**

```bash
sudo dnf install \
  texlive-collection-latex \
  texlive-collection-latexrecommended \
  texlive-collection-latexextra \
  texlive-collection-fontsextra \
  texlive-collection-fontsrecommended \
  texlive-collection-mathscience \
  texlive-collection-bibtexextra \
  texlive-collection-publishers \
  texlive-collection-pstricks \
  texlive-collection-plaingeneric \
  latexmk \
  ghostscript \
  perl
```

Fedora also packages most individual CTAN packages separately (`texlive-fourier`, `texlive-siunitx`, `texlive-algorithm2e`, `texlive-mcode` does **not** exist for the reason above). If `dnf install <collection-name>` reports "no match," run:

```bash
dnf search texlive- | grep -i <keyword>
```

to locate the exact package name for that release, since collection names occasionally get versioned suffixes.

---

### 🟣 1.3 Arch Linux / Manjaro (pacman)

Arch restructured its TeX Live packaging; the old single `texlive-most` meta-package no longer exists. The `texlive` group now contains 22 sub-packages.

**Fastest route (installs the entire group, closest equivalent to the old `texlive-most` + `texlive-latexextra`):**

```bash
sudo pacman -Syu
sudo pacman -S texlive latexmk ghostscript
```

`texlive` here is a **group**, not a single package; pacman will prompt you to select individual members or press Enter to install all of them. Selecting all is the safest choice for this template.

**Targeted install:**

```bash
sudo pacman -Syu
sudo pacman -S \
  texlive-basic \
  texlive-latex \
  texlive-latexrecommended \
  texlive-latexextra \
  texlive-fontsextra \
  texlive-fontsrecommended \
  texlive-fontutils \
  texlive-binextra \
  texlive-mathscience \
  texlive-bibtexextra \
  texlive-publishers \
  texlive-pstricks \
  texlive-plaingeneric \
  latexmk \
  ghostscript \
  perl
```

| Arch package | Provides (relevant to this template) |
|---|---|
| `texlive-basic` | Core engine, base LaTeX |
| `texlive-latex` | `book` class support |
| `texlive-latexrecommended` | `setspace`, `titlesec`, `tools` bundle |
| `texlive-latexextra` | `mathtools`, `siunitx`, `adjustbox`, `enumitem`, `tabu`, `soul`, `ragged2e`, `microtype` |
| `texlive-fontsextra` | `fourier` |
| `texlive-mathscience` | `algorithm2e`, `algorithmicx`, `algpseudocode`, `algorithm` |
| `texlive-bibtexextra` | `natbib` extras |
| `texlive-publishers` | `IEEEtran.bst` |
| `texlive-binextra` | Helper binaries (`epstopdf` script, etc.) |

This is what README.md's original `pacman -S texlive-most texlive-bibtexextra` instruction now maps to, since `texlive-most` was retired.

---

### 📁 1.4 Placing `mcode.sty`

Confirm it is sitting next to `main.tex`:

```bash
ls mcode.sty
```

If it is missing (e.g. you only downloaded the `.tex`/`.cls` files and not the full repo), pull it from the same GitHub repository (`Thesis_Template_UG_PG_BCREC`), or from the original MATLAB File Exchange listing by Florian Knorn (BSD license, as credited in `README.md` and `LICENSE`). Do not substitute `matlab-prettifier`, a different CTAN package with a different command set; `thesis.cls` calls `mcode` with `[framed,numbered,autolinebreaks,useliterate]`, options specific to Knorn's package.

---

### ✅ 1.5 Verifying the install

```bash
pdflatex --version
bibtex --version
kpsewhich fourier.sty
kpsewhich algorithm2e.sty
kpsewhich siunitx.sty
kpsewhich IEEEtran.bst
```

Each `kpsewhich` call should print a path. An empty line means that package is still missing; re-check the tables above for which distro package provides it.

For `mcode.sty`, since it lives in the project folder rather than the TeX Live tree:

```bash
ls -la mcode.sty
```

---

### ⚡ 1.6 Compiling

**Manual sequence** (same as README.md, given here for completeness):

```bash
cd /path/to/ug-thesis-template/
mkdir -p OUTPUT
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
mv main.pdf OUTPUT/
mv *.aux *.bbl *.blg *.log *.toc *.lof *.lot OUTPUT/ 2>/dev/null || true
```

**One-line alternative with `latexmk`** (automatically re-runs pdflatex/bibtex as many times as needed, and only as many times as needed, which is faster on later edits):

```bash
latexmk -pdf -output-directory=OUTPUT main.tex
```

To keep re-compiling on save while editing:

```bash
latexmk -pdf -pvc -output-directory=OUTPUT main.tex
```

`Ctrl+C` stops the watch loop.

---

### 🖥️ 1.7 Optional: VS Code offline setup

Since the compile itself needs the LaTeX Workshop extension talking to the local `pdflatex`/`bibtex`/`latexmk` binaries installed above, not Overleaf, add this to `.vscode/settings.json` in the project folder:

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

This keeps generated files inside `OUTPUT/`, matching the directory layout in `README.md`.

---

### 🛠️ 1.8 Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| `File 'fourier.sty' not found` | Missing font-extra collection | Install `texlive-fonts-extra` (apt) / `texlive-collection-fontsextra` (dnf) / `texlive-fontsextra` (pacman) |
| `File 'mcode.sty' not found` | File not copied from repo, or wrong directory | Confirm it sits beside `main.tex`; do not swap in `matlab-prettifier` |
| `Command \algorithmic already defined` or similar algorithm-package clash | `algorithm2e` and `algorithmicx`/`algpseudocode`/`algorithm` loaded together (thesis.cls lines 89-94) | This is a known combination in the class file. If your TeX Live build errors on it, temporarily comment out either the `algorithm2e`+`algcompatible` pair or the `algorithm`/`algorithmicx`/`algpseudocode` trio, matching whichever algorithm syntax your chapters actually use |
| `! LaTeX Error: File 'IEEEtran.bst' not found` | `texlive-publishers` (or equivalent) not installed | Install per the tables above |
| Figures with `.eps` fail during `pdflatex` | Ghostscript missing, `epstopdf` cannot convert | `sudo apt/dnf/pacman install ghostscript` |
| `bibtex` reports "I found no \citation commands" | Ran `bibtex` before the first `pdflatex` pass, or `\nocite{*}` missing | Always run `pdflatex` once before `bibtex`; `main.tex` already has `\nocite{*}` so every entry in `references.bib` gets pulled in regardless of in-text citations |
| Compile is slow even locally | Full four-pass manual sequence run every time | Switch to `latexmk`, which skips unnecessary passes automatically |
| `tabu`/`longtabu`-related errors after a system TeX Live update | `tabu` is unmaintained upstream (last release 2019) and occasionally breaks with newer `xcolor`/`caption` releases | Usually cosmetic; if a build actually fails, isolate the offending table and rebuild it with `tabularx` + `booktabs` instead of `tabu`/`Longtabu` |

---

### 🔍 1.9 Worked example: a required file is missing

Two concrete cases, since these are the most common blockers with this class file.

**Case A: `! LaTeX Error: File 'siunitx.sty' not found.`**

Step 1, confirm it is really missing:

```bash
kpsewhich siunitx.sty
```

An empty result confirms it. Step 2, install the package that provides it:

```bash
# Ubuntu/Debian
sudo apt install texlive-latex-extra

# Fedora
sudo dnf install texlive-collection-latexextra

# Arch/Manjaro
sudo pacman -S texlive-latexextra
```

Step 3, recompile. If your package manager genuinely has no matching package (a stripped-down repo mirror, an offline machine, a custom container image), fall back to a manual local install instead of chasing package names:

```bash
mkdir -p ~/texmf/tex/latex/local
cd /tmp
wget https://mirrors.ctan.org/install/macros/latex/contrib/siunitx.tds.zip
unzip -o siunitx.tds.zip -d ~/texmf
texhash ~/texmf      # or: mktexlsr
kpsewhich siunitx.sty   # should now print a path under ~/texmf
```

`.tds.zip` files on CTAN are pre-built, TeX-Directory-Structure archives; unzipping one straight into `~/texmf/` and refreshing the filename database (`texhash`/`mktexlsr`) works for effectively any missing LaTeX package, not just `siunitx`, without needing to compile a `.dtx` source file by hand.

**Case B: `! I couldn't open style file IEEEtran.bst` (from `bibtex`, not `pdflatex`)**

Step 1, confirm:

```bash
kpsewhich IEEEtran.bst
```

Step 2, install:

```bash
# Ubuntu/Debian
sudo apt install texlive-publishers

# Fedora
sudo dnf install texlive-collection-publishers

# Arch/Manjaro
sudo pacman -S texlive-publishers
```

Step 3, manual fallback if needed. `IEEEtran.bst` is a single file, so this is simpler than the TDS-zip route:

```bash
mkdir -p ~/texmf/bibtex/bst/local
wget https://mirrors.ctan.org/macros/latex/contrib/IEEEtran/bibtex/IEEEtran.bst -O ~/texmf/bibtex/bst/local/IEEEtran.bst
texhash ~/texmf
kpsewhich IEEEtran.bst
```

Step 4, either way, rerun the full sequence from the top since `bibtex` needs a fresh `.aux` file:

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

---

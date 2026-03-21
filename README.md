# 🎓 LaTeX Thesis Template for Dr. B. C. Roy Engineering College

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![LaTeX](https://img.shields.io/badge/LaTeX-008080?style=flat&logo=latex&logoColor=white)](https://www.latex-project.org/)
[![Version](https://img.shields.io/badge/Version-V4.1-blue.svg)](https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC)
[![Overleaf](https://img.shields.io/badge/Overleaf-47A141?style=flat&logo=overleaf&logoColor=white)](https://www.overleaf.com/)
[![YouTube](https://img.shields.io/badge/YouTube-FFFFFF?style=flat&logo=YouTube&logoColor=red)](https://www.youtube.com/@LearnWithKingsuk)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=GitHub&logoColor=white)](https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC)


A professional, feature-rich LaTeX template for undergraduate and postgraduate thesis at **Dr. B. C. Roy Engineering College, Durgapur**. This template provides automated formatting, multi-student support, and institutional compliance while maintaining academic presentation standards.

Note: 7th Sem PWEE781 implementation sample has been added [📄 Instruction](./Thesis_Template_BCREC_KM/7thSemSample)

With Regards
Kingsuk Majumdar, PhD(EE)

# Zenodo DOI Badge & Citation
```text
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19153458.svg)](https://doi.org/10.5281/zenodo.19153458)
```
## IEEE Citation (for users to copy)

K. Majumdar, "Thesis_Template_UG_PG_BCREC: Professional LaTeX Thesis and Project Report Template for BCREC (UG/PG)," version 1.0.0, Zenodo, Mar. 2026. doi: 10.5281/zenodo.19153458. [Online]. Available: https://doi.org/10.5281/zenodo.19153458

---

## BibTeX Citation ()

```bibtex
@misc{majumdar2026bcrec,
  author       = {K. Majumdar},
  title        = {{Thesis\_Template\_UG\_PG\_BCREC: Professional LaTeX
                   Thesis and Project Report Template for BCREC (UG/PG)}},
  year         = {2026},
  month        = mar,
  version      = {1.0.0},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.19153458},
  howpublished = {\url{https://doi.org/10.5281/zenodo.19153458}}
}
```
---

## 🌟 Key Features

- 📄 **Professional A4 formatting** optimized for academic thesis
- 👥 **Multi-student support** (1-3 students for UG, 1 for PG) with automatic conditional rendering
- 🖼️ **Integrated photo handling** for author biographies with wrapfigure layout
- 🎨 **Customizable headers, footers, and title pages**
- 📝 **Justified text without hyphenation** for clean appearance
- 💻 **MATLAB code highlighting** via mcode.sty package
- 🔧 **Comprehensive error handling** and wrapper commands
- 📚 **Complete frontmatter and backmatter** templates
- 🏷️ **Short title support** for footers
- 📖 **Automatic bibliography** and abbreviations handling
- 🔄 **Degree-specific configurations** (UG/PG requirements)

---

## 📁 Directory Structure

```
ug-thesis-template/
|-- main.tex                    # Main document file (User Input Section)
|-- thesis.cls                  # LaTeX class file (Formatting Engine)
|-- references.bib              # Bibliography database
|-- mcode.sty                   # MATLAB code highlighting package
|-- README.md                   # Documentation file
|-- LICENSE.lic                 # License information
|-- Frontmatter/
|   |-- Declaration.tex         # Student declaration page (Don't Change it) 
|   |-- Certificate.tex         # Supervisor approval certificate (Don't Change it)
|   |-- Acknowledgment.tex      # Acknowledgments section
|   |-- Abstract.tex           # Abstract and keywords
|   +-- Acronyms.tex           # List of abbreviations and nomenclature
|-- Chapters/
|   |-- Chapter01_Introduction.tex    # Introduction chapter (MUST BE)
|   |-- Chapter02_Literature.tex     # Literature review (MUST BE)
|   |-- Chapter02_Table.tex          # Table examples
|   |-- Chapter03_Figure.tex         # Figure examples
|   |-- Chapter04_Math.tex           # Mathematical expressions
|   |-- Chapter03_Methodology.tex    # Research methodology
|   |-- Chapter04_Implementation.tex # Implementation details
|   |-- Chapter05_Results.tex        # Results and analysis (MUST BE)
|   +-- Chapter06_Conclusion.tex     # Conclusions and future work (MUST BE)
|-- Backmatter/
|   |-- PublicationsList.tex    # Publications by authors
|   +-- AuthorBio.tex          # Author biographies (Strictly PG/PhD only)
|-- Figures/
|   |-- college_logo.png       # Institutional logo (required)
|   |-- StudentOne_photo.jpg   # Student photograph
|   |-- StudentTwo_photo.jpg   # Student photograph
|   |-- StudentThree_photo.jpg # Student photograph
|   |-- Chapter01/             # Chapter-wise figure organization
|   |-- Chapter02/
|   |-- Chapter03/
|   |-- Chapter04/
|   |-- Chapter05/
|   +-- Chapter06/
+-- OUTPUT/                    # Generated output files (after compilation)
    |-- main.pdf              # Final thesis document
    |-- main.aux              # Auxiliary file
    |-- main.bbl              # Bibliography file
    |-- main.blg              # Bibliography log
    |-- main.log              # Compilation log
    |-- main.toc              # Table of contents
    |-- main.lof              # List of figures
    +-- main.lot              # List of tables
```

---

## 🚀 Quick Start

### 📦 Requirements

- **LaTeX Distribution**: TeX Live (Linux/Mac) or MiKTeX (Windows)
- **Compiler**: pdfLaTeX
- **OS**: Manjaro Linux (recommended) or any Linux distribution
- **Editor**: TeXstudio, VS Code, Overleaf, or any LaTeX editor

### 🔧 Installation (Manjaro Linux)

```bash
# Update system repositories
sudo pacman -Syu

# Install complete LaTeX distribution
sudo pacman -S texlive-most texlive-bibtexextra

# Alternative: Install full TeX Live distribution
sudo pacman -S texlive-core texlive-bin texlive-latexextra texlive-fontsextra
```

### 📥 Getting Started

1. **Clone the repository**
   ```bash
   git clone [Repository link will be added here]
   cd ug-thesis-template
   ```

2. **Configure your thesis** (Edit `main.tex` USER INPUT SECTION)
   ```latex
   %% Thesis Information
   \ThesisTitle{Your Thesis Title Here}
   \ShortTitle{Short Title for Footer}
   \Department{Department of Electrical Engineering}
   \NumberOfStudents{3}  % 1-3 for UG, 1 for PG
   
   %% Student Information
   \StudentOne{Your Name}
   \RollOne{18/EE/001}
   \EmailOne{your.email@bcrec.ac.in}
   ```

3. **Add your content**
   - Edit `Frontmatter/Abstract.tex`
   - Edit `Frontmatter/Acknowledgment.tex`
   - Edit chapter files in `Chapters/` directory
   - Add references to `references.bib`

4. **Add images**
   - Place `college_logo.png` in `Figures/` directory
   - Add student photos as specified in configuration
   - Organize chapter figures in respective subdirectories

---

## ⚡ Compilation

### 🖥️ Offline Compilation (Manjaro Linux)

```bash
# Navigate to project directory
cd /path/to/ug-thesis-template/

# Create output directory
mkdir -p OUTPUT

# Primary compilation sequence
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex

# Move generated files to OUTPUT directory
mv main.pdf OUTPUT/
mv *.aux *.bbl *.blg *.log *.toc *.lof *.lot OUTPUT/ 2>/dev/null || true
```

### 🌐 Online Compilation (Overleaf)

1. **Import Template**: Use the Overleaf template link: [Overleaf template link will be added here]
2. **Set Compiler**: Configure to use `pdfLaTeX` (2023/24 or above)
3. **Bibliography Engine**: Set to `bibtex`
4. **Collaborate**: Share with team members for multi-student projects

---

## 🎯 Degree-Specific Configurations

### 🎓 Undergraduate (UG) Requirements

- **Maximum Students**: 3 students per group
- **Author Biography**: Not included
- **Degree Type**: Bachelor of Technology (B.TECH)
- **Paper Code**: PWEE881

```latex
% Configuration for UG
\NumberOfStudents{3}
\DegreeType{Bachelor of Technology (B. TECH)}

% Exclude author biography
%\include{Backmatter/AuthorBio} % Commented out for UG
```

### 🎓 Postgraduate (PG) Requirements

- **Number of Students**: 1 student only
- **Author Biography**: Mandatory
- **Degree Type**: Master of Technology (M.TECH)

```latex
% Configuration for PG
\NumberOfStudents{1}
\DegreeType{Master of Technology (M. TECH)}

% Include author biography
\include{Backmatter/AuthorBio} % Required for PG
```

---

## 💡 Advanced Features

### 🖥️ MATLAB Code Highlighting

```latex
\begin{lstlisting}[style=Matlab-editor]
function result = myFunction(input)
    % Your MATLAB code here
    result = input * 2;
    fprintf('Result: %f\n', result);
end
\end{lstlisting}
```

### 📊 Figure and Table Management

```latex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.8\textwidth]{Chapter01/figure_name.png}
    \caption{Descriptive caption for the figure}
    \label{fig:figurelabel}
\end{figure}
```

### 🧮 Mathematical Expressions

```latex
\begin{equation}
    P = V \cdot I \cdot \cos(\phi)
    \label{eq:power}
\end{equation}
```

---

## 🛠️ Customization

### 🎨 Colors and Styling
Modify colors in `thesis.cls`:
```latex
\definecolor{darkblue}{rgb}{0.0, 0.0, 0.5}  % Custom colors
```

### 📐 Page Layout
Adjust geometry in `thesis.cls`:
```latex
\RequirePackage[
    a4paper,
    textwidth=15.5cm,
    textheight=23cm,
    left=3cm,
    right=2.5cm,
    % ... other settings
]{geometry}
```

---

## 🏆 Best Practices

### ✅ Recommended Practices

1. **Consistent Naming**: Use descriptive file names with chapter prefixes
2. **Image Resolution**: Maintain high-resolution images (300 DPI minimum)
3. **Backup Strategy**: Regular backup using version control systems
4. **Validation Testing**: Periodic compilation testing

### ❌ Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| Missing Packages | `sudo pacman -S texlive-most texlive-bibtexextra` |
| File Path Issues | Verify relative paths for figures and includes |
| Encoding Problems | Ensure UTF-8 encoding for all text files |
| Bibliography Errors | Check reference format and .bib file syntax |

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE.lic](LICENSE.lic) file for details.

```
MIT License

Copyright (c) 2025 Kingsuk Majumdar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

### 🔖 Third-Party Components

- **mcode.sty**: BSD License (Florian Knorn)
- **Standard LaTeX Packages**: Various open-source licenses
- **TeX Live Distribution**: TeX Users Group License

---

## 🤝 Contributing

We welcome contributions! Please see our contributing guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### 🐛 Reporting Issues

When reporting issues, please include:
- LaTeX distribution and version
- Operating system
- Complete error messages
- Minimal example that reproduces the issue

---

## 📞 Support & Contact

- **GitHub Issues**: [Create an issue](https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC) for bug reports and feature requests
- **Email**: kingsuk.majumdar@bcrec.ac.in
- **Institution**: Dr. B. C. Roy Engineering College, Durgapur
- **Department**: Electrical Engineering

---

## 🔗 Quick Links

| Platform             | Link                                                                          | Description            |
| -------------------- | ----------------------------------------------------------------------------- | ---------------------- |
| 🐙 **GitHub**        | [Source Code](https://github.com/KingsukMajumdar/Thesis_Template_UG_PG_BCREC) | Source code and issues |
| 📝 **Overleaf**      | [Overleaf template link will be added here]                                   | Online template        |
| 📚 **Documentation** | [Wiki/Docs]                                                                   | Detailed documentation |
| 🏫 **Institution**   | [BCREC Website](http://www.bcrec.ac.in/)                                      | College website        |

---

## 🙏 Acknowledgments

- **Dr. B. C. Roy Engineering College** for institutional support
- **Florian Knorn** for the excellent mcode.sty package
- **LaTeX Community** for comprehensive packages and documentation
- **Contributors** who helped improve this template

---

## 📈 Version History
- **V4.1** (2026-03-22): DoI has been added
- **V4.0** (2025-12-24): 7th Sem PWEE781 implementation sample has been added [📄 Instruction](./Thesis_Template_BCREC_KM/7thSemSample)
- **V4.0** (2025-09-14): College logo updated and certificate page space adjustment
- **V3.0** (2025-07-07): Enhanced with global variables and improved structure
- **V2.0** (2025-07-05): Added multi-student support and conditional rendering
- **V1.0** (2025-07-01): Initial release with basic functionality
---

<div align="center">

**⭐ Star this repository if it helped you! ⭐**

*Made with ❤️ for students of Dr. B. C. Roy Engineering College*


[![GitHub followers](https://img.shields.io/github/followers/KingsukMajumdar?style=social)](https://github.com/KingsukMajumdar)
[![YouTube Channel Subscribers](https://img.shields.io/youtube/channel/subscribers/UCo2Rho6ypq7IkxaKwByWQRA?style=social)](https://youtube.com/@LearnWithKingsuk)
</div>

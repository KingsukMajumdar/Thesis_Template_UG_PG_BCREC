# UG Thesis LaTeX Template for Dr. B. C. Roy Engineering College

A professional, feature-rich LaTeX template for undergraduate thesis at Dr. B. C. Roy Engineering College, Durgapur. This template provides automated formatting, multi-student support, and professional academic presentation.

## 🎓 Overview

This template is specifically designed for B.Tech thesis projects at Dr. B. C. Roy Engineering College and can be easily adapted for other institutions. It supports 1-5 students per project with automatic conditional rendering and professional formatting throughout.

## ✨ Key Features

- 📄 **Professional A4 formatting** optimized for academic thesis
- 👥 **Multi-student support** (1-5 students) with automatic conditional rendering
- 🖼️ **Integrated photo handling** for author biographies with wrapfigure layout
- 🎨 **Customizable headers, footers, and title pages**
- 🏛️ **Background logo support** for certificate pages
- 📝 **Justified text without hyphenation** for clean appearance
- 💻 **MATLAB code highlighting** via mcode.sty package
- 🔧 **Comprehensive error handling** and wrapper commands
- 📚 **Complete frontmatter and backmatter** templates
- 🏷️ **Short title support** for footers
- 📖 **Automatic bibliography** and abbreviations handling

## 📋 Requirements

### Software Requirements
- **LaTeX Distribution**: TeX Live (Linux/Mac) or MiKTeX (Windows)
- **Compiler**: pdfLaTeX
- **Editor**: Any LaTeX editor (TeXstudio, VS Code, Overleaf, etc.)

### Package Dependencies
All required packages are automatically loaded by the template:
- Standard LaTeX packages (amsmath, graphicx, hyperref, etc.)
- `mcode.sty` for MATLAB code highlighting
- `background` package for certificate page logo
- `wrapfig` package for author biography layout
- `ragged2e` for text justification

## 🚀 Quick Start

### 1. Download and Setup
```bash
# Clone or download the template
git clone [repository-url]
cd ug-thesis-template

# Ensure your LaTeX distribution is up to date
sudo apt update && sudo apt install texlive-full  # Ubuntu/Debian
```

### 2. Directory Structure
```
ug-thesis-template/
├── main.tex                    # Main document file (modify this)
├── ugthesis.cls                # Class file (don't modify)
├── LICENSE.lic                 # MIT License
├── README.md                   # This file
├── mcode.sty                   # MATLAB code highlighting (included)
├── references.bib              # Bibliography file
├── Frontmatter/
│   ├── Declaration.tex         # Student declaration
│   ├── Certificate.tex         # Approval certificate
│   ├── Acknowledgment.tex      # Acknowledgments
│   ├── Abstract.tex            # Abstract
│   └── Acronyms.tex           # List of abbreviations
├── Chapters/
│   ├── Chapter01_Introduction.tex
│   ├── Chapter02_Literature.tex
│   ├── Chapter03_Methodology.tex
│   ├── Chapter04_Implementation.tex
│   ├── Chapter05_Results.tex
│   └── Chapter06_Conclusion.tex
├── Backmatter/
│   ├── AuthorBio.tex          # About the authors
│   └── PublicationsList.tex   # Publications (if any)
└── Figures/
    ├── college_logo.png       # College logo (required)
    ├── StudentOne_photo.jpg   # Student photos
    ├── StudentTwo_photo.jpg
    └── ...
```

## 📝 Usage Instructions

### Step 1: Configure Your Thesis Information

Edit the **USER INPUT SECTION** in `main.tex`:

```latex
%% Thesis Information
\ThesisTitle{Your Thesis Title Here}
\ShortTitle{Short Title for Footer}  % Optional
\Department{Department of Electrical Engineering}
\College{Dr. B. C. Roy Engineering College}
\University{Maulana Abul Kalam Azad University of Technology, West Bengal}
\DegreeType{Bachelor of Technology (B. TECH)}
\ThesisYear{2025}
\ThesisMonth{May}

%% Project Information
\GroupNo{Group 01}
\PaperName{Final Year Project Stage-II}
\PaperCode{PWEE881}

%% Number of Students (1-5)
\NumberOfStudents{3}

%% Student Information
\StudentOne{Student Name 1}
\RollOne{18/EE/001}
\RegOne{184410301001}
\EmailOne{student1@bcrec.ac.in}
\PhotoOne{Figures/StudentOne_photo.jpg}

% Add similar information for other students...

%% Supervisor Information
\HasCoSupervisor{2}  % 1=supervisor only, 2=both supervisor and co-supervisor
\Supervisor{Professor Name}
\SupervisorDesignation{Professor}
\SupervisorEmail{supervisor@bcrec.ac.in}

%% Co-supervisor (if applicable)
\CoSupervisor{Co-Supervisor Name}
\CoSupervisorDesignation{Assistant Professor}

%% Head of Department
\HoD{Prof. HoD Name}
\HoDDesignation{Professor \& Head}
```

### Step 2: Add Your Content

1. **Abstract**: Edit `Frontmatter/Abstract.tex`
2. **Acknowledgment**: Edit `Frontmatter/Acknowledgment.tex`
3. **Chapters**: Edit files in `Chapters/` directory
4. **References**: Add references to `references.bib`
5. **Author Bios**: Automatic generation from student information

### Step 3: Add Images

1. **College Logo**: Place `college_logo.png` in `Figures/` directory
2. **Student Photos**: Place photos as specified in `\PhotoOne`, `\PhotoTwo`, etc.
3. **Chapter Figures**: Place in appropriate `Figures/ChapterXX/` subdirectories

### Step 4: Compile

```bash
# Standard compilation
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex

# Or use your LaTeX editor's build system
```

## 🎨 Customization

### Colors and Styling
Modify colors in `ugthesis.cls`:
```latex
\definecolor{darkblue}{rgb}{0.0, 0.0, 0.5}  % Custom colors
```

### Page Layout
Adjust geometry in `ugthesis.cls`:
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

### Background Logo Appearance
In `Certificate.tex`, modify:
```latex
\backgroundsetup{
    scale=1,
    opacity=0.15,          % Adjust transparency (0.05-0.3)
    angle=0,               % Rotation angle
    contents={
        \includegraphics[width=0.3\paperwidth]{college_logo.png}
    },
    position=current page.center
}
```

## 💡 Advanced Features

### MATLAB Code Inclusion
```latex
\begin{lstlisting}[style=Matlab-editor]
function result = myFunction(input)
    % Your MATLAB code here
    result = input * 2;
end
\end{lstlisting}
```

### Multiple Students Handling
The template automatically handles 1-5 students. Simply set:
```latex
\NumberOfStudents{3}  % Will show only first 3 students
```

### Short Title for Footer
```latex
\ThesisTitle{Very Long Thesis Title That Would Be Too Long For Footer}
\ShortTitle{Smart Grid System}  % Shows in footer instead
```

### Custom Chapter Headers
```latex
\chapter{Your Chapter Title}
\label{ch:yourchapter}
\justifying  % Ensures proper text justification
```

## 🔧 Troubleshooting

### Common Issues and Solutions

**Issue**: Compilation errors with `\@` commands
**Solution**: Ensure you're compiling `main.tex`, not individual files

**Issue**: College logo not showing
**Solution**: 
- Check file exists: `Figures/college_logo.png`
- Use PNG format for best results
- Ensure correct file permissions

**Issue**: Student photos not appearing
**Solution**:
- Verify file paths in `\PhotoOne`, `\PhotoTwo`, etc.
- Use JPG or PNG formats
- Check file names match exactly (case-sensitive on Linux)

**Issue**: "Draft" background appearing
**Solution**: Ensure background package is properly configured in `ugthesis.cls`

**Issue**: Text not justified
**Solution**: Add `\justifying` after chapter/section commands

**Issue**: Overfull/underfull hbox warnings
**Solution**: These are mostly cosmetic; adjust `\tolerance` and `\emergencystretch` if needed

### Package Installation
If packages are missing:
```bash
# Ubuntu/Debian
sudo apt install texlive-latex-extra texlive-fonts-recommended

# Or install specific packages via your LaTeX distribution's package manager
```

## 📄 Output Files

After successful compilation:
- `main.pdf` - Your complete thesis document
- `main.aux`, `main.bbl`, `main.blg` - Auxiliary files (can be deleted)
- `main.log` - Compilation log for debugging

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Reporting Issues
When reporting issues, please include:
- LaTeX distribution and version
- Operating system
- Minimal example that reproduces the issue
- Complete error messages

## 📜 License

This template is released under the MIT License. See `LICENSE.lic` for details.

### Third-Party Components
- `mcode.sty`: BSD License (Florian Knorn)
- Standard LaTeX packages: Various licenses

## 📧 Support

For questions and support:
- Create an issue in the repository
- Check existing issues for solutions
- Refer to LaTeX documentation for package-specific questions

## 🙏 Acknowledgments

- Dr. B. C. Roy Engineering College for institutional support
- Florian Knorn for the mcode.sty package
- LaTeX community for excellent packages and documentation

---

**Happy thesis writing! 🎓**

*Remember: This template handles the formatting so you can focus on your research content.*
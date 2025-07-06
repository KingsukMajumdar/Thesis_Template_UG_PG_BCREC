# 🚀 Quick Start Guide - 5 Minutes to Your First Thesis PDF

## Step 1: Download Template (30 seconds)
```bash
# Download and extract the template
# Place all files in your working directory
```

## Step 2: Add Required Images (1 minute)
1. Place your college logo as `Figures/college_logo.png`
2. Add student photos:
   - `Figures/StudentOne_photo.jpg`
   - `Figures/StudentTwo_photo.jpg`
   - `Figures/StudentThree_photo.jpg`

## Step 3: Edit main.tex - User Input Section (2 minutes)

Find this section and modify with your details:
```latex
%%%%%%%%%% USER INPUT SECTION - MODIFY THIS SECTION ONLY %%%%%%%%%%

%% Thesis Information
\ThesisTitle{Development of Smart Grid Monitoring System Using IoT and Machine Learning}
\ShortTitle{Smart Grid Monitoring System}
\Department{Department of Electrical Engineering}

%% Number of Students (1-5)
\NumberOfStudents{3}

%% Student Information
\StudentOne{Your Name}
\RollOne{18/EE/045}
\RegOne{184410301045}
\EmailOne{your.email@bcrec.ac.in}
\PhotoOne{Figures/StudentOne_photo.jpg}

\StudentTwo{Second Student Name}
\RollTwo{18/EE/052}
\RegTwo{184410301052}
\EmailTwo{student2.email@bcrec.ac.in}
\PhotoTwo{Figures/StudentTwo_photo.jpg}

\StudentThree{Third Student Name}
\RollThree{18/EE/063}
\RegThree{184410301063}
\EmailThree{student3.email@bcrec.ac.in}
\PhotoThree{Figures/StudentThree_photo.jpg}

%% Supervisor Information
\HasCoSupervisor{2} % 1=supervisor only, 2=both supervisor and co-supervisor
\Supervisor{Professor C.V. Raman}
\SupervisorDesignation{Professor}

\CoSupervisor{Acharya Prafulla Chandra Ray}
\CoSupervisorDesignation{Assistant Professor}

%% Head of Department
\HoD{Prof. Srinivasa Ramanujan}
\HoDDesignation{Professor \& Head}
```

## Step 4: Compile (1.5 minutes)
```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

## Step 5: Check Your PDF! (30 seconds)
Open `main.pdf` and verify:
- ✅ Title page with your information
- ✅ Certificate page with background logo
- ✅ Declaration with student signatures
- ✅ About the Authors with photos

## 🎯 That's It!

You now have a complete thesis template with:
- Professional formatting
- All frontmatter pages
- Student photos and information
- Background logo on certificate
- Ready for your content

## Next Steps:
1. Edit `Frontmatter/Abstract.tex` with your abstract
2. Edit `Frontmatter/Acknowledgment.tex` with your acknowledgments
3. Add your chapter content to `Chapters/Chapter01_Introduction.tex`, etc.
4. Add references to `references.bib`

## Need Help?
- See `README.md` for detailed instructions
- Check `LICENSE.lic` for license information
- Look at the compiled PDF for examples

**Happy thesis writing! 🎓**
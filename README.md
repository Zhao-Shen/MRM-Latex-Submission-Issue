# Submitting LaTeX to Magnetic Resonance in Medicine (MRM)

There are several issues when uploading LaTeX files to the **Magnetic Resonance in Medicine (MRM)** ScholarOne submission portal using the MRM-provided template ([link](https://onlinelibrary.wiley.com/journal/15222594/la_tex_class_file)). 

### Helpful Resources
- Frank's blog provides useful advice on submitting bare-bones LaTeX to MRM: [MRM Submission Tips](https://frankong.com/blog/mrm_tips.html).

Below are some specific findings related to the MRM-provided LaTeX template.

## Common Issues and Solutions
### 1. Outdated LaTeX Compiler
The LaTeX compiler used in ScholarOne is **very old** (last checked, it was from the early 2000s). It is not as up-to-date as Overleaf or arXiv. 

### 2. MRM Template Compilation Errors
The default LaTeX template provided by MRM **does not compile successfully** on the ScholarOne portal. The errors are often caused by:
- Additional calls to external files (e.g., images) in `MRM.cls` that prevent successful typesetting.

### 3. ORCID Logo Issue
The `orcid.eps` logo used in `MRM.cls` cannot be displayed correctly. To fix this:
1. Convert `orcid.eps` to `orcid.pdf`.
2. Modify in preamble
```latex
\makeatletter
\def\orcid#1{} % Disable original macro
\def\orcid#1{\href{#1}{\includegraphics{Orcidlogo.pdf}}} % Redefine
\makeatother
```

### 4. Citation Box Display Issues
If the citation box is not displayed correctly, comment out the related line in `MRM.cls`:
```latex
% \AtEndDocument{\ifappendixsec\else\printjnlcitation\fi}%
```

### 5. Removing the Footnote
If you would like to prevent the footnote and horizontal line from appearing at the bottom of the first/second page, add the following to the preamble:
```latex
\renewcommand{\footnoterule}{}  % Disable the footnote rule (line)
```

### 6. Fixing Abstract Text Box Issues
If the abstract text box contains a lot of text, it can lead to poor typesetting on the first or next page. Since the template treats author, address, funding information, and abstract as text boxes, you may need to **adjust the text box width** to avoid formatting issues.

Solution: Adjust Text Box Width
```latex
\newskip\abs@coli@hsize%
\newskip\abs@colii@hsize%
% \abs@coli@hsize55.5mm%
\abs@coli@hsize47.5mm%
\advance\abs@coli@hsize by -14.5pt%
% \abs@colii@hsize122.3mm%
\abs@colii@hsize130.3mm%
\advance\abs@colii@hsize by -14pt%
```

## Workarounds for Submission
If you are unable to resolve all issues immediately:
1. **Upload a compiled PDF** as the main file and submit all LaTeX source files as complementary files.
2. **Use a Word (.docx) file** if necessary, though it is not ideal for typesetting equations.

## Future Updates
MRM has announced plans to switch from ScholarOne to its own submission portal in **Spring 2025**, which may resolve these long-standing LaTeX submission issues.

---

### Contributions
If you encounter additional issues or find solutions, feel free to share them in the discussion. A modified `MRM.cls` file that incorporates the fixes mentioned above is included for reference.

Hope these steps help!

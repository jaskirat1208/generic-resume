
## Quickstart:
### Use the same template to create resume.
- Copy paste the three files in overleaf.
- Click Recompile. This should render you a PDF.
- To use the template, create a new particulars file called, say, particulars_username.tex with parameters same as particulars_dummy.tex.
- In the main.tex, line 9, update the input to \input{particular_username}.
- To use this design in another template, just copy paste the

### Choose a different template for the resume:
- The files utilities.tex and particulars.tex is a library for us. We'll use the two files as input to the new template resume we are going to create:
For example, refer the following line in main.tex:
```
  \section{Education}
  \resumeSubHeadingListStart
      \resumeSubheading{\csname College@School\endcsname}
      {\csname College@Start\endcsname \ -- \csname College@End\endcsname}
      {\csname College@Course\endcsname, \csname College@Stream\endcsname}{}
  \resumeSubHeadingListEnd
\section{Achievements}
\achievements
```
Definition of `College`:
```
% # Add education item here
\EducationTemplate{College}
{Jul 2001}{Jul 2001}{ABC college }
{Loren ipsum degree}
{Loren ipsum}
```

Definition of `EducationTemplate`
```
\usepackage{forarray}

\newcommand{\EducationTemplate}[6]
{
  \DefineArrayVar{#1}{@}
  {|}{Start|End|School|Course|Stream}
  {|}{{#2}|{#3}|{#4}|{#5}|{#6}}
}
```

From the above example, college has the following properties: `start, end, name, course, stream`. 
When you fill up the details of your college, you fill it up in separate braces, which separates each param individually, so, college.start can be identified by using the function \csname.

Once you define the above latex commands, all you have to do is declare every education in the following way:
```latex
\EducationTemplate{id}{StartDate}{EndDate}{schoolname}{Coursename}{Streamname}

% Prints StartDate 
\csname id@Start\endcsname

%PrintsEndDate
\csname id@End\endcsname

% Prints schoolname
\csname id@School\endcsname
```

# Best Practices for Simulation Software Validation / Physical Validation

Best Practices articles treating simulation software validation and
physical validation, to be submitted to LiveCoMS (Living Journal of
Computational Molecular
Science, [www.livecomsjournal.org](http://www.livecomsjournal.org)).
We plan to divide the topic into two largely independent documents:

1. Best practices for simulation software verification (developer best
   practices)
2. Best practices for physical validation of simulation results (user
   best practices)

The groundwork for these articles was laid during the Best Practices
workshop organized by Michael Shirts on behalf of MolSSI, held at NIST
on Aug 24-25, 2017, by Justin Gilmer, David Kofke, Pascal Merz, Conor
Parks, Julia Rice, Matthew Spellings, Terry Stouch, and William Swope
(authors in alphabetical order). _Please contact Pascal Merz if you
would like to contribute but have not been invited to do so._


### Best practices for simulation software verification 
*Scope:* The authors are experts on simulation software, not
necessarily on general software engineering. Consequently, the scope
of the article will not be general software engineering best practices
(version control, continuous integration, unit/system/regression
testing, ...), but the testing of _simulation_ software. We will
propose a hierarchically organized set of tests intended to help
developers to detect and localize errors in simulation software.

### Best practices for physical validation of simulation results
*Scope:* A checklist of methods to analyze whether simulation results
fulfill basic physical validity, including checks of the sampled
ensemble, the equipartition principle, conservation / drift of
constants, correlation times (to be extended).

## Author guidelines
A few suggestions to simplify collaboration on a LaTeX document:

* Use
  [issues](https://github.com/shirtsgroup/software-physical-validation/issues)
  and 
  [pull requests](https://github.com/shirtsgroup/software-physical-validation/pulls)
  to keep track of to-dos, discuss issues and review and comment text.
* We are using the template of LiveCoMS. Have a look at their sample
  files
  [[1](https://github.com/livecomsjournal/article_templates/blob/master/templates/sample-document.tex),
  [2](https://github.com/livecomsjournal/article_templates/blob/master/templates/livecoms-template-bestpractices.tex)]
  for examples on how to use the different environments.
* If you need to put text-related comments or to-dos directly in the
  LaTeX files, please use
  
  ```
  \comm{Your initials}{Your comment here}
  ```
  
  and
  
  ```
  \todo{Your todo here}
  ```
  
  These commands will be compiled into the document and highlighted in
  color. They are easy to find and filter out for release versions.
* Make ample use of additional files included into `main.tex` via

  ```
  \include{file.tex}
  ```

  Please use at least one file per section (or even subsection, if
  sections get very large). This should help keeping the main file
  tidy and will make merging significantly easier.
* Use the `siunitx` package included in the LiveCoMS template to
  typeset units.

## License

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)  
The content of this repository is licensed under a
[Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

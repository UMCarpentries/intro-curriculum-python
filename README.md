# U-M Carpentries Python Curriculum

[![website](https://github.com/UMCarpentries/intro-curriculum-python/actions/workflows/website.yml/badge.svg)](https://github.com/UMCarpentries/intro-curriculum-python/actions/workflows/website.yml)
<!-- [![check-links](https://github.com/UMCarpentries/intro-curriculum-python/actions/workflows/check-links.yml/badge.svg)](https://github.com/UMCarpentries/intro-curriculum-python/actions/workflows/check-links.yml) -->
[![License](https://img.shields.io/badge/License-MIT%2BCC--BY-blue)](LICENSE.md)

This is the custom curriculum developed by the University of Michigan Software
Carpentry instance.
It is in the `beta` stage of development; we are continuing to host workshops to
gather feedback and polish the curriculum.

The rendered website can be found at [https://umcarpentries.org/intro-curriculum-python/](https://umcarpentries.org/intro-curriculum-python/).

## Repo Layout

1. Top level files

    - `index.md` - The home page.
    - `reference.md` - Reference for learners.
    - `setup.md` - Setup instructions for learners.
    - `AUTHORS` - Plain text list of the lesson authors.
    - `CITATION` - Plain text citation instructions.

1. Lesson episodes

    - `_episodes/` - Source files in Markdown. Episode order is determined by the filename. Currently the lessons are directly written in Markdown inside this folder. 
    <!-- - `_episodes_rmd/` - Source files in R Markdown. A lesson should be written in one or the other markdown style, not both. To convert R Markdown files to markdown episodes, run `make lesson-rmd`. -->
    
    <!-- Run `make lesson-check` at any time -->
    <!-- to check that the lesson files follow the formatting rules -->

1. Figures are stored in `fig/`, data sets in `data/`, source notebooks in `_episodes_ipynb/`, and miscellaneous files in `files/`.

1. `_extras/`

    - `about.md` - General notes about the curriculum.
    - `discussion.md` - For learners who would like to learn more.
    - `guide.md` - The instructor's guide for the curriculum.
    - `bonus_exercises.md` - Bonus exercises for learners who want to practice more.

<!-- ## Rendering R Markdown episodes

To render all episodes in `_episodes_rmd/`, run:

```
make site
```

This will create markdown files in `_episodes/` for GitHub Pages.

To render just one episode, e.g. `_episodes_rmd/01-r-plotting.Rmd`, run:

```
make _episodes/01-r-plotting.md
``` -->

## Workshop Schedule

For a typical 2-day workshop. Can be modified for different workshop formats.

|   | Title | Source File |
|---|-------|-------------|
| **Day 1** |   |
| 09:00 | Welcome to the workshop | `_episodes/00-intro.md` |
| 09:15 | **Python for Plotting** | `_episodes/01-python-plotting.md` |
| 10:30 | Break |  |
| 10:45 | **Python for Plotting (Continued)** | continuation of `01-python-plotting.md` |
| 12:00 | Lunch Break |  |
| 13:00 | **The Unix Shell** | `_episodes/02-unix-shell.md` |
| 14:15 | Break |  |
| 14:30 | **Intro to git & GitHub** | `_episodes/03-intro-git-github.md` |
| 16:30 | Wrap-up Day 1 |  |
| **Day 2** |   |
| 09:00 | **Python for Data Analysis** | `_episodes/04-python-data-analysis.md` |
| 10:30 | Break |  |
| 10:45 | **R for Data Analysis (Continued)** | continuation of `04-python-data-analysis.md` |
| 12:00 | Lunch Break |  |
| 13:00 | **Jupyter Notebook and Markdown** | `_episodes/05-markdown.md` |
| 14:30 | Break |  |
| 14:45 | **Jupyter Notebook and Markdown (Continued)** | at end of `05-markdown.md` |
| 16:00 | Conclusions & Wrap-up |  `_episodes/06-conclusion.md` |
| 16:15 | Exit Survey |   |
| 16:30 | End | |

## Helpful links

<!-- - How to format lesson files: https://carpentries.github.io/lesson-example/04-formatting/index.html -->
<!-- - Additional instructions for formatting R Markdown lesson files: https://carpentries.github.io/lesson-example/05-rmarkdown-example/index.html -->
- The Carpentries lesson example repo (source files for the above two links): https://github.com/carpentries/lesson-example
- Already-established SWC curricula: https://github.com/swcarpentry/swcarpentry#lesson-repositories
- Lesson style guide: https://carpentries.github.io/lesson-example/06-style-guide/index.html
- Guide to contributing with git and GitHub: https://github.com/dmgt/swc_github_flow/blob/master/for_novice_contributors.md#

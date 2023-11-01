---
title: Setup
---

## Pre-workshop setup steps

1. Install the following software (<a href="#install">all instructions are below</a>).
    - Zoom for online workshop (make sure you have the latest version)
    - A Unix shell (e.g. bash, zsh)
    - [git](https://git-scm.com/)
    - [Anaconda](https://docs.anaconda.org/free/anaconda/install/) which is a Python distribution, package manager, and comes with popular tools such as JupyterLab.
1. Create a [GitHub](https://github.com/) account if you do not already have one. You'll need to know the email associated with your account during the git lesson of the workshop.
1. After you have installed everything above, download [un-report.zip](https://github.com/UMSWC/curriculum/raw/gh-pages/files/un-report.zip). You'll need the files included during the workshop.
    1. Move `un-report.zip` to your Desktop and unzip it (usually double-clicking it will work).
    1. Start up **Anaconda Navigator**, in the box with **JupyterLab** click on the "Launch" button. In the left file browser, go to your `Desktop/`, `un-report/` folder and select the file `check_setup.ipynb` to open it in JupyterLab.
    1. In the top menu, click on **Kernel > Restart Kernel and Run All Cells**` to run the script. This script will make sure that everything is installed and setup correctly. You should see output printed at the bottom.
    1. Take a screenshot of your JupyterLab window and send the screenshot to the lead instructor. If everything worked, they'll give you the Zoom meeting ID for the workshop. Otherwise, they'll help you get everything setup correctly before giving you the Zoom ID.

If at any point you get stuck or run into problems, please don't hesitate to ask us for help!

<h2 id="install">Software Installation Instructions</h2>

{% include install_instructions/videoconferencing.html %}

{% include swc/setup.html %}

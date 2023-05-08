---
source: Rmd
title: "Python for Plotting"
teaching: 120
exercises: 30
questions:
- "What are Python and JupyterLab?"
- "How do I read data into Python?"
- "How can I use Python to create and save professional data visualizations?"
objectives:
- "To become oriented with Python and JupyterLab."
- "To be able to read in data from csv files."
- "To create plots with both discrete and continuous variables."
- "To understand transforming and plotting data using the **seaborn** library."
- "To be able to modify a plot's color, theme, and axis labels."
- "To be able to save plots to a local directory."
keypoints:
- "Python is a free general purpose programming language used by many for reproducible data analysis."
- "Use Python library **pandas**' `read_csv` function to read tabular data."
- "Use Python library **seaborn** to create and save data visualizations."

---

### Contents

1. [Introduction to Python and JupyterLab](#introduction-to-python-and-jupyterlab)
1. [Loading and reviewing data](#loading-and-reviewing-data)
1. [Understanding commands](#understanding-commands)
1. [Creating our first plot](#creating-our-first-plot)
1. [Plotting for data exploration](#plotting-for-data-exploration)
    + [Importing datasets](#importing-datasets)
    + [Discrete plots](#discrete-plots)
    + [Layers](#layers)
    + [Color vs. Fill](#color-vs-fill)
    + [Univariate plots](#univariate-plots)
    + [Plot themes](#plot-themes)
    + [Facets](#facets)
    + [Saving plots](#saving-plots)
1. [Bonus](#bonus)
    + [Creating complex plots](#creating-complex-plots)
      + [Animated plots](#animated-plots)
      + [Map plots](#map-plots)
1. [Glossary of terms](#glossary-of-terms)

> ## Bonus: why learn to program?
> Share why you're interested in learning how to code.
> > ## Solution:
> > There are lots of different reasons, including to perform data analysis and generate figures. I'm sure you have more specific reasons for why you'd like to learn!
> {: .solution}
{: .challenge}

# Introduction to Python and JupyterLab
_[Back to top](#contents)_

In this session we will be testing the hypothesis that a country's life expectancy is related to the total value of its finished goods and services, also known as the Gross Domestic Product (GDP).
To test this hypothesis, we'll need two things: data and a platform to analyze the data.

You already [downloaded the data]({{ page.root }}/setup.html). But what platform will we use to analyze the data? We have many options!

We could try to use a spreadsheet program like Microsoft Excel or Google sheets that have limited access, less flexibility, and don't easily allow for things that are critical to ["reproducible" research](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003285), like easily sharing the steps used to explore and make changes to the original data.

Instead, we'll use a programming language to test our hypothesis. Today we will use Python, but we could have also used R for the same reasons we chose Python (and we teach workshops for both languages). Both Python and R are freely available, the instructions you use to do the analysis are easily shared, and by using reproducible practices, it's straightforward to add more data or to change settings like colors or the size of a plotting symbol.

> ## But why Python and not R?
> There's no great reason.
> Although there are subtle differences between the languages, it's ultimately a matter of personal preference. Both are powerful and popular languages that have very well developed and welcoming communities of scientists that use them. As you learn more about Python, you may find things that are annoying in Python that aren't so annoying in R; the same could be said of learning R. If the community you work in uses Python, then you're in the right place.
>
{: .solution}

To run Python, all you really need is the Python program, which is available for computers running the Windows, Mac OS X, or Linux operating systems. 
In this workshop, we will use Anaconda, a popular Python distribution bundled with other popular tools (e.g., common Python libraries).
We will use JupyterLab (which come with Anaconda) as the integrated development environment (IDE) for writing and running code, managing projects, getting help, and much more. 

> Bonus Exercise: Can you think of a reason you might not want to use JupyterLab?
>
> > ## Solution:
> > On some high-performance computer systems (e.g. Amazon Web Services) you typically can't get a display like JupyterLab to open. If you're at the University of Michigan and have access to Great Lakes, then you might want to learn more about [resources](https://arc.umich.edu/open-ondemand/#document-4) to run JupyterLab on Great Lakes.
> {: .solution}
{: .challenge}

To get started, we'll spend a little time getting familiar with the JupyterLab environment and setting it up to suit your tastes. When you start JupyterLab, you'll have three panels.

<img src="{{ page.root }}/fig/r-plotting/initial_rstudio.png" width="700"/>

On the left you'll have a panel with three tabs - Console, Terminal, and Jobs. The Console tab is what running Python from the command line looks like. This is where you can enter Python code. Try typing in `2+2` at the prompt (>). In the upper right panel are tabs indicating the Environment, History, and a few other things. If you click on the History tab, you'll see the command you ran at the Python prompt.

<img src="{{ page.root }}/fig/r-plotting/history.png" width="700"/>

In the lower right panel are tabs for Files, Plots, Packages, Help, and Viewer. You used the Packages tab to install tidyverse.

We'll spend more time in each of these tabs as we go through the workshop, so we won't spend a lot of time discussing them now.

You might want to alter the appearance of your JupyterLab window. The default appearance has a white background with black text. If you go to the Tools menu at the top of your screen, you'll see a "Global options" menu at the bottom of the drop down; select that.

<img src="{{ page.root }}/fig/r-plotting/global_options.png" width="600"/>

From there you will see the ability to alter numerous things about JupyterLab. Under the Appearances tab you can select the theme you like most. As you can see there's a lot in Global options that you can set to improve your experience in JupyterLab. Most of these settings are a matter of personal preference.

However, you can update settings to help you to insure the reproducibility of your code. In the General tab, none of the selectors in the Python Sessions, Workspace, and History should be selected. In addition, the toggle next to "Save workspace to .PythonData on exit" should be set to never. These setting will help ensure that things you worked on previously don't carry over between sessions.

<img src="{{ page.root }}/fig/r-plotting/general_options.png" width="600"/>

Let's get going on our analysis!

One of the helpful features in JupyterLab is the ability to create a project. A project is a special directory that contains all of the code and data that you will need to run an analysis.

At the top of your screen you'll see the "File" menu. Select that menu and then the menu for "New Project...".

<img src="{{ page.root }}/fig/r-plotting/new_project_menu.png" width="600"/>

When the smaller window opens, select "Existing Directory" and then the "Browse" button in the next window.

<img src="{{ page.root }}/fig/r-plotting/existing_directory.png" width="600"/>

<img src="{{ page.root }}/fig/r-plotting/browse.png" width="600"/>

Navigate to the directory that contains your code and data from the setup instructions and click the "Open" button.

<img src="{{ page.root }}/fig/r-plotting/navigate_to_project.png" width="600"/>

Then click the "Create Project" button.

<img src="{{ page.root }}/fig/r-plotting/create_project.png" width="600"/>

Did you notice anything change?

In the lower right corner of your JupyterLab session, you should notice that your
Files tab is now your project directory. You'll also see a file called
un-report.Rproj in that directory.

From now on, you should start JupyterLab by double clicking on that file. This will
make sure you are in the correct directory when you run your analysis.

<img src="{{ page.root }}/fig/r-plotting/files_with_rproj.png" width="600"/>

We'd like to create a file where we can keep track of our Python code.

Back in the "File" menu, you'll see the first option is "New File". Selecting "New File" opens another menu to the right and the first option is "Python Script". Select "Python Script".

Now we have a fourth panel in the upper left corner of JupyterLab that includes an **Editor** tab with an untitled Python Script. Let's save this file as `gdp_population.R` in our project directory.

We will be entering Python code into the **Editor** tab to run in our **Console** panel.

On line 1 of `gdp_population.R`, type `2+2`.

With your cursor on the line with the `2+2`, click the button that says <kbd>Run</kbd>. You should be able to see that `2+2` was run in the Console.

As you write more code, you can highlight multiple lines and then click <kbd>Run</kbd> to run all of the lines you have selected.

Let's delete the line with 2+2 and replace it with `library(tidyverse)`.

Go ahead and run that line in the **Console** by clicking the <kbd>Run</kbd> button on the top right of the **Editor** tab and choosing <kbd>Run Selected Lines</kbd>. This loads a set of useful functions and sample data that makes it easier for us to do complex analyses and create professional visualizations in R.


~~~
import numpy as np
import pandas as pd
~~~
{: .language-python}


> ## What's with all those messages???
>
> When you loaded the `tidyverse` package, you probably got a message like the
> one we got above. Don't panic! These messages are just giving you more
> information about what happened when you loaded `tidyverse`. The `tidyverse` is
> actually a collection of several different packages, so the first section of the
> message tells us what packages were installed when we loaded `tidyverse` (these
> include `ggplot2`, which we'll be using a lot in this lesson, and `dyplr`, which
> you'll be introduced to tomorrow in the 
> [R for Data Analysis lesson]({{ page.root }}/05-r-markdown)).
>
> The second section of messages gives a list of "conflicts." Sometimes, the
> same function name will be used in two different packages, and R has to decide
> which function to use. For example, our message says that:
>
> ~~~
> dplyr::filter() masks stats::filter()
> ~~~
> {: .output}
>
> This means that two different packages (`dyplr` from `tidyverse` and `stats`
> from base R) have a function named `filter()`. By default, R uses the function
> that was most recently loaded, so if we try using the `filter()` function after
> loading `tidyverse`, we will be using the `filter()` function > from `dplyr()`.
>
{: .callout}


> ## Pro-tip
>
> Those of us that use **pandas** on a daily basis use cheat sheets to help us remember how to use various **pandas** functions. If you haven't already, print out the PDF versions of the cheat sheets that were in the setup instructions.
>
> You can also find them in JupyterLab by going to the "Help" menu and selecting "Cheat Sheets". The two that will be most helpful in this workshop are "Data Visualization with ggplot2", "Data Transformation with dplyr", "R Markdown Cheat Sheet", and "R Markdown Reference Guide".
>
> For things that aren't on the cheat sheets, [Google is your best friend]({{ page.root }}/06-conclusion/). Even expert coders use Google when they're stuck or trying something new!
>
{: .testimonial}

---

# Loading and reviewing data
_[Back to top](#contents)_

We will import a subsetted file from the gapminder dataset called `gapminder_1997.csv`. There are many ways to import data into Python but for your first plot we will use JupyterLab's file menu to import and display this data. As we move through this process, JupyterLab will translate these *point and click* commands into code for us.

In JupyterLab select "File" > "Import Dataset" > "From Text (readr)".

<img src="{{ page.root }}/fig/r-plotting/import_data.png" width="600"/>

The file is located in the main directory, click the "Browse" button and select the file named `gapminder_1997.csv`. A preview of the data will appear in the window. You can see there are a lot of Import Options listed, but R has chosen the correct defaults for this particular file.

<img src="{{ page.root }}/fig/r-plotting/import_data_file.png" width="600"/>

We can see in that box that our data will be imported with the Name: "gapminder_1997". Also note that this screen will show you all the code that will be run when you import your data in the lower right "Code Preview". Since everything looks good, click the "Import" button to bring your data into R.

After you've imported your data, a table will open in a new tab in the top left corner of JupyterLab. This is a quick way to browse your data to make sure everything looks like it has been imported correctly. To review the data, click on the new tab.

We see that our data has 5 columns (variables).

Each row contains life expectancy ("lifeExp"), the total population ("pop"), and the per capita gross domestic product ("gdpPercap") for a given country ("country").

There is also a column that says which continent each country is in ("continent"). Note that both North America and South America are combined into one category called "Americas".

After we've reviewed the data, you'll want to make sure to click the tab in the upper left to return to your `gdp_population.R` file so we can start writing some code.

Now look in the **Environment** tab in the upper right corner of JupyterLab. Here you will see a list of all the objects you've created or imported during your R session. You will now see `gapminder_1997` listed here as well.

Finally, take a look at the **Console** at the bottom left part of the JupyterLab screen. Here you will see the commands that were run for you to import your data in addition to associated metadata and warnings.

> ## Data objects
> There are many different ways to store data in R. Most objects have a table-like structure with rows and columns. We will refer to these objects generally as "data objects". If you've used R before, you many be used to calling them "data.frames". Functions from the "tidyverse" such as `read_csv` work with objects called "tibbles", which are a specialized kind of "data.frame." Another common way to store data is a "data.table". All of these types of data objects (tibbles, data.frames, and data.tables) can be used with the commands we will learn in this lesson to make plots. We may sometimes use these terms interchangeably.
{: .callout}

# Understanding commands

Let's start by looking at the code JupyterLab ran for us by copying and pasting the first line from the console into our `gdp_population.ipynb` file that is open in the **Editor** window.

~~~
import numpy as np
import pandas as pd

gapminder_1997 = pd.read_csv("gapminder_1997.csv")

gapminder_1997
~~~
{: .language-python}

~~~
                country       pop continent  lifeExp     gdpPercap
0           Afghanistan  22227415      Asia   41.763    635.341351
1               Albania   3428038    Europe   72.950   3193.054604
2               Algeria  29072015    Africa   69.152   4797.295051
3                Angola   9875024    Africa   40.963   2277.140884
4             Argentina  36203463  Americas   73.275  10967.281950
..                  ...       ...       ...      ...           ...
137             Vietnam  76048996      Asia   70.672   1385.896769
138  West Bank and Gaza   2826046      Asia   71.096   7110.667619
139          Yemen Rep.  15826497      Asia   58.020   2117.484526
140              Zambia   9417789    Africa   40.238   1071.353818
141            Zimbabwe  11404948    Africa   46.809    792.449960

[142 rows x 5 columns]
~~~
{: .output}


You should now have a line of text in your code file that started with `gapminder` and ends with a `)` symbol.

What if we want to run this command from our code file?

In order to run code that you've typed in the editor, you have a few options. We can click <kbd>Run</kbd> again from the right side of the **Editor** tab but the quickest way to run the code is by pressing <kbd>Ctrl</kbd>+<kbd>Enter</kbd> on your keyboard (<kbd>Ctrl</kbd>+<kbd>Enter</kbd> on Mac).

This will run the line of code that currently contains your cursor and will move your cursor to the next line. Note that when Rstudio runs your code, it basically just copies your code from the **Editor** window to the **Console** window, just like what happened when we selected <kbd>Run Selected Line(s)</kbd>.

Let's take a closer look at the parts of this command.

Starting from the left, the first thing we see is `gapminder_1997`. We viewed the contents of this file after it was imported so we know that `gapminder_1997` acts as a placeholder for our data.

If we highlight just `gapminder_1997` within our code file and press <kbd>Ctrl</kbd>+<kbd>Enter</kbd> on our keyboard, what do we see?

We should see a data table outputted, similar to what we saw in the Viewer tab.

In pandas terms, `gapminder_1997` is a named [**DataFrame**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) that references or stores something. In this case, `gapminder_1997` stores a specific table of data.

Looking back at the command in our code file, the second thing we see is a `=` symbol, which is the **assignment operator**. It assigns values generated or typed on the right to objects on the left. 

> ## Assigning values to objects
> Try to assign values to some objects and observe each object after you have assigned a new value. What do you notice?
>
> 
> ~~~
> name = "Ben"
> print(name)
> age = 26
> print(age)
> name = "Harry Potter"
> print(name)
> ~~~
>{: .language-python}
> > ## Solution
> > When we assign a value to an object, the object stores that value so we can access it later. However, if we store a new value in an object we have already created (like when we stored "Harry Potter" in the `name` object), it replaces the old value. The `age` object does not change, because we never assign it a new value.
> {: .solution}
{: .challenge}


> ## Guidelines on naming objects
> - You want your object names to be explicit and not too long.
> - They cannot start with a number (2x is not valid, but x2 is).
> - Python is case sensitive, so for example, weight_kg is different from Weight_kg.
> - You cannot use spaces in the name.
> - There are some names that cannot be used because they are the names of fundamental functions in Python (e.g., if, else, for; run `help("keywords")` for a complete list). 
If in doubt, check the help to see if the name is already in use (`?function_name`).
> - It's best to avoid dots (.) within names. Dots have a special meaning (methods) in Python and other programming languages.
> - It is recommended to use nouns for object names and verbs for function names.
> - Be consistent in the styling of your code, such as where you put spaces, how you name objects, etc. Using a consistent coding style makes your code clearer to read for your future self and your collaborators. The official style guide for Python code can be found [here](https://peps.python.org/pep-0008/).
{: .checklist}

> ## Bonus Exercise: Bad names for objects
> Try to assign values to some new objects. What do you notice? After running all four lines of code bellow, what value do you think the object `Flower` holds?
>
> 
> ```python
> 1number = 3
> Flower = "marigold"
> flower = "rose"
> favorite number = 12
> ```
>
> > ## Solution
> > Notice that we get an error when we try to assign values to `1number` and `favorite number`. This is because we cannot start an object name with a numeral and we cannot have spaces in object names. The object `Flower` still holds "marigold." This is because Python is case-sensitive, so running `flower = "rose"` does NOT change the `Flower` object. This can get confusing, and is why we generally avoid having objects with the same name and different capitalization.
> {: .solution}
{: .challenge}

The next part of the command is `pd.read_csv("gapminder_1997.csv")`. This has a few different key parts. The first part is `pd`, which is a nickname for pandas that we imported earlier. 
The next part is the `read_csv` function from the pandas library. In Python you call a function from a library by typing the  name followed by opening then closing parenthesis. Each function has a purpose, which is often hinted at by the name of the function. Let's try to run the function without anything inside the parenthesis.


```python
pd.read_csv()
```



~~~
TypeError: read_csv() missing 1 required positional argument: 'filepath_or_buffer'
~~~
{: .error}

We get an error message. Don't panic! Error messages pop up all the time, and can be super helpful in debugging code.

In this case, the message tells us "read_csv() missing 1 required positional argument: 'filepath_or_buffer'" Many functions, including `read_csv`, require additional pieces of information to do their job. We call these additional values "arguments" or "parameters." You pass **arguments** to a function by placing values in between the parenthesis. A function takes in these arguments and does a bunch of "magic" behind the scenes to output something we're interested in.

For example, when we loaded in our data, the command contained `"gapminder_1997.csv"` inside the `read_csv()` function. This is the value we assigned to the file argument. But we didn't say that that was the file. How does that work?

> ## Pro-tip
>
> Each function has a help page that documents what arguments the function
> expects and what value it will return. You can bring up the help page a few
> different ways. If you have typed the function name in the **Editor** windows,
> you can put your cursor on the function name and press <kbd>F1</kbd> to open
> help page in the **Help** viewer in the lower right corner of JupyterLab. You can
> also type `?` followed by the function name in the console.
>
> For example, try running `?pd.read_csv`. A help page should pop up with
> information about what the function is used for and how to use it, as well as
> useful examples of the function in action. As you can see, the first
> **argument** of `read_csv` is the file path.
>
{: .callout}

The `read_csv()` function took the file path we provided, did who-knows-what behind the scenes, and then outputted a table with the data stored in that csv file. All that, with one short line of code!

Do all functions need arguments? Let's test some other functions:

~~~
from datetime import date
date.today()
~~~
{: .language-python}



~~~
datetime.date(2023, 4, 27)
~~~
{: .output}



~~~
import os
os.getcwd()
~~~
{: .language-python}


~~~
'/Users/fredfeng/Desktop/teaching/workshops/um-carpentries/intro-curriculum-python/_episodes_ipynb'
~~~
{: .output}


While some functions, like those above, don't need any arguments, in other
functions we may want to use multiple arguments. When we're using multiple
arguments, we separate the arguments with commas. For example, we can use the
`sum()` function to add numbers together:


~~~
sum([5, 6])
~~~
{: .language-python}



~~~
11
~~~
{: .output}
> ## Learning more about functions
> Look up the function `round`. What does it do? What will you get as output for the following lines of code?
>
> 
> ~~~
> round(3.1415)
> round(3.1415, 3)
> ~~~
> {: .language-python}
>
> > ## Solution
> > `round` rounds a number. By default, it rounds it to zero digits (in our example above, to 3). If you give it a second number, it rounds it to that number of digits (in our example above, to 3.142)
> {: .solution}
{: .challenge}

Notice how in this example, we didn't include any argument names. But you can
use argument names if you want:


~~~
pd.read_csv(filepath_or_buffer="gapminder_1997.csv")
~~~
{: .language-python}

~~~
                country       pop continent  lifeExp     gdpPercap
0           Afghanistan  22227415      Asia   41.763    635.341351
1               Albania   3428038    Europe   72.950   3193.054604
2               Algeria  29072015    Africa   69.152   4797.295051
3                Angola   9875024    Africa   40.963   2277.140884
4             Argentina  36203463  Americas   73.275  10967.281950
..                  ...       ...       ...      ...           ...
137             Vietnam  76048996      Asia   70.672   1385.896769
138  West Bank and Gaza   2826046      Asia   71.096   7110.667619
139          Yemen Rep.  15826497      Asia   58.020   2117.484526
140              Zambia   9417789    Africa   40.238   1071.353818
141            Zimbabwe  11404948    Africa   46.809    792.449960

[142 rows x 5 columns]
~~~
{: .output}

> ## Position of the arguments in functions
> Which of the following lines of code will give you an output of 3.14? For the one(s) that don't give you 3.14, what do they give you?
>
> 
> ~~~
> round(number=3.1415)
> round(number=3.1415, ndigits=2)
> round(ndigits=2, number=3.1415)
> round(2, 3.1415)
> ~~~
> {: .language-python}
>
> > ## Solution
> > The 2nd and 3rd lines will give you the right answer because the arguments are named, and when you use names the order doesn't matter. The 1st line will give you 3 because the default number of digits is 0. Then 4th line will give you 2 because, since you didn't name the arguments, x=2 and digits=3.1415.
> {: .solution}
{: .challenge}

Sometimes it is helpful - or even necessary - to include the argument name, but often we can skip the argument name, if the argument values are passed in a certain order. If all this function stuff sounds confusing, don't worry! We'll see a bunch of examples as we go that will make things clearer.

> ## Reading in an excel file
> Say you have an excel file and not a csv - how would you read that in? Hint: Use the Internet to help you figure it out!
>
> {: .source}
>
> > ## Solution
> > Pandas comes with the `read_excel` function which provides the same output as the output of `read_csv`.
> {: .solution}
{: .challenge}

> ## Comments
> Sometimes you may want to write comments in your code to help you remember
> what your code is doing, but you don't want R to think these comments are a part
> of the code you want to evaluate. That's where **comments** come in! Anything
> after a `#` symbol in your code will be ignored by Python. For example, let's say we
> wanted to make a note of what each of the functions we just used do:
> 
> ~~~
> date.today()   # outputs today's date
> ~~~
> {: .language-python}
> 
> 
> 
> ~~~
> datetime.date(2023, 4, 27)
> ~~~
> {: .output}
> 
> 
> 
> ~~~
> os.getcwd()    # outputs our current working directory (folder)
> ~~~
> {: .language-python}
> 
> 
> 
> ~~~
> '/Users/fredfeng/Desktop/teaching/workshops/um-carpentries/intro-curriculum-python/_episodes_ipynb'
> ~~~
> {: .output}
> 
> 
> 
> ~~~
> sum([5, 6])   # adds numbers
> ~~~
> {: .language-python}
> 
> 
> 
> ~~~
> 11
> ~~~
> {: .output}
> 
> 
> 
> ~~~
>  pd.read_csv(filepath_or_buffer="gapminder_1997.csv")   # reads in csv file
> ~~~
> {: .language-python}
> 
{: .callout}


# Creating our first plot
_[Back to top](#contents)_

We will be using the seaborn package today to make our plots. 
This is a very popular statistical data visualization library in Python. 
We will use the [seaborn objects interface](https://seaborn.pydata.org/tutorial/objects_interface.html). 
All plots start by calling the interface's `Plot()` function.


~~~
import seaborn.objects as so

so.Plot(data=gapminder_1997)
~~~
{: .language-python}

<img src="../fig/01-plotting-blank.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


ADD X-AXIS ONLY

~~~
so.Plot(data=gapminder_1997, x="gdpPercap")
~~~
{: .language-python}

<img src="../fig/01-plotting-x-only.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


ADD Y-AXIS

~~~
so.Plot(gapminder_1997, x="gdpPercap", y="lifeExp")
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


ADD DOT

~~~
(so.Plot(gapminder_1997, x="gdpPercap", y="lifeExp")
 .add(so.Dot())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y-dot.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


ADD AXIS LABELS

~~~
(so.Plot(gapminder_1997, x="gdpPercap", y="lifeExp")
 .add(so.Dot())
 .label(x="GDP Per Capita", 
        y="Life Expectancy")
)
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y-dot-xylabels.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


ADD TITLE

~~~
(so.Plot(gapminder_1997, x="gdpPercap", y="lifeExp")
 .add(so.Dot())
 .label(x="GDP Per Capita", 
        y="Life Expectancy", 
        title = "Do people in wealthy countries live longer?")
)
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y-dot-xylabels-title.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


ADD COLOR

~~~
(so.Plot(gapminder_1997, 
         x="gdpPercap", 
         y="lifeExp", 
         color="continent")
 .add(so.Dot())
 .label(x="GDP Per Capita", 
        y="Life Expectancy", 
        title = "Do people in wealthy countries live longer?")
)
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y-color-dot.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


COLOR PALETTE

~~~
import seaborn as sns
sns.color_palette()

sns.color_palette("flare")
sns.color_palette("Set1")
~~~
{: .language-python}



CHANGE COLOR PALETTE

~~~
(so.Plot(gapminder_1997, 
         x="gdpPercap", 
         y="lifeExp", 
         color="continent")
 .add(so.Dot())
 .label(x="GDP Per Capita", 
        y="Life Expectancy", 
        title = "Do people in wealthy countries live longer?")
 .scale(color="Set1")
)
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y-color-dot-colorpalette.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


ADD POINT SIZE

~~~
(so.Plot(gapminder_1997, 
         x="gdpPercap", 
         y="lifeExp", 
         color="continent",
         pointsize="pop")
 .add(so.Dot())
 .label(x="GDP Per Capita", 
        y="Life Expectancy", 
        title = "Do people in wealthy countries live longer?")
 .scale(color="Set1")
)
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y-color-size-dot.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />



CHANGING SHAPE

~~~
(so.Plot(gapminder_1997, 
         x="gdpPercap", 
         y="lifeExp", 
         color="continent",
         pointsize="pop",
         marker="continent")
 .add(so.Dot())
 .label(x="GDP Per Capita", 
        y="Life Expectancy", 
        title = "Do people in wealthy countries live longer?")
 .scale(color="Set1")
)
~~~
{: .language-python}

<img src="../fig/01-plotting-x-y-color-size-dot-shape.png" title="plot of chunk DataOnly" alt="plot of chunk DataOnly" width="612" style="display: block; margin: auto;" />


To run code that you've typed in a cell, you have a few options. Remember
that the quickest way to run the code in the selected cell is by pressing
<kbd>Ctrl</kbd>+<kbd>Enter</kbd> on your keyboard. This will run the cell that currently contains your cursor.

When we run this code, the **Plots** tab will pop to the front in the lower
right corner of the RStudio screen. Right now, we just see a big grey rectangle.

What we've done is created a ggplot object and told it we will be using the data
from the `gapminder_1997` object that we've loaded into R. We've done this by
calling the `ggplot()` function with `gapminder_1997` as the `data` argument.

So we've made a plot object, now we need to start telling it what we actually
want to draw in this plot. The elements of a plot have a bunch of properties
like an x and y position, a size, a color, etc. These properties are called
**aesthetics**. When creating a data visualization, we  map a variable in our
dataset to an aesthetic in our plot. In ggplot, we can do this by creating an
"aesthetic mapping", which we do with the `aes()` function.

To create our plot, we need to map variables from our `gapminder_1997` object to
ggplot aesthetics using the `aes()` function. Since we have already told
`ggplot` that we are using the data in the `gapminder_1997` object, we can
access the columns of `gapminder_1997` using the object's column names.
(Remember, R is case-sensitive, so we have to be careful to match the column
names exactly!)

We are interested in whether there is a relationship between GDP and life
expectancy, so let's start by telling our plot object that we want to map our
GDP values to the x axis of our plot. We do this by adding (`+`) information to
our plot object. Add this new line to your code and run both lines by
highlighting them and pressing <kbd>Ctrl</kbd>+<kbd>Enter</kbd> on your
keyboard:


~~~
so.Plot(gapminder_1997, x="gdpPercap", y="lifeExp")
~~~
{: .language-python}

<img src="../fig/rmd-01-ggplotX-1.png" title="plot of chunk ggplotX" alt="plot of chunk ggplotX" width="612" style="display: block; margin: auto;" />

Note that we've added this new function call to a second line just to make it
easier to read. To do this we make sure that the `+` is at the end of the first
line otherwise R will assume your command ends when it starts the next row. The
`+` sign indicates not only that we are adding information, but to continue on
to the next line of code.

Observe that our **Plot** window is no longer a grey square. We now see that
we've mapped the `gdpPercap` column to the x axis of our plot. Note that that
column name isn't very pretty as an x-axis label, so let's add the `labs()`
function to make a nicer label for the x axis


~~~
so.Plot(gapminder_1997, x="gdpPercap", y="lifeExp")
~~~
{: .language-python}

<img src="../fig/rmd-01-FirstPlotAddXLabel-1.png" title="plot of chunk FirstPlotAddXLabel" alt="plot of chunk FirstPlotAddXLabel" width="612" style="display: block; margin: auto;" />

OK. That looks better. 

> ## Quotes vs No Quotes
> Notice that when we added the label value we did so by placing the values
> inside quotes. This is because we are not using a value from inside our data
> object - we are providing the name directly. When you need to include actual
> text values in R, they will be placed inside quotes to tell them apart from
> other object or variable names.
> 
> The general rule is that if you want to use values from the columns of your
> data object, then you supply the name of the column without quotes, but if you
> want to specify a value that does not come from your data, then use quotes.
{: .callout}

> ## Mapping life expectancy to the y axis
> Map our `lifeExp` values to the y axis and give them a nice label.
> {: .source}
>
>
> > ## Solution
> > 
> > ~~~
> > ggplot(data = gapminder_1997) +
> >   aes(x = gdpPercap) +
> >   labs(x = "GDP Per Capita") +
> >   aes(y = lifeExp) +
> >   labs(y = "Life Expectancy")
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-FirstPlotAddY-1.png" title="plot of chunk FirstPlotAddY" alt="plot of chunk FirstPlotAddY" width="612" style="display: block; margin: auto;" />
> > {: .source}
> {: .solution}
{: .challenge}

Excellent. We've now told our plot object where the x and y values are coming
from and what they stand for. But we haven't told our object how we want it to
draw the data. There are many different plot types (bar charts, scatter plots,
histograms, etc). We tell our plot object what to draw by adding a "geometry"
("geom" for short) to our object. We will talk about many different geometries
today, but for our first plot, let's draw our data using the "points" geometry
for each value in the data set. To do this, we add `geom_point()` to our plot
object:


~~~
ggplot(data = gapminder_1997) +
  aes(x = gdpPercap) +
  labs(x = "GDP Per Capita") +
  aes(y = lifeExp) +
  labs(y = "Life Expectancy") +
  geom_point()
~~~
{: .language-r}

<img src="../fig/rmd-01-FirstPlotAddPoints-1.png" title="plot of chunk FirstPlotAddPoints" alt="plot of chunk FirstPlotAddPoints" width="612" style="display: block; margin: auto;" />

Now we're really getting somewhere. It finally looks like a proper plot!  We can
now see a trend in the data. It looks like countries with a larger GDP tend to
have a higher life expectancy. Let's add a title to our plot to make that
clearer. Again, we will use the `labs()` function, but this time we will use the
`title =` argument.


~~~
ggplot(data = gapminder_1997) +
  aes(x = gdpPercap) +
  labs(x = "GDP Per Capita") +
  aes(y = lifeExp) +
  labs(y = "Life Expectancy") +
  geom_point() +
  labs(title = "Do people in wealthy countries live longer?")
~~~
{: .language-r}

<img src="../fig/rmd-01-FirstPlotAddTitle-1.png" title="plot of chunk FirstPlotAddTitle" alt="plot of chunk FirstPlotAddTitle" width="612" style="display: block; margin: auto;" />

No one can deny we've made a very handsome plot! But now looking at the data, we
might be curious about learning more about the points that are the extremes of
the data. We know that we have two more pieces of data in the `gapminder_1997`
object that we haven't used yet. Maybe we are curious if the different
continents show different patterns in GDP and life expectancy. One thing we
could do is use a different color for each of the continents. To map the
continent of each point to a color, we will again use the `aes()` function:


~~~
ggplot(data = gapminder_1997) +
  aes(x = gdpPercap) +
  labs(x = "GDP Per Capita") +
  aes(y = lifeExp) +
  labs(y = "Life Expectancy") +
  geom_point() +
  labs(title = "Do people in wealthy countries live longer?") +
  aes(color = continent)
~~~
{: .language-r}

<img src="../fig/rmd-01-FirstPlotAddColor-1.png" title="plot of chunk FirstPlotAddColor" alt="plot of chunk FirstPlotAddColor" width="612" style="display: block; margin: auto;" />

Here we can see that in 1997 the African countries had much lower life
expectancy than many other continents. Notice that when we add a mapping for
color, ggplot automatically provided a legend for us. It took care of assigning
different colors to each of our unique values of the `continent` variable. (Note
that when we mapped the x and y values, those drew the actual axis labels, so in
a way the axes are like the legends for the x and y values). The colors that
ggplot uses are determined by the color "scale". Each aesthetic value we can
supply (x, y, color, etc) has a corresponding scale. Let's change the colors to
make them a bit prettier.


~~~
ggplot(data = gapminder_1997) +
  aes(x = gdpPercap) +
  labs(x = "GDP Per Capita") +
  aes(y = lifeExp) +
  labs(y = "Life Expectancy") +
  geom_point() +
  labs(title = "Do people in wealthy countries live longer?") +
  aes(color = continent) +
  scale_color_brewer(palette = "Set1")
~~~
{: .language-r}

<img src="../fig/rmd-01-FirstPlotAddColorScale-1.png" title="plot of chunk FirstPlotAddColorScale" alt="plot of chunk FirstPlotAddColorScale" width="612" style="display: block; margin: auto;" />

The `scale_color_brewer()` function is just one of many you can use to change
colors. There are bunch of "palettes" that are build in. You can view them all
by running `RColorBrewer::display.brewer.all()` or check out the [Color Brewer
website](https://colorbrewer2.org/) for more info about choosing plot colors.

There are also lots of other fun options:

- [Viridis](https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html)
- [National parks](https://github.com/katiejolly/nationalparkcolors)
- [LaCroix](https://github.com/johannesbjork/LaCroixColoR)
- [Wes Anderson](https://github.com/karthik/wesanderson)

> ## Bonus Exercise: Changing colors
> Play around with different color palettes. Feel free to install another
> package and choose one of those if you want. Pick your favorite!
> {: .source}
>
> > ## Solution
> > You can use RColorBrewer::display.brewer.all() to pick a color palette. 
> > As a bonus, you can also use one of the packages listed above. 
> > Here's an example:
> > 
> > 
> > ~~~
> > #install.packages("wesanderson") # install package from GitHub
> > library(wesanderson)
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > Error in library(wesanderson): there is no package called 'wesanderson'
> > ~~~
> > {: .error}
> > 
> > 
> > 
> > ~~~
> > ggplot(data = gapminder_1997) +
> > aes(x = gdpPercap) +
> > labs(x = "GDP Per Capita") +
> > aes(y = lifeExp) +
> > labs(y = "Life Expectancy") +
> > geom_point() +
> > labs(title = "Do people in wealthy countries live longer?") +
> > aes(color = continent) +
> > scale_color_manual(values = wes_palette('Cavalcanti1'))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > Error in wes_palette("Cavalcanti1"): could not find function "wes_palette"
> > ~~~
> > {: .error}
> > {: .source}
> {: .solution}
{: .challenge}

Since we have the data for the population of each country, we might be curious
what effect population might have on life expectancy and GDP per capita. Do you
think larger countries will have a longer or shorter life expectancy? Let's find
out by mapping the population of each country to the size of our points.


~~~
ggplot(data = gapminder_1997) +
  aes(x = gdpPercap) +
  labs(x = "GDP Per Capita") +
  aes(y = lifeExp) +
  labs(y = "Life Expectancy") +
  geom_point() +
  labs(title = "Do people in wealthy countries live longer?") +
  aes(color = continent) +
  scale_color_brewer(palette = "Set1") +
  aes(size = pop)
~~~
{: .language-r}

<img src="../fig/rmd-01-FirstPlotAddSize-1.png" title="plot of chunk FirstPlotAddSize" alt="plot of chunk FirstPlotAddSize" width="612" style="display: block; margin: auto;" />

There doesn't seem to be a very strong association with population size. We can
see two very large countries with relatively low GDP per capita (but since the
per capita value is already divided by the total population, there is some
problems with separating those two values). We got another legend here for size
which is nice, but the values look a bit ugly in scientific notation. Let's
divide all the values by 1,000,000 and label our legend "Population (in
millions)"


~~~
ggplot(data = gapminder_1997) +
  aes(x = gdpPercap) +
  labs(x = "GDP Per Capita") +
  aes(y = lifeExp) +
  labs(y = "Life Expectancy") +
  geom_point() +
  labs(title = "Do people in wealthy countries live longer?") +
  aes(color = continent) +
  scale_color_brewer(palette = "Set1") +
  aes(size = pop/1000000) +
  labs(size = "Population (in millions)")
~~~
{: .language-r}

<img src="../fig/rmd-01-FirstPlotAddPop-1.png" title="plot of chunk FirstPlotAddPop" alt="plot of chunk FirstPlotAddPop" width="612" style="display: block; margin: auto;" />

This works because you can treat the columns in the aesthetic mappings just like
any other variables and can use functions to transform or change them at plot
time rather than having to transform your data first.

Good work! Take a moment to appreciate what a cool plot you made with a few
lines of code. In order to fully view its beauty you can click the "Zoom" button
in the **Plots** tab - it will break free from the lower right corner and open
the plot in its own window.

> ## Changing shapes
> Instead of (or in addition to) color, change the shape of the points so each continent has a different shape. (I'm not saying this is a great thing to do - it's just for practice!) HINT: Is size an aesthetic or a geometry? If you're stuck, feel free to Google it, or look at the help menu.
> {: .source}
>
> > ## Solution
> > You'll want to use the `aes` aesthetic function to change the shape:
> > 
> > ~~~
> > ggplot(data = gapminder_1997) +
> >   aes(x = gdpPercap) +
> >   labs(x = "GDP Per Capita") +
> >   aes(y = lifeExp) +
> >   labs(y = "Life Expectancy") +
> >   geom_point() +
> >   labs(title = "Do people in wealthy countries live longer?") +
> >   aes(color = continent) +
> >   scale_color_brewer(palette = "Set1") +
> >   aes(size = pop/1000000) +
> >   labs(size = "Population (in millions)") +
> >   aes(shape = continent)
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-Shape-1.png" title="plot of chunk Shape" alt="plot of chunk Shape" width="612" style="display: block; margin: auto;" />
> > {: .source}
> {: .solution}
{: .challenge}

For our first plot we added each line of code one at a time so you could see the
exact affect it had on the output. But when you start to make a bunch of plots,
we can actually combine many of these steps so you don't have to type as much.
For example, you can collect all the `aes()` statements and all the `labs()`
together. A more condensed version of the exact same plot would look like this:


~~~
ggplot(data = gapminder_1997) +
  aes(x = gdpPercap, y = lifeExp, color = continent, size = pop/1000000) +
  geom_point() +
  scale_color_brewer(palette = "Set1") +
  labs(x = "GDP Per Capita", y = "Life Expectancy",
    title = "Do people in wealthy countries live longer?", size = "Population (in millions)")
~~~
{: .language-r}

<img src="../fig/rmd-01-FirstPlotCondensed-1.png" title="plot of chunk FirstPlotCondensed" alt="plot of chunk FirstPlotCondensed" width="612" style="display: block; margin: auto;" />

# Plotting for data exploration
_[Back to top](#contents)_

Many datasets are much more complex than the example we used for the first plot.
How can we find meaningful patterns in complex data and create visualizations to
convey those patterns?

## Importing datasets
_[Back to top](#contents)_

In the first plot, we looked at a smaller slice of a large dataset. To gain a
better understanding of the kinds of patterns we might observe in our own data,
we will now use the full dataset, which is stored in a file called
"gapminder_data.csv".

To start, we will read in the data without using the interactive RStudio file navigation.

> ## Read in your own data
>
> What argument should be provided in the below code to read in the full dataset?
>
> 
> ~~~
gapminder_data = pd.read_csv()
> ~~~
> {: .language-python}
>
> > ## Solution
> >
> > 
> > ~~~
> > gapminder_data = pd.read_csv("gapminder_data.csv")
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

Let's take a look at the full dataset. We could use `View()`, the way we did for the smaller dataset, but if your data is too big, it might take too long to load. Luckily, R offers a way to look at parts of the data to get an idea of what your dataset looks like, without having to examine the whole thing. Here are some commands that allow us to get the dimensions of our data and look at a snapshot of the data. Try them out!


~~~
gapminder_data.shape
~~~
{: .language-python}

~~~
gapminder_data.head()
~~~
{: .language-python}

Notice that this dataset has an additional column `year` compared to the smaller dataset we started with.

> ## Predicting `seaborn` outputs
> Now that we have the full dataset read into our R session, let's plot the data placing our new `year` variable on the x axis and life expectancy on the y axis. We've provided the code below. Notice that we've collapsed the plotting function options and left off some of the labels so there's not as much code to work with.
> Before running the code, read through it and see if you can predict what the plot output will look like. Then run the code and check to see if you were right!
>
> 
> ~~~
> (so.Plot(data=gapminder_data, 
>          x="year", 
>          y="lifeExp",
>          color="continent")
>  .add(so.Dot())
> )
> ~~~
> {: .language-python}
> 
> <img src="../fig/01-plotting-PlotFullGapminder-1.png" title="plot of chunk PlotFullGapminder" alt="plot of chunk PlotFullGapminder" width="612" style="display: block; margin: auto;" />
>
{: .challenge}

Hmm, the plot we created in the last exercise isn't very clear. What's going on? Since the dataset is more complex, the plotting options we used for the smaller dataset aren't as useful for interpreting these data. Luckily, we can add additional attributes to our plots that will make patterns more apparent. For example, we can generate a different type of plot - perhaps a line plot - and assign attributes for columns where we might expect to see patterns.

Let's review the columns and the types of data stored in our dataset to decide how we should group things together. To get an overview of our data object, we can look at the structure of `gapminder_data` using the `str()` function.

~~~
gapminder_data.info()
~~~
{: .language-python}
(You can also review the structure of your data in the **Environment** tab by clicking on the blue circle with the arrow in it next to your data object name.)

So, what do we see? The column names are listed after a `$` symbol, and then we have a `:` followed by a text label. These labels correspond to the type of data stored in each column.

What kind of data do we see?
* "int64"= Integer (or whole number)
* "float64" = Numeric (or non-whole number)
* "object" = Character (categorical data)

**Note** In anything before R 4.0, categorical variables used to be read in as factors, which are a [special data object](https://www.tutorialspoint.com/r/r_factors.htm) that are used to store categorical data and have limited numbers of unique values. The unique values of a factor are tracked via the "levels" of a factor. A factor will always remember all of its levels even if the values don't actually appear in your data. The factor will also remember the order of the levels and will always print values out in the same order (by default this order is alphabetical).

If your columns are stored as character values but you need factors for plotting, ggplot will convert them to factors for you as needed.

Our plot has a lot of points in columns which makes it hard to see trends over time. A better way to view the data showing changes over time is to use a [line plot](http://www.sthda.com/english/wiki/ggplot2-line-plot-quick-start-guide-r-software-and-data-visualization). Let's try changing the geom to a line and see what happens.


~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         color="continent")
 .add(so.Lines())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapMinderLinePlotBad-1.png" title="plot of chunk GapMinderLinePlotBad" alt="plot of chunk GapMinderLinePlotBad" width="612" style="display: block; margin: auto;" />

Hmm. This doesn't look right. By setting the color value, we got a line for each continent, but we really wanted a line for each country. We need to tell ggplot that we want to connect the values for each `country` value instead. To do this, we need to use the `group=` aesthetic.


~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         group="country",
         color="continent")
 .add(so.Line())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapMinderLinePlot-1.png" title="plot of chunk GapMinderLinePlot" alt="plot of chunk GapMinderLinePlot" width="612" style="display: block; margin: auto;" />

Sometimes plots like this are called "spaghetti plots" because all the lines look like a bunch of wet noodles.

> ## Bonus Exercise: More line plots
> Now create your own line plot comparing population and life expectancy! Looking at your plot, can you guess which two countries have experienced massive change in population from 1952-2007?
>
> > ## Solution
> > 
> > ~~~
> > (so.Plot(data=gapminder_data, 
> >          x="pop", 
> >          y="lifeExp",
> >          group="country",
> >          color="continent")
> >  .add(so.Line())
> > )
> > ~~~
> > {: .language-python}
> > 
> > <img src="../fig/01-plotting-gapminderMoreLines-1.png" title="plot of chunk gapminderMoreLines" alt="plot of chunk gapminderMoreLines" width="612" style="display: block; margin: auto;" />
> > (China and India are the two Asian countries that have experienced massive population growth from 1952-2007.)
> {: .solution}
{: .challenge}

## Discrete Plots
_[Back to top](#contents)_

So far we've looked at two plot types (`geom_point` and `geom_line`) which work when both the x and y values are numeric. But sometimes you may have one of your values be discrete (a factor or character).

We've previously used the discrete values of the `continent` column to color in our points and lines. But now let's try moving that variable to the `x` axis. Let's say we are curious about comparing the distribution of the life expectancy values for each of the different continents for the `gapminder_1997` data. We can do so using a box plot. Try this out yourself in the exercise below!

> ## Box plots
> Using the `gapminder_1997` data, use ggplot to create a box plot with continent on the x axis and life expectancy on the y axis. You can use the examples from earlier in the lesson as a template to remember how to pass ggplot data and map aesthetics and geometries onto the plot. If you're really stuck, feel free to use the internet as well!
>
> > ## Solution
> > 
> > ~~~
> > ggplot(data = gapminder_1997) +
> >  aes(x = continent, y = lifeExp) +
> >  geom_boxplot()
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-GapBox-1.png" title="plot of chunk GapBox" alt="plot of chunk GapBox" width="612" style="display: block; margin: auto;" />
> {: .solution}
{: .challenge}

This type of visualization makes it easy to compare the range and spread of values across groups. The "middle" 50% of the data is located inside the box and outliers that are far away from the central mass of the data are drawn as points.

> ## Bonus Exercise: Other discrete geoms
> Take a look a the ggplot [cheat sheet](https://ggplot2.tidyverse.org/). Find all the geoms listed under "Discrete X, Continuous Y". Try replacing `geom_boxplot` with one of these other functions.
>
> > ## Example solution
> > 
> > ~~~
> > ggplot(data = gapminder_1997) +
> >   aes(x = continent, y = lifeExp) +
> >   geom_violin()
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-GapViol-1.png" title="plot of chunk GapViol" alt="plot of chunk GapViol" width="612" style="display: block; margin: auto;" />
> {: .solution}
{: .challenge}

## Layers
_[Back to top](#contents)_

So far we've only been adding one geom to each plot, but each plot object can actually contain multiple layers and each layer has it's own geom. Let's start with a basic violin plot:


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_violin()
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolin-1.png" title="plot of chunk GapViolin" alt="plot of chunk GapViolin" width="612" style="display: block; margin: auto;" />

Violin plots are similar to box plots, but they show the range and spread of values with curves rather than boxes (wider curves = more observations) and they do not include outliers. Also note you need a minimum number of points so they can be drawn - because Oceania only has two values, it doesn't get a curve. We can include the Oceania data by adding a layer of points on top that will show us the "raw" data:


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_violin() +
  geom_point()
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinPoints-1.png" title="plot of chunk GapViolinPoints" alt="plot of chunk GapViolinPoints" width="612" style="display: block; margin: auto;" />

OK, we've drawn the points but most of them stack up on top of each other. One way to make it easier to see all the data is to "jitter" the points, or move them around randomly so they don't stack up on top of each other. To do this, we use `geom_jitter` rather than `geom_point`


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_violin() +
  geom_jitter()
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinJitter-1.png" title="plot of chunk GapViolinJitter" alt="plot of chunk GapViolinJitter" width="612" style="display: block; margin: auto;" />

Be aware that these movements are random so your plot will look a bit different each time you run it!

Now let's try switching the order of `geom_violin` and `geom_jitter`. What happens? Why?


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_jitter() +
  geom_violin()
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinJitterLayers-1.png" title="plot of chunk GapViolinJitterLayers" alt="plot of chunk GapViolinJitterLayers" width="612" style="display: block; margin: auto;" />

Since we plot the `geom_jitter` layer first, the violin plot layer is placed on top of the `geom_jitter` layer, so we cannot see most of the points.

Note that each layer can have it's own set of aesthetic mappings. So far we've been using `aes()` outside of the other functions. When we do this, we are setting the "default" aesthetic mappings for the plot. We could do the same thing by passing the values to the `ggplot()` function call as is sometimes more common:


~~~
ggplot(data = gapminder_1997, mapping = aes(x = continent, y = lifeExp)) +
  geom_violin() +
  geom_jitter()
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinJitter2-1.png" title="plot of chunk GapViolinJitter2" alt="plot of chunk GapViolinJitter2" width="612" style="display: block; margin: auto;" />

However, we can also use aesthetic values for only one layer of our plot. To do that, you an place an additional `aes()` inside of that layer. For example, what if we want to change the size for the points so they are scaled by population, but we don't want to change the violin plot? We can do:


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_violin() +
  geom_jitter(aes(size = pop))
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinJitterAes-1.png" title="plot of chunk GapViolinJitterAes" alt="plot of chunk GapViolinJitterAes" width="612" style="display: block; margin: auto;" />

Both `geom_violin` and `geom_jitter` will inherit the default values of `aes(continent, lifeExp)` but only `geom_jitter` will also use `aes(size = pop)`.

> ## Functions within functions
>
> In the two examples above, we placed the `aes()` function inside another function - see how in the line of code `geom_jitter(aes(size = pop))`, `aes()` is nested **inside** `geom_jitter()`? When this happens, R evaluates the inner function first, then passes the output of that function as an argument to the outer function.
>
> Take a look at this simpler example. Suppose we have:
>
> 
> ~~~
> sum(2, max(6,8))
> ~~~
> {: .language-r}
> First R calculates the maximum of the numbers 6 and 8 and returns the value 8. It passes the output 8 into the sum function and evaluates:
> 
> ~~~
> sum(2, 8)
> ~~~
> {: .language-r}
> 
> 
> 
> ~~~
> [1] 10
> ~~~
> {: .output}
>
{: .solution}


## Color vs. Fill 
_[Back to top](#contents)_

Let's say we want to spice up our plot a bit by adding some color. Maybe we want our violin color to a fancy color like "darkolivegreen." We can do this by explicitly setting the color aesthetic inside the `geom_violin` function. Note that because we are assigning a color directly and not using any values from our data to do so, we do not need to use the `aes()` mapping function. Let's try it out:


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_violin(color="pink")
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinColor-1.png" title="plot of chunk GapViolinColor" alt="plot of chunk GapViolinColor" width="612" style="display: block; margin: auto;" />
Well, that didn't get all that colorful. That's because objects like these violins have two different parts that have a color: the shape outline, and the inner part of the shape. For geoms that have an inner part, you change the fill color with `fill=` rather than `color=`, so let's try that instead


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_violin(fill="pink")
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinFill-1.png" title="plot of chunk GapViolinFill" alt="plot of chunk GapViolinFill" width="612" style="display: block; margin: auto;" />

That's some plot now isn't it! Compare this to what you see when you map the fill property to your data rather than setting a specific value.


~~~
ggplot(data = gapminder_1997) +
  aes(x = continent, y = lifeExp) +
  geom_violin(aes(fill=continent))
~~~
{: .language-r}

<img src="../fig/rmd-01-GapViolinFillMap-1.png" title="plot of chunk GapViolinFillMap" alt="plot of chunk GapViolinFillMap" width="612" style="display: block; margin: auto;" />

So "darkolivegreen" maybe wasn't the prettiest color. R knows lots of color names. You can see the full list if you run `colors()` in the console. Since there are so many, you can randomly choose 10 if you run `sample(colors(), size = 10)`.

> ## choosing a color
>  Use `sample(colors(), size = 10)` a few times until you get an interesting sounding color name and swap that out for "darkolivegreen" in the violin plot example.
>
{: .challenge}


> ## Bonus Exercise: Transparency
> Another aesthetic that can be changed is how transparent our colors/fills are. The `alpha` parameter decides how transparent to make the colors. By default, `alpha = 1`, and our colors are completely opaque. Decreasing `alpha` increases the transparency of our colors/fills. Try changing the transparency of our violin plot. (**Hint:** Should alpha be inside or outside `aes()`?)
> > ## Solution
> > 
> > ~~~
> > ggplot(data = gapminder_1997) +
> >   aes(x = continent, y = lifeExp) +
> >   geom_violin(fill="darkblue", alpha = 0.5)
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-GapViolinFillSoln-1.png" title="plot of chunk GapViolinFillSoln" alt="plot of chunk GapViolinFillSoln" width="612" style="display: block; margin: auto;" />
> {: .solution}
{: .challenge}

> ## Changing colors
> What happens if you run:
> 
> ~~~
>  ggplot(data = gapminder_1997) +
>  aes(x = continent, y = lifeExp) +
>  geom_violin(aes(fill = "springgreen"))
> ~~~
> {: .language-r}
> 
> <img src="../fig/rmd-01-GapViolinAesFillMap-1.png" title="plot of chunk GapViolinAesFillMap" alt="plot of chunk GapViolinAesFillMap" width="612" style="display: block; margin: auto;" />
> Why doesn't this work? How can you fix it? Where does that color come from?
>
> > ## Solution
> > In this example, you placed the fill inside the `aes()` function. Because you are using an aesthetic mapping, the "scale" for the fill will assign colors to values - in this case, you only have one value: the word "springgreen." Instead, try `geom_violin(fill = "springgreen")`.
> {: .solution}
{: .challenge}

## Univariate Plots
_[Back to top](#contents)_

We jumped right into make plots with multiple columns. But what if we wanted to take a look at just one column? In that case, we only need to specify a mapping for `x` and choose an appropriate geom. Let's start with a [histogram](https://www.thoughtco.com/what-is-a-histogram-3126359) to see the range and spread of the life expectancy values.


~~~
(so.Plot(data=gapminder_1997, x="lifeExp")
 .add(so.Bars(), so.Hist())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapLifeHist-1.png" title="plot of chunk GapLifeHist" alt="plot of chunk GapLifeHist" width="612" style="display: block; margin: auto;" />

You should not only see the plot in the plot window, but also a message telling you to choose a better bin value. Histograms can look very different depending on the number of bars you decide to draw. The default is 30. Let's try setting a different value by explicitly passing a `bin=` argument to the `geom_histogram` later.


~~~
(so.Plot(data=gapminder_1997, x="lifeExp")
 .add(so.Bars(), so.Hist(bins=20))
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapLifeHistBins-1.png" title="plot of chunk GapLifeHistBins" alt="plot of chunk GapLifeHistBins" width="612" style="display: block; margin: auto;" />

Try different values like 5 or 50 to see how the plot changes.



SET BIN END POINTS


~~~
(so.Plot(data=gapminder_1997, x="lifeExp")
 .add(so.Bars(), 
      so.Hist(bins=20, binwidth=2, binrange=(0, 100)))
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapLifeHistBins-2.png" title="plot of chunk GapLifeHistBins" alt="plot of chunk GapLifeHistBins" width="612" style="display: block; margin: auto;" />


SET LAYOUT


~~~
(so.Plot(data=gapminder_1997, x="lifeExp")
 .add(so.Bars(), 
      so.Hist(bins=20, binwidth=2, binrange=(0, 100)))
 .layout(size=(10,5))
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapLifeHistBins-3.png" title="plot of chunk GapLifeHistBins" alt="plot of chunk GapLifeHistBins" width="612" style="display: block; margin: auto;" />


> ## Bonus Exercise: One variable plots
> Rather than a histogram, choose one of the other geometries listed under "One Variable" plots on the ggplot [cheat sheet](https://ggplot2.tidyverse.org/). Note that we used `lifeExp` here which has continuous values. If you want to try the discrete options, try mapping `continent` to x instead.
>
> > ## Example solution
> > 
> > ~~~
> > (so.Plot(data=gapminder_1997, x="lifeExp")
> >  .add(so.Line(), so.KDE())
> > )
> > ~~~
> > {: .language-python}
> > 
> > <img src="../fig/01-plotting-GapLifeDens1-1.png" title="plot of chunk GapLifeDens1" alt="plot of chunk GapLifeDens1" width="612" style="display: block; margin: auto;" />
> {: .solution}
{: .challenge}


## Plot Themes
_[Back to top](#contents)_

Our plots are looking pretty nice, but what's with that grey background? While you can change various elements of a `ggplot` object manually (background color, grid lines, etc.) the `ggplot` package also has a bunch of nice built-in themes to change the look of your graph. For example, let's try adding `theme_classic()` to our histogram:

~~~
from matplotlib import style
style.available
~~~
{: .language-python}


~~~
['Solarize_Light2',
 '_classic_test_patch',
 '_mpl-gallery',
 '_mpl-gallery-nogrid',
 'bmh',
 'classic',
 'dark_background',
 'fast',
 'fivethirtyeight',
 'ggplot',
 'grayscale',
 'seaborn-v0_8',
 'seaborn-v0_8-bright',
 'seaborn-v0_8-colorblind',
 'seaborn-v0_8-dark',
 'seaborn-v0_8-dark-palette',
 'seaborn-v0_8-darkgrid',
 'seaborn-v0_8-deep',
 'seaborn-v0_8-muted',
 'seaborn-v0_8-notebook',
 'seaborn-v0_8-paper',
 'seaborn-v0_8-pastel',
 'seaborn-v0_8-poster',
 'seaborn-v0_8-talk',
 'seaborn-v0_8-ticks',
 'seaborn-v0_8-white',
 'seaborn-v0_8-whitegrid',
 'tableau-colorblind10']
~~~
{: .output}

~~~
(so.Plot(data=gapminder_1997, x="lifeExp")
 .add(so.Bars(), so.Hist(bins=20))
 .theme({**style.library["classic"]})
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapLifeHistBinsClassicTheme-1.png" title="plot of chunk GapLifeHistBinsClassicTheme" alt="plot of chunk GapLifeHistBinsClassicTheme" width="612" style="display: block; margin: auto;" />

Try out a few other themes, to see which you like: `theme_bw()`, `theme_linedraw()`, `theme_minimal()`.

> ## Rotating x axis labels
> Often, you'll want to change something about the theme that you don't know how to do off the top of your head. When this happens, you can do an Internet search to help find what you're looking for. To practice this, search the Internet to figure out how to rotate the x axis labels 90 degrees. Then try it out using the histogram plot we made above. 
>
> > ## Solution
> > 
> > ~~~
> > ggplot(gapminder_1997) +
> >   aes(x = lifeExp) +
> >   geom_histogram(bins = 20) + 
> >   theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-GapLifeDens2-1.png" title="plot of chunk GapLifeDens2" alt="plot of chunk GapLifeDens2" width="612" style="display: block; margin: auto;" />
> {: .solution}
{: .challenge}

## Facets
_[Back to top](#contents)_

If you have a lot of different columns to try to plot or have distinguishable subgroups in your data, a powerful plotting technique called faceting might come in handy. When you facet your plot, you basically make a bunch of smaller plots and combine them together into a single image. Luckily, `ggplot` makes this very easy. Let's start with a simplified version of our first plot







~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         group="country",
         color="continent")
 .add(so.Line())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapNoFacet-1.png" title="plot of chunk GapNoFacet" alt="plot of chunk GapNoFacet" width="612" style="display: block; margin: auto;" />

The first time we made this plot, we colored the points differently for each of the continents. This time let's actually draw a separate box for each continent. We can do this with `facet_wrap()`


~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         group="country",
         color="continent")
 .facet("continent")
 .add(so.Line())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapFacetWrap-1.png" title="plot of chunk GapFacetWrap" alt="plot of chunk GapFacetWrap" width="612" style="display: block; margin: auto;" />
Note that `facet_wrap` requires this extra helper function called `vars()` in order to pass in the column names. It's a lot like the `aes()` function, but it doesn't require an aesthetic name. We can see in this output that we get a separate box with a label for each continent so that only the points for that continent are in that box.

The other faceting function ggplot provides is `facet_grid()`. The main difference is that `facet_grid()` will make sure all of your smaller boxes share a common axis. In this example, we will stack all the boxes on top of each other into rows so that their x axes all line up.


~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         group="country",
         color="continent")
 .facet("continent", wrap=3)
 .add(so.Line())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapFacetWrap-2.png" title="plot of chunk GapFacetWrap" alt="plot of chunk GapFacetWrap" width="612" style="display: block; margin: auto;" />


~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         color="continent")
 .facet("continent", wrap=3)
 .add(so.Line(), so.Agg())
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapFacetWrap-3.png" title="plot of chunk GapFacetWrap" alt="plot of chunk GapFacetWrap" width="612" style="display: block; margin: auto;" />


~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         color="continent")
 .facet("continent", wrap=3)
 .add(so.Line(linewidth=3), so.Agg())
 .add(so.Line(alpha=.3), so.Agg(), col=None)
)
~~~
{: .language-python}

<img src="../fig/01-plotting-GapFacetWrap-4.png" title="plot of chunk GapFacetWrap" alt="plot of chunk GapFacetWrap" width="612" style="display: block; margin: auto;" />



Unlike the `facet_wrap` output where each box got its own x and y axis, with `facet_grid()`, there is only one x axis along the bottom.

## Saving plots
_[Back to top](#contents)_

We've made a bunch of plots today, but we never talked about how to share them with your friends who aren't running R! It's wise to keep all the code you used to draw the plot, but sometimes you need to make a PNG or PDF version of the plot so you can share it with your PI or post it to your Instagram story.

One that's easy if you are working in RStudio interactively is to use "Export" menu on the **Plots** tab. Clicking that button gives you three options "Save as Image", "Save as PDF", and "Copy To Clipboard". These options will bring up a window that will let you resize and name the plot however you like.

A better option if you will be running your code as a script from the command line or just need your code to be more reproducible is to use the `ggsave()` function. When you call this function, it will write the last plot printed to a file in your local directory. It will determine the file type based on the name you provide. So if you call `ggsave("plot.png")` you'll get a PNG file or if you call `ggsave("plot.pdf")` you'll get a PDF file. By default the size will match the size of the **Plots** tab. To change that you can also supply `width=` and `height=` arguments. By default these values are interpreted as inches. So if you want a wide 4x6 image you could do something like:


~~~
(so.Plot(data=gapminder_data, 
         x="year", 
         y="lifeExp",
         color="continent")
 .facet("continent", wrap=3)
 .add(so.Line(linewidth=3), so.Agg())
 .add(so.Line(alpha=.3), so.Agg(), col=None)
 .save("awesome_plot.png", bbox_inches='tight', dpi=200)
)
~~~
{: .language-python}

> ## Saving a plot
>
> Try rerunning one of your plots and then saving it using `save()`. Find and open the plot to see if it worked!
>
> > ## Example solution
> > 
> > ~~~
> > (so.Plot(data=gapminder_1997, x="lifeExp")
> >  .add(so.Bars(), 
> >       so.Hist(bins=20, binwidth=2, binrange=(0, 100)))
> >  .save("awesome_histogram.png")
> > )
> > ~~~
> > {: .language-python}
> > 
> > <img src="../fig/01-plotting-savingPlotExercise-1.png" title="plot of chunk savingPlotExercise" alt="plot of chunk savingPlotExercise" width="612" style="display: block; margin: auto;" />
> > 
> >
> > Check your current working directory to find the plot!
> {: .solution}
{: .challenge}

You also might want to just temporarily save a plot while you're using R, so that you can come back to it later. Luckily, a plot is just an object, like any other object we've been working with! Let's try storing our violin plot from earlier in an object called `violin_plot`:


~~~
violin_plot <- ggplot(data = gapminder_1997) +
                  aes(x = continent, y = lifeExp) +
                  geom_violin(aes(fill=continent))
~~~
{: .language-r}

Now if we want to see our plot again, we can just run:


~~~
violin_plot
~~~
{: .language-r}

<img src="../fig/rmd-01-outputViolinPlot-1.png" title="plot of chunk outputViolinPlot" alt="plot of chunk outputViolinPlot" width="612" style="display: block; margin: auto;" />

We can also add changes to the plot. Let's say we want our violin plot to have the black-and-white theme:


~~~
violin_plot + theme_bw()
~~~
{: .language-r}

<img src="../fig/rmd-01-violinPlotBWTheme-1.png" title="plot of chunk violinPlotBWTheme" alt="plot of chunk violinPlotBWTheme" width="612" style="display: block; margin: auto;" />

Watch out! Adding the theme does not change the `violin_plot` object! If we want to change the object, we need to store our changes:


~~~
violin_plot <- violin_plot + theme_bw()
~~~
{: .language-r}

We can also save any plot object we have named, even if they were not the plot that we ran most recently. We just have to tell `ggsave()` which plot we want to save:


~~~
ggsave("awesome_violin_plot.jpg", plot = violin_plot, width=6, height=4)
~~~
{: .language-r}

> ## Bonus Exercise: Create and save a plot
> Now try it yourself! Create your own plot using `ggplot()`, store it in an object named `my_plot`, and save the plot using `ggsave()`.
>
> > ## Example solution
> > 
> > ~~~
> > my_plot <- ggplot(data = gapminder_1997)+
> >   aes(x = continent, y = gdpPercap)+
> >   geom_boxplot(fill = "orange")+
> >   theme_bw()+
> >   labs(x = "Continent", y = "GDP Per Capita")
> > 
> > ggsave("my_awesome_plot.jpg", plot = my_plot, width=6, height=4)
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}



# Bonus

## Creating complex plots

### Animated plots
_[Back to bonus](#bonus)_

Sometimes it can be cool (and useful) to create animated graphs, like [this
famous one](https://www.youtube.com/watch?v=FTu4dDHpfdU&feature=youtu.be) by
Hans Rosling using the Gapminder dataset that plots GDP vs. Life Expectancy over
time. Let's try to recreate this plot!

First, we need to install and load the `gganimate` package, which allows us to
use ggplot to create animated visuals:


~~~
install.packages(c("gganimate", "gifski"))
library(gganimate)
library(gifski)
~~~
{: .language-r}


> ## Reviewing how to create a scatter plot
> **Part 1:**
> Let's start by creating a static plot using `ggplot()`, as we've been doing so
> far. This time, lets put `log(gdpPercap)` on the x-axis, to help spread out our
> data points, and life expectancy on our y-axis. Also map the point size to the
> population of the country, and the color of the points to the continent.
>
> > ## Solution
> >
> > 
> > ~~~
> > ggplot(data = gapminder_data)+
> >  aes(x = log(gdpPercap), y = lifeExp, size = pop, color = continent)+
> >  geom_point()
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-hansGraphStaticSolution-1.png" title="plot of chunk hansGraphStaticSolution" alt="plot of chunk hansGraphStaticSolution" width="612" style="display: block; margin: auto;" />
>{: .solution}

> **Part 2:**
> Before we start to animate our plot, let's make sure it looks pretty. Add some better axis and legend labels, change the plot theme, and otherwise fix up the plot so it looks nice. Then save the plot into an object called `staticHansPlot`. When you're ready, check out how we've edited our plot, below.
>
> > ## A pretty plot (yours may look different)
> > 
> > ~~~
> > staticHansPlot <- ggplot(data = gapminder_data)+
> >  aes(x = log(gdpPercap), y = lifeExp, size = pop/1000000, color = continent)+
> >  geom_point(alpha = 0.5) + # we made our points slightly transparent, because it makes it easier to see overlapping points
> >  scale_color_brewer(palette = "Set1") +
> >  labs(x = "GDP Per Capita", y = "Life Expectancy", color= "Continent", size="Population (in millions)")+
> > theme_classic()
> > 
> > staticHansPlot
> > ~~~
> > {: .language-r}
> > 
> > <img src="../fig/rmd-01-hansGraphStaticPrettySolution-1.png" title="plot of chunk hansGraphStaticPrettySolution" alt="plot of chunk hansGraphStaticPrettySolution" width="612" style="display: block; margin: auto;" />
> {: .solution}
{: .challenge}


~~~
 staticHansPlot <- ggplot(data = gapminder_data)+
  aes(x = log(gdpPercap), y = lifeExp, size = pop/1000000, color = continent)+
  geom_point(alpha = 0.5) + # we made our points slightly transparent, because it makes it easier to see overlapping points
  scale_color_brewer(palette = "Set1") +
  labs(x = "GDP Per Capita", y = "Life Expectancy", color= "Continent", size="Population (in millions)")+
 theme_classic()

 staticHansPlot
~~~
{: .language-r}

<img src="../fig/rmd-01-hansGraphStatic-1.png" title="plot of chunk hansGraphStatic" alt="plot of chunk hansGraphStatic" width="612" style="display: block; margin: auto;" />

Ok, now we're getting somewhere! But right now we're plotting all of the years
of our dataset on one plot - now we want to animate the plot so each year shows
up on its own. This is where `gganimate` comes in! We want to add the
`transition_states()` function to our plot. (Note that this might not show up as
animated here on the website.) <!-- TODO: see if it works or not. -->


~~~
import plotly.express as px

px.scatter(data_frame=gapminder_data, 
           x="gdpPercap", 
           y="lifeExp", 
           size="pop", 
           animation_frame="year", 
           hover_name="country", 
           color="continent", 
           height=600, 
           size_max=80
           )
~~~
{: .language-python}



<img src="../fig/01-plotting-hansGraphAnimated-1.png" title="plot of chunk hansGraphAnimated" alt="plot of chunk hansGraphAnimated" width="612" style="display: block; margin: auto;" />

Awesome! This is looking sweet! Let's make sure we understand the code above:

1. The first argument of the `transition_states()` function tells `ggplot()`
which variable should be different in each frame of our animation: in this case,
we want each frame to be a different `year`.
1. The `transition_length` and `state_length` arguments are just some of the
`gganimate` arguments you can use to adjust how the animation progresses from
one frame to the next. Feel free to play around with those parameters, to see
how they affect the animation (or check out more `gganmiate` options
[here](https://gganimate.com/articles/gganimate.html)!).
1. Finally, we want the title of our plot to tell us which year our animation is
currently showing. Using "{closest_state}" as our title allows the title of our
plot to show which `year` is currently being plotted.

So we've made this cool animated plot - how do we save it? For `gganimate`
objects, we can use the `anim_save()` function. It works just like `ggsave()`,
but for animated objects.

<!-- TODO: mention renderer / save_animation options -->

~~~
fig = px.scatter(data_frame=gapminder_data, 
           x="gdpPercap", 
           y="lifeExp", 
           size="pop", 
           animation_frame="year", 
           hover_name="country", 
           color="continent", 
           height=600, 
           size_max=80
           )

fig.write_html("hansAnimatedPlot.html")
~~~
{: .language-python}

### Map plots
_[Back to bonus](#bonus)_

The `ggplot` library also has useful functions to draw your data on a map. There
are lots of different ways to draw maps but here's a quick example using the
gampminder data. Here we will plot each country with a color indicating the life
expectancy in 1997.


~~~
# make sure names of countries match between the map info and the data
# NOTE: we haven't learned how to modify the data in this way yet, but we'll learn about that in the next lesson. Just take for granted that it works for now :)
mapdata <- map_data("world") %>%
  mutate(region = recode(region,
                         USA="United States",
                         UK="United Kingdom"))

#install.packages("mapproj")
gapminder_1997 %>%
  ggplot() +
  geom_map(aes(map_id=country, fill=lifeExp), map=mapdata) +
  expand_limits(x = mapdata$long, y = mapdata$lat) +
  coord_map(projection = "mollweide", xlim = c(-180, 180)) +
  ggthemes::theme_map()
~~~
{: .language-r}

<img src="../fig/rmd-01-mapPlots-1.png" title="plot of chunk mapPlots" alt="plot of chunk mapPlots" width="612" style="display: block; margin: auto;" />

Notice that this map helps to show that we actually have some gaps in the data.
We are missing observations for counties like Russia and many countries in
central Africa. Thus, it's important to acknowledge that any patterns or trends
we see in the data might not apply to those regions.

# Glossary of terms
_[Back to top](#contents)_

- Aesthetic: a visual property of the objects (geoms) drawn in your plot (like x position, y position, color, size, etc)
- Aesthetic mapping (aes): This is how we connect a visual property of the plot to a column of our data
- Comments: lines of text in our code after a `#` that are ignored (not evaluated) by R
- Geometry (geom): this describes the things that are actually drawn on the plot (like points or lines)
- Facets: Dividing your data into non-overlapping groups and making a small plot for each subgroup
- Layer: Each ggplot is made up of one or more layers. Each layer contains one geometry and may also contain custom aesthetic mappings and private data
- Factor: a way of storing data to let R know the values are discrete so they get special treatment



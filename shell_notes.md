Shell Notes
================
Rob Taylor
14 December, 2022

### Introduction

These notes simply reflect my learning and the things I found useful. In
part, I’m hoping this works as a reference tool, providing quick access
to some of the more common shell commands.

### Basic Commands

- `pwd`: gets the current working directory.
- `cd`: changes directory to the path provided.
- `..`: used in conjunction with `cd`, shifts up one level in the
  directory hierarchy.
- `ls`: lists the files and folders in the current directory.
- `~`: this is the home path.

**Example**

List the folders in the home path:

``` bash
ls ~
```

    ## Applications
    ## Desktop
    ## Documents
    ## Downloads
    ## Google Drive
    ## Library
    ## Movies
    ## Music
    ## Pictures
    ## Public

### Absolute versus Relative Path

In general, if the path begins with an `/` then it’s absolute;
otherwise, it’s relative. For example, suppose you’re in the directory
`/home/mydir` and there is a file called `myfile.txt` located in it. The
*relative path* to the file is simply

``` bash
myfile.txt
```

That is, because you’re already in the directory you don’t need to
specify the file’s path.

The *absolute path* for the file, however, is

``` bash
/home/mydir/myfile.txt
```

In this case, you can access the file from anywhere because the full
path has been provided.

Listing files in directories works the same way.

``` bash
ls /home/mydir
```

**Example**

From the current directory, list the folders in Documents directory
using an absolute path:

``` bash
ls ~/Documents
```

    ## Technical Analyst Technical Test September 2022.docx
    ## regexcite
    ## rob-macbook-pro-git
    ## stripe

### Changing directories

The `..` notation shifts you up one level to the parent directory. So,
if you wanted to list the contents of the parent directory you can use

``` bash
ls ..
```

    ## Applications
    ## Becasue It's Fun
    ## Blogs
    ## GOPI
    ## Packages
    ## Project List.docx
    ## Publications
    ## _CODE_BASE
    ## d3
    ## shell_basics
    ## test_1.txt

or the directory above that

``` bash
ls ../..
```

    ## AWS
    ## Admin
    ## Algorithms
    ## Archive
    ## Business Admin
    ## Business Overview.gdoc
    ## Excel
    ## Github Setup
    ## Mac essentials.docx
    ## PostgreSQL
    ## Projects
    ## Reference
    ## Resources
    ## SQL
    ## barchart.js
    ## untitled folder.textClipping

You can also navigate using this notation, or using relative and
absolute paths. To change directories you use the `cd` command.

``` bash
cd ../..
pwd
```

    ## /Users/robtaylor/Library/CloudStorage/GoogleDrive-taylor.rt17@gmail.com/My Drive/_Dataforyou

and then list the contents using a relative path

``` bash
ls 
```

    ## README.md
    ## dir
    ## shell_basics.Rproj
    ## shell_notes.Rmd
    ## shell_notes.md

or change the directory using an absolute path, for example

``` bash
cd /home/mydir
```

From home, your root directory is two levels up

``` bash
ls ~/../..
```

    ## Applications
    ## Library
    ## System
    ## Users
    ## Volumes
    ## bin
    ## cores
    ## dev
    ## etc
    ## home
    ## opt
    ## private
    ## sbin
    ## tmp
    ## usr
    ## var

### Creating a File

The simplest way to create a file is to use the redirection operator `>`
or `>>`. The `>` will overwrite an existing file of the same name,
whereas the `>>` will append to it. To create an empty zero line file
you can use the the following

``` bash
> file.txt
```

### Creating and Removing Directories

To create a directory use the `mkdir` command. For example

``` bash
mkdir new_dir
```

or

``` bash
mkdir home/mydir/new_dir
```

To add another folder

``` bash
mkdir home/mydir/new_dir/sub_folder
```

To delete a directory use the `rmdir` command. This will only work if
the directory is empty, so you must delete all files inside first. Note:
the command `rm -r` will do the same thing.

**Project** First, create a file called `original.txt` in current
working directory, and create two folders called `backup`, `test`, and
`moved`

``` bash
> original.txt
mkdir backup test moved
```

Next, create two files in the test folder called `test_1.txt` and
`test_2.txt`

``` bash
> test/test_1.txt 
> test/test_2.txt
ls test
```

    ## test_1.txt
    ## test_2.txt

### Copying Files

To copy a file use the `cp` command. This command makes a simple copy of
the original files. If a file with the same name already exists, then
the copy command will overwrite the existing file.

``` bash
cp old_name.txt new_name.txt
```

If the file simply needed to be copied to a new folder, then you can
specify the destination at the end of the call

``` bash
cp old_name.txt new_folder
```

This will then copy the existing file to the new folder location
`~/new_folder/old_name.txt`. If the file is being copied to a new
location, and given a new name, then the folder and new name needs to be
specified

``` bash
cp old_name.txt new_folder/new_name.txt
```

**Project** Create a new file called `duplicate.txt` by copying
`original.txt`

``` bash
cp original.txt duplicate.txt
ls
```

    ## README.md
    ## backup
    ## dir
    ## duplicate.txt
    ## moved
    ## original.txt
    ## shell_basics.Rproj
    ## shell_notes.Rmd
    ## shell_notes.md
    ## test

Copy both `original.txt` and `duplicate.txt` to the `backup` folder

``` bash
cp original.txt duplicate.txt backup
ls backup
```

    ## duplicate.txt
    ## original.txt

Next, copy the files `test_1.txt` and `test_2.txt` to `backup`, and do
so without changing directories.

``` bash
cp test/test_1.txt test/test_2.txt backup
ls backup
```

    ## duplicate.txt
    ## original.txt
    ## test_1.txt
    ## test_2.txt

Now, copy the file `test/test_1.txt` to `backup` but rename the file
`shifted_test_1.txt`

``` bash
cp test/test_1.txt backup/shifted_test_1.txt
ls backup
```

    ## duplicate.txt
    ## original.txt
    ## shifted_test_1.txt
    ## test_1.txt
    ## test_2.txt

Finally, make a copy of `test_1.txt` in `backup` to the parent directory

``` bash
cp backup/test_1.txt ..
ls ..
```

    ## Applications
    ## Becasue It's Fun
    ## Blogs
    ## GOPI
    ## Packages
    ## Project List.docx
    ## Publications
    ## _CODE_BASE
    ## d3
    ## shell_basics
    ## test_1.txt

### Moving Files

To copy a file use the `mv` command. This command works similarly to
`cp`. To move a file to another directory specify the directory at the
end

``` bash
mv file.txt new_folder
mv file_1.txt file_2.txt new_folder
mv old_folder/file_1.txt new_folder
```

This command can also be used to rename files by creating a new file and
moving the contents of the old file. Like `cp`, if the new file already
exists, it will be overwritten by the old contents.

``` bash
mv old_file.txt new_file.txt
mv old_file.txt new_folder/new_file.txt
mv old_folder/old_file.txt new_folder/new_file.txt
```

This command also works for directories, so it treats folders and paths
like files, but leaves the contents of the renamed folder intact.

``` bash
mv old_folder_name new_folder_name
```

**Project** Move the files `test_1.txt` and `test_2.txt` in the `test`
folder to the `moved` folder

``` bash
mv test/test_1.txt test/test_2.txt moved
ls moved
```

    ## test_1.txt
    ## test_2.txt

Next, rename `test_2.txt` in `moved` to `test_2_renamed.txt`

``` bash
mv moved/test_2.txt moved/test_2_renamed.txt
ls moved
```

    ## test_1.txt
    ## test_2_renamed.txt

Rename the folder `backup` to `backup_new`

``` bash
mv backup backup_new
ls backup_new
```

    ## duplicate.txt
    ## original.txt
    ## shifted_test_1.txt
    ## test_1.txt
    ## test_2.txt

### Deleting Files

To delete a file use the `rm` command. Once the file removed it is not
shifted to the bin, it is removed properly.

``` bash
rm file.txt
rm file_1.txt file_2.txt
rm folder/file.txt
```

**Project** First, remove all files in the `moved` folder. To make
things easier, change directories, delete files, and then change back to
current directory

``` bash
cd moved
rm test_1.txt test_2_renamed.txt
cd ..
```

Next, delete all files in the `backup_new` folder (changing directories)

``` bash
cd backup_new
rm duplicate.txt original.txt shifted_test_1.txt test_2.txt test_1.txt
cd ..
```

Check that both directories are empty

``` bash
ls moved
ls backup_new
```

Finally, remove the directories `backup_new`, `moved`, and `test`

``` bash
rmdir moved backup_new test
```

and remove the files `original.txt` and `duplicate.txt`

``` bash
rm original.txt duplicate.txt
ls
```

    ## README.md
    ## dir
    ## shell_basics.Rproj
    ## shell_notes.Rmd
    ## shell_notes.md

### /tmp Folder

This is where temporary files can be stored and is located below the
root directory

``` bash
ls /
```

    ## Applications
    ## Library
    ## System
    ## Users
    ## Volumes
    ## bin
    ## cores
    ## dev
    ## etc
    ## home
    ## opt
    ## private
    ## sbin
    ## tmp
    ## usr
    ## var

### Viewing contents of file

To view file contents use the `cat` command.

``` bash
cat dir/file.txt
```

    ## This is some text!
    ## Name: Rob Taylor
    ## Street Cred: High

To view just the first few lines of a file use the `head` function

``` bash
head dir/file_list.txt 
```

    ## This is a list of random items I can see:
    ## 01. Computer
    ## 02. Table
    ## 03. Bottle
    ## 04. Chair
    ## 05. Bench
    ## 06. Phone
    ## 07. Notebook
    ## 08. Pen
    ## 09. Cookies

``` bash
head dir/file.txt 
```

    ## This is some text!
    ## Name: Rob Taylor
    ## Street Cred: High

To return a specific number of lines the command line flag `-n` is used
(here n referes to number of lines). Typically, it’s good practice to
specifiy the flag prior to the filename.

``` bash
head -n 5 dir/file_list.txt 
```

    ## This is a list of random items I can see:
    ## 01. Computer
    ## 02. Table
    ## 03. Bottle
    ## 04. Chair

``` bash
head -n 15 dir/file_list.txt 
```

    ## This is a list of random items I can see:
    ## 01. Computer
    ## 02. Table
    ## 03. Bottle
    ## 04. Chair
    ## 05. Bench
    ## 06. Phone
    ## 07. Notebook
    ## 08. Pen
    ## 09. Cookies
    ## 10. Tissue
    ## 11. Candle
    ## 12. Jug
    ## 13. PostIt
    ## 14. Stone

The file `file_list.txt` is much longer than `file.txt`. If we wanted to
see it’s entire contents a useful way to do this is to use `less`. This
command let’s you scroll through the contents of the file. Pressing
space jumps to the bottom half of the file, whereas typing `:p` allows
you to scroll through the contents using the arrow keys. To exit out use
the `:q` command.

``` bash
less dir/file_list.txt
```

### Command Flags

Flags modify the output of shell commands in various ways.

- `-R` shows every file and directory beneath the current directory, no
  matter how deeply nested
- `-F` prints a `/` after the name of every directory and a `*` after
  all executable files. For all other files it places nothing after it.
  This helps determine what is what in the directory.

For example, to see all directories and files in current working
directory run

``` bash
ls -R -F
```

    ## README.md
    ## dir/
    ## shell_basics.Rproj
    ## shell_notes.Rmd
    ## shell_notes.md
    ## 
    ## ./dir:
    ## file.txt
    ## file_list.txt
    ## final.txt
    ## last.txt

The `-F` flag isn’t strictly necessary, but it’s useful to include.

To see everything under the parent folder For example, to see all
directories and files in current working directory run

``` bash
ls -R -F ..
```

    ## Applications/
    ## Becasue It's Fun/
    ## Blogs/
    ## GOPI/
    ## Packages/
    ## Project List.docx
    ## Publications/
    ## _CODE_BASE/
    ## d3/
    ## shell_basics/
    ## test_1.txt
    ## 
    ## ../Applications:
    ## currency-converter/
    ## dashboard_template.R
    ## data-explorer/
    ## data_cleaning/
    ## mean-sse-app/
    ## ml-application/
    ## 
    ## ../Applications/currency-converter:
    ## R/
    ## README.md
    ## app.r
    ## currency-converter-doc.Rmd
    ## currency-converter-doc.md
    ## currency-converter.Rproj
    ## www/
    ## 
    ## ../Applications/currency-converter/R:
    ## global.R
    ## utils.R
    ## 
    ## ../Applications/currency-converter/www:
    ## dropdown.css
    ## 
    ## ../Applications/data-explorer:
    ## README.md
    ## app.r
    ## data-explorer.Rproj
    ## 
    ## ../Applications/data_cleaning:
    ## data_clean/
    ## 
    ## ../Applications/data_cleaning/data_clean:
    ## R/
    ## server.R
    ## ui.R
    ## 
    ## ../Applications/data_cleaning/data_clean/R:
    ## mod_load_data.R
    ## 
    ## ../Applications/mean-sse-app:
    ## README.md
    ## app.R
    ## mean-sse-app.Rproj
    ## 
    ## ../Applications/ml-application:
    ## R/
    ## README.md
    ## app.R
    ## ml-application.Rproj
    ## www/
    ## 
    ## ../Applications/ml-application/R:
    ## global.R
    ## 
    ## ../Applications/ml-application/www:
    ## dropdown.css
    ## 
    ## ../Becasue It's Fun:
    ## Mental Health New Zealand/
    ## New Zealand Football Results/
    ## 
    ## ../Becasue It's Fun/Mental Health New Zealand:
    ## 2021_rc_pop_estimates.csv
    ## 2021_ta_pop_estimates.csv
    ## Occ Type_Full Data_data.csv
    ## app/
    ## clean_data.R
    ## mental_health_data.rds
    ## mental_health_nz 2.Rmd
    ## mental_health_nz 2.html
    ## mental_health_nz 3.Rmd
    ## mental_health_nz 3.html
    ## mental_health_nz 4.Rmd
    ## mental_health_nz 4.html
    ## mental_health_nz 5.Rmd
    ## mental_health_nz 5.html
    ## mental_health_nz.Rmd
    ## mental_health_nz.html
    ## mental_health_nz.knit 2.md
    ## mental_health_nz.knit 3.md
    ## mental_health_nz.knit 4.md
    ## mental_health_nz.knit.md
    ## 
    ## ../Becasue It's Fun/Mental Health New Zealand/app:
    ## app.R
    ## data/
    ## 
    ## ../Becasue It's Fun/Mental Health New Zealand/app/data:
    ## mental_health_data.rds
    ## test.gpkg
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results:
    ## data_processing/
    ## football-app/
    ## nzfootball-app/
    ## project_overview.Rmd
    ## project_overview.html
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/data_processing:
    ## data/
    ## src/
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/data_processing/data:
    ## database_tables.RData
    ## source_data.RData
    ## yearly_fixtures.RData
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/data_processing/src:
    ## create_tables.R
    ## source_update_data.R
    ## summary_tables.R
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/football-app:
    ## fun/
    ## old/
    ## server.R
    ## ui.R
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/football-app/fun:
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/football-app/old:
    ## app.R
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/nzfootball-app:
    ## data/
    ## global.R
    ## server.R
    ## ui.R
    ## 
    ## ../Becasue It's Fun/New Zealand Football Results/nzfootball-app/data:
    ## yearly_fixtures.RData
    ## 
    ## ../Blogs:
    ## 000_Multicolinearity_problem_or_not/
    ## 001_A_case_for_a_duel_axe_attack/
    ## 002_Central_tendencies_part_1_arithmetic_mean/
    ## 003_Confidence_Intervals/
    ## 004_Probability_v_likelihood/
    ## 005_Maximimum_likelihood_estimation/
    ## 006_Lets_talk_about_averages/
    ## 007_Linear_digressions/
    ## 008_Kicking_it_with_the_Poisson_distirbution/
    ## 009_Probability_Odds_Log_Odds/
    ## Wald and his plane.docx
    ## poisson_distribution.png
    ## 
    ## ../Blogs/000_Multicolinearity_problem_or_not:
    ## Multicollinearity.docx
    ## matrix_stuff.R
    ## 
    ## ../Blogs/001_A_case_for_a_duel_axe_attack:
    ## Doubling up your axes.docx
    ## case_1_base_plot.png
    ## case_1_final_plot.png
    ## case_2_base_plot.png
    ## case_2_final_plot.png
    ## case_2_raw_plot.png
    ## double_axis_plots.R
    ## 
    ## ../Blogs/002_Central_tendencies_part_1_arithmetic_mean:
    ## 
    ## ../Blogs/003_Confidence_Intervals:
    ## Confidence Intervals.docx
    ## ICOTS10_8A2.pdf
    ## 
    ## ../Blogs/004_Probability_v_likelihood:
    ## plot_figures.R
    ## prob_v_like.png
    ## 
    ## ../Blogs/005_Maximimum_likelihood_estimation:
    ## scrapbook.R
    ## 
    ## ../Blogs/006_Lets_talk_about_averages:
    ## 
    ## ../Blogs/007_Linear_digressions:
    ## CodeCogsEqn.svg
    ## code.R
    ## model_plot.png
    ## sim_plot.png
    ## 
    ## ../Blogs/008_Kicking_it_with_the_Poisson_distirbution:
    ## poisson_bayes_horse_kicks/
    ## 
    ## ../Blogs/008_Kicking_it_with_the_Poisson_distirbution/poisson_bayes_horse_kicks:
    ## README.md
    ## bayes.R
    ## data/
    ## figs/
    ## main.R
    ## poisson_bayes_horse_kicks.Rproj
    ## samples/
    ## src/
    ## 
    ## ../Blogs/008_Kicking_it_with_the_Poisson_distirbution/poisson_bayes_horse_kicks/data:
    ## Prussion Horse-Kick Data.csv*
    ## 
    ## ../Blogs/008_Kicking_it_with_the_Poisson_distirbution/poisson_bayes_horse_kicks/figs:
    ## bayes_plots.png
    ## plot_mle.png
    ## plot_pooled.png
    ## 
    ## ../Blogs/008_Kicking_it_with_the_Poisson_distirbution/poisson_bayes_horse_kicks/samples:
    ## pooled_samples.Rdata
    ## 
    ## ../Blogs/008_Kicking_it_with_the_Poisson_distirbution/poisson_bayes_horse_kicks/src:
    ## bayes.R
    ## code.R
    ## functions.R
    ## model_conjugate.txt
    ## model_conjugate_hier.txt
    ## 
    ## ../Blogs/009_Probability_Odds_Log_Odds:
    ## Probability, Odds, and Log Odds.docx
    ## code.R
    ## plot.png
    ## 
    ## ../GOPI:
    ## 2016_surevey_data_raw.rds
    ## dash/
    ## data/
    ## data_extract.R
    ## data_shaping.R
    ## dev_analysis.R
    ## dev_maps.R
    ## geocodes.csv
    ## geocodes.xlsx
    ## report_reference.csv
    ## reports/
    ## 
    ## ../GOPI/dash:
    ## R/
    ## app.R
    ## archive/
    ## data/
    ## styles.css
    ## 
    ## ../GOPI/dash/R:
    ## global.R
    ## 
    ## ../GOPI/dash/archive:
    ## app.R
    ## 
    ## ../GOPI/dash/data:
    ## complete_survey_data_long.rds
    ## geocodes.csv
    ## survey_ref_tables.rds
    ## 
    ## ../GOPI/data:
    ## 2013_survey_data_long.rds
    ## 2013_survey_data_raw.rds
    ## 2013_survey_data_wide.rds
    ## 2016_survey_data_long.rds
    ## 2016_survey_data_raw.rds
    ## 2016_survey_data_wide.rds
    ## 2020_survey_data_long.rds
    ## 2020_survey_data_wide.rds
    ## 2020_survey_ref_tables.rds
    ## complete_survey_data_long.rds
    ## complete_survey_data_wide.rds
    ## initial_extract.rds
    ## survey_ref_tables.rds
    ## 
    ## ../GOPI/reports:
    ## GOPI-cockle-survey-1992.pdf
    ## GOPI-cockle-survey-1995.pdf
    ## GOPI-cockle-survey-1998.pdf
    ## GOPI-cockle-survey-2001.pdf
    ## GOPI-cockle-survey-2004.pdf
    ## GOPI-cockle-survey-2007.pdf
    ## GOPI-cockle-survey-2010.pdf
    ## GOPI-cockle-survey-2013.pdf
    ## GOPI-cockle-survey-2016.pdf
    ## GOPI-cockle-survey-2020.pdf
    ## 
    ## ../Packages:
    ## binomBayes/
    ## initalise_package.R
    ## test/
    ## 
    ## ../Packages/binomBayes:
    ## DESCRIPTION
    ## NAMESPACE
    ## R/
    ## README.md
    ## binomBayes.Rproj
    ## man/
    ## 
    ## ../Packages/binomBayes/R:
    ## get_posterior.R
    ## helpers.R
    ## 
    ## ../Packages/binomBayes/man:
    ## get_posterior.Rd
    ## 
    ## ../Packages/test:
    ## DESCRIPTION
    ## NAMESPACE
    ## R/
    ## test.Rproj
    ## 
    ## ../Packages/test/R:
    ## 
    ## ../Publications:
    ## maximum_likelihhod_estimation.aux
    ## maximum_likelihhod_estimation.bbl
    ## maximum_likelihhod_estimation.blg
    ## maximum_likelihhod_estimation.log
    ## maximum_likelihhod_estimation.pdf
    ## maximum_likelihhod_estimation.synctex.gz
    ## maximum_likelihhod_estimation.tex
    ## 
    ## ../_CODE_BASE:
    ## Shiny/
    ## useful_r_code.R
    ## 
    ## ../_CODE_BASE/Shiny:
    ## R/
    ## app.R
    ## dist_function_helpers 2.R
    ## dist_function_helpers.R
    ## selectize.bootstrap3.css
    ## www/
    ## 
    ## ../_CODE_BASE/Shiny/R:
    ## 
    ## ../_CODE_BASE/Shiny/www:
    ## dfy_logo_1.png
    ## dfy_logo_2 2.png
    ## dfy_logo_2.png
    ## dfy_theme.css
    ## logo_1.svg
    ## 
    ## ../d3:
    ## axes/
    ## bar-event-listener/
    ## csv-import/
    ## d3.js
    ## d3.min.js
    ## project-folder/
    ## simple-bar/
    ## simple-html/
    ## simple-scatter/
    ## start_local_server.txt
    ## 
    ## ../d3/axes:
    ## d3.js
    ## svg-dynamic-scatter.html
    ## 
    ## ../d3/bar-event-listener:
    ## bar-dynamic.html
    ## d3.js
    ## test.html
    ## test_1.html
    ## 
    ## ../d3/csv-import:
    ## csv-import.html
    ## d3.js
    ## food.csv
    ## 
    ## ../d3/project-folder:
    ## d3.js
    ## d3.min.js
    ## index.html
    ## package/
    ## 
    ## ../d3/project-folder/package:
    ## LICENSE
    ## README.md
    ## dist/
    ## package.json
    ## src/
    ## 
    ## ../d3/project-folder/package/dist:
    ## d3.js
    ## d3.min.js
    ## 
    ## ../d3/project-folder/package/src:
    ## index.js
    ## 
    ## ../d3/simple-bar:
    ## bar-dynamic.html
    ## d3.js
    ## div-bar.html
    ## svg-bar.html
    ## 
    ## ../d3/simple-html:
    ## html_template.html
    ## styles.css
    ## 
    ## ../d3/simple-scatter:
    ## d3.js
    ## svg-dynamic-scatter.html
    ## svg-scatter.html
    ## 
    ## ../shell_basics:
    ## README.md
    ## dir/
    ## shell_basics.Rproj
    ## shell_notes.Rmd
    ## shell_notes.md
    ## 
    ## ../shell_basics/dir:
    ## file.txt
    ## file_list.txt
    ## final.txt
    ## last.txt

### Help

To see what a function does use the `man` command. To exit press `:q`.

### History

To get recently used commands you can simply use the up-arrow key to
scroll through. However, an easier way to see all previous commands is
to use `history`

``` bash
history
```

A numbered list of commands is then printed. To rerun an earlier command
you can use ! plus the number. For example, to rerun the 113th command
use `!113`.

``` bash
!113
```

Another approach is to use in ! front of the last command used. For
example, to rerun the last `head` command `!head` can be used.

### Using grep

The `grep` command is used to select rows that contain specific pieces
of text. It can also be used to search for regualr expressions and
patterns. It takes the following flags

- `-c`: print a count of the matching lines rather than the lines
- `-h`: do not print the names of files when searching multiple files
- `-i`: ignore case (e.g., treat “Regression” and “regression” as
  matches)
- `-l`: print the names of files that contain matches, not the matches
- `-n`: print line numbers for matching lines
- `-v`: invert the match, i.e., only show lines that don’t match

For example, to search for specific items in `file_list.txt` we can use
`grep` to search for them.

``` bash
grep Stone dir/file_list.txt
```

    ## 14. Stone

Rather then remember whether items were capitalized we can supply a flag
to ignore case

``` bash
grep -i stone dir/file_list.txt
```

    ## 14. Stone

If the line number is required then the following can be used

``` bash
grep -i -n stone dir/file_list.txt
```

    ## 15:14. Stone

To count the number of lines use

``` bash
grep -i -c stone dir/file_list.txt
```

    ## 1

You can also supply multiple files

``` bash
grep -i -c stone dir/file_list.txt dir/file.txt    
```

    ## dir/file_list.txt:1
    ## dir/file.txt:0

### Saving Outputs

The redirection operator `>` can be used to assign outputs to a
specified file. For example, to save the last 5 lines of `file_list.txt`
to a file called `last.txt` use

``` bash
tail -n 5 dir/file_list.txt > dir/last.txt
ls dir
```

    ## file.txt
    ## file_list.txt
    ## final.txt
    ## last.txt

To check that it’s work, print the file to the console

``` bash
cat dir/last.txt
```

    ## 16. Speaker
    ## 17. Faucet
    ## 18. Coffee
    ## 19. Glass
    ## 20. Iron

However, what if you wanted to only get items 16, 17, and 18. One way to
do this is to first create `last.txt` as above and then use the `head`
command to retrieve the top three rows

``` bash
head -n 3 dir/last.txt
```

    ## 16. Speaker
    ## 17. Faucet
    ## 18. Coffee

This works, but can be a little awkward. Instead, the pipe operator `|`
can be used to string command together (much like tidyverse). To get the
exact same result the following can be run

``` bash
tail -n 5 dir/file_list.txt | head -n 3 
```

    ## 16. Speaker
    ## 17. Faucet
    ## 18. Coffee

Note that no intermediate file need to be saved. Now the final results
can be saved to an output file called `final.txt`

``` bash
tail -n 5 dir/file_list.txt | head -n 3 > dir/final.txt
ls dir
```

    ## file.txt
    ## file_list.txt
    ## final.txt
    ## last.txt

Confirming output is correct

``` bash
cat dir/final.txt
```

    ## 16. Speaker
    ## 17. Faucet
    ## 18. Coffee

If you then only wanted to view all items that aren’t ‘Coffee’ use
`grep` with an inverted match

``` bash
tail -n 5 dir/file_list.txt | head -n 3 | grep -v Coffee 
```

    ## 16. Speaker
    ## 17. Faucet

### Word Count

The command `wc` (word count) counts text in files. The following flags
are availbale:

- `-c` count the number of characters
- `-l` count the number of lines
- `-w` count the number of words

For example, the following counts the number of lines following the
earlier piping

``` bash
tail -n 5 dir/file_list.txt | head -n 3 | wc -l 
```

    ##        3

Or, count the number of characters for the line with ‘Coffee’

``` bash
tail -n 5 dir/file_list.txt | head -n 3 | grep Coffee | wc -c
```

    ##       11

### Wildcards

Rather than writing out file paths in full wildcards can be used. One
very useful wildcard is `*` which matches all characters. For example,
to get the first 2 lines in `file.txt` and `file_list.txt`, but not
`final.txt` or `last.txt` the following command can be used

``` bash
head -n 2 dir/fil*.txt
```

    ## ==> dir/file.txt <==
    ## This is some text!
    ## Name: Rob Taylor
    ## 
    ## ==> dir/file_list.txt <==
    ## This is a list of random items I can see:
    ## 01. Computer

To get the first three lines of all files the following command can be
used

``` bash
head -n 3 dir/*
```

    ## ==> dir/file.txt <==
    ## This is some text!
    ## Name: Rob Taylor
    ## Street Cred: High
    ## 
    ## ==> dir/file_list.txt <==
    ## This is a list of random items I can see:
    ## 01. Computer
    ## 02. Table
    ## 
    ## ==> dir/final.txt <==
    ## 16. Speaker
    ## 17. Faucet
    ## 18. Coffee
    ## 
    ## ==> dir/last.txt <==
    ## 16. Speaker
    ## 17. Faucet
    ## 18. Coffee

Other wildcards include:

- `?`: matches a single character. For example, `202?.txt` will match
  `2021.txt` and `2022.txt`, but not `2022_new.txt`.
- `[...]`: matches any one of the characters inside the square brackets.
  For example, `202[12].txt` will match `2021.txt` and `2022.txt`, but
  not `2020.txt`.
- `{...}`: matches any of the comma-separated patterns inside the curly
  brackets. For example, `{*.txt, *.csv}` will match all `.txt` and all
  `.csv` files, but not `.pdf` files.

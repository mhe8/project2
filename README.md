Project 1: predictive models
================
Min He
July 2, 2020 (updated 2020-07-03)

## Introduction about the data

This dataset summarizes a heterogeneous set of features about articles
published by Mashable in a period of two years. The goal is to predict
the number of shares in social networks (popularity).
[source](https://archive.ics.uci.edu/ml/datasets/Online+News+Popularity).
In this project, I will try to use the logistic regression and bagging
to classify whether the shares exceeds 1400 or not.

## Generate the report for all days automatically

``` r
#get unique days
days <-  c("Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday")
# output_file <- paste0(days,"Analysis.md")
# params = lapply(days,FUN = function(x){list(weekday = x)})
# reports <- tibble(output_file,params)
# apply(reports, MARGIN =1,FUN = function(x){rmarkdown::render(input="Project2.Rmd",output_file=x[[1]],params=x[[2]])})
for(d in days){
  #create filenames
  output_file <- paste0( d, 'Analysis', ".md")
  #create a list for each team with just the team name parameter
  d
  render("Project2.Rmd", output_file = output_file, params = list(weekday = d))
}
```

    ##   |                                                                              |                                                                      |   0%  |                                                                              |...                                                                   |   4%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |.....                                                                 |   7%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |........                                                              |  11%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........                                                            |  15%
    ## label: unnamed-chunk-1

    ## Warning in in_dir(input_dir(), evaluate(code, envir = env, new_device = FALSE, :
    ## You changed the working directory to /home/aaron/Documents/NCSU_MinHe/ST558/
    ## project2_question (probably via setwd()). It will be restored to /home/aaron/
    ## Documents/NCSU_MinHe/ST558/Project2. See the Note section in ?knitr::knit

    ##   |                                                                              |.............                                                         |  19%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................                                                      |  22%
    ## label: unnamed-chunk-2
    ##   |                                                                              |..................                                                    |  26%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.....................                                                 |  30%
    ## label: unnamed-chunk-3
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........................                                            |  37%
    ## label: unnamed-chunk-4
    ##   |                                                                              |.............................                                         |  41%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................                                       |  44%
    ## label: unnamed-chunk-5

    ##   |                                                                              |..................................                                    |  48%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  52%
    ## label: unnamed-chunk-6

    ##   |                                                                              |.......................................                               |  56%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................                             |  59%
    ## label: unnamed-chunk-7

    ##   |                                                                              |............................................                          |  63%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: unnamed-chunk-8
    ##   |                                                                              |.................................................                     |  70%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................................                  |  74%
    ## label: unnamed-chunk-9
    ##   |                                                                              |......................................................                |  78%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  81%
    ## label: unnamed-chunk-10
    ##   |                                                                              |............................................................          |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............................................................        |  89%
    ## label: unnamed-chunk-11
    ##   |                                                                              |.................................................................     |  93%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...................................................................   |  96%
    ## label: unnamed-chunk-12
    ##   |                                                                              |......................................................................| 100%
    ##   ordinary text without R code
    ## 
    ## 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS Project2.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output MondayAnalysis.md --standalone --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/default.md 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS MondayAnalysis.md --to html4 --from gfm --output MondayAnalysis.html --standalone --self-contained --highlight-style pygments --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/preview.html --variable 'github-markdown-css:/home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/github.css' --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |...                                                                   |   4%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |.....                                                                 |   7%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |........                                                              |  11%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........                                                            |  15%
    ## label: unnamed-chunk-1

    ## Warning in in_dir(input_dir(), evaluate(code, envir = env, new_device = FALSE, :
    ## You changed the working directory to /home/aaron/Documents/NCSU_MinHe/ST558/
    ## project2_question (probably via setwd()). It will be restored to /home/aaron/
    ## Documents/NCSU_MinHe/ST558/Project2. See the Note section in ?knitr::knit

    ##   |                                                                              |.............                                                         |  19%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................                                                      |  22%
    ## label: unnamed-chunk-2
    ##   |                                                                              |..................                                                    |  26%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.....................                                                 |  30%
    ## label: unnamed-chunk-3
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........................                                            |  37%
    ## label: unnamed-chunk-4
    ##   |                                                                              |.............................                                         |  41%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................                                       |  44%
    ## label: unnamed-chunk-5

    ##   |                                                                              |..................................                                    |  48%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  52%
    ## label: unnamed-chunk-6

    ##   |                                                                              |.......................................                               |  56%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................                             |  59%
    ## label: unnamed-chunk-7

    ##   |                                                                              |............................................                          |  63%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: unnamed-chunk-8
    ##   |                                                                              |.................................................                     |  70%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................................                  |  74%
    ## label: unnamed-chunk-9
    ##   |                                                                              |......................................................                |  78%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  81%
    ## label: unnamed-chunk-10
    ##   |                                                                              |............................................................          |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............................................................        |  89%
    ## label: unnamed-chunk-11
    ##   |                                                                              |.................................................................     |  93%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...................................................................   |  96%
    ## label: unnamed-chunk-12
    ##   |                                                                              |......................................................................| 100%
    ##   ordinary text without R code
    ## 
    ## 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS Project2.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output TuesdayAnalysis.md --standalone --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/default.md 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS TuesdayAnalysis.md --to html4 --from gfm --output TuesdayAnalysis.html --standalone --self-contained --highlight-style pygments --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/preview.html --variable 'github-markdown-css:/home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/github.css' --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |...                                                                   |   4%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |.....                                                                 |   7%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |........                                                              |  11%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........                                                            |  15%
    ## label: unnamed-chunk-1

    ## Warning in in_dir(input_dir(), evaluate(code, envir = env, new_device = FALSE, :
    ## You changed the working directory to /home/aaron/Documents/NCSU_MinHe/ST558/
    ## project2_question (probably via setwd()). It will be restored to /home/aaron/
    ## Documents/NCSU_MinHe/ST558/Project2. See the Note section in ?knitr::knit

    ##   |                                                                              |.............                                                         |  19%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................                                                      |  22%
    ## label: unnamed-chunk-2
    ##   |                                                                              |..................                                                    |  26%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.....................                                                 |  30%
    ## label: unnamed-chunk-3
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........................                                            |  37%
    ## label: unnamed-chunk-4
    ##   |                                                                              |.............................                                         |  41%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................                                       |  44%
    ## label: unnamed-chunk-5

    ##   |                                                                              |..................................                                    |  48%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  52%
    ## label: unnamed-chunk-6

    ##   |                                                                              |.......................................                               |  56%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................                             |  59%
    ## label: unnamed-chunk-7

    ##   |                                                                              |............................................                          |  63%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: unnamed-chunk-8
    ##   |                                                                              |.................................................                     |  70%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................................                  |  74%
    ## label: unnamed-chunk-9
    ##   |                                                                              |......................................................                |  78%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  81%
    ## label: unnamed-chunk-10
    ##   |                                                                              |............................................................          |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............................................................        |  89%
    ## label: unnamed-chunk-11
    ##   |                                                                              |.................................................................     |  93%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...................................................................   |  96%
    ## label: unnamed-chunk-12
    ##   |                                                                              |......................................................................| 100%
    ##   ordinary text without R code
    ## 
    ## 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS Project2.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output WednesdayAnalysis.md --standalone --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/default.md 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS WednesdayAnalysis.md --to html4 --from gfm --output WednesdayAnalysis.html --standalone --self-contained --highlight-style pygments --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/preview.html --variable 'github-markdown-css:/home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/github.css' --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |...                                                                   |   4%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |.....                                                                 |   7%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |........                                                              |  11%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........                                                            |  15%
    ## label: unnamed-chunk-1

    ## Warning in in_dir(input_dir(), evaluate(code, envir = env, new_device = FALSE, :
    ## You changed the working directory to /home/aaron/Documents/NCSU_MinHe/ST558/
    ## project2_question (probably via setwd()). It will be restored to /home/aaron/
    ## Documents/NCSU_MinHe/ST558/Project2. See the Note section in ?knitr::knit

    ##   |                                                                              |.............                                                         |  19%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................                                                      |  22%
    ## label: unnamed-chunk-2
    ##   |                                                                              |..................                                                    |  26%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.....................                                                 |  30%
    ## label: unnamed-chunk-3
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........................                                            |  37%
    ## label: unnamed-chunk-4
    ##   |                                                                              |.............................                                         |  41%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................                                       |  44%
    ## label: unnamed-chunk-5

    ##   |                                                                              |..................................                                    |  48%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  52%
    ## label: unnamed-chunk-6

    ##   |                                                                              |.......................................                               |  56%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................                             |  59%
    ## label: unnamed-chunk-7

    ##   |                                                                              |............................................                          |  63%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: unnamed-chunk-8
    ##   |                                                                              |.................................................                     |  70%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................................                  |  74%
    ## label: unnamed-chunk-9
    ##   |                                                                              |......................................................                |  78%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  81%
    ## label: unnamed-chunk-10
    ##   |                                                                              |............................................................          |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............................................................        |  89%
    ## label: unnamed-chunk-11
    ##   |                                                                              |.................................................................     |  93%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...................................................................   |  96%
    ## label: unnamed-chunk-12
    ##   |                                                                              |......................................................................| 100%
    ##   ordinary text without R code
    ## 
    ## 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS Project2.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output ThursdayAnalysis.md --standalone --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/default.md 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS ThursdayAnalysis.md --to html4 --from gfm --output ThursdayAnalysis.html --standalone --self-contained --highlight-style pygments --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/preview.html --variable 'github-markdown-css:/home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/github.css' --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |...                                                                   |   4%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |.....                                                                 |   7%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |........                                                              |  11%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........                                                            |  15%
    ## label: unnamed-chunk-1

    ## Warning in in_dir(input_dir(), evaluate(code, envir = env, new_device = FALSE, :
    ## You changed the working directory to /home/aaron/Documents/NCSU_MinHe/ST558/
    ## project2_question (probably via setwd()). It will be restored to /home/aaron/
    ## Documents/NCSU_MinHe/ST558/Project2. See the Note section in ?knitr::knit

    ##   |                                                                              |.............                                                         |  19%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................                                                      |  22%
    ## label: unnamed-chunk-2
    ##   |                                                                              |..................                                                    |  26%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.....................                                                 |  30%
    ## label: unnamed-chunk-3
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........................                                            |  37%
    ## label: unnamed-chunk-4
    ##   |                                                                              |.............................                                         |  41%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................                                       |  44%
    ## label: unnamed-chunk-5

    ##   |                                                                              |..................................                                    |  48%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  52%
    ## label: unnamed-chunk-6

    ##   |                                                                              |.......................................                               |  56%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................                             |  59%
    ## label: unnamed-chunk-7

    ##   |                                                                              |............................................                          |  63%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: unnamed-chunk-8
    ##   |                                                                              |.................................................                     |  70%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................................                  |  74%
    ## label: unnamed-chunk-9
    ##   |                                                                              |......................................................                |  78%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  81%
    ## label: unnamed-chunk-10
    ##   |                                                                              |............................................................          |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............................................................        |  89%
    ## label: unnamed-chunk-11
    ##   |                                                                              |.................................................................     |  93%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...................................................................   |  96%
    ## label: unnamed-chunk-12
    ##   |                                                                              |......................................................................| 100%
    ##   ordinary text without R code
    ## 
    ## 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS Project2.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output FridayAnalysis.md --standalone --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/default.md 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS FridayAnalysis.md --to html4 --from gfm --output FridayAnalysis.html --standalone --self-contained --highlight-style pygments --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/preview.html --variable 'github-markdown-css:/home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/github.css' --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |...                                                                   |   4%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |.....                                                                 |   7%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |........                                                              |  11%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........                                                            |  15%
    ## label: unnamed-chunk-1

    ## Warning in in_dir(input_dir(), evaluate(code, envir = env, new_device = FALSE, :
    ## You changed the working directory to /home/aaron/Documents/NCSU_MinHe/ST558/
    ## project2_question (probably via setwd()). It will be restored to /home/aaron/
    ## Documents/NCSU_MinHe/ST558/Project2. See the Note section in ?knitr::knit

    ##   |                                                                              |.............                                                         |  19%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................                                                      |  22%
    ## label: unnamed-chunk-2
    ##   |                                                                              |..................                                                    |  26%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.....................                                                 |  30%
    ## label: unnamed-chunk-3
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........................                                            |  37%
    ## label: unnamed-chunk-4
    ##   |                                                                              |.............................                                         |  41%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................                                       |  44%
    ## label: unnamed-chunk-5

    ##   |                                                                              |..................................                                    |  48%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  52%
    ## label: unnamed-chunk-6

    ##   |                                                                              |.......................................                               |  56%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................                             |  59%
    ## label: unnamed-chunk-7

    ##   |                                                                              |............................................                          |  63%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: unnamed-chunk-8
    ##   |                                                                              |.................................................                     |  70%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................................                  |  74%
    ## label: unnamed-chunk-9
    ##   |                                                                              |......................................................                |  78%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  81%
    ## label: unnamed-chunk-10
    ##   |                                                                              |............................................................          |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............................................................        |  89%
    ## label: unnamed-chunk-11
    ##   |                                                                              |.................................................................     |  93%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...................................................................   |  96%
    ## label: unnamed-chunk-12
    ##   |                                                                              |......................................................................| 100%
    ##   ordinary text without R code
    ## 
    ## 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS Project2.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output SaturdayAnalysis.md --standalone --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/default.md 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS SaturdayAnalysis.md --to html4 --from gfm --output SaturdayAnalysis.html --standalone --self-contained --highlight-style pygments --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/preview.html --variable 'github-markdown-css:/home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/github.css' --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |...                                                                   |   4%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |.....                                                                 |   7%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |........                                                              |  11%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........                                                            |  15%
    ## label: unnamed-chunk-1

    ## Warning in in_dir(input_dir(), evaluate(code, envir = env, new_device = FALSE, :
    ## You changed the working directory to /home/aaron/Documents/NCSU_MinHe/ST558/
    ## project2_question (probably via setwd()). It will be restored to /home/aaron/
    ## Documents/NCSU_MinHe/ST558/Project2. See the Note section in ?knitr::knit

    ##   |                                                                              |.............                                                         |  19%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................                                                      |  22%
    ## label: unnamed-chunk-2
    ##   |                                                                              |..................                                                    |  26%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.....................                                                 |  30%
    ## label: unnamed-chunk-3
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..........................                                            |  37%
    ## label: unnamed-chunk-4
    ##   |                                                                              |.............................                                         |  41%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................                                       |  44%
    ## label: unnamed-chunk-5

    ##   |                                                                              |..................................                                    |  48%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  52%
    ## label: unnamed-chunk-6

    ##   |                                                                              |.......................................                               |  56%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................                             |  59%
    ## label: unnamed-chunk-7

    ##   |                                                                              |............................................                          |  63%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: unnamed-chunk-8
    ##   |                                                                              |.................................................                     |  70%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................................                  |  74%
    ## label: unnamed-chunk-9
    ##   |                                                                              |......................................................                |  78%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  81%
    ## label: unnamed-chunk-10
    ##   |                                                                              |............................................................          |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............................................................        |  89%
    ## label: unnamed-chunk-11
    ##   |                                                                              |.................................................................     |  93%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...................................................................   |  96%
    ## label: unnamed-chunk-12
    ##   |                                                                              |......................................................................| 100%
    ##   ordinary text without R code
    ## 
    ## 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS Project2.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output SundayAnalysis.md --standalone --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/default.md 
    ## /usr/lib/rstudio/bin/pandoc/pandoc +RTS -K512m -RTS SundayAnalysis.md --to html4 --from gfm --output SundayAnalysis.html --standalone --self-contained --highlight-style pygments --template /home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/preview.html --variable 'github-markdown-css:/home/aaron/R/x86_64-pc-linux-gnu-library/4.0/rmarkdown/rmarkdown/templates/github_document/resources/github.css' --email-obfuscation none --metadata pagetitle=PREVIEW

The analysis for [Monday is available here](MondayAnalysis.md) The
analysis for [Tuesday is available here](TuesdayAnalysis.md) The
analysis for [Wednesday is available here](WednesdayAnalysis.md) The
analysis for [Thursday is available here](ThursdayAnalysis.md) The
analysis for [Friday is available here](FridayAnalysis.md) The analysis
for [Saturday is available here](SaturdayAnalysis.md) The analysis for
[Sunday is available here](SundayAnalysis.md)

# decampr

<!-- badges: start -->
<!-- badges: end -->

`decampr` consists of some simple utilities to process R-based DataCamp lessons to Ines' gatsby/binder based course setup available here: https://github.com/ines/course-starter-r 

`decampr` speeds up building courses by parsing the DataCamp format and outputting the correct files (chapter.mds, exercises, solutions, and multiple choice questions).   

Note that I'm not a regular expression master and I don't have access to any DataCamp repositories other than my own online one. If you have an example chapter and would like to contribute it, please add a PR and put it in `inst/extdata`. 

## Installation

You can install the github version of `decampr` with:

``` r
install.packages("remotes")
remotes::install_github("laderast/decampr")
```

## Prepping your DataCamp Repo

`decampr` is based on some rather fragile regular expressions, particularly for extracting the exercise code. It assumes that you have at least two linebreaks separating each exercise. That is:

```

```

Make sure the last exercise also has at least two linebreaks and is followed by a `---`.

## Using `decampr`

`decampr` assumes that your datacamp repo is local to your system.

The first thing to do is to use `usethis::create_from_github()` to clone Ines' basic course repository

```r
usethis::create_from_github("ines/course-starter-r")
```

This will clone the repo to your computer (by default, it saves it to your Desktop) and open up a new project with your cloned repo.

Now you can start processing your DataCamp repo:

``` r
library(decampr)
repo_path <- "c:/Code/RBootcamp-old"

#get all chapters in the repo path
chapter_list <- get_chapters(repo_path)

#get all exercises for chapter 1
exercise_list <- get_exercises(chapter_list[[1]])

#extract exercise information
exercise_list <- parse_exercise_list(test_list)

#number the exercises
exercise_list <- number_ex_list(exercise_list, basename = "01")

#save the exercises and rewritten chapter.md
save_exercise_list(exercise_list, "chapter1.md")
```

Exercises/solutions will be written to `exercises/` and the chapter.md files will be written to `chapters/`. 

## Contributing

Please note that the 'decampr' project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By contributing to this project, you agree to abide by its terms.

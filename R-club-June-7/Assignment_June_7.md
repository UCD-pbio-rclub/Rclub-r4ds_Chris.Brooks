# R Notebook

Assignment June 7 



```r
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```




```r
read_csv("a,b,c
1,2,3
4,5,6")
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

```r
#> # A tibble: 2 × 3
#>       a     b     c
#>   <int> <int> <int>
#> 1     1     2     3
#> 2     4     5     6
```




```r
read_csv("The first line of metadata
  The second line of metadata
  x,y,z
  1,2,3", skip = 2)
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

```r
#> # A tibble: 1 × 3
#>       x     y     z
#>   <int> <int> <int>
#> 1     1     2     3

read_csv("# A comment I want to skip
  x,y,z
  1,2,3", comment = "#")
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```

```r
#> # A tibble: 1 × 3
#>       x     y     z
#>   <int> <int> <int>
#> 1     1     2     3
```



```r
read_csv("1,2,3\n4,5,6", col_names = FALSE)
```

```
## # A tibble: 2 × 3
##      X1    X2    X3
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

```r
#> # A tibble: 2 × 3
#>      X1    X2    X3
#>   <int> <int> <int>
#> 1     1     2     3
#> 2     4     5     6
```


### Exercise 11.2.2



##### question 1

What function would you use to read a file where fields were separated with
“|”?


```r
?read_delim()
```


You could use read_delim, and specify the delim as |.


##### question 2



```r
# Apart from file, skip, and comment, what other arguments do read_csv() and read_tsv() have in common?

?read_csv
?read_tsv
```


They also have col_names, col_types, locale, na = , quote, trim_ws, n_max, progress bar, and guess_max.


##### Question 3


```r
#What are the most important arguments to read_fwf()?

?read_fwf
```

Col_positions, which are created by fwf_widths or fwf_positions


##### question 4


```r
#Sometimes strings in a CSV file contain commas. To prevent them from causing problems they need to be surrounded by a quoting character, like " or '. By convention, read_csv() assumes that the quoting character will be ", and if you want to change it you’ll need to use read_delim() instead. What arguments do you need to specify to read the following text into a data frame?


"x,y\n1,'a,b'"
```

```
## [1] "x,y\n1,'a,b'"
```

```r
?read_delim
read_csv("x,y\n1,'a,b'", quote = "'")
```

```
## # A tibble: 1 × 2
##       x     y
##   <int> <chr>
## 1     1   a,b
```


##### Question 5


```r
# Identify what is wrong with each of the following inline CSV files. What happens when you run the code?

#read_csv("a,b\n1,2,3\n4,5,6")

read_csv("a,b,c\n1,2,3\n4,5,6")
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

```r
read_csv("a,b,c\n1,2\n1,2,3,4")
```

```
## Warning: 2 parsing failures.
## row col  expected    actual         file
##   1  -- 3 columns 2 columns literal data
##   2  -- 3 columns 4 columns literal data
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2    NA
## 2     1     2     3
```

```r
read_csv("a,b,c,d\n1,2\n1,2,3,4")
```

```
## Warning: 1 parsing failure.
## row col  expected    actual         file
##   1  -- 4 columns 2 columns literal data
```

```
## # A tibble: 2 × 4
##       a     b     c     d
##   <int> <int> <int> <int>
## 1     1     2    NA    NA
## 2     1     2     3     4
```

```r
#read_csv("a,b\n\"1")
#read_csv("a,b\n\"1"", quote = "" )
#read_csv("a,b\n1,2\na,b")
#read_csv("a;b\n1;3")
```



### Exercise 11.3.5


##### Question 1

What are the most important arguments to locale()?


```r
?locale()
```

The decimal_mark argument is the most important. 


##### Question 2


```r
# What happens if you try and set decimal_mark and grouping_mark to the same character? What happens to the default value of grouping_mark when you set decimal_mark to “,”? What happens to the default value of decimal_mark when you set the grouping_mark to “.”?

#locale(decimal_mark = ".", grouping_mark = ".")
# does not work
locale(decimal_mark = ",")
```

```
## <locale>
## Numbers:  123.456,78
## Formats:  %AD / %AT
## Timezone: UTC
## Encoding: UTF-8
## <date_names>
## Days:   Sunday (Sun), Monday (Mon), Tuesday (Tue), Wednesday (Wed),
##         Thursday (Thu), Friday (Fri), Saturday (Sat)
## Months: January (Jan), February (Feb), March (Mar), April (Apr), May
##         (May), June (Jun), July (Jul), August (Aug), September
##         (Sep), October (Oct), November (Nov), December (Dec)
## AM/PM:  AM/PM
```

```r
# it swapped the default

locale(grouping_mark = ".")
```

```
## <locale>
## Numbers:  123.456,78
## Formats:  %AD / %AT
## Timezone: UTC
## Encoding: UTF-8
## <date_names>
## Days:   Sunday (Sun), Monday (Mon), Tuesday (Tue), Wednesday (Wed),
##         Thursday (Thu), Friday (Fri), Saturday (Sat)
## Months: January (Jan), February (Feb), March (Mar), April (Apr), May
##         (May), June (Jun), July (Jul), August (Aug), September
##         (Sep), October (Oct), November (Nov), December (Dec)
## AM/PM:  AM/PM
```

```r
# switches the default
```



##### Question 3



```r
#I didn’t discuss the date_format and time_format options to locale(). What do they do? Construct an example that shows when they might be useful

# they change the format of how you can inout the date or time.
?date_format
locale(date_format = "%m-%d-%Y")
```

```
## <locale>
## Numbers:  123,456.78
## Formats:  %m-%d-%Y / %AT
## Timezone: UTC
## Encoding: UTF-8
## <date_names>
## Days:   Sunday (Sun), Monday (Mon), Tuesday (Tue), Wednesday (Wed),
##         Thursday (Thu), Friday (Fri), Saturday (Sat)
## Months: January (Jan), February (Feb), March (Mar), April (Apr), May
##         (May), June (Jun), July (Jul), August (Aug), September
##         (Sep), October (Oct), November (Nov), December (Dec)
## AM/PM:  AM/PM
```

```r
?parse_date()
parse_date("12-27-1991", locale = locale(date_format = "%m-%d-%Y"))
```

```
## [1] "1991-12-27"
```


##### Question 4


```r
# If you live outside the US, create a new locale object that encapsulates the settings for the types of file you read most commonly.

# Germany does day month year, months in numbers 
locale(date_format = "%d-%m-%Y")
```

```
## <locale>
## Numbers:  123,456.78
## Formats:  %d-%m-%Y / %AT
## Timezone: UTC
## Encoding: UTF-8
## <date_names>
## Days:   Sunday (Sun), Monday (Mon), Tuesday (Tue), Wednesday (Wed),
##         Thursday (Thu), Friday (Fri), Saturday (Sat)
## Months: January (Jan), February (Feb), March (Mar), April (Apr), May
##         (May), June (Jun), July (Jul), August (Aug), September
##         (Sep), October (Oct), November (Nov), December (Dec)
## AM/PM:  AM/PM
```

```r
# or change locale to German and use month names
locale("de", date_format = "%d-%b-%Y")
```

```
## <locale>
## Numbers:  123,456.78
## Formats:  %d-%b-%Y / %AT
## Timezone: UTC
## Encoding: UTF-8
## <date_names>
## Days:   Sonntag (So.), Montag (Mo.), Dienstag (Di.), Mittwoch (Mi.),
##         Donnerstag (Do.), Freitag (Fr.), Samstag (Sa.)
## Months: Januar (Jan.), Februar (Feb.), März (März), April (Apr.), Mai
##         (Mai), Juni (Juni), Juli (Juli), August (Aug.), September
##         (Sep.), Oktober (Okt.), November (Nov.), Dezember (Dez.)
## AM/PM:  vorm./nachm.
```



##### Question 5

What’s the difference between read_csv() and read_csv2()?

csv is comma deliminated and csv2 is semi-colon deliminated



##### Question 6

What are the most common encodings used in Europe? What are the most common encodings used in Asia? Do some googling to find out.


##### Question 7

Generate the correct format string to parse each of the following dates and times:


```r
d1 <- "January 1, 2010"
d2 <- "2015-Mar-07"
d3 <- "06-Jun-2017"
d4 <- c("August 19 (2015)", "July 1 (2015)")
d5 <- "12/30/14" # Dec 30, 2014
t1 <- "1705"
t2 <- "11:15:10.12 PM"


#d1
parse_date(d1, locale = locale(date_format = "%B %d, %Y"))
```

```
## [1] "2010-01-01"
```

```r
#d2
parse_date(d2, locale = locale(date_format = "%Y-%b-%d"))
```

```
## [1] "2015-03-07"
```

```r
#d3
parse_date(d3, locale = locale(date_format = "%d-%b-%Y"))
```

```
## [1] "2017-06-06"
```

```r
#d4
parse_date(d4, locale = locale(date_format = "%B %d (%Y)"))
```

```
## [1] "2015-08-19" "2015-07-01"
```

```r
#d5
parse_date(d5, locale = locale(date_format = "%m/%d/%y"))
```

```
## [1] "2014-12-30"
```

```r
#t1
parse_time(t1, locale = locale(time_format = "%H%M"))
```

```
## 17:05:00
```

```r
#t2
parse_time(t2, locale = locale(time_format = "%H:%M:%OS %p"))
```

```
## 23:15:10.12
```








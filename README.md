# Reading-Data-From-Excel-Files-xls-xlsx-csv-into-R-Quick-Guide

Reading Data From Excel Files into R, so many people still saving their dataset in R but sometimes coming to data analysis facing lots of difficulties, while loading data set into R, we can make use of the power of R functions.

In this tutorial we are going to describe how to read excel data xls or xlsx file formats into R. This can be done based on using readxl, xlsx, openxlsx, or XLConnect package.
Reading Data From Excel Files into R
1. readxl package

If you are not installed readxl package then you can use below code

Repeated Measures of ANOVA in R Complete Tutorial »

install.packages("readxl")

Load readxl package into R.

library("readxl")

Reading xls and xlsx format is given below.

For xls files

data<- read_excel("file.xls")

For xlsx files

data <- read_excel("file.xlsx")

You can choose a file interactively based on file.choose() function. This is time consuming so not recommended.

data <- read_excel(file.choose())

Imagine if you have multiple sheets then you can make use of argument sheet.

You need to specify sheet by its name

data <- read_excel("my_file.xlsx", sheet = "sheetname")

You can specify sheet by its index

data <- read_excel("my_file.xlsx", sheet = 2)

Sometimes in excel sheet contains the missing values, if you are reading the file in R it will display as a blank cell, You can avoid these kinds of issues while setting na argument.

data <- read_excel("file.xlsx", na = "---")

If you want to read multiple excel files then,

library(readxl)
file.list <- list.files(pattern='*.xlsx')
df.list <- lapply(file.list, read_excel)

If you also want to include the files in subdirectories, then

file.list <- list.files(pattern='*.xlsx', recursive = TRUE)

Suppose all the sheets have same column name then you can make use of bind_rows,

library(dplyr)
df <- bind_rows(df.list, .id = "id")

2. xlsx Package

One of the another package is xlsx,  java-based solution, for reading, writing and formatting excel files in R.

If you are not installed you can install the package based on below code.

install.packages("xlsx")

Let’s load the xlsx package in R.

library("xlsx")

How to use xlsx package?

In xlsx pakage mainly two functions read.xlsx() and read.xlsx2()

Suppose if you have bigger files then read.xlsx2() function recommended because it’s load faster than read.xlsx.

Xlsx package format is given below.

read.xlsx(file, sheetIndex, header=TRUE)
read.xlsx2(file, sheetIndex, header=TRUE)

file indicating the file path

sheetIndex indicate the index of the sheet to be read

header indicates a logical value. If header is TRUE then the first row is considered as column names.

library("xlsx")
data <- read.xlsx(file.choose(), 1)  # read first sheet
data <- read.xlsx(“file.xlsx”, 1)  # read first sheet
data <- read.xlsx(“file.xlsx”, sheetName=”Sheet1”)  # read the data contains in Sheet1

Another way of importing data is copying from Excel and import into R

If you are using windows system the,

eXtreme Gradient Boosting in R » Ultimate Guide »

data <- read.table(file = "clipboard", sep = "\t", header=TRUE)

MAC OSX system

data <- read.table(pipe("pbpaste"), sep="\t", header = TRUE)

this is not the better way of importing data into R
3. openxlsx Package

openxlsx package is an another alternative to readxl package

library(openxlsx)
read.xlsx(file_path)

or

read.xlsx(file_path, cols = 1:2, rows = 2:3)

4. XLConnect package

XLConnect is an alternative to the xlsx package

install.packages("XLConnect")
library(XLConnect)
data <- readWorksheetFromFile(file_path, sheet = "list-column",
                              startRow = 1, endRow = 10,
                              startCol = 1, endCol = 3)

If you want to read several sheets then

Reading several sheets

load <- loadWorkbook(file_path)
data <- readWorksheet(load, sheet = "list-column",
                      startRow = 1, endRow = 10,
                      startCol = 1, endCol = 3)
data2 <- readWorksheet(load, sheet = "two-row-header",
                       startRow = 1, endRow = 10,
                       startCol = 1, endCol = 4)

In this package yu can Import a named region once

data <- readNamedRegionFromFile(file, # File path
                                name, # Region name
                                ...)  # Arguments of readNamedRegion()

Reading several named regions

load <- loadWorkbook(file_path)
data <- readNamedRegion(load, name_Region_1, ...)
data2 <- readNamedRegion(load, name_Region_2, ...)

If you have csv file then

data<-read.csv(“file.csv”,1)

Sometimes reading excel files JAVA errors can occur, you can avoid those issues while seting the java path in R

Prints the path of JAVA Home in R

Sys.getenv("JAVA_HOME")

Sets the path of JAVA

Sys.setenv(JAVA_HOME = "path_to_jre_java_folder")

jre folder contains inside the Java folder of your computer (Program Files)

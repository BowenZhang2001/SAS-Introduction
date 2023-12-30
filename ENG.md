# All You Need to Know about SAS

## 1 Introduction

### 1.1 The SAS Language

Unlike many ohter software applications which are either menu driven, or command driven, SAS uses statements to write a series of instructions called a SAS program.

A SAS program is a sequence of statements executed in order. A statement gives information or instructions to SAS and must be appropriately placed in the program. The order of the subsequent statements may not be important, but you must start with the general statement of what you want to do, such as two basic building blocks: `DATA` steps and `PROC` steps.

As with any language, there are a few rules to follow when writing SAS programs. The most important rule is **Every SAS statement ends with a semicolon**.

There really aren't any rules about how to format your SAS program. While it is helpful to have a neat looking program with each statement on a line by itself and indentions to show the various parts of the program, it isn't necessary.

* SAS statements can be in upper- or lowercase, (similar to SQL).
* Statements can continue on the next line.
* Statements can be on the same line as other statements. (You can write several statements on a single line, as long as you put a semicolon in the middle of two statements).
* Statements can start in any column, (different from Python).

To make your programs more understandable, you can insert comments into your programs. There are two styles of comments you can use: one starts with an asterisk (\*) and ends with a semicolon (;). The other style starts with a slash asterisk (/\*) and ends with an asterisk slash (\*/).

```sas
* This is a comment;
/* This is also a comment*/
```

Since some operating environments interpret a slash asterisk (/\*) in the first column as the end of a job, be careful when using this style of comment not to place it in the first column.

### 1.2 SAS Data Sets

Data, of course, are the primary constituent of any data set. In traditional SAS terminology the data consist of variables and observations. Adopting the terminology of relational databases, SAS data sets are also called tables, observations are also called rows, and variables are also called columns.

Raw data come in many different forms, but SAS simplifies this. In SAS there are just two data types: numeric and character. Numeric variables can be added and subtracted, can have any number of decimal places, and can be positive or negative.  In addition, numeric variables can contain plus signs (+), minus signs (-), decimal points (.), or "E" for scientific notation. Character data are everything else. They may contain numerals, letters, or special characters (such as \$ or !), and can be up to 32,767 characters long.

If a variable contains letters or special characters, it must be a character variable. However, if it contains only numbers, then it may be numeric or character.

Sometimes despite your best efforts, your data may be incomplete. The value of a particular variable may be missing for some observations. In those cases, missing character data are represented by blanks, and missing numeric data are represented by a single period (.).

Prior to SAS 9.1, SAS data sets could contain up to 32,767 variables. Beginning with SAS 9.1, the maximum number of variables in a SAS data set is limited by the resources available on your computer but SAS data sets with more than 32,767 variables cannot be used with earlier versions of SAS. The number of observations, no matter which version of SAS you are using, is limited only by your computer's capacity to handle and store them.

You make up names for the variables in your data and for the data sets themselves. Follow these simple rules when making up names for variables and data set members:

* Names must be 32 characters or fewer in length. 
* Names must start with a letter or an underscore ( _ ).
* Names can contain only letters, numerals, or underscores ( _ ).
* Names can contain upper- and lowercase letters. 

This last point is an important one. SAS is insensitive to case so you can use uppercase, lowercase, or mixed case. For example, `Height`, `HEIGHT`, `height` are considered the same variable in SAS.  However, there is one difference for variable names. SAS remembers the case of the first occurrence of each variable name and uses that case when printing results.

In addition to your actual data, SAS data sets contain information about the data set such as its name, the date that you created it, and the version of SAS you used to create it. SAS also stores information about each variable, including its name, label (if any), type (numeric or character), length (or storage size), and position within the data set. This information is sometimes called the descriptor portion of the data set, and it makes SAS data sets self-documenting.

### 1.3 DATA and PROC Steps

SAS programs are constructed from two basic building blocks: DATA steps and PROC steps. A typical program starts with a DATA step to create a SAS data set and then passes the data to a PROC step for processing.

DATA and PROC steps are made up of statements. A step may have as few as one or as many as hundreds of statements. Most statements work in only one type of step — in DATA steps but not PROC steps, or vice versa. In most cases, DATA steps read and modify data while PROC steps analyze data, perform utility functions, or print reports.

DATA steps start with the `DATA` statement. This keyword is followed by a name that you make up for a SAS data set.  In addition to reading data from external, raw data files, DATA steps can include DO loops, IF-THEN/ELSE logic, and a large assortment of numeric and character functions. DATA steps can also combine data sets in just about any way you want, including concatenation and match-merge.

Procedures, on the other hand, start with a `PROC` statement in which the keyword is followed by the name of the procedure (PRINT, SORT, or MEANS, for example). SAS procedures do everything from simple sorting and printing to analysis of variance and 3D graphics.

A step ends when SAS encounters a new step(marked by a `DATA` or `PROC` statement); a `RUN`, `QUIT`, `STOP`, or `ABORT` statement; or, if you are running in batch mode, the end of the program. RUN statements tell SAS to run all the preceding lines of the step and are among those rare, global statements that are not part of a DATA or PROC step.

### 1.4 The DATA Step's Built-in Loop

DATA steps have an underlying structure, an implicit, built-in loop. **DATA steps execute line by line and observation by observation**. The idea that DATA steps execute line by line is fairly straightforward and easy to understand. It means that, by default, SAS executes line one of your DATA step before it executes line two, and line two before line three, and so on. The idea that DATA steps execute observation by observation means SAS takes the first observation and runs it all the way through the DATA step (line by line, of course) before looping back to pick up the second observation. In this way, SAS sees only one observation at a time.

This diagram illustrates how an observation flows through a DATA step:

![Img](./FILES/ENG.md/img-20231229184406.png)

SAS reads observation number one and processes it using line one of the DATA step, then line two, and so on until SAS reaches the end of the DATA step. Then SAS writes the observation in the output data set. This diagram10shows the first execution of the line-by-line loop. Once SAS finishes with the first observation, it loops back to the top of the DATA step and picks up observation two. When SAS reaches the last observation, it automatically stops.

Apart from that, SAS offers a number of ways to override the line-by-line and observation-by-observation structure. These include the `RETAIN` statement, and the `OUTPUT` statement.

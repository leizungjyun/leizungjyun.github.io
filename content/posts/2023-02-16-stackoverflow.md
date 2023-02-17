---
title: "Stack Overflow Developer Survey"
date: 2023-02-16T21:41:23+08:00
draft: false
cover:
    image: https://survey.stackoverflow.co/2022/up_/src/img/dev-survey-2022.png
---

## Developer Survey Datasets

Stack Overflow has been carrying out an annual developer survey since 2011. [Datasets](https://insights.stackoverflow.com/survey/?_ga=2.4656628.677002830.1676555026-674836096.1676555026) in CSV files can be downloaded for your own purpose.

## Dataset Profiling

Python offers a built-in package called `csv` to read and write CSV files. We can definitely use it to read the CSV file. However, data scientists prefer `pandas`, which provides more powerful data structures such as `DataFrame` for data analysis. So I use `pandas` to read the CSV file.

    # import pandas and read the csv file into a DataFrame
    import pandas as pd
    data = pd.read_csv("survey_results_public.csv")

`pandas` provides a method called `info()` to get a concise summary of data and a method called `describe()` to get a summary of the numerical columns. An alternative and more powerful way to do it is to use `ydata-profiling` package. It generates an HTML report with a lot of useful information. 

    # install ydata-profiling by pip
    $ pip install ydata-profiling

Let's use `ydata-profiling` to profile the dataset.

    # import ydata-profiling and profile the dataset
    import ydata_profiling as yp
    yp.ProfileReport(data, minimal=True, title="Stack Overflow Developer Survey 2022")
    yp.to_file("StackOverflow2022.html") # generate html report

The HTML report is generated and can be viewed in a browser. Here's the [result](/StackOverflow2022.html).

As you can see, `ydata-profiling` generates a plethora of information. We can use the report to clean up the dataset. For example, we can fill N/A data with medians and drop outliers according to the report. Meanwhile, we can see some columns are further filled with into semicolon-separated data. For example, the column "LanguageWorkedWith" is filled with multiple languages separated by semicolon. In this case, profiling fails to provide useful information. We need to preprocess the data to meet our need.


## The Most Popular Languages

I'm interested in the most popular languages for developers. So I do the statistics based on the 2022 dataset. Here's the top-10 result.

![Most_Popular_Languages](/img/posts/All-Developers.png)


We can also do the statistics based on the developer type. Here are results for "Data or Business Analyst" and "Data Scientist or Machine Learning Specialist".
![Most Popular Languages for Data or Business Analyst](/img/posts/Data-or-Business-Analyst.png)

![Most_Popular_Languages for Data Scientist or Machine Learning](/img/posts/Data-Scientist-or-Machine-Learning-Specialist.png)

We will explore more interesting results in the future.
# example-report

```
docker run --rm -v $PWD:$PWD -w $PWD -it quay.io/lifebitai/biobank-gwas:1.1dev

# inside the container

bash run_report.sh


# OR

Rscript -e "rmarkdown::render('gwas_report.Rmd', params = list(manhattan='manhattan.png',qqplot='qqplot_ci.png', gwascat='gwascat_subset.csv', saige_results='saige_results_top_n.csv', trait_type='binary'))"
```


# How to provide custom parameters to the Rmd report file


![](https://user-images.githubusercontent.com/38183826/123424349-a1316600-d5b8-11eb-9c06-23d89c1a9883.png)

Example code snippet for defining params [here](https://github.com/lifebit-ai/example-report/blob/9ce5a0832d15f613fee1deaf65177c7124aaae95/gwas_report.Rmd#L12-L18)

```YAML
---
output: 
  html_document:
    code_download: false
    toc: true                  # table of content true
    toc_depth: 3               # upto three depths of headings (specified by #, ## and ###)
    toc_float: true
    number_sections: true      # if you want number sections at each table header
    theme: united              # many options for theme, this one is my favorite.
    highlight: tango           # specifies the syntax highlighting style
    css: 'style.css'
params:
  manhattan:  "covid_1_manhattan.png"
  qqplot:  "covid_1_qqplot_ci.png"
  gwascat: "gwascat_subset.csv"
  trait_type: 'binary'
  saige_results: "saige_results_top_n.csv"
  ldsc_log: "None"
title: "`r paste0('GWAS Report' , '') `"
author: ""
date: ""
---
```

We care about the parameters section:

```
params:
  manhattan:  "covid_1_manhattan.png"
```

- The variable `manhattan` is a parameter.
- The value `covid_1_manhattan.png` is just the default, it will be overwritten from the cli when defined in Rscript -e "rmarkdown::render('gwas_report.Rmd', params = list(manhattan='manhattan.png', trait_type='binary'))"
- The Rmd report file picks up the value by mentioning the variable as written in [gwas_report.Rmd#L56](https://github.com/lifebit-ai/example-report/blob/9ce5a0832d15f613fee1deaf65177c7124aaae95/gwas_report.Rmd#L56)


```R
my_custom_manhattan <- params$manhattan
```

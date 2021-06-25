# example-report

```
docker run --rm -v $PWD:$PWD -w $PWD -it quay.io/lifebitai/biobank-gwas:1.1dev

# inside the container

bash run_report.sh


# OR

Rscript -e "rmarkdown::render('gwas_report.Rmd', params = list(manhattan='manhattan.png',qqplot='qqplot_ci.png', gwascat='gwascat_subset.csv', saige_results='saige_results_top_n.csv', trait_type='binary'))"
```

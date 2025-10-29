---
permalink: /code.html
title: "Public Code Repositories"
author_profile: true
redirect_from: 
  - /code/
---


I/O Tools
----------

Working with data across programs can be a pain.  So I made a tool to load SAS data in  [Polars](https://pola.rs/) and to use parquet files in Stata.

### [polars-readstat](https://github.com/jrothbaum/polars_readstat)

This is a Polars IO plugin to read SAS (sas7bdat), Stata (dta), and SPSS (sav) files.
It is generally as fast or faster than pandas and pyreadstat, particularly for SAS files and reading subsets of columns from files.

Available on [PyPi](https://pypi.org/project/polars-readstat/).


### [pq/stata-parquet-io](https://github.com/jrothbaum/stata_parquet_io/)

pq is a Stata package that enables reading and writing Parquet files directly in Stata. This plugin bridges the gap between Stata's data analysis capabilities and the increasingly popular Parquet file format, which is optimized for storage and performance with large datasets.  This is slower than reading/writing a dta file in Stata (Stata is really good at that), but makes it easier to use Stata in multi-language workflows (using dta files is slow in R and Python).  It can be as fast as Stata when loading a small subset of columns from large files.

Available on [SSC](https://ideas.repec.org/c/boc/bocode/s459458.html)

Tools for missing data issues (Coming soon)
----------------------------------
I've been trying to take advantage of the extended shutdown of 2025 to make some tools available that mirror what I use on the [NEWS project](/news.html) to address missing data issues that can bias estimates from survey AND administrative data.

These tools will include a super fast algorithm for calibration to reweight a dataset to make it representative (hat tip to Carl Sanders's [entropy-balance-weighting](https://github.com/uscensusbureau/entropy-balance-weighting) package).  Calibration can help address nonresponse bias in survey data (see [this blog](https://www.census.gov/newsroom/blogs/research-matters/2025/09/administrative-data-nonresponse-bias-cps-asec.html), [this paper on the CPS ASEC](https://www.census.gov/library/working-papers/2020/demo/SEHSD-WP2020-10.html), or [this paper on the ACS](https://www.census.gov/content/dam/Census/library/working-papers/2021/acs/2021_Rothbaum_01.pdf)) and representativeness in administrative data.

The package will also include tools to use machine learning ([LightGBM](https://lightgbm.readthedocs.io/en/stable/)) to impute for missing data.  This can be useful in addressing nonrandom nonresponse in [survey data](https://academic.oup.com/jssam/article-abstract/10/1/81/5943180) and [missing administrative data](https://www.aeaweb.org/articles?id=10.1257/pandp.20221040).

It has tools for simpler imputation as well (hot deck/stat match, regression-based imputation, etc.) and to generate multiple imputation statistics with bootstrap or replicate weights and easily make comparisons.

The package uses [Narwhals](https://narwhals-dev.github.io/narwhals/) to be (mostly) dataframe agnostic - which means you pass in a Pandas dataframe (or polars or duckdb, etc.) and that's what you get back.  It does require polars and pyarrow, unfortunately, because there's some logic that I couldn't do in Narwhals.

When complete, I'll push this python package to PyPi.
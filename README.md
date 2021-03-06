# fGWAS

The data analysis package for Functional Genome-wide Association Study(fGWAS)

# Reference

[1] Wang, Z., Wang, N., Wu, R., & Wang, Z. (2018). fGWAS: An R package for genome-wide association analysis with longitudinal phenotypes. Journal of genetics and genomics= Yi chuan xue bao, 2018 Jul 10. [URL](https://linkinghub.elsevier.com/retrieve/pii/S1673-8527(18)30120-6).

## Abstract:

The fGWAS package is aiming to identify significant SNPs that control longitudinal phenotypic traits and estimate their additive and dominant genetic effects based on the Functional Mapping model. This model is cornerstone for identifying the relation between genes and longitudinal traits in this fGWAS package. 

## Document

> 1) Vignette (https://github.com/wzhy2000/fGWAS/blob/master/fgwas.vignette.pdf)

> 2) Manual (https://github.com/wzhy2000/fGWAS/blob/master/fgwas.manual.pdf)

## Installation Instructions:

### Required software and packages
    
> 1. R (http://www.r-project.org/)
    
> 2. Package [minpack.lm](https://cran.r-project.org/web/packages/minpack.lm/index.html), [snpStats](http://bioconductor.org/packages/release/bioc/html/snpStats.html), mvtnorm, parallel (required in R >= 2.14.0 ).

Please install the required R packages before you install the fGWAS package. After the  installation of the dependencies, please install the **fGWAS** as following steps.

### Install fGWAS on LINUX or Mac OSX

1) use install_github function in R console

```
library("devtools");
install_github("wzhy2000/fGWAS/pkg")
```
2) use command lines in a command window  

```
git clone https://github.com/wzhy2000/fGWAS.git
cd fGWAS
R CMD INSTALL pkg
```

### Install fGWAS on Windows

1) Install from source codes using devtools library

```
>library("devtools");
>install_github("wzhy2000/fGWAS/pkg")
```

GeABEL is necessary in the current version. If it can not be installed by the command 'install.packages', please install it from GitHub:

```
> library(devtools)
> install_github("cran/GenABEL.data")
> install_github("cran/GenABEL")
```

MVTNORM is a dependend package and now unavailable for new R(maybe>3.5.0), please download it from CRAN and then install it using install.packages command;
https://cran.r-project.org/web/packages/mvtnorm/index.html

MSBVAR also is not available for new R(maybe>3.5.0) please using the following command to install from GitHub

```
> library("devtools");
> install_github("cran/MSBVAR")
```

2) Install from pre-compile package in Windows

>1 Please download windows package from (https://github.com/wzhy2000/fGWAS/raw/master/windows/fGWAS.zip)

>2 Install the package in R GUI by selecting the menu "Packages|Install package(s) from local zip files..."

## Usage Instructions

fGWAS is an R package which provides:

> 1) Loading the genotype data(SNP) from PLINK data files or simple SNP data table.

> 2) Loading the longitudinal phenotype data(traits) from CSV file with the covariate file or the measure time file.

> 3) Scaning SNP data set to estimate log-likelihood ratio and the genetic effetcs of each genotype.

> 4) Detecting the significant SNPs and export the results.

> 5) Drawing the genetic effects for each significant SNP.


The following codes show how to call above steps in R.

We don't attach any data set in the package, so here we use the simulation to generate the phenotype taits andgenotype data. The simulation function returns a list containing one phenotype object and one genotype object.

```
library(fGWAS);
r<-fg.simulate("Logistic", "AR1", 2000, 500, 1:7, sig.pos=250 );
```

Call SNP scaning in a short range (245:255) using 'fgwas' method. 

```
obj.scan <- fg.snpscan(r$obj.gen, r$obj.phe, method="fgwas", snp.sub=c(245:255) );
obj.scan;
```

Plot Manhattan figure for all SNPs in a PDF file.

```
plot(obj2.scan, file.pdf="temp.fwgas.obj2.scan.pdf");
```

Select significant SNPs and plot the varing genetic effects in PDF.

```
tb.sig <- fg.select.sigsnp(obj2.scan, sig.level=0.001, pv.adjust = "bonferroni")
plot.fgwas.curve( obj2.scan, tb.sig$INDEX, file.pdf="temp.fwgas.obj2.curve.pdf");
```

All functions and examples in the fGWAS are available in the manual (https://github.com/wzhy2000/fGWAS/blob/master/fgwas.manual.pdf).

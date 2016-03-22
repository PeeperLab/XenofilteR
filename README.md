# XenofilteR
XenofilteR: separate graft from host reads in xenograft sequencing

Human tumour samples or cancer cell lines, transplanted into mice are widely used as a 
model to study cancer. However, genomic analysis of tumour material derived from these 
xenografts is challenging. The sequence data not only contains reads that originate from 
the graft (human tumour or cell line) but also reads from host (mouse). We developed 
XenofilteR, an R-package for filtering host from graft reads in next generation sequence 
data. XenofilteR is a novel method that utilizes the edit distance of each read for 
classification. XenofilteR outperforms existing methods as validated on artificially 
mixed mouse/human samples and sets of patient derived xenograft samples. 

## Bioconductor

XenofilteR will be submitted to Bioconductor.org. 


## Installation (not via Bioconductor)

Installation of XenofilteR should be performed as
follows:

    > source("http://bioconductor.org/biocLite.R")
    > biocLite(c("Rsamtools", "GenomicAlignments", "BiocParallel", "futile.logger"))

As the last step in the installation process, the latest XenofilteR package can
be downloaded from the
[XenoFilteR releases webpage](https://github.com/PeeperLab/XenoFilteR/releases)
and installed using the following command:

    $ R CMD INSTALL XenofilteR*.tar.gz

Now you are all set to start your analysis.

## XenofilteR usage:


Load the XenofilteR package in R using:

    > library("XenofilteR")

XenofilteR fully supports paralel computing and is implemented in such a way
that every sample is processed on a single core. XenofilteR uses the
BiocParallel for parallel computing. This package requires the user to
specify which parallel environment is used by creating an instance of
BiocParallelParam. Here, we use the 'snow' environment and specify a SnowParam. 
The number of workers represents the number of CPUs used for the analysis and thereby 
the number of samples analyses simultaneously. Hence, it is wise to keep the number of 
CPUs low when analysing large samples as memory usage might be high. 

	> bp.param <- SnowParam(workers = 1, type = "SOCK")

XenofilteR requires a dataframe or matrix, named 'sample.list', with in the first 
column the bam file names as mapped to the graft reference. The second column contains the 
file names and paths to the bam files as mapped to the host reference. Each row in 
'sample.list' represents a single sequence run or sample. An optional list may be provided with 
alternative names for output files, 'output.names	'. Especially for RNAseq samples aligned with for example 
Tophat this may be convenient since all .bam files are named identical. 
The XenofilteR package and data are run in the following way: 

	> XenofilteR(sample.list, destination.folder = "./", bp.param = bp.param, output.names)


## Contact
## 
We have tried to make the XenofilteR code readable and its use as easy
as possible. If any questions arise regarding the package, or if you
want to report any bugs, please do not hesitate and contact:

- [Oscar Krijgsman](mailto:o.krijgsman@nki.nl) 
- [Roel Kluin](mailto:r.kluin@nki.nl)

Oscar and Roel both work at the NKI, Oscar in the lab of Prof. Daniel
Peeper, Roel in the Genome Core Facility.


## Changes and additions we are currently working on
## 
- [ ] Optionally output bam file with mouse reads
- [ ] Improve the vignette
- [ ] Make Xenofilter more efficient in memory usage	
- [x] Add read-count statistics to the log file
- [x] Change output name and structure for RNAseq data
- [x] Making XenofilteR into an R-package 
- [x] Initial loop running the basic function of XenofilteR


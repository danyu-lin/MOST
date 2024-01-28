# **MOST**

# **MOST: Multivariate Outcome Score Test**

Genetic association studies often collect data on multiple traits that
are correlated. Discovery of genetic variants influencing multiple
traits can lead to better understanding of the etiology of complex human
diseases. Conventional univariate association tests may miss variants
which have weak or moderate effects on individual traits. We propose
several multivariate test statistics to complement univariate tests. Our
framework covers both studies of unrelated individuals and family
studies and allows any type/mixture of traits. We construct score-type
statistics, which are computationally fast and numerically stable even
in the presence of covariates and which can be combined efficiently
across studies with different designs and arbitrary patterns of missing
data. We also provide a strategy to determine genomewide significance
that properly accounts for the linkage disequilibrium (LD) of genetic
variants.

## **General information**

Our MOST will output three multivariate statistics, Q, T, and T’. The T
test is more powerful when the genetic effect sizes are close to each
other across different traits; the T’ test is more powerful when the
standardized genetic effects are similar to each other; the Q test is
more powerful when the genetic effects vary dramatically (possibly with
opposite effects) for different traits. If one already knows that some
of the traits are ‘healthy’ traits and the other traits are ‘unhealthy’
traits (for example, HDL versus LDL), the user should arrange the
multiple traits in the plausibly same direction (this can be done by
multiply each of the ‘unhealthy’ traits by -1). For the user’s
convenience, MOST will also output the univariate analysis results for
each trait. MOST is written in C.

## **SYNOPSIS**

**MOST** \[**-geno** geno\] \[**-ngeno** ngeno\] \[**-pheno** pheno\]
\[**-npheno** npheno\] \[**-trait** trait\]\[**-covar**
covar\]\[**-bin** bin\] \[**-monte** monte\]

## **INPUT FILES**

### **phenotype file**

| ID   |   trait1 |   trait2 |   covariate1 |   covariate2 |
|:-----|:---------|:---------|:-------------|:-------------|
| A101 |   0      |   -0.30  |   -1.59      |   -0.62      |
| A102 |   1      |   4.29   |   -0.04      |   0.38       |
| :    |   :      |          |   :          |   :          |

### **genotype file**

| ID   |   FID  |   rs111 |   rs222 |   rs333 |   … |
|:-----|:-------|:--------|:--------|:--------|:----|
| A101 |   B101 |   0     |   2     |   1     |   … |
| A102 |   B102 |   2     |   1     |   1     |   … |
| :    |   :    |   :     |   :     |   :     |   … |

In the above genotype file, FID refers to Family ID. For data with no
family structures, one needs to simply copy the column of ID to the
column of FID.

## **EXAMPLE**

### **The example files are in the download.**

1\) If one is not interested in obtaining the Monte-Carlo threshold,
then use the following command

>   
> MOST -geno geno.txt -ngeno 1000 -pheno pheno_and_covariates.txt
> -npheno 1000 -trait 2 -covar 2 -bin 1 0  

The “`-geno geno.txt`” specifies the name of the genotype file.

The “`-ngeno 1000`” tells MOST that there are 1000 subjects in the
genotype files.

The “`-pheno`” specifies the name of the phenotype file.

The “`-npheno 1000`” tells MOST that there are 1000 subjects in the
phenotype files. MOST allows that the genotype file and phenotype file
to have different number of subjects; it will sort out the subjects and
use those overlapping subjects.

The “`-traits 2`” tells MOST that your pheno file contains 2 traits.

The “`-covar 2`” tells MOST that your pheno file contains 2 covariates.

The “`-bin 1 0`” tells MOST that the first trait is binary and the 2nd
trait is continuous. If you have, say 4 traits and only the 3rd trait is
binary, then you would specify  
“`-bin 0 0 1 0`“.

2\) If one wishes to obtain the Monte-Carlo threshold, use the following
command

> MOST -geno geno.txt -ngeno 1000 -pheno pheno_and_covariates.txt
> -npheno 1000 -trait 2 -covar 2 -bin 1 0 -monte 1

The “`-monte 1`” tells MOST to invoke the Monte-Carlo procedure.

## **RESULTS**

### **The example files are in the download.**

The main results will be saved to Result.txt — this file contains the Q,
T^2, T’^2, and the Z_k^2 for all the K traits. The p-values for these
statistics are also contained in this file.

If the Monte-Carlo procedure was invoked, two files will be generated:
Monte_U_and_V.txt — this file is organized in blocks, and each block
contains the U-vector and the V-matrix for a SNP. Within each block, the
first line is the SNP-ID, the 2nd line is the U-vector, and the
remaining lines are for the V-matrix. (for information on U and V, see
the Reference Paper.) This file is useful for Meta-analysis (if any).

T_max.txt — this file contains results from the Monte-Carlo procedure.
The first column represents the simulation index. Each of the other
columns represents the Monte-Carlo realization of a statistic. This file
is useful for determining the Monte-Carlo Threshold for declaring
genome-wide significance. We provide a simple R program to use the
T_max.txt to get the Monte-Carlo Threshold.

## **REFERENCE**

Qianchuan He, Christy L. Avery, Dan-Yu Lin. (2013). A General Framework
for Association Tests With Multivariate Traits. To be submitted.

## **DOWNLOAD**

#### **MOST for 64-bit x86 based Linux \[updated Jan 04, 2013\]**

executable (zip archive)
**»** [MOST-1.0-linux-64.zip](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/MOST-1.0-linux-64.zip)

#### **Example files \[updated Jan 04, 2013\]**

zip archive
**»** [MOST-1.0-example.zip](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2013/01/MOST-1.0-example.zip)

## **VERSION HISTORY**

| Version | Date            | Description            |
|:--------|:----------------|:-----------------------|
| 1       | January 4, 2013 | First version released |

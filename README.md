
# HGN package


## Hypergeometric-Normal Random-Effects Model with Augmented Pseudo-Observations

In meta-analyses of binary outcomes, two-stage methods based on the DerSimonian–Laird-type random-effects model have been widely used, but these methods fix the within-study variances to their asymptotic estimates and rely on normality assumptions of the outcome measures. Such strict and often unrealistic assumptions can yield biased or inefficient inference. The hypergeometric–normal (HGN) random-effects model alleviates some of these issues by using an exact conditional likelihood. Noma (2025) developed an effective inference method that enables direct estimation of the risk ratio through a pseudo–data augmentation approach under the HGN formulation. Higher-order inference is achieved via jackknife bias and variance corrections, ensuring accurate coverage even in small or sparse datasets. This package implements HGN-based meta-analysis methods for both the odds ratio and the risk ratio, incorporating jackknife-based higher-order inference procedures.



## Installation

Please download "HGN_1.1-1.tar.gz" and install it by R menu: "packages" -> "Install package(s) from local files...".

Download: [please click this link](https://github.com/nomahi/HGN/raw/main/HGN_1.1-1.tar.gz)

Manual: [please click this link](https://github.com/nomahi/HGN/raw/main/HGN_1.1-1.pdf)



## Example code

```r

#  R example code for implementing the hypergeometric-normal (HGN) random-effects model analysis with augmented pseudo-data

# The "HGN" package
# GitHub webpage: https://github.com/nomahi/HGN/

###

# Download the R package file from the following URL:
# https://github.com/nomahi/HGN/raw/main/HGN_1.1-1.tar.gz

# Then, install the package (tar.gz format) by R menu: "packages" -> "Install package(s) from local files...".

###

pkgCheck <- function(pkg) {
  if (!requireNamespace(pkg, quietly = TRUE)) install.packages(pkg)
  suppressPackageStartupMessages( library(pkg, character.only = TRUE) )
}

pkgCheck("statmod")				# load or/and install the "statmod" package

library("HGN")					# load the "HGN" package

##

# Analyzing the example dataset "PAP" using the HGN model

data("PAP")

print(PAP)
attach(PAP)

m1 <- n1 + d1		# pseudo-data augmentation
m2 <- n2 + d2

hgn_fit(d1, n1, d2, n2)			# Ordinary analysis using the HGN model (odds-ratio estimation)
hgn_fit(d1, m1, d2, m2)			# Pseudo-data augmentation analysis using the HGN model (risk-ratio estimation)

hgn_jackknife(d1, m1, d2, m2, center = "mle", ref_dist = "t")			# Jackknife inference
hgn_jackknife(d1, m1, d2, m2, center = "jkbc", ref_dist = "t")			# Jackknife inference with the bias-correction estimator

detach(PAP)

##
##

# Analyzing the example dataset "rosiglitazone" using the HGN model

data("rosiglitazone")

print(rosiglitazone)
attach(rosiglitazone)

m1 <- n1 + d1		# pseudo-data augmentation
m2 <- n2 + d2

hgn_fit(d1, n1, d2, n2)			# Ordinary analysis using the HGN model (odds-ratio estimation)
hgn_fit(d1, m1, d2, m2)			# Pseudo-data augmentation analysis using the HGN model (risk-ratio estimation)

hgn_jackknife(d1, m1, d2, m2, center = "mle", ref_dist = "t")			# Jackknife inference
hgn_jackknife(d1, m1, d2, m2, center = "jkbc", ref_dist = "t")			# Jackknife inference with the bias-correction estimator

detach(rosiglitazone)


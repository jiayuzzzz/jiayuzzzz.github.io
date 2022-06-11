# PCA method by Stata
#### _Data source: Statistics Sweden(SCB)_ 
We are going to use the demographic data after normalization. The analysis is used for my master thesis named "The Impact of Swedish Public Finance Factors on the Local Real Estate Market — Based on the GMM PVAR Approach" at KTH. The codes tutorial comes from [Principal Component Analysis and Factor Analysis in Stata](https://www.youtube.com/watch?v=xNTsAVj0t7U) by econometricsacademy.
```markdown
* use data1.dta, clear
# We set the panel data identifier here
# now we look at the basic information of the dataset
* describe $xlist
* corr $xlist
* summarize $xlist
```
<img src="pca_info.png" width="500">

```markdown
* xtset code year
* global xlist pop_den tax edu_rate inmi_rate employ_rate dipo_inc
* pca $xlist
```
<img src="pca_result.png" width="600">
we should choose two main components based on the eigenvalues >1. They can explain about 67% variance of the data.

The linear equations are:


_C1 = 0.3930*pop_den - 0.4384*tax + 0.5171*edu_rate - 0.1110*inmi_rate + 0.3728*employ_rate + 0.4845*dipo_inc_

_C2 = 0.3553*pop_den - 0.2353*tax + 0.0298*edu_rate + 0.7907*inmi_rate - 0.4382*employ_rate - 0.0146*dipo_inc_

```markdown
# we hide the items with loadings < 0.3, because that indicates they are not the dominant factors.
* pca $xlist, blanks(0.3)
```

* screeplot, yline(1)

* Loading scores
* estat loadings
* predict pc1 pc2 pc3, score
* estat kmo

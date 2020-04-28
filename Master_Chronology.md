---
title: "Master Chronology Development"
author: "Jen Baron, j.baron@alumni.ubc.ca, UBC Tree Ring Lab"
date: 'April 1, 2020'
output:
  html_document:
    keep_md: true
    toc: true
    toc_float: true
    toc_depth: 3  # upto three depths of headings (specified by #, ## and ###)
    number_sections: true  ## if you want number sections at each table header
    theme: sandstone
---


# Packages


```r
library(dplR) # dendrochronology
library(tidyr)
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(ggplot2)
library(corrplot)
```

```
## corrplot 0.84 loaded
```

```r
library(stringr)
```


# Read in Data 

![Locations of Chronologies](figures/chronologies.jpg)


## Cook - Longfellow Trail - PIST - ITRDB PA008

NOAA Study Page: https://www.ncdc.noaa.gov/paleo-search/study/2993

Chronology file name   : PA008.CRN
Measurement file name  : PA008.RWL  
Date checked           : 02DEC94
Technician's name      : MARIETTE SEKLECKI
Supervisor's name      : HENRI D. GRISSINO-MAYER
Beginning year         : 1679
Ending year            : 1981
Principal investigators: ED COOK
Site name              : LONGFELLOW TRAIL
Site location          : PENNSYLVANIA, USA
Species information    : PIST WHITE PINE
Latitude               : 4120N 
Longitude              : 7912W 
Elevation              : N/A M
Series intercorrelation: 0.658
Avg mean sensitivity   : 0.211
Avg standard deviation : 0.591
Avg autocorrelation    : 0.856
Number dated series    : 24
Segment length tested  : 50
Number problem segments: 0
Pct problem segments   : 0.00

Are there obvious misdated series? NO
Number possible misdated series  : N/A
Percent misdated series          : 0.00

Comments: 
NO ELEVATION GIVEN
EXELLENT HIGH QUALITY CHRONOLOGY



```r
pa008.crn <- read.crn("data/pa008.crn")
```

```
## There appears to be a header in the crn file
## There is 1 series
```

```r
crn.plot(pa008.crn, add.spline = TRUE, nyrs=30)
```

![](Master_Chronology_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

```r
pa008.rwl <- read.rwl("data/pa008.rwl")
```

```
## Attempting to automatically detect format.
## Assuming a Tucson format file.
## There does not appear to be a header in the rwl file
## There are 24 series
## 1    	058021  	 1679	 1981	0.01
## 2    	058022  	 1721	 1981	0.01
## 3    	058031  	 1702	 1939	0.01
## 4    	058032  	 1689	 1939	0.01
## 5    	058051  	 1720	 1956	0.01
## 6    	058052  	 1693	 1940	0.01
## 7    	058061  	 1685	 1967	0.01
## 8    	058062  	 1687	 1968	0.01
## 9    	058071  	 1700	 1970	0.01
## 10   	058072  	 1691	 1970	0.01
## 11   	058081  	 1706	 1970	0.01
## 12   	058082  	 1693	 1967	0.01
## 13   	058101  	 1693	 1970	0.01
## 14   	058102  	 1698	 1970	0.01
## 15   	058121  	 1696	 1981	0.01
## 16   	058122  	 1711	 1981	0.01
## 17   	058141  	 1712	 1981	0.01
## 18   	058142  	 1699	 1981	0.01
## 19   	058151  	 1705	 1970	0.01
## 20   	058152  	 1692	 1981	0.01
## 21   	058191  	 1685	 1968	0.01
## 22   	058201  	 1730	 1940	0.01
## 23   	058202  	 1684	 1981	0.01
## 24   	058211  	 1749	 1979	0.01
```

```r
rwl.report(pa008.rwl)
```

```
## Number of dated series: 24 
## Number of measurements: 6435 
## Avg series length: 268.125 
## Range:  303 
## Span:  1679 - 1981 
## Mean (Std dev) series intercorrelation: 0.6192482 (0.0761018)
## Mean (Std dev) AR1: 0.8445 (0.07192569)
## -------------
## Years with absent rings listed by series 
##     Series 058061 -- 1934 
## 1 absent rings (0.016%)
## -------------
## Years with internal NA values listed by series 
##     None
```

```r
seg.plot(pa008.rwl)
```

![](Master_Chronology_files/figure-html/unnamed-chunk-1-2.png)<!-- -->


## Guyette - Dividing Lake - PIST - ITRDB CANA127

NOAA Study Page: https://www.ncdc.noaa.gov/paleo-search/study/3448

Chronology file name   : CANA127.CRN
Measurement file name  : CANA127.RWL
Date checked           : 17JUL96
Technician's name      : MARIETTE SEKLECKI
Supervisor's name      : HENRI D. GRISSINO-MAYER
Beginning year         : 1662
Ending year            : 1994
Principal investigators: R.P. GUYETTE
Site name              : DIVIDING LAKE
Site location          : ONTARIO, CANADA
Species information    : PIST EASTERN WHITE PINE
Latitude               : 4525N 
Longitude              : 7836W 
Elevation              : 500 M
Series intercorrelation: 0.572
Avg mean sensitivity   : 0.209
Avg standard deviation : 0.648
Avg autocorrelation    : 0.828
Number dated series    : 47
Segment length tested  : 50
Number problem segments: 34
Pct problem segments   : 8.15

Are there obvious misdated series? YES
Number possible misdated series  : 3
Percent misdated series          : 6.38
Do they affect chronology quality? N/A
Recommend withhold from ITRDB?     N/A

Comments: 
#4 DLW04B, #5 DLW05B, #40 DLW19A ARE MISDATED
#8 DLW09A 1736-1849, #32 LDW09B 1741-1824 HAVE LOW CORRELATIONS
DATA SET COULD BE IMPROVED


```r
cana127.crn <- read.crn("data/cana127.crn")
```

```
## There appears to be a header in the crn file
## There is 1 series
```

```r
crn.plot(cana127.crn, add.spline = TRUE, nyrs=30)
```

![](Master_Chronology_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
cana127.rwl <- read.rwl("data/cana127.rwl")
```

```
## Attempting to automatically detect format.
## Assuming a Tucson format file.
## There appears to be a header in the rwl file
## There are 47 series
## 1    	dlw01a  	 1764	 1994	0.01
## 2    	dlw02a  	 1716	 1994	0.01
## 3    	dlw03a  	 1762	 1994	0.01
## 4    	DLW04B  	 1688	 1994	0.01
## 5    	dlw05b  	 1771	 1994	0.01
## 6    	dlw07a  	 1889	 1994	0.01
## 7    	dlw08a  	 1788	 1994	0.01
## 8    	DLW09A  	 1736	 1994	0.01
## 9    	dlw10a  	 1798	 1994	0.01
## 10   	dlw11a  	 1741	 1994	0.01
## 11   	dlw12a  	 1704	 1994	0.01
## 12   	dlw13a  	 1743	 1994	0.01
## 13   	dlw14a  	 1662	 1994	0.01
## 14   	dlw16a  	 1676	 1991	0.01
## 15   	dlw15a  	 1830	 1994	0.01
## 16   	dlw17a  	 1730	 1992	0.01
## 17   	dlw18b  	 1777	 1994	0.01
## 18   	dlw19b  	 1862	 1994	0.01
## 19   	dlw20b  	 1805	 1994	0.01
## 20   	dlw23b  	 1762	 1994	0.01
## 21   	dlw24b  	 1775	 1994	0.01
## 22   	dlw25b  	 1777	 1994	0.01
## 23   	dlw26b  	 1790	 1994	0.01
## 24   	dlw27b  	 1757	 1994	0.01
## 25   	dlw029  	 1800	 1994	0.01
## 26   	dlw01b  	 1770	 1994	0.01
## 27   	dlw03b  	 1762	 1994	0.01
## 28   	dlw05a  	 1773	 1994	0.01
## 29   	dlw06a  	 1757	 1994	0.01
## 30   	dlw07b  	 1880	 1994	0.01
## 31   	dlw08b  	 1766	 1994	0.01
## 32   	dlw09b  	 1741	 1994	0.01
## 33   	dlw11c  	 1687	 1994	0.01
## 34   	dlw12b  	 1665	 1992	0.01
## 35   	dlw14b  	 1669	 1994	0.01
## 36   	dlw15b  	 1860	 1994	0.01
## 37   	dlw16b  	 1693	 1994	0.01
## 38   	dlw17b  	 1692	 1992	0.01
## 39   	dlw18a  	 1765	 1940	0.01
## 40   	dlw19a  	 1784	 1994	0.01
## 41   	DLW20A  	 1763	 1994	0.01
## 42   	dlw22a  	 1830	 1994	0.01
## 43   	dlw24a  	 1850	 1994	0.01
## 44   	DLW25A  	 1764	 1994	0.01
## 45   	dlw26a  	 1707	 1994	0.01
## 46   	dlw27a  	 1752	 1994	0.01
## 47   	dlw28a  	 1830	 1994	0.01
```

```r
rwl.report(cana127.rwl)
```

```
## Number of dated series: 47 
## Number of measurements: 10839 
## Avg series length: 230.617 
## Range:  333 
## Span:  1662 - 1994 
## Mean (Std dev) series intercorrelation: 0.5399936 (0.1049041)
## Mean (Std dev) AR1: 0.815617 (0.1225253)
## -------------
## Years with absent rings listed by series 
##     None 
## -------------
## Years with internal NA values listed by series 
##     None
```

```r
seg.plot(cana127.rwl)
```

![](Master_Chronology_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

## Guyette - Dividing Lake Aquatic - PIST - ITRDB CANA148

NOAA Study Page: https://www.ncdc.noaa.gov/paleo-search/study/3449

Chronology file name   : CANA148.CRN
Measurement file name  : CANA148.RWL
Date checked           : 14MAR05
Checked by             : H. ADAMS AND J. LUKAS
Beginning year         :  950
Ending year            : 1993
Principal investigators: R.P. GUYETTE, B. COLE                         
Site name              : DIVIDING LAKE AQUATIC
Site location          : CANADA       
Species information    : PIST EASTERN WHITE PINE
Latitude               :   4524
Longitude              : -07836
Elevation              :  400M

Series intercorrelation: 0.561
Avg mean sensitivity   : 0.182
Avg standard deviation : 0.589
Avg autocorrelation    : 0.862
Number dated series    : 50
Segment length tested  : 50

Number problem segments: 29
Pct problem segments   : 8.22


```r
cana148.crn <- read.crn("data/cana148.crn")
```

```
## There appears to be a header in the crn file
## There is 1 series
```

```r
crn.plot(cana148.crn, add.spline = TRUE, nyrs=30)
```

![](Master_Chronology_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
cana148.rwl <- read.rwl("data/cana148.rwl")
```

```
## Attempting to automatically detect format.
## Assuming a Tucson format file.
## There appears to be a header in the rwl file
## There are 50 series
## 1    	DLA015  	 1648	 1908	0.01
## 2    	DLA025  	 1658	 1974	0.01
## 3    	DLA014  	 1675	 1944	0.01
## 4    	DLA020  	 1675	 1947	0.01
## 5    	DLA024  	 1843	 1945	0.01
## 6    	DLA011  	 1680	 1920	0.01
## 7    	DLA007  	 1551	 1668	0.01
## 8    	DLA013  	 1665	 1874	0.01
## 9    	DLA023  	 1699	 1906	0.01
## 10   	DLA008  	 1737	 1915	0.01
## 11   	DLA018  	 1665	 1873	0.01
## 12   	DLA012  	 1707	 1823	0.01
## 13   	DLA005  	 1835	 1992	0.01
## 14   	DLA03   	 1793	 1983	0.01
## 15   	DLA022  	 1709	 1912	0.01
## 16   	dla100  	 1531	 1756	0.01
## 17   	DLA097  	 1719	 1967	0.01
## 18   	DLA069  	 1568	 1692	0.01
## 19   	DLA109  	 1555	 1668	0.01
## 20   	DLA067  	 1637	 1782	0.01
## 21   	DL122B  	 1555	 1780	0.01
## 22   	DLA087  	 1684	 1800	0.01
## 23   	DLA044  	 1552	 1709	0.01
## 24   	DLA098  	 1776	 1917	0.01
## 25   	DLA060  	 1398	 1574	0.01
## 26   	DLA041  	 1625	 1895	0.01
## 27   	DLA047  	 1687	 1804	0.01
## 28   	DLA111  	 1552	 1688	0.01
## 29   	DLA104  	 1477	 1725	0.01
## 30   	DLA107  	 1675	 1876	0.01
## 31   	DLA051  	 1884	 1993	0.01
## 32   	DLA066  	  950	 1152	0.01
## 33   	DLA126  	 1650	 1822	0.01
## 34   	DLA101  	 1662	 1869	0.01
## 35   	DLA064  	 1320	 1436	0.01
## 36   	DLA105  	 1665	 1810	0.01
## 37   	DLA075  	 1705	 1938	0.01
## 38   	DLA128  	 1800	 1954	0.01
## 39   	DLA068  	 1042	 1319	0.01
## 40   	DLA123  	 1750	 1948	0.01
## 41   	DLA130  	 1605	 1831	0.01
## 42   	DLA057  	 1507	 1701	0.01
## 43   	DLA052  	 1754	 1944	0.01
## 44   	DLA050  	 1636	 1803	0.01
## 45   	DLA056  	 1568	 1734	0.01
## 46   	DLA131  	 1730	 1841	0.01
## 47   	DLA63   	 1392	 1493	0.01
## 48   	DLA122  	 1517	 1650	0.01
## 49   	DLA65B  	 1322	 1442	0.01
## 50   	DLA088  	 1388	 1550	0.01
```

```r
rwl.report(cana148.rwl)
```

```
## Number of dated series: 50 
## Number of measurements: 9119 
## Avg series length: 182.38 
## Range:  1044 
## Span:  950 - 1993 
## Mean (Std dev) series intercorrelation: 0.4970208 (0.1131863)
## Mean (Std dev) AR1: 0.84128 (0.09196873)
## -------------
## Years with absent rings listed by series 
##     None 
## -------------
## Years with internal NA values listed by series 
##     None
```

```r
seg.plot(cana148.rwl)
```

![](Master_Chronology_files/figure-html/unnamed-chunk-3-2.png)<!-- -->

## Wyse - Platte Plains - PIST - ITRDB MI015

NOAA Study Page: https://www.ncdc.noaa.gov/paleo/study/5358

Platte Plains, Michigan Pinus strobus - MI015
Additional Site Information
Thomas C. Wyse, P. Charles Goebel

Purpose of Collection:  
Forest disturbance history and recruitment patterns.  

Cores are stored at: 
Forest Ecosystem Restoration & Ecology School of Natural Resources OARDC 
The Ohio State University 1680 Madison Avenue Wooster, OH 44691-4096

Description:
The site is a sandy lake plain adjacent to Lake Michigan in northwest lower Michigan.  
These cores were used with others to investigate forest disturbance history and recruitment patterns.  
All ring width measurements were done with WinDENDRO.  Cores were visually cross dated, 
and the cross dating was verified with COFECHA.


```r
mi015.rwl <- read.rwl("data/mi015.rwl")
```

```
## Attempting to automatically detect format.
## Assuming a Tucson format file.
## There appears to be a header in the rwl file
## There are 21 series
## 1    	36-1    	 1920	 2002	0.01
## 2    	13-3    	 1912	 2002	0.01
## 3    	19-3    	 1937	 2002	0.01
## 4    	28-1    	 1933	 2002	0.01
## 5    	5-1     	 1937	 2002	0.01
## 6    	10-4    	 1928	 2002	0.01
## 7    	26-3    	 1929	 2002	0.01
## 8    	12-4    	 1962	 2002	0.01
## 9    	1-4     	 1950	 2002	0.01
## 10   	2-1     	 1936	 2002	0.01
## 11   	32-3    	 1916	 2002	0.01
## 12   	12-1    	 1958	 2002	0.01
## 13   	34-2    	 1943	 2002	0.01
## 14   	6-4     	 1987	 2002	0.01
## 15   	33-1    	 1917	 2002	0.01
## 16   	9-2     	 1916	 2002	0.01
## 17   	7-2     	 1973	 2002	0.01
## 18   	14-4    	 1973	 2002	0.01
## 19   	28-3    	 1922	 2002	0.01
## 20   	6-2     	 1928	 2002	0.01
## 21   	8-1     	 1984	 2002	0.01
```

```r
rwl.report(mi015.rwl)
```

```
## Number of dated series: 21 
## Number of measurements: 1302 
## Avg series length: 62 
## Range:  91 
## Span:  1912 - 2002 
## Mean (Std dev) series intercorrelation: 0.4915569 (0.1124546)
## Mean (Std dev) AR1: 0.7149524 (0.1194401)
## -------------
## Years with absent rings listed by series 
##     Series 19-3 -- 2002 
## 1 absent rings (0.077%)
## -------------
## Years with internal NA values listed by series 
##     None
```

```r
seg.plot(mi015.rwl)
```

![](Master_Chronology_files/figure-html/unnamed-chunk-4-1.png)<!-- -->




# Create Master Chronology


## Join Chronologies


Series summary:

- pa008: 24 series; format 058xxx
- cana127: 47 series; format dlw 00x
- cana148: 50 series; format DLA 00x
- mi015: 21 series; format 00-0



```r
master.rwl <- combine.rwl(list(pa008.rwl, cana127.rwl,cana148.rwl, mi015.rwl))
rwl.report(master.rwl)
```

```
## Number of dated series: 142 
## Number of measurements: 27695 
## Avg series length: 195.0352 
## Range:  1053 
## Span:  950 - 2002 
## Mean (Std dev) series intercorrelation: 0.4408118 (0.1237108)
## Mean (Std dev) AR1: 0.8146479 (0.1121976)
## -------------
## Years with absent rings listed by series 
##     Series 058061 -- 1934 
##     Series 19-3 -- 2002 
## 2 absent rings (0.007%)
## -------------
## Years with internal NA values listed by series 
##     None
```


## Initial Removal of Series

Remove chronologies known to be misdated, problematic, or are much older than the rest of the series

4 DLW04B, #5 DLW05B, #40 DLW19A ARE MISDATED
8 DLW09A 1736-1849, #32 LDW09B 1741-1824 HAVE LOW CORRELATIONS


```r
master.stats <- rwl.stats(master.rwl) #calculate statistics
old <- filter(master.stats, first < 1600) #filter for start date
old$series #generates list of old series to remove
```

```
##  [1] DLA007 dla100 DLA069 DLA109 DL122B DLA044 DLA060 DLA111 DLA104 DLA066
## [11] DLA064 DLA068 DLA057 DLA056 DLA63  DLA122 DLA65B DLA088
## 142 Levels: 058021 058022 058031 058032 058051 058052 058061 ... dlw28a
```




```r
master.rwl <- master.rwl %>% select(-DLW04B, -dlw05b, -dlw19a, #misdated
                                    -DLW09A, -dlw09b, #low correlations
                                    -DLA060, -DLA066, -DLA068, -DLA064, -DLA65B, -DLA63, -DLA088,
                                    -DLA007, -dla100, -DLA069, -DLA109, -DL122B, -DLA044, -DLA111, 
                                    -DLA104, -DLA057, -DLA056, -DLA122 #start before 1600
                                    )
```


### Write RWL to file

```r
write.rwl(master.rwl, "outputs/master_all.rwl", format = "tucson")
```

```
## Warning in fix.names(col.names, name.width, mapping.fname, mapping.append):
## characters outside a-z, A-Z, 0-9 present: renaming series
```

```
## [1] "outputs/master_all.rwl"
```


## Plot Series & Correlate

Series summary:

- pa008: 24 series (20%); format 058xxx
- cana127: 47-5 = 42 series (35%); format dlw 00x
- cana148: 50-18 = 32 series (27%); format DLA 00x
- mi015: 21 series (18%); format 00-0


```r
rwl.report(master.rwl)
```

```
## Number of dated series: 119 
## Number of measurements: 23430 
## Avg series length: 196.8908 
## Range:  398 
## Span:  1605 - 2002 
## Mean (Std dev) series intercorrelation: 0.4439349 (0.1245525)
## Mean (Std dev) AR1: 0.8091849 (0.1173493)
## -------------
## Years with absent rings listed by series 
##     Series 058061 -- 1934 
##     Series 19-3 -- 2002 
## 2 absent rings (0.009%)
## -------------
## Years with internal NA values listed by series 
##     None
```

```r
seg.plot(master.rwl, xlim=c(1600,2010))
```

![](Master_Chronology_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

```r
master.stats <- rwl.stats(master.rwl)
```


```r
corr.master <- corr.rwl.seg(master.rwl, xlim=c(1600,2010))
```

![](Master_Chronology_files/figure-html/unnamed-chunk-10-1.png)<!-- -->



```r
flags <- as.data.frame(corr.master$flags)
head(flags)
```

```
##        corr.master$flags
## 058022         1875.1924
## 058032         1775.1824
## 058051         1900.1949
## 058061         1850.1899
## 058062         1850.1899
## 058082         1850.1899
```

```r
overall <- corr.master$overall
head(overall)
```

```
##              rho        p-val
## 058021 0.3514356 3.250403e-10
## 058022 0.4109475 1.504866e-11
## 058031 0.4939740 0.000000e+00
## 058032 0.4381695 1.654348e-13
## 058051 0.4310429 3.075955e-12
## 058052 0.5100904 0.000000e+00
```

```r
avg.seg.rho <- as.data.frame(corr.master$avg.seg.rho)
tail(avg.seg.rho)
```

```
##           corr.master$avg.seg.rho
## 1825.1874               0.5549633
## 1850.1899               0.4453117
## 1875.1924               0.4736762
## 1900.1949               0.4743822
## 1925.1974               0.3928621
## 1950.1999               0.2744713
```

There is (at least) one other way of looking at the average interseries correlation of a data set. The interseries.cor function in dplR gives a measure of average interseries correlation that is different from the rbar measurements from rwi.stats. In this function, correlations are calculated serially between each tree-ring series and a master chronology built from all the other series in the rwl object (leave-one-out principle).


```r
master.cor <- interseries.cor(master.rwl)
```

```
## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties
```

```r
head(master.cor)
```

```
##          res.cor        p.val
## 058021 0.3514356 3.250403e-10
## 058022 0.4109475 1.504866e-11
## 058031 0.4939740 0.000000e+00
## 058032 0.4381695 1.654348e-13
## 058051 0.4310429 3.075955e-12
## 058052 0.5100904 0.000000e+00
```


## Adjust Sample Size

Right now, there are a disproportionate number of samples from the cana sites, despite the three sites all being approximatly equal distance from the Pinery. I'm going to remove the samples that correlate the weakest with the rest of the chronology so that it is more representative and not bias by one location. I'll do this iteratively, by removing series based on a cutoff in groups and then re-computing the correlations. 

Series summary:

- pa008: 24 series (20%); format 058xxx
- cana127: 47-5 = 42 series (35%); format dlw 00x
- cana148: 50-18 = 32 series (27%); format DLA 00x
- mi015: 21 series (18%); format 00-0


### Remove Flags

Remove flags, only from cana sites for now because of the disproportionate number of samples


```r
flags <- tibble::rownames_to_column(flags, "sample") #add years from row names
str(flags)
```

```
## 'data.frame':	27 obs. of  2 variables:
##  $ sample           : chr  "058022" "058032" "058051" "058061" ...
##  $ corr.master$flags: Factor w/ 14 levels "1700.1749","1750.1799",..: 9 6 10 8 8 8 12 4 12 10 ...
```

```r
flags.cana <- flags %>% filter(str_detect(sample, fixed('dl', ignore_case=TRUE)))
flags.cana$sample
```

```
## [1] "dlw02a" "dlw12a" "dlw17a" "dlw24b" "dlw12b" "dlw24a" "DLA020" "DLA008"
## [9] "DLA105"
```


Remove from RWL file


```r
#Remove flags
master.rwl <- master.rwl %>% select(-dlw02a, -dlw12a, -dlw17a, -dlw24b, -dlw12b, -dlw24a, -DLA020, -DLA008, -DLA105)

#Re-compute correlation
master.cor <- interseries.cor(master.rwl)
```

```
## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties
```


### Remove by Correlation 



```r
master.cor <- tibble::rownames_to_column(master.cor, "sample") #add years from row names

#Correlations for each site
master.cor.pa008 <- master.cor %>% filter(str_detect(sample, '^058'))
master.cor.cana127 <- master.cor %>% filter(str_detect(sample, fixed('dlw', ignore_case=TRUE)))
master.cor.cana148 <- master.cor %>% filter(str_detect(sample, fixed('dla', ignore_case=TRUE)))
master.cor.mi015 <- master.cor %>% filter(str_detect(sample, '-'))

#Correlations for both Cana sites
master.cor.cana <- master.cor %>% filter(str_detect(sample, fixed('dl', ignore_case=TRUE))) 
master.cor.cana %>% arrange(res.cor)
```

```
##    sample   res.cor        p.val
## 1  DLA024 0.2568955 5.219461e-03
## 2  dlw10a 0.3518071 3.829818e-07
## 3  dlw28a 0.3605749 1.332793e-06
## 4  DLA128 0.3606778 2.706800e-06
## 5  DLA098 0.3648655 6.718499e-06
## 6  dlw14a 0.3782481 1.386151e-12
## 7   DLA03 0.4080823 2.542894e-09
## 8  DLA075 0.4167618 8.511832e-11
## 9  dlw14b 0.4240592 6.433539e-16
## 10 DLA005 0.4254169 1.395845e-08
## 11 DLA014 0.4378191 8.356880e-14
## 12 dlw26a 0.4492272 0.000000e+00
## 13 DLA025 0.4495683 0.000000e+00
## 14 DLA131 0.4586181 2.074375e-07
## 15 dlw029 0.4682962 2.877052e-12
## 16 DLA012 0.4784070 4.135438e-08
## 17 dlw01b 0.4786063 0.000000e+00
## 18 dlw16a 0.4789021 0.000000e+00
## 19 DLA011 0.4801881 0.000000e+00
## 20 dlw22a 0.4854468 3.150749e-11
## 21 DLA107 0.4892444 0.000000e+00
## 22 DLA018 0.4900316 0.000000e+00
## 23 DLA013 0.4906000 0.000000e+00
## 24 dlw01a 0.4919291 0.000000e+00
## 25 DLW25A 0.4935558 0.000000e+00
## 26 dlw18b 0.5069303 0.000000e+00
## 27 DLA050 0.5129378 0.000000e+00
## 28 DLA022 0.5146810 0.000000e+00
## 29 dlw19b 0.5148882 2.177016e-10
## 30 dlw18a 0.5152435 0.000000e+00
## 31 dlw15a 0.5166273 7.134241e-13
## 32 dlw17b 0.5172328 0.000000e+00
## 33 DLA067 0.5184551 5.617419e-12
## 34 dlw07a 0.5188136 7.152354e-09
## 35 DLA130 0.5205056 0.000000e+00
## 36 DLA023 0.5205723 0.000000e+00
## 37 dlw15b 0.5211638 6.857381e-11
## 38 dlw03b 0.5222324 6.195625e-18
## 39 dlw07b 0.5237383 2.543440e-09
## 40 DLA047 0.5269973 7.986906e-10
## 41 dlw13a 0.5341388 0.000000e+00
## 42 DLA051 0.5396964 6.990243e-10
## 43 DLA015 0.5429470 0.000000e+00
## 44 DLA123 0.5443831 0.000000e+00
## 45 DLA041 0.5478259 0.000000e+00
## 46 dlw03a 0.5484566 0.000000e+00
## 47 dlw16b 0.5505385 0.000000e+00
## 48 DLA101 0.5513817 0.000000e+00
## 49 dlw23b 0.5549251 0.000000e+00
## 50 dlw11c 0.5560829 0.000000e+00
## 51 dlw27a 0.5640770 0.000000e+00
## 52 dlw08a 0.5657135 0.000000e+00
## 53 DLW20A 0.5691734 0.000000e+00
## 54 DLA126 0.5692780 0.000000e+00
## 55 DLA052 0.5804622 0.000000e+00
## 56 dlw11a 0.5894172 0.000000e+00
## 57 dlw27b 0.5972429 0.000000e+00
## 58 dlw08b 0.5989879 0.000000e+00
## 59 dlw25b 0.6036693 0.000000e+00
## 60 dlw26b 0.6057657 0.000000e+00
## 61 dlw06a 0.6081993 0.000000e+00
## 62 dlw20b 0.6235699 0.000000e+00
## 63 DLA087 0.6309674 0.000000e+00
## 64 dlw05a 0.6355094 0.000000e+00
## 65 DLA097 0.6455966 0.000000e+00
```

```r
#Filter based on correlation
master.cor.cana.low <- master.cor.cana %>% filter(res.cor < 0.51) #cutoff correlation of 0.51
master.cor.cana.low$sample
```

```
##  [1] "dlw01a" "dlw10a" "dlw14a" "dlw16a" "dlw18b" "dlw029" "dlw01b"
##  [8] "dlw14b" "dlw22a" "DLW25A" "dlw26a" "dlw28a" "DLA025" "DLA014"
## [15] "DLA024" "DLA011" "DLA013" "DLA018" "DLA012" "DLA005" "DLA03" 
## [22] "DLA098" "DLA107" "DLA075" "DLA128" "DLA131"
```

Remove from RWL file


```r
#Remove low correlations
master.rwl <- master.rwl %>% select(-dlw01a, -dlw10a, -dlw14a, -dlw16a, -dlw18b, -dlw029, 
                                    -dlw01b, -dlw14b, -dlw22a, -DLW25A, -dlw26a, -dlw28a, 
                                    -DLA025, -DLA014, -DLA024, -DLA011, -DLA013, -DLA018, 
                                    -DLA012, -DLA005, -DLA03, -DLA098, -DLA107, -DLA075,
                                    -DLA128, -DLA131)
#Re-compute correlations
master.cor <- interseries.cor(master.rwl)
```

```
## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties
```

### Repeat Removal by Correlation

Series summary:

- pa008: 24 series; format 058xxx
- cana127: 24 series; format dlw 00x
- cana148: 15 series; format DLA 00x
- mi015: 21 series; format 00-0


```r
master.cor <- tibble::rownames_to_column(master.cor, "sample") #add years from row names

#Correlations for each site
master.cor.cana127 <- master.cor %>% filter(str_detect(sample, fixed('dlw', ignore_case=TRUE)))
master.cor.cana148
```

```
##    sample   res.cor        p.val
## 1  DLA015 0.5429470 0.000000e+00
## 2  DLA025 0.4495683 0.000000e+00
## 3  DLA014 0.4378191 8.356880e-14
## 4  DLA024 0.2568955 5.219461e-03
## 5  DLA011 0.4801881 0.000000e+00
## 6  DLA013 0.4906000 0.000000e+00
## 7  DLA023 0.5205723 0.000000e+00
## 8  DLA018 0.4900316 0.000000e+00
## 9  DLA012 0.4784070 4.135438e-08
## 10 DLA005 0.4254169 1.395845e-08
## 11  DLA03 0.4080823 2.542894e-09
## 12 DLA022 0.5146810 0.000000e+00
## 13 DLA097 0.6455966 0.000000e+00
## 14 DLA067 0.5184551 5.617419e-12
## 15 DLA087 0.6309674 0.000000e+00
## 16 DLA098 0.3648655 6.718499e-06
## 17 DLA041 0.5478259 0.000000e+00
## 18 DLA047 0.5269973 7.986906e-10
## 19 DLA107 0.4892444 0.000000e+00
## 20 DLA051 0.5396964 6.990243e-10
## 21 DLA126 0.5692780 0.000000e+00
## 22 DLA101 0.5513817 0.000000e+00
## 23 DLA075 0.4167618 8.511832e-11
## 24 DLA128 0.3606778 2.706800e-06
## 25 DLA123 0.5443831 0.000000e+00
## 26 DLA130 0.5205056 0.000000e+00
## 27 DLA052 0.5804622 0.000000e+00
## 28 DLA050 0.5129378 0.000000e+00
## 29 DLA131 0.4586181 2.074375e-07
```

```r
master.cor.cana148 <- master.cor %>% filter(str_detect(sample, fixed('dla', ignore_case=TRUE)))

#Correlations for both Cana sites
master.cor.cana <- master.cor %>% filter(str_detect(sample, fixed('dl', ignore_case=TRUE))) 
master.cor.cana %>% arrange(res.cor)
```

```
##    sample   res.cor        p.val
## 1  DLA022 0.4488990 2.019798e-11
## 2  dlw03b 0.4618952 5.800152e-14
## 3  dlw07b 0.4643370 1.750415e-07
## 4  dlw17b 0.4648089 0.000000e+00
## 5  dlw15a 0.4662471 1.567261e-10
## 6  DLA023 0.4663880 7.738514e-13
## 7  DLA050 0.4703203 1.346069e-10
## 8  dlw15b 0.4767652 5.041995e-09
## 9  dlw18a 0.4791546 1.482691e-11
## 10 dlw16b 0.4798712 0.000000e+00
## 11 dlw13a 0.4840109 0.000000e+00
## 12 dlw19b 0.4883468 2.564729e-09
## 13 DLA047 0.4913606 1.435773e-08
## 14 dlw03a 0.4923310 0.000000e+00
## 15 DLA101 0.4932673 0.000000e+00
## 16 DLA130 0.5005158 0.000000e+00
## 17 dlw11c 0.5115456 0.000000e+00
## 18 DLA123 0.5123951 0.000000e+00
## 19 DLA067 0.5141387 1.660480e-11
## 20 DLA015 0.5188559 0.000000e+00
## 21 DLA051 0.5204812 3.294156e-09
## 22 dlw07a 0.5208196 6.151237e-09
## 23 dlw27a 0.5211824 0.000000e+00
## 24 DLA041 0.5281951 0.000000e+00
## 25 DLW20A 0.5295994 0.000000e+00
## 26 dlw08a 0.5327771 0.000000e+00
## 27 dlw11a 0.5332317 0.000000e+00
## 28 DLA126 0.5335612 0.000000e+00
## 29 dlw23b 0.5413676 0.000000e+00
## 30 dlw27b 0.5491772 0.000000e+00
## 31 dlw26b 0.5557607 0.000000e+00
## 32 DLA052 0.5664747 0.000000e+00
## 33 dlw25b 0.5665841 0.000000e+00
## 34 dlw06a 0.5672082 0.000000e+00
## 35 dlw05a 0.5674017 0.000000e+00
## 36 dlw08b 0.5687433 0.000000e+00
## 37 DLA097 0.5728154 0.000000e+00
## 38 dlw20b 0.5806139 0.000000e+00
## 39 DLA087 0.5830704 0.000000e+00
```

```r
#Filter based on correlation
master.cor.cana.low <- master.cor.cana %>% filter(res.cor < 0.50) #cutoff correlation of 0.50
master.cor.cana.low$sample
```

```
##  [1] "dlw03a" "dlw13a" "dlw15a" "dlw19b" "dlw03b" "dlw07b" "dlw15b"
##  [8] "dlw16b" "dlw17b" "dlw18a" "DLA023" "DLA022" "DLA047" "DLA101"
## [15] "DLA050"
```

Remove from RWL file


```r
#Remove low correlations
master.rwl <- master.rwl %>% select(-dlw03a, dlw13a, -dlw15a, -dlw19b, -dlw03b, 
                                    -dlw07b, -dlw15b, -dlw16b, -dlw17b, -dlw18a, 
                                    -DLA023, -DLA022, -DLA047, -DLA101, -DLA050)
#Re-compute correlations
master.cor <- interseries.cor(master.rwl)
```

```
## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties
```


## Refine Master Chronology (Correlation & Flags)

### First Iteration

Series summary:

- pa008: 24 series (34%); format 058xxx
- cana127: 15 series (21%); format dlw 00x
- cana148: 10 series (14%); format DLA 00x
- mi015: 21 series (30%); format 00-0

Now that the three locations all comprise ~33% of the samples in the master chronology, I'm going to look for any samples with low correlations or that flag to remove. 


```r
master.cor <- tibble::rownames_to_column(master.cor, "sample") #add years from row names
master.cor %>% arrange(res.cor)
```

```
##    sample   res.cor        p.val
## 1    33-1 0.2435760 1.290095e-02
## 2  058211 0.2489064 1.453309e-04
## 3     1-4 0.2548450 3.423378e-02
## 4    10-4 0.2586449 1.317238e-02
## 5    13-3 0.2603466 7.255618e-03
## 6    28-3 0.2700097 8.176187e-03
## 7     6-2 0.2746686 9.069438e-03
## 8     5-1 0.2934003 9.000939e-03
## 9    34-2 0.2935495 1.283978e-02
## 10   12-1 0.2945840 2.612242e-02
## 11    6-4 0.3142857 1.367468e-01
## 12   19-3 0.3332022 3.341767e-03
## 13    7-2 0.3393541 3.890638e-02
## 14   14-4 0.3418719 3.503401e-02
## 15 058122 0.3445983 8.769858e-09
## 16   28-1 0.3476434 1.796192e-03
## 17   36-1 0.3567332 5.370362e-04
## 18   32-3 0.3876692 1.259478e-04
## 19    2-1 0.3942308 6.279258e-04
## 20    9-2 0.3962869 9.770187e-05
## 21   26-3 0.4374614 6.353902e-05
## 22 dlw13a 0.4379234 3.495205e-13
## 23 058021 0.4395980 0.000000e+00
## 24 dlw11c 0.4412800 0.000000e+00
## 25 DLA130 0.4514978 1.002231e-11
## 26 DLA015 0.4529062 0.000000e+00
## 27 DLA041 0.4587786 0.000000e+00
## 28 DLA067 0.4713568 1.896147e-09
## 29 058152 0.4730440 9.139860e-18
## 30 dlw08a 0.4788281 0.000000e+00
## 31 dlw27a 0.4792008 0.000000e+00
## 32 dlw11a 0.4800313 0.000000e+00
## 33 DLW20A 0.4838462 0.000000e+00
## 34 DLA123 0.4841609 2.043172e-12
## 35 dlw07a 0.4853488 7.707901e-08
## 36 058022 0.4880301 0.000000e+00
## 37 dlw05a 0.4990640 0.000000e+00
## 38 DLA051 0.4998622 1.567310e-08
## 39 dlw26b 0.5019498 0.000000e+00
## 40 dlw23b 0.5026996 0.000000e+00
## 41 dlw27b 0.5038942 0.000000e+00
## 42 058141 0.5044776 0.000000e+00
## 43 058071 0.5055818 0.000000e+00
## 44 DLA087 0.5061015 7.408914e-09
## 45 dlw06a 0.5083696 0.000000e+00
## 46 058151 0.5096539 0.000000e+00
## 47    8-1 0.5098039 1.932078e-02
## 48 DLA126 0.5107752 0.000000e+00
## 49 DLA097 0.5127873 0.000000e+00
## 50 dlw20b 0.5189875 0.000000e+00
## 51 dlw08b 0.5210804 0.000000e+00
## 52 058121 0.5253849 0.000000e+00
## 53 058202 0.5272316 0.000000e+00
## 54 058142 0.5326683 0.000000e+00
## 55 058102 0.5344544 8.544697e-22
## 56 058191 0.5359554 0.000000e+00
## 57 dlw25b 0.5385741 0.000000e+00
## 58 DLA052 0.5455557 0.000000e+00
## 59   12-4 0.5497186 1.495766e-04
## 60 058061 0.5546450 0.000000e+00
## 61 058051 0.5577048 0.000000e+00
## 62 058062 0.5794697 6.663897e-27
## 63 058082 0.5818860 0.000000e+00
## 64 058101 0.5840903 0.000000e+00
## 65 058032 0.5910455 0.000000e+00
## 66 058031 0.6077885 0.000000e+00
## 67 058081 0.6108825 0.000000e+00
## 68 058052 0.6133857 0.000000e+00
## 69 058072 0.6247410 6.601451e-32
## 70 058201 0.7086074 0.000000e+00
```



```r
corr.master <- corr.rwl.seg(master.rwl, xlim=c(1600,2010))
```

![](Master_Chronology_files/figure-html/unnamed-chunk-20-1.png)<!-- -->



```r
flags <- as.data.frame(corr.master$flags)
flags
```

```
##                      corr.master$flags
## 058121                       1925.1974
## 058122                       1925.1974
## 058141                       1925.1974
## 058202                       1925.1974
## 058211 1775.1824, 1900.1949, 1925.1974
## dlw11c                       1875.1924
## DLA015                       1725.1774
## DLA126                       1700.1749
## DLA130                       1750.1799
## 13-3                         1950.1999
## 33-1                         1925.1974
```

Here I'm remove any samples that both have a flag/correlate poorly while ensuring proportional sample sizes. 

The mi015 samples have the lowest correlations, but they are the most recent and still are adequete so I'm not removing many of them.

Remove from RWL file


```r
#Remove low flags/correlations
master.rwl <- master.rwl %>% select(-"058211", -"33-1", -"058122", -"13-3", -dlw11c, -DLA130, -"058121", -"058122", -"058141", -DLA015, -DLA126, -DLA130)

#Re-compute correlations
master.cor <- interseries.cor(master.rwl)
```

```
## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties
```

```r
master.cor <- tibble::rownames_to_column(master.cor, "sample") #add years from row names
```


### Second Iteration

Locations of Samples:

- pa008: 20 series (33%); format 058xxx
- cana127: 14 series (23%); format dlw 00x
- cana148: 7 series (12%); format DLA 00x
- mi015: 19 series (31%); format 00-0


```r
corr.master <- corr.rwl.seg(master.rwl, xlim=c(1600,2010))
```

![](Master_Chronology_files/figure-html/unnamed-chunk-23-1.png)<!-- -->

```r
flags <- as.data.frame(corr.master$flags)
flags
```

```
##           corr.master$flags
## 058202            1925.1974
## DLA067            1700.1749
## DLA041 1700.1749, 1725.1774
```

The two samples from cana148 flagging are older and can be removed


```r
#Remove flags/low correlations
master.rwl <- master.rwl %>% select(-"058202", -DLA067, -DLA041)

#Re-compute correlations
master.cor <- interseries.cor(master.rwl)
```

```
## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties

## Warning in cor.test.default(series[, i], master[, i], method = method2, :
## Cannot compute exact p-value with ties
```

```r
master.cor <- tibble::rownames_to_column(master.cor, "sample") #add years from row names
```


## Summary of Master Chronology

Series summary:

- pa008: 19 series (33%); format 058xxx
- cana127: 14 series (24%); format dlw 00x
- cana148: 5 series (9%); format DLA 00x
- mi015: 19 series (33%); format 00-0



```r
rwl.report(master.rwl)
```

```
## Number of dated series: 57 
## Number of measurements: 10137 
## Avg series length: 177.8421 
## Range:  324 
## Span:  1679 - 2002 
## Mean (Std dev) series intercorrelation: 0.4719945 (0.09495867)
## Mean (Std dev) AR1: 0.7817895 (0.1135489)
## -------------
## Years with absent rings listed by series 
##     Series 058061 -- 1934 
##     Series 19-3 -- 2002 
## 2 absent rings (0.02%)
## -------------
## Years with internal NA values listed by series 
##     None
```

As compared to the initial report:

- Number of dated series: 142 
- Number of measurements: 27695 
- Avg series length: 195.0352 
- Range:  1053 
- Span:  950 - 2002 
- Mean (Std dev) series intercorrelation: 0.4408118 (0.1237108)
- Mean (Std dev) AR1: 0.8146479 (0.1121976)


```r
seg.plot(master.rwl, xlim=c(1675,2010))
```

![](Master_Chronology_files/figure-html/unnamed-chunk-26-1.png)<!-- -->


```r
corr.master <- corr.rwl.seg(master.rwl, xlim=c(1675,2005))
```

![](Master_Chronology_files/figure-html/unnamed-chunk-27-1.png)<!-- -->


```r
avg.seg.rho <- as.data.frame(corr.master$avg.seg.rho)
tail(avg.seg.rho)
```

```
##           corr.master$avg.seg.rho
## 1825.1874               0.6061646
## 1850.1899               0.5187919
## 1875.1924               0.4866719
## 1900.1949               0.4784519
## 1925.1974               0.3938473
## 1950.1999               0.4344786
```


### Write RWL to file


```r
write.rwl(master.rwl, "outputs/master.rwl", format = "tucson")
```

```
## Warning in fix.names(col.names, name.width, mapping.fname, mapping.append):
## characters outside a-z, A-Z, 0-9 present: renaming series
```

```
## [1] "outputs/master.rwl"
```



## Detrend

Probably the most common method for detrending is what is often called the “conservative” approach of attempting to fit a negative exponential curve
to a series. In the dplR implementation the "ModNegExp" method of detrend attempts to fit a classic nonlinear model of biological growth of the form f(t) = a exp(bt) + k, where the argument of the function is time, using nls.


```r
master.rwi <- detrend(rwl = master.rwl, method = "ModNegExp")
```


### Compute Statistics

Can also be done with a moving window


```r
rwi.stats(master.rwi)
```

```
##   n.cores n.trees     n n.tot n.wt n.bt rbar.tot rbar.wt rbar.bt c.eff
## 1      57      57 9.627  1236    0 1236    0.134      NA   0.134     1
##   rbar.eff   eps   snr
## 1    0.134 0.599 1.491
```


### Build Chronology


```r
master.crn <- chron(master.rwi)
plot(master.crn, add.spline=TRUE, nyrs=30, xlim=c(1675,2010))
```

![](Master_Chronology_files/figure-html/unnamed-chunk-32-1.png)<!-- -->

### Add Uncertainty Estimates


```r
master.avg <- apply(master.rwi,1,mean,na.rm=TRUE)

yrs <- time(master.crn)


se <- function(x){
  x2 <- na.omit(x)
  n <- length(x2)
  sd(x2)/sqrt(n)}


master.se <- apply(master.rwi,1,se)

master.sd <- apply(master.rwi,1,sd,na.rm=TRUE)

par(mar = c(2, 2, 2, 2), mgp = c(1.1, 0.1, 0), tcl = 0.25, xaxs='i')

plot(yrs, master.avg, type = "n", xlab = "Year", ylab = "RWI", axes=FALSE, xlim=c(1675,2010))
xx <- c(yrs,rev(yrs))
yy <- c(master.avg+master.se*2,rev(master.avg-master.se*2))
polygon(xx,yy,col="grey80",border = NA)
lines(yrs, master.avg, col = "black")
lines(yrs, ffcsaps(master.avg, nyrs = 30), col = "red", lwd = 2)
axis(1); axis(2); axis(3); axis(4)
box()
```

![](Master_Chronology_files/figure-html/unnamed-chunk-33-1.png)<!-- -->


# Conclude Session


```r
sessionInfo()
```

```
## R version 3.6.2 (2019-12-12)
## Platform: x86_64-apple-darwin15.6.0 (64-bit)
## Running under: macOS Catalina 10.15.3
## 
## Matrix products: default
## BLAS:   /Library/Frameworks/R.framework/Versions/3.6/Resources/lib/libRblas.0.dylib
## LAPACK: /Library/Frameworks/R.framework/Versions/3.6/Resources/lib/libRlapack.dylib
## 
## locale:
## [1] en_CA.UTF-8/en_CA.UTF-8/en_CA.UTF-8/C/en_CA.UTF-8/en_CA.UTF-8
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] stringr_1.4.0 corrplot_0.84 ggplot2_3.2.1 dplyr_0.8.3   tidyr_1.0.2  
## [6] dplR_1.6.9   
## 
## loaded via a namespace (and not attached):
##  [1] Rcpp_1.0.3         compiler_3.6.2     pillar_1.4.3      
##  [4] plyr_1.8.5         iterators_1.0.12   R.methodsS3_1.7.1 
##  [7] R.utils_2.9.2      tools_3.6.2        digest_0.6.23     
## [10] gtable_0.3.0       evaluate_0.14      tibble_2.1.3      
## [13] lifecycle_0.1.0    lattice_0.20-38    pkgconfig_2.0.3   
## [16] png_0.1-7          rlang_0.4.3        foreach_1.4.7     
## [19] Matrix_1.2-18      yaml_2.2.0         xfun_0.7          
## [22] withr_2.1.2        knitr_1.23         vctrs_0.2.2       
## [25] grid_3.6.2         tidyselect_1.0.0   glue_1.3.1        
## [28] R6_2.4.1           XML_3.98-1.20      rmarkdown_1.13    
## [31] animation_2.6      purrr_0.3.3        magrittr_1.5      
## [34] codetools_0.2-16   scales_1.1.0       matrixStats_0.54.0
## [37] htmltools_0.4.0    MASS_7.3-51.5      assertthat_0.2.1  
## [40] colorspace_1.4-1   stringi_1.4.5      lazyeval_0.2.2    
## [43] munsell_0.5.0      signal_0.7-6       crayon_1.3.4      
## [46] R.oo_1.23.0
```





Final Project Dataset
================
Maya Bunyan, Lunbei Hu, Michelle Lui, Ling Yi, Gauri Bhatkhande, Pallavi
Krishnamurthy

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(rnoaa)

# Get a list of all NY station IDs
stations <- ghcnd_stations()
```

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/ghcnd-stations.rds

    ## date created (size, mb): 2020-11-02 08:56:45 (2.084)

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/ghcnd-inventory.rds

    ## date created (size, mb): 2020-11-02 08:57:35 (2.572)

``` r
stationids <-  stations %>% 
  filter(state %in% c("AL","AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA", "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY")) %>%
  distinct(id, .keep_all = T) %>%
  select(id, state)

ids = stationids %>% group_by(state) %>% sample_n(10)


# Pull the desired weather data for all of these stations
noaadat <- meteo_pull_monitors(ids$id, 
                             date_min = "2020-01-01", 
                             date_max = "2020-10-31", 
                             var = c("PRCP", "TAVG", "TMAX", "TMIN"))
```

    ## file min/max dates: 1932-04-01 / 1946-06-30

    ## file min/max dates: 1996-12-01 / 1998-08-31

    ## file min/max dates: 1996-08-01 / 1998-04-30

    ## file min/max dates: 1975-11-01 / 1976-04-30

    ## file min/max dates: 1996-08-01 / 2013-07-31

    ## file min/max dates: 1991-07-01 / 2020-11-30

    ## file min/max dates: 1973-11-01 / 1975-11-30

    ## file min/max dates: 1905-08-01 / 1976-10-31

    ## file min/max dates: 1917-10-01 / 1933-01-31

    ## file min/max dates: 1996-12-01 / 2019-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ALWS0005.dly

    ## date created (size, mb): 2020-11-02 09:48:37 (0.017)

    ## file min/max dates: 2008-01-01 / 2009-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ALMN0006.dly

    ## date created (size, mb): 2020-11-02 09:46:20 (0.015)

    ## file min/max dates: 2018-08-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ALCS0002.dly

    ## date created (size, mb): 2020-11-02 09:41:36 (0.05)

    ## file min/max dates: 2007-11-01 / 2012-04-30

    ## file min/max dates: 1900-01-01 / 1967-09-30

    ## file min/max dates: 2006-08-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CHARM182.dly

    ## date created (size, mb): 2020-11-02 10:29:17 (0.028)

    ## file min/max dates: 2007-11-01 / 2008-12-31

    ## file min/max dates: 1949-01-01 / 1949-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CHARM053.dly

    ## date created (size, mb): 2020-11-02 10:28:31 (0.217)

    ## file min/max dates: 2007-10-01 / 2017-04-30

    ## file min/max dates: 1900-12-01 / 2013-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ALBW0019.dly

    ## date created (size, mb): 2020-11-02 09:40:28 (0.04)

    ## file min/max dates: 2008-01-01 / 2011-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARBX0028.dly

    ## date created (size, mb): 2020-11-02 09:49:36 (0.055)

    ## file min/max dates: 2012-08-01 / 2017-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARFK0001.dly

    ## date created (size, mb): 2020-11-02 09:00:42 (0.062)

    ## file min/max dates: 2009-02-01 / 2017-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARBT0002.dly

    ## date created (size, mb): 2020-11-02 09:48:55 (0.018)

    ## file min/max dates: 2009-04-01 / 2009-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARCN0001.dly

    ## date created (size, mb): 2020-11-02 09:50:05 (0.095)

    ## file min/max dates: 2010-09-01 / 2016-09-30

    ## file min/max dates: 1985-05-01 / 2017-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARFK0011.dly

    ## date created (size, mb): 2020-11-02 09:50:46 (0.095)

    ## file min/max dates: 2012-06-01 / 2020-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARSL0033.dly

    ## date created (size, mb): 2020-11-02 09:01:09 (0.026)

    ## file min/max dates: 2017-03-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARSB0001.dly

    ## date created (size, mb): 2020-11-02 09:54:38 (0.012)

    ## file min/max dates: 2009-04-01 / 2009-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ARLF0004.dly

    ## date created (size, mb): 2020-11-02 09:52:07 (0.015)

    ## file min/max dates: 2012-06-01 / 2013-05-31

    ## file min/max dates: 2011-01-01 / 2015-01-31

    ## file min/max dates: 1944-06-01 / 1975-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1AZCH0005.dly

    ## date created (size, mb): 2020-11-02 09:56:31 (0.101)

    ## file min/max dates: 2009-08-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1AZMH0004.dly

    ## date created (size, mb): 2020-11-02 09:58:11 (0.1)

    ## file min/max dates: 1998-06-01 / 2018-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1AZYV0056.dly

    ## date created (size, mb): 2020-11-02 10:08:06 (0.02)

    ## file min/max dates: 2014-08-01 / 2015-12-31

    ## file min/max dates: 1957-10-01 / 2012-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1AZPM0085.dly

    ## date created (size, mb): 2020-11-02 10:03:36 (0.031)

    ## file min/max dates: 2001-07-01 / 2018-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1AZMR0200.dly

    ## date created (size, mb): 2020-11-02 10:00:01 (0.022)

    ## file min/max dates: 2009-12-01 / 2014-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1AZGH0003.dly

    ## date created (size, mb): 2020-11-02 09:57:57 (0.02)

    ## file min/max dates: 2009-12-01 / 2011-06-30

    ## file min/max dates: 1995-06-01 / 2020-11-30

    ## file min/max dates: 1963-06-01 / 2020-11-30

    ## file min/max dates: 1918-01-01 / 1977-02-28

    ## file min/max dates: 1948-07-01 / 1950-01-31

    ## file min/max dates: 1906-04-01 / 2010-12-31

    ## file min/max dates: 2001-06-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CAYB0003.dly

    ## date created (size, mb): 2020-11-02 10:27:51 (0.086)

    ## file min/max dates: 2011-11-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CASS0001.dly

    ## date created (size, mb): 2020-11-02 10:25:50 (0.36)

    ## file min/max dates: 1998-06-01 / 2020-10-31

    ## file min/max dates: 1980-06-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CAFR0022.dly

    ## date created (size, mb): 2020-11-02 10:11:01 (0.041)

    ## file min/max dates: 2015-10-01 / 2020-05-31

    ## file min/max dates: 1943-11-01 / 1957-12-31

    ## file min/max dates: 1933-09-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COAU0013.dly

    ## date created (size, mb): 2020-11-02 10:34:11 (0.045)

    ## file min/max dates: 2009-04-01 / 2012-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COBO0318.dly

    ## date created (size, mb): 2020-11-02 10:38:20 (0.019)

    ## file min/max dates: 2012-06-01 / 2013-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COWE0068.dly

    ## date created (size, mb): 2020-11-02 11:28:24 (0.064)

    ## file min/max dates: 1999-06-01 / 2003-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COBO0468.dly

    ## date created (size, mb): 2020-11-02 10:39:22 (0.083)

    ## file min/max dates: 2017-06-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COLG0007.dly

    ## date created (size, mb): 2020-11-02 11:02:49 (0.04)

    ## file min/max dates: 2002-06-01 / 2004-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COAD0087.dly

    ## date created (size, mb): 2020-11-02 10:30:17 (0.319)

    ## file min/max dates: 2005-04-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COEL0001.dly

    ## date created (size, mb): 2020-11-02 10:47:53 (0.15)

    ## file min/max dates: 2000-05-01 / 2009-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COCF0014.dly

    ## date created (size, mb): 2020-11-02 10:40:35 (0.088)

    ## file min/max dates: 2004-06-01 / 2018-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COGF0050.dly

    ## date created (size, mb): 2020-11-02 10:53:45 (0.061)

    ## file min/max dates: 2009-12-01 / 2014-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1COFM0032.dly

    ## date created (size, mb): 2020-11-02 10:52:44 (0.06)

    ## file min/max dates: 2004-04-01 / 2007-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CTFR0055.dly

    ## date created (size, mb): 2020-11-02 11:32:48 (0.049)

    ## file min/max dates: 2018-04-01 / 2020-10-31

    ## file min/max dates: 1916-02-01 / 2014-03-31

    ## file min/max dates: 1949-06-01 / 1960-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CTTL0013.dly

    ## date created (size, mb): 2020-11-02 11:35:12 (0.014)

    ## file min/max dates: 2016-04-01 / 2017-09-30

    ## file min/max dates: 1948-06-01 / 2020-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CTMD0018.dly

    ## date created (size, mb): 2020-11-02 11:34:15 (0.026)

    ## file min/max dates: 2018-04-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CTHR0080.dly

    ## date created (size, mb): 2020-11-02 11:33:39 (0.021)

    ## file min/max dates: 2018-09-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CTTL0016.dly

    ## date created (size, mb): 2020-11-02 11:35:15 (0.032)

    ## file min/max dates: 2016-04-01 / 2018-09-30

    ## file min/max dates: 1949-09-01 / 1960-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1CTLT0004.dly

    ## date created (size, mb): 2020-11-02 11:33:44 (0.023)

    ## file min/max dates: 2009-06-01 / 2010-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1DESS0031.dly

    ## date created (size, mb): 2020-11-02 11:36:44 (0.102)

    ## file min/max dates: 2014-12-01 / 2020-10-31

    ## file min/max dates: 1952-09-01 / 1988-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1DEKN0020.dly

    ## date created (size, mb): 2020-11-02 11:35:50 (0.084)

    ## file min/max dates: 2016-03-01 / 2020-11-30

    ## file min/max dates: 1946-07-01 / 1970-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1DEKN0026.dly

    ## date created (size, mb): 2020-11-02 11:35:55 (0.063)

    ## file min/max dates: 2017-09-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1DEKN0010.dly

    ## date created (size, mb): 2020-11-02 11:35:44 (0.024)

    ## file min/max dates: 2014-11-01 / 2017-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1DENC0028.dly

    ## date created (size, mb): 2020-11-02 11:36:16 (0.065)

    ## file min/max dates: 2016-04-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1DESS0007.dly

    ## date created (size, mb): 2020-11-02 11:36:36 (0.049)

    ## file min/max dates: 2009-09-01 / 2012-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1DEKN0001.dly

    ## date created (size, mb): 2020-11-02 11:35:38 (0.163)

    ## file min/max dates: 2009-09-01 / 2020-11-30

    ## file min/max dates: 2002-11-01 / 2015-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLCR0024.dly

    ## date created (size, mb): 2020-11-02 11:40:20 (0.056)

    ## file min/max dates: 2011-05-01 / 2014-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLSL0041.dly

    ## date created (size, mb): 2020-11-02 11:55:24 (0.036)

    ## file min/max dates: 2015-09-01 / 2018-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLDV0033.dly

    ## date created (size, mb): 2020-11-02 11:41:45 (0.163)

    ## file min/max dates: 2008-09-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLDV0003.dly

    ## date created (size, mb): 2020-11-02 11:41:30 (0.168)

    ## file min/max dates: 2007-10-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLLV0001.dly

    ## date created (size, mb): 2020-11-02 11:48:01 (0.218)

    ## file min/max dates: 2007-09-01 / 2020-11-30

    ## file min/max dates: 1940-03-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLBW0087.dly

    ## date created (size, mb): 2020-11-02 11:39:16 (0.052)

    ## file min/max dates: 2014-10-01 / 2019-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLBW0130.dly

    ## date created (size, mb): 2020-11-02 11:39:30 (0.015)

    ## file min/max dates: 2017-09-01 / 2019-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLOK0004.dly

    ## date created (size, mb): 2020-11-02 11:50:42 (0.025)

    ## file min/max dates: 2007-10-01 / 2010-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1FLHN0019.dly

    ## date created (size, mb): 2020-11-02 11:45:32 (0.076)

    ## file min/max dates: 2009-06-01 / 2015-12-31

    ## file min/max dates: 1953-01-01 / 1956-03-31

    ## file min/max dates: 1996-01-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1GAER0002.dly

    ## date created (size, mb): 2020-11-02 12:04:27 (0.008)

    ## file min/max dates: 2011-08-01 / 2012-02-29

    ## file min/max dates: 1891-11-01 / 1914-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1GALR0003.dly

    ## date created (size, mb): 2020-11-02 12:08:46 (0.073)

    ## file min/max dates: 2008-05-01 / 2013-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1GADG0002.dly

    ## date created (size, mb): 2020-11-02 12:03:09 (0.047)

    ## file min/max dates: 2009-06-01 / 2012-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1GADK0051.dly

    ## date created (size, mb): 2020-11-02 12:03:55 (0.055)

    ## file min/max dates: 2017-10-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1GADK0035.dly

    ## date created (size, mb): 2020-11-02 12:03:48 (0.076)

    ## file min/max dates: 2014-03-01 / 2018-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1GATE0004.dly

    ## date created (size, mb): 2020-11-02 12:12:13 (0.028)

    ## file min/max dates: 2016-10-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1GATF0002.dly

    ## date created (size, mb): 2020-11-02 12:12:13 (0.017)

    ## file min/max dates: 2008-07-01 / 2009-12-31

    ## file min/max dates: 1941-01-01 / 1963-04-30

    ## file min/max dates: 1999-07-01 / 2020-11-30

    ## file min/max dates: 1905-01-01 / 1908-02-29

    ## file min/max dates: 1981-10-01 / 1993-09-30

    ## file min/max dates: 1923-05-01 / 1940-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1HIHI0003.dly

    ## date created (size, mb): 2020-11-02 12:13:37 (0.138)

    ## file min/max dates: 2009-07-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/USC00510507.dly

    ## date created (size, mb): 2020-11-07 08:27:23 (2.862)

    ## file min/max dates: 1905-01-01 / 2006-06-30

    ## file min/max dates: 1923-01-01 / 1931-07-31

    ## file min/max dates: 2000-05-01 / 2019-09-30

    ## file min/max dates: 1965-07-01 / 1971-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IADC0001.dly

    ## date created (size, mb): 2020-11-02 12:16:55 (0.015)

    ## file min/max dates: 2007-08-01 / 2010-05-31

    ## file min/max dates: 1893-01-01 / 1959-10-31

    ## file min/max dates: 1950-10-01 / 1951-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IACD0005.dly

    ## date created (size, mb): 2020-11-02 12:15:54 (0.01)

    ## file min/max dates: 1998-06-01 / 2018-11-30

    ## file min/max dates: 1948-04-01 / 1948-08-31

    ## file min/max dates: 1938-08-01 / 1962-09-30

    ## file min/max dates: 2011-06-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IACR0007.dly

    ## date created (size, mb): 2020-11-02 12:16:32 (0.053)

    ## file min/max dates: 2017-04-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IAST0029.dly

    ## date created (size, mb): 2020-11-02 12:22:02 (0.023)

    ## file min/max dates: 2014-07-01 / 2017-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IADL0001.dly

    ## date created (size, mb): 2020-11-02 12:17:00 (0.105)

    ## file min/max dates: 2007-08-01 / 2016-09-30

    ## file min/max dates: 1978-09-01 / 2020-11-30

    ## file min/max dates: 1992-03-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IDCR0001.dly

    ## date created (size, mb): 2020-11-02 12:25:10 (0.223)

    ## file min/max dates: 2009-03-01 / 2020-11-30

    ## file min/max dates: 1955-11-01 / 2020-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IDID0003.dly

    ## date created (size, mb): 2020-11-02 12:25:57 (0.049)

    ## file min/max dates: 2009-02-01 / 2011-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IDLT0002.dly

    ## date created (size, mb): 2020-11-02 12:26:35 (0.031)

    ## file min/max dates: 2009-02-01 / 2010-12-31

    ## file min/max dates: 1986-11-01 / 1997-05-31

    ## file min/max dates: 1991-07-01 / 1998-04-30

    ## file min/max dates: 1986-11-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1IDEL0001.dly

    ## date created (size, mb): 2020-11-02 12:25:40 (0.224)

    ## file min/max dates: 2009-01-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILMCL032.dly

    ## date created (size, mb): 2020-11-02 12:43:36 (0.138)

    ## file min/max dates: 2013-12-01 / 2019-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILCR0009.dly

    ## date created (size, mb): 2020-11-02 12:32:25 (0.01)

    ## file min/max dates: 2008-06-01 / 2009-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILBU0010.dly

    ## date created (size, mb): 2020-11-02 12:27:39 (0.015)

    ## file min/max dates: 2015-07-01 / 2018-06-30

    ## file min/max dates: 1893-01-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILDP0048.dly

    ## date created (size, mb): 2020-11-02 12:33:40 (0.018)

    ## file min/max dates: 2009-01-01 / 2009-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILGY0009.dly

    ## date created (size, mb): 2020-11-02 12:35:52 (0.133)

    ## file min/max dates: 2013-01-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILLS0049.dly

    ## date created (size, mb): 2020-11-02 12:41:50 (0.078)

    ## file min/max dates: 2012-07-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILMCL021.dly

    ## date created (size, mb): 2020-11-02 12:43:25 (0.01)

    ## file min/max dates: 2010-11-01 / 2011-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ILWD0005.dly

    ## date created (size, mb): 2020-11-02 12:47:54 (0.187)

    ## file min/max dates: 2007-04-01 / 2020-11-30

    ## file min/max dates: 1912-09-01 / 2020-11-30

    ## file min/max dates: 1948-07-01 / 1951-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INAL0078.dly

    ## date created (size, mb): 2020-11-02 12:51:05 (0.029)

    ## file min/max dates: 2018-06-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INDL0006.dly

    ## date created (size, mb): 2020-11-02 12:53:34 (0.048)

    ## file min/max dates: 2007-02-01 / 2013-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INJS0054.dly

    ## date created (size, mb): 2020-11-02 12:59:43 (0.105)

    ## file min/max dates: 2010-07-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INPT0128.dly

    ## date created (size, mb): 2020-11-02 13:08:10 (0.156)

    ## file min/max dates: 2012-05-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INPT0064.dly

    ## date created (size, mb): 2020-11-02 13:07:30 (0.141)

    ## file min/max dates: 2007-10-01 / 2015-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INMR0025.dly

    ## date created (size, mb): 2020-11-02 13:04:07 (0.015)

    ## file min/max dates: 2006-12-01 / 2007-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INDL0023.dly

    ## date created (size, mb): 2020-11-02 12:53:40 (0.048)

    ## file min/max dates: 2011-12-01 / 2015-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INHM0014.dly

    ## date created (size, mb): 2020-11-02 12:56:25 (0.021)

    ## file min/max dates: 2006-12-01 / 2007-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1INBL0002.dly

    ## date created (size, mb): 2020-11-02 12:51:07 (0.02)

    ## file min/max dates: 2006-11-01 / 2007-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KSRS0031.dly

    ## date created (size, mb): 2020-11-02 13:30:08 (0.093)

    ## file min/max dates: 2009-09-01 / 2015-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KSBT0022.dly

    ## date created (size, mb): 2020-11-02 13:13:33 (0.01)

    ## file min/max dates: 2013-08-01 / 2014-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KSEL0060.dly

    ## date created (size, mb): 2020-11-02 13:18:04 (0.045)

    ## file min/max dates: 2011-05-01 / 2020-09-30

    ## file min/max dates: 1925-01-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KSSA0018.dly

    ## date created (size, mb): 2020-11-02 13:30:27 (0.046)

    ## file min/max dates: 2013-09-01 / 2020-09-30

    ## file min/max dates: 1946-08-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KSPR0004.dly

    ## date created (size, mb): 2020-11-02 13:26:59 (0.182)

    ## file min/max dates: 1998-06-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KSHG0006.dly

    ## date created (size, mb): 2020-11-02 13:20:58 (0.068)

    ## file min/max dates: 2007-04-01 / 2010-11-30

    ## file min/max dates: 1900-12-01 / 1982-07-31

    ## file min/max dates: 1923-11-01 / 1933-09-30

    ## file min/max dates: 1941-05-01 / 1949-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KYCB0004.dly

    ## date created (size, mb): 2020-11-02 13:36:22 (0.134)

    ## file min/max dates: 2014-02-01 / 2020-11-30

    ## file min/max dates: 1893-11-01 / 2017-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1KYHR0003.dly

    ## date created (size, mb): 2020-11-02 13:37:52 (0.018)

    ## file min/max dates: 2010-07-01 / 2015-03-31

    ## file min/max dates: 2011-03-01 / 2013-07-31

    ## file min/max dates: 1893-06-01 / 1942-05-31

    ## file min/max dates: 1948-01-01 / 2020-11-30

    ## file min/max dates: 1989-03-01 / 2003-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/USC00155415.dly

    ## date created (size, mb): 2020-11-07 09:15:58 (0.061)

    ## file min/max dates: 1962-03-01 / 1963-10-31

    ## file min/max dates: 1951-10-01 / 1971-03-31

    ## file min/max dates: 2009-05-01 / 2018-01-31

    ## file min/max dates: 1944-02-01 / 1946-11-30

    ## file min/max dates: 1954-07-01 / 1961-06-30

    ## file min/max dates: 1996-07-01 / 2020-11-30

    ## file min/max dates: 1940-05-01 / 2015-01-31

    ## file min/max dates: 1911-06-01 / 1920-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/USW00012958.dly

    ## date created (size, mb): 2020-11-07 09:16:47 (3.932)

    ## file min/max dates: 1956-06-01 / 2012-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1LAVM0004.dly

    ## date created (size, mb): 2020-11-02 13:44:50 (0.107)

    ## file min/max dates: 2012-10-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1LASB0002.dly

    ## date created (size, mb): 2020-11-02 13:44:11 (0.093)

    ## file min/max dates: 2014-11-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1LAST0015.dly

    ## date created (size, mb): 2020-11-02 13:44:28 (0.032)

    ## file min/max dates: 2015-11-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MAWR0001.dly

    ## date created (size, mb): 2020-11-02 13:49:46 (0.182)

    ## file min/max dates: 2009-02-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MAMD0125.dly

    ## date created (size, mb): 2020-11-02 13:48:39 (0.061)

    ## file min/max dates: 2018-09-01 / 2020-11-30

    ## file min/max dates: 1893-01-01 / 1978-12-31

    ## file min/max dates: 1888-06-01 / 1892-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MABA0013.dly

    ## date created (size, mb): 2020-11-02 13:45:19 (0.166)

    ## file min/max dates: 2011-02-01 / 2020-11-30

    ## file min/max dates: 1930-10-01 / 1960-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MAES0049.dly

    ## date created (size, mb): 2020-11-02 13:47:01 (0.013)

    ## file min/max dates: 2018-06-01 / 2019-10-31

    ## file min/max dates: 1942-01-01 / 1948-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MAHD0025.dly

    ## date created (size, mb): 2020-11-02 13:47:24 (0.055)

    ## file min/max dates: 2017-10-01 / 2020-10-31

    ## file min/max dates: 1885-01-01 / 1887-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MDPG0008.dly

    ## date created (size, mb): 2020-11-02 13:56:56 (0.155)

    ## file min/max dates: 1998-06-01 / 2014-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MDQA0012.dly

    ## date created (size, mb): 2020-11-02 13:57:50 (0.02)

    ## file min/max dates: 2017-02-01 / 2018-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MDDR0010.dly

    ## date created (size, mb): 2020-11-02 13:53:30 (0.06)

    ## file min/max dates: 2015-07-01 / 2020-10-31

    ## file min/max dates: 1896-02-01 / 1898-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MDMG0003.dly

    ## date created (size, mb): 2020-11-02 13:55:22 (0.215)

    ## file min/max dates: 2005-10-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MDWR0026.dly

    ## date created (size, mb): 2020-11-02 13:59:17 (0.013)

    ## file min/max dates: 2018-12-01 / 2019-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MDAA0064.dly

    ## date created (size, mb): 2020-11-02 13:51:18 (0.043)

    ## file min/max dates: 2014-08-01 / 2019-12-31

    ## file min/max dates: 1958-05-01 / 1960-12-31

    ## file min/max dates: 1916-03-01 / 2020-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MDCV0011.dly

    ## date created (size, mb): 2020-11-02 13:53:15 (0.072)

    ## file min/max dates: 2006-12-01 / 2010-02-28

    ## file min/max dates: 2004-12-01 / 2013-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MESG0009.dly

    ## date created (size, mb): 2020-11-02 14:03:13 (0.068)

    ## file min/max dates: 2010-05-01 / 2018-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MEAR0015.dly

    ## date created (size, mb): 2020-11-02 13:59:39 (0.164)

    ## file min/max dates: 2013-03-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MEKB0020.dly

    ## date created (size, mb): 2020-11-02 14:01:50 (0.035)

    ## file min/max dates: 2010-12-01 / 2015-10-31

    ## file min/max dates: 1943-09-01 / 1944-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MEPN0007.dly

    ## date created (size, mb): 2020-11-02 14:02:52 (0.084)

    ## file min/max dates: 2009-09-01 / 2015-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MEYK0018.dly

    ## date created (size, mb): 2020-11-02 14:04:15 (0.161)

    ## file min/max dates: 2009-12-01 / 2020-10-31

    ## file min/max dates: 1894-01-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MESG0016.dly

    ## date created (size, mb): 2020-11-02 14:03:15 (0.079)

    ## file min/max dates: 2016-03-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MEOX0019.dly

    ## date created (size, mb): 2020-11-02 14:02:44 (0.069)

    ## file min/max dates: 2014-03-01 / 2018-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MIWS0049.dly

    ## date created (size, mb): 2020-11-02 14:16:15 (0.04)

    ## file min/max dates: 2018-04-01 / 2020-10-31

    ## file min/max dates: 1892-12-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MIWY0013.dly

    ## date created (size, mb): 2020-11-02 14:16:22 (0.11)

    ## file min/max dates: 2008-08-01 / 2013-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MIBR0012.dly

    ## date created (size, mb): 2020-11-02 14:05:46 (0.05)

    ## file min/max dates: 2009-09-01 / 2020-11-30

    ## file min/max dates: 2004-01-01 / 2018-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MIRS0003.dly

    ## date created (size, mb): 2020-11-02 14:15:07 (0.118)

    ## file min/max dates: 2009-03-01 / 2020-09-30

    ## file min/max dates: 1893-01-01 / 1916-04-30

    ## file min/max dates: 1987-08-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MIIH0003.dly

    ## date created (size, mb): 2020-11-02 14:08:16 (0.038)

    ## file min/max dates: 2008-10-01 / 2013-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MIHL0001.dly

    ## date created (size, mb): 2020-11-02 14:07:51 (0.209)

    ## file min/max dates: 2008-06-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MNWD0001.dly

    ## date created (size, mb): 2020-11-02 14:30:13 (0.015)

    ## file min/max dates: 2011-03-01 / 2012-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MNCV0022.dly

    ## date created (size, mb): 2020-11-02 14:19:12 (0.158)

    ## file min/max dates: 2014-06-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MNCG0028.dly

    ## date created (size, mb): 2020-11-02 14:18:27 (0.069)

    ## file min/max dates: 2016-04-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MNHN0241.dly

    ## date created (size, mb): 2020-11-02 14:23:40 (0.024)

    ## file min/max dates: 2019-06-01 / 2020-10-31

    ## file min/max dates: 1896-02-01 / 2020-10-31

    ## file min/max dates: 2004-02-01 / 2011-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MNKD0016.dly

    ## date created (size, mb): 2020-11-02 14:24:28 (0.008)

    ## file min/max dates: 2019-03-01 / 2020-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MNAA0028.dly

    ## date created (size, mb): 2020-11-02 14:17:15 (0.032)

    ## file min/max dates: 2011-12-01 / 2013-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MNGH0027.dly

    ## date created (size, mb): 2020-11-02 14:21:28 (0.012)

    ## file min/max dates: 2018-03-01 / 2019-04-30

    ## file min/max dates: 1926-02-01 / 1977-10-31

    ## file min/max dates: 2008-08-01 / 2016-11-30

    ## file min/max dates: 2008-08-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MODK0001.dly

    ## date created (size, mb): 2020-11-02 14:36:34 (0.248)

    ## file min/max dates: 2006-05-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MOFSA017.dly

    ## date created (size, mb): 2020-11-02 14:37:48 (0.193)

    ## file min/max dates: 2006-05-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MOLW0031.dly

    ## date created (size, mb): 2020-11-02 14:44:06 (0.009)

    ## file min/max dates: 2013-08-01 / 2014-03-31

    ## file min/max dates: 1893-01-01 / 1915-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MOGR0027.dly

    ## date created (size, mb): 2020-11-02 14:41:16 (0.21)

    ## file min/max dates: 2007-07-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MOLW0005.dly

    ## date created (size, mb): 2020-11-02 14:43:57 (0.056)

    ## file min/max dates: 2006-07-01 / 2017-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MOBN0002.dly

    ## date created (size, mb): 2020-11-02 14:32:09 (0.221)

    ## file min/max dates: 2006-01-01 / 2019-03-31

    ## file min/max dates: 2006-06-01 / 2020-11-30

    ## file min/max dates: 1946-09-01 / 2015-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MSHD0004.dly

    ## date created (size, mb): 2020-11-02 14:51:19 (0.086)

    ## file min/max dates: 2008-08-01 / 2013-03-31

    ## file min/max dates: 1958-11-01 / 1970-12-31

    ## file min/max dates: 1893-12-01 / 2020-11-30

    ## file min/max dates: 1893-01-01 / 1899-05-31

    ## file min/max dates: 1935-01-01 / 1937-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MSPR0007.dly

    ## date created (size, mb): 2020-11-02 14:54:00 (0.043)

    ## file min/max dates: 2010-05-01 / 2016-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MSRN0036.dly

    ## date created (size, mb): 2020-11-02 14:54:27 (0.019)

    ## file min/max dates: 2011-09-01 / 2013-07-31

    ## file min/max dates: 1894-12-01 / 2016-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MSRN0037.dly

    ## date created (size, mb): 2020-11-02 14:54:28 (0.025)

    ## file min/max dates: 2012-12-01 / 2019-10-31

    ## file min/max dates: 2001-02-01 / 2020-11-30

    ## file min/max dates: 1952-06-01 / 1952-12-31

    ## file min/max dates: 1905-03-01 / 2020-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MTCB0001.dly

    ## date created (size, mb): 2020-11-02 14:55:40 (0.101)

    ## file min/max dates: 2007-05-01 / 2011-10-31

    ## file min/max dates: 1987-11-01 / 2020-02-29

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1MTFL0002.dly

    ## date created (size, mb): 2020-11-02 14:57:00 (0.056)

    ## file min/max dates: 2007-05-01 / 2014-06-30

    ## file min/max dates: 1987-06-01 / 2020-11-30

    ## file min/max dates: 1903-05-01 / 1906-08-31

    ## file min/max dates: 1910-04-01 / 2020-11-30

    ## file min/max dates: 1963-10-01 / 2020-11-30

    ## file min/max dates: 1956-02-01 / 1966-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NCBK0006.dly

    ## date created (size, mb): 2020-11-02 15:04:24 (0.105)

    ## file min/max dates: 2013-05-01 / 2020-02-29

    ## file min/max dates: 1940-10-01 / 1951-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NCAS0015.dly

    ## date created (size, mb): 2020-11-02 15:02:02 (0.014)

    ## file min/max dates: 2013-06-01 / 2014-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NCPM0003.dly

    ## date created (size, mb): 2020-11-02 15:20:32 (0.053)

    ## file min/max dates: 2009-03-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NCTR0020.dly

    ## date created (size, mb): 2020-11-02 15:23:33 (0.01)

    ## file min/max dates: 2012-10-01 / 2013-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NCCN0063.dly

    ## date created (size, mb): 2020-11-02 15:07:59 (0.088)

    ## file min/max dates: 2014-04-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NCBR0001.dly

    ## date created (size, mb): 2020-11-02 15:04:31 (0.251)

    ## file min/max dates: 2007-09-01 / 2020-10-31

    ## file min/max dates: 1893-02-01 / 1937-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NCCL0002.dly

    ## date created (size, mb): 2020-11-02 15:06:27 (0.096)

    ## file min/max dates: 2007-10-01 / 2014-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NDBH0007.dly

    ## date created (size, mb): 2020-11-02 15:28:17 (0.039)

    ## file min/max dates: 2008-11-01 / 2012-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NDLM0008.dly

    ## date created (size, mb): 2020-11-02 15:30:11 (0.011)

    ## file min/max dates: 2016-03-01 / 2020-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NDWM0007.dly

    ## date created (size, mb): 2020-11-02 15:31:13 (0.029)

    ## file min/max dates: 2013-06-01 / 2014-07-31

    ## file min/max dates: 1948-08-01 / 1951-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NDSK0004.dly

    ## date created (size, mb): 2020-11-02 15:30:53 (0.032)

    ## file min/max dates: 2009-05-01 / 2010-07-31

    ## file min/max dates: 1916-05-01 / 2007-04-30

    ## file min/max dates: 1950-08-01 / 1958-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NDCS0024.dly

    ## date created (size, mb): 2020-11-02 15:29:07 (0.047)

    ## file min/max dates: 2010-05-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NDCS0020.dly

    ## date created (size, mb): 2020-11-02 15:29:04 (0.12)

    ## file min/max dates: 2010-03-01 / 2017-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NDWL0003.dly

    ## date created (size, mb): 2020-11-02 15:31:12 (0.061)

    ## file min/max dates: 2012-04-01 / 2020-08-31

    ## file min/max dates: 1889-06-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US10chas005.dly

    ## date created (size, mb): 2020-11-02 09:19:09 (0.06)

    ## file min/max dates: 2004-06-01 / 2010-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US10furn001.dly

    ## date created (size, mb): 2020-11-02 09:24:27 (0.047)

    ## file min/max dates: 2004-06-01 / 2007-03-31

    ## file min/max dates: 1893-01-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US10otoe009.dly

    ## date created (size, mb): 2020-11-02 09:32:25 (0.132)

    ## file min/max dates: 2006-08-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US10dund017.dly

    ## date created (size, mb): 2020-11-02 09:23:33 (0.123)

    ## file min/max dates: 2005-02-01 / 2020-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US10sher021.dly

    ## date created (size, mb): 2020-11-02 09:36:27 (0.112)

    ## file min/max dates: 2009-06-01 / 2020-10-31

    ## file min/max dates: 1998-02-01 / 2013-10-31

    ## file min/max dates: 1948-10-01 / 2000-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US10fron002.dly

    ## date created (size, mb): 2020-11-02 09:24:08 (0.168)

    ## file min/max dates: 2004-07-01 / 2017-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NHBK0001.dly

    ## date created (size, mb): 2020-11-02 15:33:46 (0.286)

    ## file min/max dates: 2009-06-01 / 2020-11-30

    ## file min/max dates: 1926-05-01 / 1981-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NHCR0007.dly

    ## date created (size, mb): 2020-11-02 15:34:28 (0.026)

    ## file min/max dates: 2009-07-01 / 2011-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NHRC0004.dly

    ## date created (size, mb): 2020-11-02 15:36:38 (0.008)

    ## file min/max dates: 2009-07-01 / 2009-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NHHL0078.dly

    ## date created (size, mb): 2020-11-02 15:35:51 (0.022)

    ## file min/max dates: 2016-03-01 / 2018-03-31

    ## file min/max dates: 1947-01-01 / 1957-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NHHL0087.dly

    ## date created (size, mb): 2020-11-02 15:35:55 (0.053)

    ## file min/max dates: 2017-07-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NHRC0005.dly

    ## date created (size, mb): 2020-11-02 15:36:38 (0.012)

    ## file min/max dates: 2009-07-01 / 2010-05-31

    ## file min/max dates: 2012-11-01 / 2016-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NHCR0016.dly

    ## date created (size, mb): 2020-11-02 15:34:41 (0.153)

    ## file min/max dates: 2009-11-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJBG0029.dly

    ## date created (size, mb): 2020-11-02 15:38:17 (0.129)

    ## file min/max dates: 2010-09-01 / 2017-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJSM0064.dly

    ## date created (size, mb): 2020-11-02 15:47:17 (0.077)

    ## file min/max dates: 2016-01-01 / 2020-11-30

    ## file min/max dates: 1893-01-01 / 1949-12-31

    ## file min/max dates: 1973-09-01 / 2000-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJSM0034.dly

    ## date created (size, mb): 2020-11-02 15:46:59 (0.094)

    ## file min/max dates: 2011-05-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJMN0070.dly

    ## date created (size, mb): 2020-11-02 15:43:38 (0.116)

    ## file min/max dates: 2016-02-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJHN0031.dly

    ## date created (size, mb): 2020-11-02 15:41:15 (0.141)

    ## file min/max dates: 2012-07-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJWR0030.dly

    ## date created (size, mb): 2020-11-02 15:48:23 (0.006)

    ## file min/max dates: 2015-08-01 / 2015-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJHN0047.dly

    ## date created (size, mb): 2020-11-02 15:41:23 (0.034)

    ## file min/max dates: 2016-11-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NJBT0011.dly

    ## date created (size, mb): 2020-11-02 15:38:34 (0.029)

    ## file min/max dates: 2009-06-01 / 2016-01-31

    ## file min/max dates: 1910-09-01 / 1961-03-31

    ## file min/max dates: 1931-03-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NMRA0018.dly

    ## date created (size, mb): 2020-11-02 16:02:32 (0.078)

    ## file min/max dates: 2005-08-01 / 2015-11-30

    ## file min/max dates: 1910-11-01 / 2020-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NMDA0165.dly

    ## date created (size, mb): 2020-11-02 15:54:58 (0.03)

    ## file min/max dates: 2007-11-01 / 2010-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NMSJ0024.dly

    ## date created (size, mb): 2020-11-02 16:05:30 (0.014)

    ## file min/max dates: 2010-07-01 / 2011-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NMBR0007.dly

    ## date created (size, mb): 2020-11-02 15:48:37 (0.231)

    ## file min/max dates: 2005-03-01 / 2020-11-30

    ## file min/max dates: 1938-09-01 / 2020-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NMGR0057.dly

    ## date created (size, mb): 2020-11-02 15:58:34 (0.112)

    ## file min/max dates: 2014-08-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NMDA0011.dly

    ## date created (size, mb): 2020-11-02 15:53:19 (0.186)

    ## file min/max dates: 2005-03-01 / 2020-10-31

    ## file min/max dates: 1913-12-01 / 1952-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NVEL0015.dly

    ## date created (size, mb): 2020-11-02 16:10:50 (0.019)

    ## file min/max dates: 2012-05-01 / 2012-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NVEL0001.dly

    ## date created (size, mb): 2020-11-02 16:10:42 (0.018)

    ## file min/max dates: 2009-02-01 / 2009-07-31

    ## file min/max dates: 1890-02-01 / 1911-03-31

    ## file min/max dates: 1980-07-01 / 2020-11-30

    ## file min/max dates: 1949-04-01 / 1962-11-30

    ## file min/max dates: 1905-05-01 / 1907-08-31

    ## file min/max dates: 1897-08-01 / 1906-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NVWH0114.dly

    ## date created (size, mb): 2020-11-02 16:12:59 (0.082)

    ## file min/max dates: 2013-01-01 / 2017-10-31

    ## file min/max dates: 1987-03-01 / 2020-11-30

    ## file min/max dates: 1952-11-01 / 1953-12-31

    ## file min/max dates: 1922-04-01 / 1948-04-30

    ## file min/max dates: 1943-07-01 / 1961-02-28

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NYSL0013.dly

    ## date created (size, mb): 2020-11-02 16:24:37 (0.036)

    ## file min/max dates: 2013-11-01 / 2017-12-31

    ## file min/max dates: 1927-08-01 / 1978-02-28

    ## file min/max dates: 2011-04-01 / 2020-11-30

    ## file min/max dates: 1893-01-01 / 1956-01-31

    ## file min/max dates: 1888-01-01 / 1959-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1NYNS0022.dly

    ## date created (size, mb): 2020-11-02 16:20:39 (0.017)

    ## file min/max dates: 2016-08-01 / 2017-07-31

    ## file min/max dates: 1934-02-01 / 2020-08-31

    ## file min/max dates: 1905-02-01 / 2020-09-30

    ## file min/max dates: 1939-07-01 / 1955-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1OHMD0006.dly

    ## date created (size, mb): 2020-11-02 16:34:05 (0.013)

    ## file min/max dates: 2014-03-01 / 2014-11-30

    ## file min/max dates: 1953-07-01 / 1987-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1OHWD0008.dly

    ## date created (size, mb): 2020-11-02 16:36:36 (0.047)

    ## file min/max dates: 2009-04-01 / 2011-01-31

    ## file min/max dates: 1894-08-01 / 1915-04-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1OHLC0001.dly

    ## date created (size, mb): 2020-11-02 16:33:13 (0.201)

    ## file min/max dates: 2009-02-01 / 2020-11-30

    ## file min/max dates: 1939-01-01 / 2020-08-31

    ## file min/max dates: 1900-01-01 / 1982-06-30

    ## file min/max dates: 1943-02-01 / 1944-07-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1OKJC0010.dly

    ## date created (size, mb): 2020-11-02 16:40:40 (0.03)

    ## file min/max dates: 2017-07-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1OKCV0114.dly

    ## date created (size, mb): 2020-11-02 16:39:43 (0.082)

    ## file min/max dates: 2014-09-01 / 2020-10-31

    ## file min/max dates: 1893-01-01 / 1951-12-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1OKCN0015.dly

    ## date created (size, mb): 2020-11-02 16:38:16 (0.018)

    ## file min/max dates: 2013-04-01 / 2017-04-30

    ## file min/max dates: 1937-04-01 / 2018-03-31

    ## file min/max dates: 1988-11-01 / 2005-03-31

    ## file min/max dates: 1948-01-01 / 2015-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1OKCN0019.dly

    ## date created (size, mb): 2020-11-02 16:38:19 (0.103)

    ## file min/max dates: 2013-05-01 / 2017-12-31

    ## file min/max dates: 1894-01-01 / 2016-12-31

    ## file min/max dates: 1900-11-01 / 2006-04-30

    ## file min/max dates: 1913-02-01 / 1927-06-30

    ## file min/max dates: 1902-05-01 / 1949-05-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ORMT0077.dly

    ## date created (size, mb): 2020-11-02 16:58:48 (0.029)

    ## file min/max dates: 2015-03-01 / 2017-03-31

    ## file min/max dates: 1987-01-01 / 2002-12-31

    ## file min/max dates: 2006-09-01 / 2020-11-30

    ## file min/max dates: 1980-06-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ORPK0026.dly

    ## date created (size, mb): 2020-11-02 16:59:25 (0.083)

    ## file min/max dates: 2012-11-01 / 2016-04-30

    ## file min/max dates: 2003-02-01 / 2010-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1ORDG0013.dly

    ## date created (size, mb): 2020-11-02 16:49:13 (0.023)

    ## file min/max dates: 2008-01-01 / 2009-01-31

    ## file min/max dates: 1996-04-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1PACW0001.dly

    ## date created (size, mb): 2020-11-02 17:09:01 (0.018)

    ## file min/max dates: 2009-05-01 / 2010-04-30

    ## file min/max dates: 1893-01-01 / 2020-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1PALH0019.dly

    ## date created (size, mb): 2020-11-02 17:10:34 (0.039)

    ## file min/max dates: 2016-06-01 / 2020-11-30

    ## file min/max dates: 2015-09-01 / 2017-12-31

    ## file min/max dates: 2016-11-01 / 2018-01-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1PALC0008.dly

    ## date created (size, mb): 2020-11-02 17:10:19 (0.147)

    ## file min/max dates: 2006-12-01 / 2020-08-31

    ## file min/max dates: 1963-12-01 / 1996-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1PACB0024.dly

    ## date created (size, mb): 2020-11-02 17:07:29 (0.112)

    ## file min/max dates: 2007-08-01 / 2013-06-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1PALZ0014.dly

    ## date created (size, mb): 2020-11-02 17:10:57 (0.042)

    ## file min/max dates: 2010-06-01 / 2013-03-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1PAMT0042.dly

    ## date created (size, mb): 2020-11-02 17:12:08 (0.092)

    ## file min/max dates: 2008-04-01 / 2012-09-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1RINW0019.dly

    ## date created (size, mb): 2020-11-07 08:41:54 (0.042)

    ## file min/max dates: 2018-03-01 / 2020-11-30

    ## file min/max dates: 1948-07-01 / 2020-11-30

    ## file min/max dates: 2011-06-01 / 2020-11-30

    ## file min/max dates: 2008-05-01 / 2010-02-28

    ## file min/max dates: 2018-04-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/USW00054797.dly

    ## date created (size, mb): 2020-11-07 09:34:13 (0.339)

    ## file min/max dates: 2001-12-01 / 2020-11-30

    ## file min/max dates: 1948-06-01 / 1956-11-30

    ## file min/max dates: 1893-01-01 / 1913-11-30

    ## file min/max dates: 1991-07-01 / 1994-03-31

    ## file min/max dates: 2016-10-01 / 2018-08-31

    ## file min/max dates: 2010-04-01 / 2019-09-30

    ## file min/max dates: 2018-03-01 / 2020-10-31

    ## file min/max dates: 2019-01-01 / 2020-11-30

    ## file min/max dates: 2007-01-01 / 2020-09-30

    ## file min/max dates: 2008-04-01 / 2019-01-31

    ## file min/max dates: 2017-03-01 / 2020-04-30

    ## file min/max dates: 2008-05-01 / 2015-06-30

    ## file min/max dates: 2014-06-01 / 2016-02-29

    ## file min/max dates: 1952-01-01 / 2004-09-30

    ## file min/max dates: 2013-09-01 / 2017-12-31

    ## file min/max dates: 2007-08-01 / 2015-09-30

    ## file min/max dates: 2007-05-01 / 2020-09-30

    ## file min/max dates: 1998-06-01 / 2020-10-31

    ## file min/max dates: 1913-01-01 / 2020-08-31

    ## file min/max dates: 1913-05-01 / 1919-02-28

    ## file min/max dates: 2007-08-01 / 2009-12-31

    ## file min/max dates: 1893-01-01 / 2012-04-30

    ## file min/max dates: 2007-06-01 / 2020-10-31

    ## file min/max dates: 2012-09-01 / 2020-10-31

    ## file min/max dates: 1974-09-01 / 1977-05-31

    ## file min/max dates: 2005-08-01 / 2016-11-30

    ## file min/max dates: 2013-02-01 / 2017-11-30

    ## file min/max dates: 1896-05-01 / 1901-09-30

    ## file min/max dates: 2010-02-01 / 2012-04-30

    ## file min/max dates: 2007-04-01 / 2020-10-31

    ## file min/max dates: 2016-12-01 / 2017-11-30

    ## file min/max dates: 2007-07-01 / 2020-10-31

    ## file min/max dates: 2008-01-01 / 2008-12-31

    ## file min/max dates: 1954-04-01 / 2020-11-30

    ## file min/max dates: 1948-09-01 / 1951-07-31

    ## file min/max dates: 2011-11-01 / 2020-01-31

    ## file min/max dates: 1950-12-01 / 1956-09-30

    ## file min/max dates: 2010-02-01 / 2010-06-30

    ## file min/max dates: 1979-07-01 / 2018-03-31

    ## file min/max dates: 2007-09-01 / 2020-10-31

    ## file min/max dates: 1941-01-01 / 1958-01-31

    ## file min/max dates: 2007-03-01 / 2020-10-31

    ## file min/max dates: 2016-06-01 / 2020-10-31

    ## file min/max dates: 2000-09-01 / 2020-10-31

    ## file min/max dates: 1914-05-01 / 1972-09-30

    ## file min/max dates: 2008-06-01 / 2020-10-31

    ## file min/max dates: 1920-07-01 / 1928-08-31

    ## file min/max dates: 1941-01-01 / 1942-04-30

    ## file min/max dates: 1916-11-01 / 1992-07-31

    ## file min/max dates: 2008-07-01 / 2008-12-31

    ## file min/max dates: 1913-12-01 / 1953-08-31

    ## file min/max dates: 1987-10-01 / 1993-04-30

    ## file min/max dates: 2009-07-01 / 2014-05-31

    ## file min/max dates: 1930-03-01 / 1984-07-31

    ## file min/max dates: 1949-08-01 / 1951-02-28

    ## file min/max dates: 1941-05-01 / 1974-08-31

    ## file min/max dates: 2003-12-01 / 2007-08-31

    ## file min/max dates: 1981-04-01 / 1988-10-31

    ## file min/max dates: 1945-08-01 / 1949-12-31

    ## file min/max dates: 1943-07-01 / 1982-10-31

    ## file min/max dates: 1979-08-01 / 2020-11-30

    ## file min/max dates: 2010-10-01 / 2020-11-30

    ## file min/max dates: 1949-12-01 / 1970-10-31

    ## file min/max dates: 1930-11-01 / 1940-09-30

    ## file min/max dates: 2006-01-01 / 2013-07-31

    ## file min/max dates: 1935-07-01 / 1947-03-31

    ## file min/max dates: 2008-09-01 / 2014-10-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1VTFR0019.dly

    ## date created (size, mb): 2020-11-07 09:40:30 (0.077)

    ## file min/max dates: 2017-02-01 / 2020-11-30

    ## file min/max dates: 2009-08-01 / 2017-04-30

    ## file min/max dates: 2018-05-01 / 2020-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1VTCH0009.dly

    ## date created (size, mb): 2020-11-07 08:46:00 (0.037)

    ## file min/max dates: 2009-05-01 / 2012-12-31

    ## file min/max dates: 2014-11-01 / 2020-11-30

    ## file min/max dates: 1998-06-01 / 2019-11-30

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/US1VTWH0006.dly

    ## date created (size, mb): 2020-11-07 08:45:57 (0.222)

    ## file min/max dates: 2009-04-01 / 2019-08-31

    ## file min/max dates: 1985-07-01 / 2010-08-31

    ## file min/max dates: 1972-05-01 / 1995-02-28

    ## file min/max dates: 2010-04-01 / 2013-06-30

    ## file min/max dates: 2017-02-01 / 2017-11-30

    ## file min/max dates: 1894-07-01 / 2015-11-30

    ## file min/max dates: 1936-06-01 / 1979-01-31

    ## file min/max dates: 2013-12-01 / 2016-08-31

    ## file min/max dates: 1985-01-01 / 2020-11-30

    ## file min/max dates: 2009-06-01 / 2014-02-28

    ## file min/max dates: 2006-09-01 / 2020-11-30

    ## file min/max dates: 1951-04-01 / 2008-12-31

    ## file min/max dates: 2010-04-01 / 2020-11-30

    ## file min/max dates: 2007-07-01 / 2010-06-30

    ## file min/max dates: 2014-04-01 / 2020-05-31

    ## file min/max dates: 2015-03-01 / 2020-11-30

    ## file min/max dates: 1938-08-01 / 2009-10-31

    ## file min/max dates: 1910-11-01 / 2009-12-31

    ## file min/max dates: 2012-08-01 / 2013-06-30

    ## file min/max dates: 1893-03-01 / 2005-04-30

    ## file min/max dates: 2007-04-01 / 2012-07-31

    ## file min/max dates: 1962-06-01 / 2002-12-31

    ## file min/max dates: 1994-06-01 / 2020-07-31

    ## file min/max dates: 1893-02-01 / 2016-01-31

    ## file min/max dates: 1980-11-01 / 1986-10-31

    ## file min/max dates: 2013-07-01 / 2020-11-30

    ## file min/max dates: 1938-02-01 / 1954-08-31

    ## using cached file: /Users/mayabunyan/Library/Caches/R/noaa_ghcnd/USC00464045.dly

    ## date created (size, mb): 2020-11-07 08:48:46 (0.206)

    ## file min/max dates: 1877-01-01 / 1889-01-31

    ## file min/max dates: 1902-05-01 / 2020-11-30

    ## file min/max dates: 1948-08-01 / 1951-08-31

    ## file min/max dates: 1945-09-01 / 1954-11-30

    ## file min/max dates: 1923-08-01 / 1964-09-30

    ## file min/max dates: 1920-01-01 / 2020-07-31

    ## file min/max dates: 1927-03-01 / 2020-08-31

    ## file min/max dates: 1939-01-01 / 1940-09-30

    ## file min/max dates: 2010-01-01 / 2020-08-31

    ## file min/max dates: 1999-06-01 / 2020-11-30

    ## file min/max dates: 2017-05-01 / 2020-09-30

    ## file min/max dates: 2010-10-01 / 2020-11-30

    ## file min/max dates: 2011-01-01 / 2014-12-31

    ## file min/max dates: 2007-09-01 / 2012-11-30

    ## file min/max dates: 2015-05-01 / 2020-10-31

``` r
noaadata = inner_join(ids, noaadat, by = "id")

# Save the resulting data
write.csv(noaadata, "./data/noaadata.csv")
```

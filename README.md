### What are Climate Stripes?

Climate stripes are visualisations of climate change from a temperature
time series (Climate Lab 2018). They are meant mostly as a communication
tool to a lay public and can be grasped almost instantly. They were
developed to have minimal annotation almost like a colour bar code.
Legend and time axis options have been included here if one wants to
convey a bit more information.

Installation
------------

    library(devtools)
    install_github("duplisea/climatestripes")

    library(climatestripes)

Make climate stripe plots for data downloaded from NASA’s GISS Surface Temperature Analysis
-------------------------------------------------------------------------------------------

Suface air temperature data was downloaded for St Margaret’s Bay, Nova
Scotia, Canada to use as an example.

    temperature.vector= stmargaretsbay$metANN
    # set the missing value code (999.9) to NA
    temperature.vector[temperature.vector==999.9]=NA
    time.vector= stmargaretsbay$YEAR

    climate.col.stripes.f(time.vector= time.vector,temperature.vector= temperature.vector,
      colour.vec=c("navyblue", "red"),
      title="Annual Average Temperature - St Margaret's Bay, NS, Canada",
      legend=T,
      legend.text.col="yellow")

![](README_files/figure-markdown_strict/annualplot-1.png)

This clearly shows a warming particularly since the early 1980s. There
is a cooling from the mid 1990s to early 2000s and then the temperature
increases in the second decade of the 2000s which includes the warmest
years on record. The legend shows that the warmest year was 8.6 °C while
the coldest was 4.1 °C. Years without data are shown without colour.

This is not exactly the same as climate lab’s plots who use a three
colour gradient and they do not seem to use datasets with missing values
or perhaps their missing data are colour coded with the average (white).
The climate lab climate stripes also tend to work on anomalies in which
case a three colour gradient makes a lot of sense.

<img src="README_files/figure-markdown_strict/uk-stripes-1.png" style="width:60.0%" />

From
<a href="https://www.climate-lab-book.ac.uk/2018/climate-stripes-for-the-uk/" class="uri">https://www.climate-lab-book.ac.uk/2018/climate-stripes-for-the-uk/</a>

You can make colour stripes plot closer to the look of those developed
by climate lab using a multicolour gradient. In the one below, “white”
was added as the middle colour and different points along the gradients
were marked with particular colours. Experiment with different gradients
and you may find something that works better for you. You could add as
many colours as years even.

    climate.col.stripes.f(time.vector= time.vector,temperature.vector= temperature.vector,
      colour.vec=c("navyblue","lightblue","white","red","darkred"),
      title="Annual Average Temperature - St Margaret's Bay, NS, Canada",
      legend=T,
      legend.text.col="yellow")

![](README_files/figure-markdown_strict/climatelabplot-1.png)

This missing data in the 2012 period now look like average data though
so it is deceptive. I personally prefer the two colour gradient on
absolutes and not anomalies with missing data coded white. I think it is
the most intuitive since anomalies are more difficult to explain to the
lay public and it is easy to show missing data points.

Make a climate stripe plot for just one month from the GISS dataset
-------------------------------------------------------------------

    temperature.vector= stmargaretsbay$SEP
    temperature.vector[temperature.vector==999.9]=NA
    time.vector= stmargaretsbay$YEAR
    climate.col.stripes.f(time.vector= time.vector,temperature.vector= temperature.vector,
      colour.vec=c("navyblue", "red"),
      title="September Average Temperature - St Margaret's Bay, NS, Canada",
      legend=T,
      legend.text.col="white")

![](README_files/figure-markdown_strict/septemberplot-1.png)

An annual climate stripe image with one plot for each month of the year
-----------------------------------------------------------------------

    months=c("JAN","FEB","MAR","APR","MAY","JUN","JUL","AUG","SEP","OCT","NOV","DEC")
    monthcols= match(months,names(stmargaretsbay))
    time.vector= stmargaretsbay$YEAR
    par(mfcol=c(6,2),mar=c(.2,.1,.5,.1))
    for (i in monthcols){
      temperature.vector= stmargaretsbay[,i]
      temperature.vector[temperature.vector==999.9]=NA
      climate.col.stripes.f(time.vector= time.vector,temperature.vector, colour.vec=c("navyblue","red"),title=months[i-1], time.scale=F)
    }

![](README_files/figure-markdown_strict/allmonthplot-1.png)

The axis has been omitted to bring out the general pattern and
comparison between months. The legends give an idea of the actual
temperature each month.

References
==========

Climate Lab. 2018.
<a href="https://www.climate-lab-book.ac.uk/2018/warming-stripes/" class="uri">https://www.climate-lab-book.ac.uk/2018/warming-stripes/</a>

Enfield, D.B., A.M. Mestas-Nunez, and P.J. Trimble, 2001: The Atlantic
Multidecadal Oscillation and its relationship to rainfall and river
flows in the continental U.S., Geophys. Res. Lett., 28: 2077-2080.

GISTEMP Team, 2019: GISS Surface Temperature Analysis (GISTEMP), version
4. NASA Goddard Institute for Space Studies. Dataset accessed 2019-06-20
at
<a href="https://data.giss.nasa.gov/gistemp/" class="uri">https://data.giss.nasa.gov/gistemp/</a>.

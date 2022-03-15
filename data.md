# Data (Big)

Big data is a means of processing data that is so large, or varied, or generated so quickly that to process the information requires more than one computer. 

Various tools, runners, and languages are available. 

This page is the definitive source for current big data information - imagine this is the Wikipedia page for big data, which I won't link to as it would extend our web, but credit is given and much appreciated.

## MiniWeb to Practice Big Data Techniques

This set of web pages represents a small world-wide web. 
Some pages link to other pages (the page has an 'out-going' link). In PageRank (the algorithm secret to Google's success), a page is more important if more pages (and more important pages) point to it.  

First, we crawl the web, check each page and record each outgoing link. 

There are 5 pages:

1. beam
2. data
3. golang
4. java
5. python

The only outgoing links we will find (the first time around) are:

1. golang.md -> beam.md
2. java.md -> beam.md
3. python.md -> beam.md
4. beam.md -> data.md

Read the file and keep only the link information. In Big Data, we use transformations (e.g. map) on our raw data. We read and process each line just once across many machines concurrently - never read files into arrays or any other data structure that is not set up to be handed out to many machines - we must be scalable across billions, trillions of pages and lines. 

Unlike arrays, some special big data structures such as a Spark RDD (resilient distributed dataset) are set up to be processed on many machines concurrently. 

## Simplified Web for Easier Parsing

This initial small web is created out of several somewhat easy to parse pages. 

- In this starter version, all outgoing links are the only thing on their own line and follow GitHub Markdown syntax. 
- Look for square brackets with the display text, immediately followed by parenthesis with the URL of the outgoing link. 
- Pages with no outgoing links add a special challenge. In this starter version, all pages will have at least one outgoing link to simplify the process. 

The simplified parsing helps us focus on generating the map reduce processing jobs needed to implement pagerank:

Job 1 - Crawl web, map each page, outgoing link. Reduce by page key to create a list of outgoing links from each page. Add initial PR=1 (page rank) to each page. Output of Job 1 is input to Job 2.

Job 2 - Reverse and Iterate to get PR. Map each item in the list to its incoming page and keep track of how many outgoing links (votes) that incoming page made. Calculate new PR values for each key page and interate until we get the correct page values based on importance. Output of Job 2 is input to Job 3.

JOb 3 - Rank pages based on value, highest value first. 

## Process Flow

Source data -> MAP1 -> REDUCE1 -> MAP2 -> REDUCE2 -> MAP3 -> REDUCE3 output/sink

## Job 1 Input

Read each page, each line: if link is found, then map to key-value pairs consisting of page, outlinkpage:

1. golang.md, beam.md
2. java.md, beam.md
3. python.md, beam.md
4. beam.md,data.md

Reduce by key - for each page key, list all its outgoing links together as the value. For example:

1. (golang.md, [beam.md])

## About Big Data (borrowed from Wikipedia)

Big data is a field that treats ways to analyze, systematically extract information from, or otherwise deal with data sets that are too large or complex to be dealt with by traditional data-processing application software. Data with many fields (columns) offer greater statistical power, while data with higher complexity (more attributes or columns) may lead to a higher false discovery rate. Big data analysis challenges include capturing data, data storage, data analysis, search, sharing, transfer, visualization, querying, updating, information privacy, and data source. Big data was originally associated with three key concepts: volume, variety, and velocity. The analysis of big data presents challenges in sampling, and thus previously allowing for only observations and sampling. Therefore, big data often includes data with sizes that exceed the capacity of traditional software to process within an acceptable time and value.

Current usage of the term big data tends to refer to the use of predictive analytics, user behavior analytics, or certain other advanced data analytics methods that extract value from big data, and seldom to a particular size of data set. "There is little doubt that the quantities of data now available are indeed large, but that's not the most relevant characteristic of this new data ecosystem." Analysis of data sets can find new correlations to "spot business trends, prevent diseases, combat crime and so on". Scientists, business executives, medical practitioners, advertising and governments alike regularly meet difficulties with large data-sets in areas including Internet searches, fintech, healthcare analytics, geographic information systems, urban informatics, and business informatics. Scientists encounter limitations in e-Science work, including meteorology, genomics, connectomics, complex physics simulations, biology, and environmental research.

The size and number of available data sets have grown rapidly as data is collected by devices such as mobile devices, cheap and numerous information-sensing Internet of things devices, aerial (remote sensing), software logs, cameras, microphones, radio-frequency identification (RFID) readers and wireless sensor networks.[8][9] The world's technological per-capita capacity to store information has roughly doubled every 40 months since the 1980s; as of 2012, every day 2.5 exabytes (2.5×260 bytes) of data are generated. Based on an IDC report prediction, the global data volume was predicted to grow exponentially from 4.4 zettabytes to 44 zettabytes between 2013 and 2020. By 2025, IDC predicts there will be 163 zettabytes of data. One question for large enterprises is determining who should own big-data initiatives that affect the entire organization.

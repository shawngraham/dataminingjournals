# Implementing Goldstone's DFR Topic Model Browser
### Shawn Graham"
### Sept 29 2014


Set up:
+ set java as high as you've got it.

	    options(java.parameters="-Xmx3584m")

+ The first time you try this script:

	    library(devtools)
    	install_github("dfrtopics","agoldst")
	
Comment the above out any subsequent time.

+ libraries

	    library(rJava)
	    library(mallet)
	    library(dfrtopics)

+ set working directory

	    setwd("~/Desktop/data mining and tools/datasets/20000/")

+ Run the model

	    m <- model_documents(citations_files="/wordcounts/citations.CSV",
    	     dirs="/wordcounts/",stoplist_file="archaestoplist3.txt",
        	 n_topics=100)
 
+ Get doc-topic matrix joined with metadata

	    dtw <- doc_topics_wide(m$doc_topics,m$metadata)
 
+ Convert that into a data frame of topic yearly time series

	   series <- topic_proportions_series_frame(topic_year_matrix(dtw))

+ Make a faceted plot

	    topic_yearly_lineplot(series,facet=T)

	    output_model(m, "data")


+ export
	
    	export_browser_data("data",
 	    	m$metadata,
      	    m$wkf,
      	    m$doc_topics,
      	    topic_scaled_2d(m$trainer),
      	    zipped=F
	    )


+ save meta.csv into meta.csv.zip, move into data folder
+ find dt.json, send it to dt.json.zip, move into data folder

+ Move the data folder onto your server. 
 output of this model can be viewed at http://graeworks.net/digitalarchae/20000
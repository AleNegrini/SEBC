# Treasure hunt

## What is ubertask optimization?
Uberstask optimization is a YARN feature that allows to runs "sufficiently small" jobs sequentially within a single JVM. 
By default it is disabled; by typing on the top right corner of the CM "uberstask" you get some configurations.
First thing is to enable it in the YARN configuration tab. 
Via search bar you can also get access to ubertask configuration settings, like:
* mapreduce.job.ubertask.maxmaps
* mapreduce.job.ubertask.maxreduces
* mapreduce.job.ubertask.maxbytes 
that define what "small" mean. 
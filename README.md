# Datapipeline-Project
Created a 4-step data pipeline to download podcasts. Airflow was used to make the pipeline automated.  

The project starts by converting podcast XML files into a dictionary using xmltodict. This is followed by a cleaning process that removes duplicates and empty variables from the dictionary. Next, the dictionary is passed into an SQLLite database, which works with Airflow to then download the podcasts. Airflow allows the user to control different parameters of the pipeline, such as how often podcasts should be downloaded. Airflow's dashboard also provides further statistical analysis and visualization. 

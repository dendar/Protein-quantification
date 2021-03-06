<h1><center>Harnessing Data Science to Streamline Biomedical Research</center></h1>


Science is one of the most important channels of knowledge and scientific advances the cornerstone of a modern developed world. This has never been clearer than now. The COVID-19 pandemic and the quest to develop effective vaccines and/or cures for COVID-19 has put biomedical research on the map. However, the lay man still has very little understanding of what biomedical research entails. Before I got a job in a biomedical research laboratory, I too had a very skewed idea of what biomedical research is in practical matters. Probably conditioned by what we see in movies and on TV, I thought the world of working in a laboratory and doing biomedical research meant that everything is powered by cutting edge technology. However, very soon after starting my job, I realized that even though scientists push the boundaries of our knowledge, the way they approach the day to day analysis of their data is rather “old school”.  Don’t get me wrong biomedical research is powered by cutting edge technology and high-level data analysis. This is obvious through the Human Genome Project, which was an effort to decipher the sequence of the human DNA and has transformed medicine allowing for more precise diagnostics and personalized medicine.  However, the day to day work done in a biomedical laboratory significantly relies on very basic data analysis tools that are not automated (e.g. Microsoft Excel spreadsheets). 


I’m not sure why this is. Maybe biomedical scientists are too busy thinking about the biological problems and doing experiments to create new data analysis tools and it’s just easy to do it how they have always done it.  Maybe they just don’t know how to automatize it. What I found most interesting about this is  that a programmer can easily help by building some basic automated tools for day to day data analysis in the lab, which in turn could save a significant amount of time to devote to experimentation. Part of this problem comes from the fact that lab research and coding are very different areas and data scientists don’t know what tools biomedical scientists doing basic research in the lab need and scientists don’t know that data scientists can help to build tools for them. To fully understand this problem and how data scientists can make lab scientists work more streamlined, we really have to dive deeper into the day to day of a basic scientist working in a lab. My time working in the lab allowed me the opportunity to see these two different worlds and think about the practical aspects behind scientific discoveries. 


A good example of empowering daily lab research with data science tools is basic protein quantification, which everyone in biological/biomedical laboratories all around the world use daily. The method for protein quantification is based on a chemical reaction in which proteins in a sample react with a chemical and produce a color. The intensity of the color is proportional to the amount of protein in a sample which researchers measure using a specific equipment called spectrophotometer (which is capable of measuring the differences in color intensity – different color intensities result in different absorbances which is measured by the spectrophotometer). The principle of this method lays on using a standard curve with multiple concentration points of known concentrations of a known protein, which is then used to mathematically estimate the concentration of the unknown samples.   Once I saw how long it took for my lab mates to go from the spectrophotometer data to the concentrations of the proteins, I realize how much time they would save if they had a simple tool where they could just input the absorbance values from the spectrophotometer and immediately get the concentrations of their samples. So, I decided to build a basic python module to determine protein quantification in an automated fashion from absorbance values measured spectrophotometrically. Here I described how to use this module:


1- Prepare the Excel file that contains the absorbance levels to import into the python protein quantification module as follows:



<img src="image/Picture1.png" width=90%>

Notes: 

 - This python protein quantification module assumes that each sample (or standard) is read in triplicate (each replica’s absorbance goes in a different column as shown above).
 

 - You can directly import your excel file and modify my code to make the table match the formatting required for analysis by dropping columns/rows that are not necessary (as I did), or you if you are not comfortable using python you can do it on excel before importing the data. 


2- Import the Excel file that contains the absorbance levels into the python protein quantification module. To do that just change the name of the file in the python module as follows:

<img src="image/Picture2.png" width=90%>

The data will now look like this: 

<img src="image/Picture3.png" width=90%>

And this is how the module will see the identity of each value on the table:

<img src="image/Picture4.png" width=90%>

3- Now that the data is imported into the module, the first thing the module does is to calculate the average of each triplicate so that a single absorbance value is used in the downstream analysis.  A scatter plot containing the standard curve data is then generated and a regression analysis is performed to determine the relationship between protein concentration and absorbance measurements. The degree of confidence is shown by the R2 of the regression and the intercept and coefficient values that allow for estimation of protein concentration in the samples are automatically determined and displayed as follows:

<img src="image/Picture5.png" width=100%>

4- With this information the module can directly estimate the protein concentration in every sample in an automated way. This is done using a loop to iterate over all the samples present in the data set a code that predicts the protein concentration in each sample using the regression model generated by the standard curve (which follows the y=mx+b equation, where y is the absorbance and x the sample to be predicted). This will give the predicted concentration in every sample in mg/ml and will look as follows:

<img src="image/Picture6.png" width=40%>

And we are done! You can find and use the python module that I described in this post in the following URL:
<a href="https://github.com/dendar/Protein-quantification" target="_blank">Protein quantification</a>

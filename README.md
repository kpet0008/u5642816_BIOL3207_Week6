# u5642816_BIOL3207_Week6	
# Data files				
Provide details about the workflow (i.e., which files are used, when and why) and write a detailed description of the data file used. Include the details about what the column means and which data file someone should use. 

Data was acquired from:
 Clark, T.D., Raby, G.D., Roche D.G., Binning, S.A., Speers-Roesch, B., Jutfelt, F. and Sudin, J. 2020. Ocean acidification does not impair the behaviour of coral reef fishes. Nature, 577: 370-375.

OA_activitydat_20190302.csv was the only data file used, and was renamed to OA_activitydat_20190302_Biol3207.csv. This data file is stored in the ‘data’ folder.
		
			
### OA_activitydat_20190302_Biol3207.csv ###			
Column descriptions from Clark et al, 2020:	
| Column Heading | Description |
|-------------|-----------	
|loc | Location, and year, where the data were collected. AIMS = Australian Institute of Marine Science; LIRS = Lizard Island Research Station |
|species | Species name: acantho = Acanthochromis; Ambon = Pomacentrus amboinensis; Chromis = Chromis atripectoralis; Humbug = Dascyllus aruanus; |Lemon = Pomacentrus moluccensis |
|treatment | Elevated CO2 [CO2] (850-1,050 µatm) or control [Control] (400 - 450 µatm) groups |
|animal_id | Fish identity |
|sl | Standard length of the fish in mm |
|size | Size grouping of the fish, separated at 15 mm standard length into 'big' or 'small' |
|activity | Number of seconds the fish was active per minute, averaged across the duration of the trial |
|comment | Comment with notes on the origin of the data |
		

For the purposes of this project, only the columns ‘species’, ‘treatment’, ‘sl’, and ‘activity’
were used. Any rows in these columns containing an NA value were also dropped.


### Image files ###	
Images featuring each of the six fish species included in the study were also sourced from Clark et al, 2020, and are stored in the ‘pics’ folder.
						
# Script files			
The analysis conducted in this project takes place in a single RMD document, titled 'git_fishes_student'

The following libraries are used in this project:  
--------------------------------------------------
pacman,  
bookdown,  
tidyverse,  
ggforce,  
flextable,  
latex2exp,  
png,  
magick  

### Code Workflow ###
-----------------------
The RMD file contains large chunks of plain and markdown text which are not R code. These are not detailed here, because they are just text in plain English.

**Question 3**  
A file pathway is saved into the object 'path'  
The data is read using the read_csv function, taking the file from the assigned pathway, and saved into the object 'data'

**Question 4**  
A new file pathway is saved into the object 'path'  
The object 'data' is output to the assigned pathway.  

**Task 4**  
Across several coding blocks, the data is cleaned.  

First, rows with NA values are removed, and character variables are converted to factors.  

In the second coding block, all unnecessary columns are removed, leaving only ‘species’, ‘treatment’, ‘sl’, and ‘activity’. This is saved to the object 'data_clean'.  

In the third coding block, the structure of the cleaned data is viewed. We can see that the 'species' and 'treatment' columns contain 6 levels and 2 levels respectively, which is expected. This tells us that there are no typos in the data.

In the fourth block, the cleaned data is saved to the output to the output folder. This overrides the output in Question 4.  

In the next four coding blocks, the data is divided into the control and treatment groups, and summary statistics are viewed in tables.  These two blocks follow the same structure.  
An object called 'mean_temp' is created. To fill this object, data_clean is first filtered by treatment group, and grouped by species. Then new columns for the means of sl and activity, and the standard errors of sl and activity, are created and filled with the means and standard errors for each species. This object has the same number of rows as data_clean, so each row with the same species contains the same value in the new columns.  

After this, another object (means.control or means.CO2, respectively) is created, and filled with only the unique values from 'mean_temp'. This reduces the data down to six rows, representing each species.  

Then, this data is viewed in a table using flextable.

**Task 5**  
A six-panel box-plot is created, one panel for each species. Each panel consists of two boxplots of activity, one for each treatment group.  
This figure is then output to the output/figures folder, with the title 'control.acid.species.png'
![control acid species](https://user-images.githubusercontent.com/62368915/189127279-18e24128-f85e-40db-8e4f-988e362dc6bf.png)

Into six new objects, named for each of the six species, are saved an image file of each fish. These images are read out of the pics folder.  

A single-panel plot is created, containing boxplots of the activity of three species grouped by treatment group.  
This plot is annotated with images of each of the three species, above the boxplots representing data for the species.  
This figure is then output to the output/figures folder, with the title 'species.activity.boxplot.png'. 
![species activity boxplot](https://user-images.githubusercontent.com/62368915/189127322-b80584d7-03b7-48e3-b683-3f77c1f437c2.png)


**Task 6**
'data_clean' is filted to the species "chromis", "lemon", and "acantho", and is used to create a single-panel figure.
![colab fig](https://user-images.githubusercontent.com/62368915/189127950-d94d0ad6-119c-49a7-82c2-16e9de48747a.png)

**Task 9**
A t-test is performed on two continuous variables in the cleaned data (activity and sl), and its results displayed in two tables. These tables contain one row representing each species, with columns for species name, difference in mean, t-statistic, p-statistic, confidence interval, and degrees of freedom.  

In order to achieve this, a for-loop is used.  
First, tibbles to store the results are created, called results_activity and results_sl. This object contains the aforementioned columns and six rows.
An identically-structured loop is run for each of the two treatment groups. The only difference between the two loops is which continuous variable is tested.  

Each of the two loops runs six times, each time corresponding to one of the six species.  
Within the loop, first a temporary object called 'temp_data' is created and filled with the data for the corresponding species.  
Another temporary object, 'temp_test', is then created and filled with the results of a t-test with equal variance (variances were confirmed to be identical in a test not included in this RMD file), comparing the two treatment groups.  
The relevant variables in the temp_test are extracted and stored in the corresponding results tibble.  
After the loops have run, the data within the two results tibbles are displayed in two flextables, as described above.

**Question 8**
Here, a permutation analysis is conducted for one of the species, acantho, for the difference in activity level between the two treatment groups. This is another method to generate a p-value associated with this difference.  

An object called 'samp_dist' is created, with two columns for each permutation's test statistic, and whether or not this statistic is more extreme than the t-statistic calculated in **Task 9**.  
5000 permutations are conducted. Accordingly, the samp_dist object has 5000 rows, and a for-loop creating the permutations runs 5000 times.  
Inside the for-loop, a temporary object, temp_data, is created, and filed with the data for the acantho species, with the treatment column shuffled.  
A t-test is then conducted in the same manner as in **Task 9**, and the resulting t-statistic is saved in the appropriate row of the samp_dist object.  
Then, this statistic is compared to the t-statistic calculated in **Task 9**, and a value of TRUE or FALSE is recorded according to whether the permutation statistic is greater in absolute value.  
Once the loop is completed, the number of TRUE values is divided by the number of FALSE values. This produces a p-statistic.

# Output files
This project outputs three files, neither of which are included in the repository.  
  
OA_activitydat_20190302_BIOL3207_output.csv is output into output/data.  
  
Two graphs, control.acid.species.png and species.activity.boxplot.png, are output into output/figures.  
  
The two output folders contain a .gitignore file set up such that the folders are included in the repository despite being seen as otherwise empty. This is done because the folders are necessary for the code to output to.  


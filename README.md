# u5642816_BIOL3207_Week6
##################			
# DATA files			
##################			
Provide details about the workflow (i.e., which files are used, when and why) and write a detailed description of the data file used. Include the details about what the column means and which data file someone should use. 

Data was acquired from:
 Clark, T.D., Raby, G.D., Roche D.G., Binning, S.A., Speers-Roesch, B., Jutfelt, F. and Sudin, J. 2020. Ocean acidification does not impair the behaviour of coral reef fishes. Nature, 577: 370-375.

OA_activitydat_20190302.csv was the only data file used, and was renamed to OA_activitydat_20190302_Biol3207.csv. This data file is stored in the ‘data’ folder.
		
			
### OA_activitydat_20190302_Biol3207.csv ###			
			
columnHeading		description	
-------------		-----------	
loc			Location, and year, where the data were collected. AIMS = Australian Institute of Marine Science; LIRS = Lizard Island Research Station
species			Species name: acantho = Acanthochromis; Ambon = Pomacentrus amboinensis; Chromis = Chromis atripectoralis; Humbug = Dascyllus aruanus; Lemon = Pomacentrus moluccensis	
treatment		Elevated CO2 [CO2] (850-1,050 µatm) or control [Control] (400 - 450 µatm) groups
animal_id		Fish identity
sl			Standard length of the fish in mm
size			Size grouping of the fish, separated at 15 mm standard length into 'big' or 'small'
activity		Number of seconds the fish was active per minute, averaged across the duration of the trial
comment			Comment with notes on the origin of the data
		

For the purposes of this project, only the columns ‘species’, ‘treatment’, ‘sl’, and ‘activity’
were used. Any rows in these columns containing an NA value were also dropped.

Images featuring each of the six fish species included in the study were also sourced from Clark et al, 2020, and are stored in the ‘pics’ folder.
			
##################			
# SCRIPT files			
##################			
			
			


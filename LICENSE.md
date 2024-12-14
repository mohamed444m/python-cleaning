import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
data = pd.read_excel("Airplane_Crashes_and_Fatalities_Since_1908.xlsx")
data
Date	Time	Location	Operator	Flight #	Route	Type	Registration	cn/In	Aboard	Fatalities	Ground	Summary
0	1908-09-17	17:18:00	Fort Myer, Virginia	Military - U.S. Army	NaN	Demonstration	Wright Flyer III	NaN	1	2.0	1.0	0.0	During a demonstration flight, a U.S. Army fly...
1	1912-07-12	06:30:00	AtlantiCity, New Jersey	Military - U.S. Navy	NaN	Test flight	Dirigible	NaN	NaN	5.0	5.0	0.0	First U.S. dirigible Akron exploded just offsh...
2	1913-08-06	NaN	Victoria, British Columbia, Canada	Private	-	NaN	Curtiss seaplane	NaN	NaN	1.0	1.0	0.0	The first fatal airplane accident in Canada oc...
3	1913-09-09	18:30:00	Over the North Sea	Military - German Navy	NaN	NaN	Zeppelin L-1 (airship)	NaN	NaN	20.0	14.0	0.0	The airship flew into a thunderstorm and encou...
4	1913-10-17	10:30:00	Near Johannisthal, Germany	Military - German Navy	NaN	NaN	Zeppelin L-2 (airship)	NaN	NaN	30.0	30.0	0.0	Hydrogen gas which was being vented was sucked...
...	...	...	...	...	...	...	...	...	...	...	...	...	...
5263	2009-05-20	06:30:00	Near Madiun, Indonesia	Military - Indonesian Air Force	NaN	Jakarta - Maduin	Lockheed C-130 Hercules	A-1325	1982	112.0	98.0	2.0	While on approach, the military transport cras...
5264	2009-05-26	NaN	Near Isiro, DemocratiRepubliCongo	Service Air	NaN	Goma - Isiro	Antonov An-26	9Q-CSA	5005	4.0	4.0	NaN	The cargo plane crashed while on approach to I...
5265	2009-06-01	00:15:00	AtlantiOcean, 570 miles northeast of Natal, Br...	Air France	447	Rio de Janeiro - Paris	Airbus A330-203	F-GZCP	660	228.0	228.0	0.0	The Airbus went missing over the AtlantiOcean ...
5266	2009-06-07	08:30:00	Near Port Hope Simpson, Newfoundland, Canada	Strait Air	NaN	Lourdes de BlanSablon - Port Hope Simpson	Britten-Norman BN-2A-27 Islander	C-FJJRÂ	424	1.0	1.0	0.0	The air ambulance crashed into hills while att...
5267	2009-06-08	NaN	State of Arunachal Pradesh, India	Military - Indian Air Force	NaN	Mechuka for Jorhat	Antonov An-32	NaN	NaN	13.0	13.0	0.0	The military transport went missing while en r...
5268 rows × 13 columns

data.head()
data.head()
Date	Time	Location	Operator	Flight #	Route	Type	Registration	cn/In	Aboard	Fatalities	Ground	Summary
0	1908-09-17	17:18:00	Fort Myer, Virginia	Military - U.S. Army	NaN	Demonstration	Wright Flyer III	NaN	1	2.0	1.0	0.0	During a demonstration flight, a U.S. Army fly...
1	1912-07-12	06:30:00	AtlantiCity, New Jersey	Military - U.S. Navy	NaN	Test flight	Dirigible	NaN	NaN	5.0	5.0	0.0	First U.S. dirigible Akron exploded just offsh...
2	1913-08-06	NaN	Victoria, British Columbia, Canada	Private	-	NaN	Curtiss seaplane	NaN	NaN	1.0	1.0	0.0	The first fatal airplane accident in Canada oc...
3	1913-09-09	18:30:00	Over the North Sea	Military - German Navy	NaN	NaN	Zeppelin L-1 (airship)	NaN	NaN	20.0	14.0	0.0	The airship flew into a thunderstorm and encou...
4	1913-10-17	10:30:00	Near Johannisthal, Germany	Military - German Navy	NaN	NaN	Zeppelin L-2 (airship)	NaN	NaN	30.0	30.0	0.0	Hydrogen gas which was being vented was sucked...
data.tail()
Date	Time	Location	Operator	Flight #	Route	Type	Registration	cn/In	Aboard	Fatalities	Ground	Summary
5263	2009-05-20	06:30:00	Near Madiun, Indonesia	Military - Indonesian Air Force	NaN	Jakarta - Maduin	Lockheed C-130 Hercules	A-1325	1982	112.0	98.0	2.0	While on approach, the military transport cras...
5264	2009-05-26	NaN	Near Isiro, DemocratiRepubliCongo	Service Air	NaN	Goma - Isiro	Antonov An-26	9Q-CSA	5005	4.0	4.0	NaN	The cargo plane crashed while on approach to I...
5265	2009-06-01	00:15:00	AtlantiOcean, 570 miles northeast of Natal, Br...	Air France	447	Rio de Janeiro - Paris	Airbus A330-203	F-GZCP	660	228.0	228.0	0.0	The Airbus went missing over the AtlantiOcean ...
5266	2009-06-07	08:30:00	Near Port Hope Simpson, Newfoundland, Canada	Strait Air	NaN	Lourdes de BlanSablon - Port Hope Simpson	Britten-Norman BN-2A-27 Islander	C-FJJRÂ	424	1.0	1.0	0.0	The air ambulance crashed into hills while att...
5267	2009-06-08	NaN	State of Arunachal Pradesh, India	Military - Indian Air Force	NaN	Mechuka for Jorhat	Antonov An-32	NaN	NaN	13.0	13.0	0.0	The military transport went missing while en r...
data.info()
data.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 5268 entries, 0 to 5267
Data columns (total 13 columns):
 #   Column        Non-Null Count  Dtype         
---  ------        --------------  -----         
 0   Date          5268 non-null   datetime64[ns]
 1   Time          3049 non-null   object        
 2   Location      5248 non-null   object        
 3   Operator      5250 non-null   object        
 4   Flight #      1069 non-null   object        
 5   Route         3561 non-null   object        
 6   Type          5241 non-null   object        
 7   Registration  4933 non-null   object        
 8   cn/In         4040 non-null   object        
 9   Aboard        5246 non-null   float64       
 10  Fatalities    5256 non-null   float64       
 11  Ground        5246 non-null   float64       
 12  Summary       4878 non-null   object        
dtypes: datetime64[ns](1), float64(3), object(9)
memory usage: 535.2+ KB
data.describe()
Date	Aboard	Fatalities	Ground
count	5268	5246.000000	5256.000000	5246.000000
mean	1971-10-23 15:50:42.369020480	27.554518	20.068303	1.608845
min	1908-09-17 00:00:00	0.000000	0.000000	0.000000
25%	1954-04-11 18:00:00	5.000000	3.000000	0.000000
50%	1973-03-04 00:00:00	13.000000	9.000000	0.000000
75%	1990-06-26 18:00:00	30.000000	23.000000	0.000000
max	2009-06-08 00:00:00	644.000000	583.000000	2750.000000
std	NaN	43.076711	33.199952	53.987827
data.isnull().sum()
Date               0
Time            2219
Location          20
Operator          18
Flight #        4199
Route           1707
Type              27
Registration     335
cn/In           1228
Aboard            22
Fatalities        12
Ground            22
Summary          390
dtype: int64
data.dropna(inplace=True)
data.isnull().sum()
Date            0
Time            0
Location        0
Operator        0
Flight #        0
Route           0
Type            0
Registration    0
cn/In           0
Aboard          0
Fatalities      0
Ground          0
Summary         0
dtype: int64
data['Operator'].value_counts()
Operator
United Air Lines                             36
Pan American World Airways                   30
American Airlines                            26
Eastern Air Lines                            20
Northwest Orient Airlines                    20
                                             ..
VASP                                          1
Air Florida                                   1
Inex Adria Aviopromet (Yugoslavia)            1
NLM (Nederlandse Luchtvaart Maatschappij)     1
Mimika Air                                    1
Name: count, Length: 528, dtype: int64
ta
data.drop_duplicates(inplace = True)
data.info()
<class 'pandas.core.frame.DataFrame'>
Index: 944 entries, 208 to 5265
Data columns (total 13 columns):
 #   Column        Non-Null Count  Dtype         
---  ------        --------------  -----         
 0   Date          944 non-null    datetime64[ns]
 1   Time          944 non-null    object        
 2   Location      944 non-null    object        
 3   Operator      944 non-null    object        
 4   Flight #      944 non-null    object        
 5   Route         944 non-null    object        
 6   Type          944 non-null    object        
 7   Registration  944 non-null    object        
 8   cn/In         944 non-null    object        
 9   Aboard        944 non-null    float64       
 10  Fatalities    944 non-null    float64       
 11  Ground        944 non-null    float64       
 12  Summary       944 non-null    object        
dtypes: datetime64[ns](1), float64(3), object(9)
memory usage: 103.2+ KB
5
data.head(5)
Date	Time	Location	Operator	Flight #	Route	Type	Registration	cn/In	Aboard	Fatalities	Ground	Summary
208	1930-01-19	18:23:00	Oceanside, California	Maddux Airlines	7	Aqua Caliente, Mexico - Los Angeles	Ford 5-AT-C Tri Motor	NC9689	5-AT-046	16.0	16.0	0.0	While en route to Los Angeles, the pilot, flyi...
236	1931-03-31	10:45:00	Bazaar, Kansas	Trans Continental and Western Air	599	Kansas City - Wichita - Los Angeles	Fokker F10A Trimotor	NC-999	1063	8.0	8.0	0.0	Shortly after taking off from Kansas City, one...
334	1934-08-31	23:42:00	Amazonia, Missouri	Rapid Air Transport	6	Omaha - St. Joseph	Stinson SM-6000B	NC10809	5004	5.0	5.0	0.0	The plane crashed about 11 miles from St. Jose...
354	1935-05-06	03:30:00	Atlanta, Missouri	Trans Continental and Western Air	6	Los Angeles - Albuquerque - Kanasas City - Wa...	Douglas DC-2-112	NC13785	1295	14.0	5.0	0.0	The plane crashed while en route from Albuquer...
365	1935-08-14	23:45:00	Near Gilmer, Texas	Delta Air Lines	4	Dallas - Atlanta	Stinson Model A	NC14599	9103	4.0	4.0	0.0	Crashed 3 miles south of Gilmer. The outboard ...
​

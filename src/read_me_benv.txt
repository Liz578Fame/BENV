

--------------------------------|
	 BENV directions            |
--------------------------------|--------------------------|
                                                           |
Credits:                                                   |  
                                                           |
BENV 2.0                                                   |
eb_v3.f                                                    |
                                                           |
-eb version 4.0                                            | 
                                                           | 
                                                           |
Additional code and modifcations by Randy Millerson        |
                                                           |
To run simply type "python skval_v3.py into the console    |
                                                           |
Output:                                                    |
                                                           |
out_pars_tables.srt                                        |
out_skin_table.srt                                         |
                                                           |
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
The BENV (Binding energy/Nucleon Values) program takes a two equations of state; e0 and e1, and atomic values for a    |
specific nucleus and returns the values of the nucleon radii, charge radius, binding energy, neutron skin,             |
symmetry energy coefficient and reference density.                                                                     |
                                                                                                                       |
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
                                                                                                                       | 
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
There are three parameter files which can be used to quickly and efficiently modify how the program runs:              |
                                                                                                                       | 
"par.don"                                                                                                              |
"serv_par.don"                                                                                                         |
"values.don"                                                                                                           |
                                                                                                                       |
                                                                                                                       |
The details on the input of each of these files is below:                                                              |
                                                                                                                       |
"par.don" : contains the controls for which nuclear density function to use and the formatting of the nuclear EOS      |
                                                                                                                       |
"serv_par.don" : contains the controls for looping over the program so as to calculate many different nuclei           |
                 calculations in the same run.                                                                         |
                                                                                                                       |
"values.in2016" : contains the atomic number and atomic mass of the nuclei whose atomic values are to be calculated    |
                                                                                                                       |
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
                                                                                                                       | 
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
                                                                                                                       |
"par.don" parameters:                                                                                                  | 
                                                                                                                       |
Standard Input: 19 2 3 19 19                                                                                           |    
Format is:      I1 I2 I3 I4 I5                                                                                         | 
                                                                                                                       |
I1: number of points if a single EOS is chosen                                                                         |
I2: Choice of density function:                                                                                        | 
	2: 2pf                                                                                                             |
	3: 3pf                                                                                                             |
	4: Folded-Yukawa                                                                                                   |
I3: Choice of EOS input:                                                                                               |
	0: "ex_nxlo.don": e0 and e1 same length; format: "kf  e0  e1"                                                      |
	1: "e0_nxlo.don" & "e1_nxlo.don": various lengths, adjusted e0 kf to den: "kf  e0"  &  "kf  e1"                    |
	2: "e0_nxlo.don" only: "kf  e0"                                                                                    |   
I4: Number of points e0 if differing length EOS                                                                        |
I5: Number of points e1 if differing length EOS                                                                        |
                                                                                                                       |
                                                                                                                       |
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
                                                                                                                       |
"serv_par.don" parameters:                                                                                             |
                                                                                                                       | 
Standard Input: 1 1 1 2 0                                                                                              | 
Format is:      I1 I2 I3 I4 I5                                                                                         |
                                                                                                                       |
I1: Number of Atomic Number increments (e.g. 1 time, 2 times...)                                                       |
I2: Number of Atomic Mass increments (e.g. 1 time, 2 times...)                                                         | 
I3: Reset the "values.in2016" file to original state, else incrementation is preserved: 1 is on, anything else is off. | 
I4: Value of incrementation (e.g. by 1, 2, 3...)                                                                       |
I5: Mirror nuclei option: 1 is on, anything else is off                                                                |
                                                                                                                       |
                                                                                                                       |
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
                                                                                                                       | 
"values.in2016"                                                                                                        | 
                                                                                                                       |
Standard Input: 64 64 64                                                                                               |
                0.0 20.0                                                                                               |
                208.0 82.0                                                                                             |
Format is:      I1 I2 I3                                                                                               |
                F1 F2                                                                                                  |
                F3 F4                                                                                                  |  
                                                                                                                       |
I1,I2,I3: Gaussian Quadrature Points                                                                                   |
F1: Radial Integration Start Point: Low limit                                                                          |
F2: Radial Integration Terminal Point: Upper limit                                                                     |
F3: Atomic Mass                                                                                                        |
F4: Atomic Number                                                                                                      |
                                                                                                                       |
                                                                                                                       |
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
Output Files:                                                                                                          |
                                                                                                                       | 
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       | 
"out_pars_table.srt"                                                                                                   |
                                                                                                                       |
Standard Output: 6.84521  0.42469  0.00000  6.92377  0.49904  0.00000                                                  |
                                                                                                                       | 
Format is:       rp       cp       wp       rn       cn       wn                                                       |
                                                                                                                       |
r: radius constant                                                                                                     | 
c: diffuse constant                                                                                                    |
w: polynomial constant                                                                                                 |
-p : proton matter                                                                                                     |
-n : neutron matter                                                                                                    | 
                                                                                                                       |  
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |
"out_skin_table.srt"                                                                                                   |
                                                                                                                       |
Standard Output: 208  79  5.700  5.517  0.183  5.583  -7.883  23.991  0.09234                                          |
                                                                                                                       |
Format is:       A    Z   N_rad  P_rad  NS     Chr     BE     Esymc   Ref_d                                            |
                                                                                                                       |
A: Mass Number                                                                                                         |
Z: Atomic Number                                                                                                       |
N_rad: Neutron Radius                                                                                                  |
P_rad: Proton Radius                                                                                                   |    
NS:    Neutron Skin                                                                                                    | 
Chr:   Charge Radius                                                                                                   |
BE:    Binding Energy                                                                                                  |
Esymc: Symmetry Energy Coefficient                                                                                     |
Ref_d: Reference Density                                                                                               |
                                                                                                                       |     
-----------------------------------------------------------------------------------------------------------------------|                                                                                                                                |
Le sommaire: Le logiciel "Benv_eb_3.0" calcule les parameters que ont a voir avec l'energie de liason et la peau de    |  
             neutron. Il est compatible avec plusieurs styles d'equation du l'etat nuclaire et peut accepter de        |   
             multiples entrees. Il existe des options a augmenter graduellement le numero atomique et nombre de masse. |
                                                                                                                       |  
-----------------------------------------------------------------------------------------------------------------------|
                                                                                                                       |      
  ______        _    _           _                 _____         _____                                                 | 
 |  ____|      | |  | |         | |               |_   _|       |  __ \                                                |
 | |__  __  __ | |  | |_ __ ___ | |__  _ __ __ _    | |  _ __   | |__) | __ _   _ _ __   __ _ ___                      |
 |  __| \ \/ / | |  | | '_ ` _ \| '_ \| '__/ _` |   | | | '_ \  |  ___/ '__| | | | '_ \ / _` / __|                     |
 | |____ >  <  | |__| | | | | | | |_) | | | (_| |  _| |_| | | | | |   | |  | |_| | | | | (_| \__ \                     |
 |______/_/\_\  \____/|_| |_| |_|_.__/|_|  \__,_| |_____|_| |_| |_|   |_|   \__,_|_| |_|\__,_|___/                     |
                                                                                                                       |
                                                                                                                       |
                                                                                                                       |  
-----------------------------------------------------------------------------------------------------------------------|
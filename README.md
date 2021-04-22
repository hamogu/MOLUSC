# MOLUSC
MOLUSC (Multi Observational Limits on Unseen Stellar Companions) is a python tool for determining constraints on possible stellar companions to a target star by combining RV, High Resolution Imaging and Gaia data.

## Purpose

See Wood et al. (2021) for more detail.

## Requirements
This code requires Python 3 and the following packages:
- Numpy
- Scipy
- Astropy
- Astroquery

The files BHAC15_2MASS.txt, BHAC15_CFHT.txt, BHAC15_GAIA.txt, gaia_contrast.txt, and RUWETableGP.txt to be present in the same folder.

## Use
MOLUSC can be used in two ways through the GUI or command line interfaces. The GUI provides a user-friendly interface with which to easily input parameters and read output, and includes slightly more functionality than the command line version, but is not as friendly to large sequences of runs or running on a cluster. The command line option makes it easy to script mutliple runs but is offers slighty fewer user options. 
Regardless of which interface is used the user will need to provide the following information about the code parameters and target star:
- RA and Dec
- Stellar Mass
- Star Age (if not provided a default age of 5 Gyr will be assumed)
- Number of companions to generate
- Output file prefix

The following information is optional, depending on which types of analysis are being used.

**Radial Velocity**
- File containing RV measurements, times and errors
- Spectral resolution of RV measurements
- Added Jitter
- RV Sensitivity Floor

**High Resolution Imaging**
- File containing contrast curve
- Filter in which imaging was taken (2MASS J, H, K, Gaia G, and CFHT R, I are available)

**Additional Input**
There are a number of additional options allowing you to alter the generated distribution of companions. You can choose to limit any of the six orbital parameters, $P$, $q$, $e$, $i$, $\omega$, and $\varphi$, to have fixed, minimum or maximum values. The mean and standard deviation of the log-normal period distribution can be altered, as can the exponent for the power-law mass ratio distribution. Finally, you can choose to use either the more conservative 18th mag or more complete 20th mag completeness limits for Gaia imaging limits.

![MOLUSC GUI]<img width="1180" alt="image" src="https://user-images.githubusercontent.com/64872115/115775317-bb648300-a380-11eb-9f91-2bf03128681a.png">

### Command Line
The command line interface does not offer the full range of user options. Specifically, using the command line interface it is **not** possible to:
- Use multiple contrast curves in one run
- Limit most orbital parameters (it is still possible to limit to only eclipsing companions)
- Adjust the Period or Mass Ratio distributions
- Use the 20th magnitude Gaia completeness limit

## Results
Results from MOLUSC are written out into one or two .csv files. The first file, which is always written out, is output_kept.csv. This includes the generated orbital parameters and calculated parameters (such as projected separation) for all simulated companions which were not ruled out by the analysis.
The second file, output_all.csv, is only written out if you choose to do so. It includes generated and calculated parameters for all simulated companions. For a typical star and 5 million simulated companions these files are often 1GB or more in size, so you may only want to write it out when necessary.

## Plotting

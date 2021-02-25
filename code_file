clear

** Make sure to open the dataset.
use "H:\Vedant\Econ\car_fatalities.dta"

*EDA
summarize
correlate mrall unrate perinc beertax mlda vmiles jaild comserd
describe
*variable transformation
gen vfrall=mrall*10000
gen mmiles=vmiles/1000
gen lnperinc=ln(perinc)
gen punish=0
replace punish = 1 if jaild==1
replace punish =1 if comserd==1

summarize vfrall beertax

*Correlation Test
corr mrall unrate perinc beertax mlda vmiles jaild comserd
*dry Regression model 1
reg vfrall beertax

*PANEL DATA (Fixed effect State fixed) model 2
xtset state year
xtreg vfrall unrate lnperinc beertax mlda mmiles i.jaild i.comserd, fe
estimates store fixed
areg vfrall unrate lnperinc beertax mlda mmiles i.jaild i.comserd, absorb(state)

*PANEL DATA (Random effect)
xtreg vfrall unrate lnperinc beertax mlda mmiles i.jaild i.comserd, re ( screenshot needed)
estimates store random
*HAUSMAN TEST
hausman fixed random
*Moving forward with FIXED EFFECTS MODEL for beertax
xtreg vfrall beertax,fe
*Exploratory models - examining correlation and other possible explanatory variables.

*PANEL DATA (Fixed effect State and Time fixed) 
* model 3
xtreg vfrall beertax i.year ,fe

xtreg vfrall unrate lnperinc beertax mlda mmiles i.punish i.year, absorb(state)
* model 4 not containing any economic variables
xtreg vfrall beertax mlda mmiles i.punish i.year, fe

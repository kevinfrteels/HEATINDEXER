# HEATINDEXER
A custom function for Google Sheets to calculate the heat index when the temp and humidity are entered into cells. 

I was looking for a simple plugin for Sheets that would calculate the heat index when given the temp and humidity. I could find calculators to do this online but none that provided the code to do so. Initially I wanted it for a weather conditions tracking calendar that pulled the temp and humidity from my own weather station but I quickly found some additional uses. 

I thought it would be a simple matter but after some reasearch, I landed on how the calculation is performed on the National Weather Service website where they provide a heat index calculator, but I wanted to be able to have it automatically calculate daily based on the high for each day and store it in a calendar. The calculation method is below:

Unable to find a calculator to do this for the needs that I had, I decided to use Google sheets to retrieve the data from the weather station and then used the formula below to create a custom function that could be used to drop into any cell and when the next two cells below pull the high temp and humidity for the day, it calculates the heat index per the formula below.

I've never put a project up before but the calculations were a pain in the rear so I thought I would post it to save others who might want it from having to spend so much time on it. 

https://www.wpc.ncep.noaa.gov/html/heatindex_equation.shtml

 
The computation of the heat index is a refinement of a result obtained by multiple regression analysis carried out by Lans P. Rothfusz and described in a 1990 National Weather Service (NWS) Technical Attachment (SR 90-23).  The regression equation of Rothfusz is
HI = -42.379 + 2.04901523*T + 10.14333127*RH - .22475541*T*RH - .00683783*T*T - .05481717*RH*RH + .00122874*T*T*RH + .00085282*T*RH*RH - .00000199*T*T*RH*RH
where T is temperature in degrees F and RH is relative humidity in percent.  HI is the heat index expressed as an apparent temperature in degrees F.  If the RH is less than 13% and the temperature is between 80 and 112 degrees F, then the following adjustment is subtracted from HI:
ADJUSTMENT = [(13-RH)/4]*SQRT{[17-ABS(T-95.)]/17}
where ABS and SQRT are the absolute value and square root functions, respectively.  On the other hand, if the RH is greater than 85% and the temperature is between 80 and 87 degrees F, then the following adjustment is added to HI:
ADJUSTMENT = [(RH-85)/10] * [(87-T)/5]
The Rothfusz regression is not appropriate when conditions of temperature and humidity warrant a heat index value below about 80 degrees F. In those cases, a simpler formula is applied to calculate values consistent with Steadman's results:
HI = 0.5 * {T + 61.0 + [(T-68.0)*1.2] + (RH*0.094)}
In practice, the simple formula is computed first and the result averaged with the temperature. If this heat index value is 80 degrees F or higher, the full regression equation along with any adjustment as described above is applied.
The Rothfusz regression is not valid for extreme temperature and relative humidity conditions beyond the range of data considered by Steadman.


# HEATINDEXER
A custom function for Google Sheets to calculate the heat index when the temp and humidity are entered into cells. 

I was looking for a simple plugin for Sheets that would calculate the heat index when given the temp and humidity. I could find calculators to do this online but none that provided the code to do so. Initially I wanted it for a weather conditions tracking calendar that pulled the temp and humidity from my own weather station but I quickly found some additional uses. 

I thought it would be a simple matter but after some reasearch, I landed on how the calculation is performed on the National Weather Service website where they provide a heat index calculator, but I wanted to be able to have it automatically calculate daily based on the high for each day and store it in a calendar. The calculation method is at the bottom of this page.

Unable to find a calculator to do this, I decided to use Google sheets to retrieve the data from the weather station and then converted the calculations at the bottom of this page into a single formula that takes the heat and humidity from two cells and generates the heat index. 

This will do the job but for each cell, one would need to modify the formula to account for the location of the temp and humidity. To make it easier to place anywhere I needed and as often as needed, I converted it to a custom function so that I can just drop it in from the functions menu when and where I needed it.

I've never put a project up before but the calculations were a pain in the rear so I thought I would post it to save others who might want it from having to spend so much time on it.

HOW TO USE

The formula is contained in the file, not as a script, but as a Google Sheets formula. It uses cell A1 for temperature input and A2 for humidity input and calculates it wherever the formula is placed. To use it, simply drop it into the cell you want to display the heat index, then replace A1 with the cell that will contain the temperature and A2 with the cell that will contain the humidity. Just as with any other function, a change to the reference cells will automatically change the cell value. 

CONVERTING TO A CUSTOM FUNCTION

I wanted to make it easy to add into any cell so I could create a calendar in Sheets, feed it daily highs for temp and humidity each day from my weather station and calculate the heat index each day. There are 19 occurances of the temperature variable and 15 of the humidity variable in the formula. To modify it for each cell would take far too long...especially as there are 365 days in a year. While I constructed the formula to allow the variables to change in reference to other cells when pasting, I wanted a simpler way to insert it into other sheets so I converted it to a custom function. This allows me to use it in any cell by simply typing =HEA which pops up the list of functions and eliminates everything from the dropdown except for HEATINDEXER which is the name I gave it. 

I click it and enter the reference location for the cell that contains the temperature followed by a comma, a space then the cell reference for the humidity, then press enter. That's it. Then I can copy and paste it elsewhere and as long as the location of the temp and humidity are in the same relative position it will work without any further input. 

To convert it to a custom function in Google Sheets, the cell references need to be changed to Named Variables. When using the function, it needs to be told where to look for the temp and humidity. They can't be reversed. So it's important that when creating the function, that the argument placeholders have a descriptive name. As there are 19 references to A1 (temperature) and 15 for A2 (humidity) it's easiest to use the Find and Replace feature in notepad for this. 

To setup the custom function, these are the steps:
1.) Copy the formula from the custom formula file and paste in into Notepad
2.) Use find/replace to replace the cell reference A1 with TEMP and repeat for A2, using HUM. 
3.) Copy the modified text from Notepad
4.) Open Google Sheets and go to DATA>NAMED FUNCTIONS
5.) Click on ADD NEW FUNCTION and give it a name such as HEATINDEXER
6.) Under ARGUMENT PLACEHOLDERS, Add two placeholders, one for TEMP and another for HUM
7.) Paste the modified formula into the FORMULA DEFINITION box 
9.) SAVE the function. 

It is not necessary to include any information in the Function Description or the fields below the Formula Definition box. They are just there for reference.
What is important is that the argument placeholders are descriptive enough to easily identify which is the temperature and which is the humidity and then that the placeholder names match what was used in Notepad to replace the cell references. Assuming this was done correctly, your placeholder names will each be assigned a color and the text in the Formula Definition box will show the matched text in the same color. 

And that's it. From there you can use it just as you would with any other function, by either typing = and selecting it from the list, =hea which should remove everything from the list not beginning with hea, or by going to INSERT>FUNCTION>NAMED FUNCTION where you can select it. Or you can simply type =HEATINDEXER (cell with temperature, cell with humidity). You can then copy/paste it wherever else you need it and as long as the temp and humidity are in the same relative positions as the first one, it will work. 

NEXT STEPS

When I next have some time, I'll convert it to an apps script. Enjoy! 

HEAT INDEX CALCULATION EXPLAINED

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


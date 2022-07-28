
KNIME Project
============================================================

You are given an excel file with the name Height of Male and Female by Country 2022. The file contains two sheets; Cm and Ft. Both sheets contain data of males and females heights by country. In the first sheet, the heights are in centimeters, while in the second sheet, the heights are in feet. 

The goal of this Lab is to:
- load and view the sheets into KNIME,  

- filter out a specific column,  

- join the tables containing the separate sheets into one,   

- filter the heights for a specific country, 

- compute the total height of female and male for the specific 

To accomplish this, go through the following steps. Your solution should be a KNIME Workflow where you show how you can solve the above tasks. 

(1) Create a Workflow called Lab 1.

(2) Load the sheet Cm from the Excel file in KNIME 
 - Use the Excel Reader Node.
 - Configuration: Browse for the file and specify which sheet you want to load (sheet Cm). 
 - After executing the Excel Reader Node, right click on the node and choose the last option “File Table”.
The columns Rank, Male in Height and Femal in Height are numbers, in particular, integers, while the column Country Name is a string, meaning, it contains text data. 
 
(3) Filter out the column Rank. 
 - You can use the Column Filter Node
 - Connect the output port of the Excel Reader Node to the input port of the Column Filter Node (drag and drop).
 Configuration: There are two boxes in the middle of the configuration window. The green box on the left are columns that you want to include, while the red box on the right are columns that you want to exclude. Click on the column Rank and then “<” which will move the column to the left.
 After configuring and executing the node, look at your filtered table, by making a right click on the node and then choose the last option “Filtered Table”. The output table does no longer contain the column Rank.

(4) Repeat (a) and (b) for the second sheet Ft of the Excel File.

(5) Join both sheets into one table.
 - To join two tables you can use the Joiner Node.
 Connect the output port of the Column Filter Node to the upper input port of the Joiner Node. Further connect the output port of the second Excel Reader Node to the lower input port of the Joiner Node.
 Configuration:  
- Select the columns from the top input ('left' table) and the bottom input ('right' table) that should be used for joining. Each pair of columns defines an equality constraint of the form A = B.  

- Next select “Matching rows”, this will include the joined rows in the output.   

- Select “Merge join columns”: If active, the join columns of the right input table are merged into their join partners of the left input table. 

- Finally select “Assign new row keys sequentially”: Combined rows are assigned row keys in the order they are produced, e.g., the first row in the join result is assigned row key Row0, the second row is assigned key Row1, etc. 

# Remark: In the above configuration we chose “Matching rows” which is a so-called INNER JOIN. There are different types of Join’s 

(6) Filter the joined table for the Country Ghana.
 - You can use the Row Filter Node.  
 - Connect the first output port of the Joiner Node to the input port of the Row Filter Node.
Configuration: Select Country Name as the column to test. Under Matching criteria, type Ghana and on the left specify that you want to include the rows for the country Ghana. 

# Remark: If you want to remove Ghana from the joined table, or any other country, you can apply the same configurations but choose “Exclude rows by attribute values” on the left side of the above configuration window.  

(7) Compute total height (female + male) in centimeters for the country Ghana. 
 - You can use the Math Formula Node. 
 - Connect the output port of the Row Filter Node to the input port of the Math Formula Node
 - Configuration: Select the column Female Height from the upper left part of the configuration window. The column will then appear on the lower middle part of the window with $ signs on each side. Next type + and select the column Male Height. With this statement, the node will add each row value of the column Female Height with the corresponding rows of the column Male Height. 
# Project Overview

Your dataset contains property sales for one-family dwellings in Manhattan over the last 12 months, including each property's zip code, building class, square feet, and sale price. However, records have have a sale price of $0 whenever there was a transfer of ownership without a cash consideration (like from parents to children).


## Objective

My task is create a new market value column that uses the recorded sale price when available, or estimates it by using the average price per square foot from properties within the same zip code and building class.


### Tools Used
- Microsoft Excel
- Excel Tables
- Functions Used:
  - AVERAGEIFS
  - IF
  - Pivot Tables
  - Pivot Charts / dashboard elements

### Dataset Fields Used

The analysis relied on the following columns:

- Neighborhood
- Address
- Zip Code
- Building Class
- Square Feet
- Sale Price


Step-by-Step Process
1. Import and review the dataset
Open the dataset in Excel
Review the available columns and identify the key variables needed for valuation
Confirm that some records have a Sale Price of 0
2. Convert the raw data into an Excel Table
Highlight the full dataset
Select Insert > Table
Ensure headers are included
Rename the table if needed

This makes formulas easier to manage and keeps the analysis scalable.

3. Create a Price per Square Foot column

Add a new column to calculate the recorded price per square foot for valid sales.

Example logic:

=IF([@[Sale Price]]>0,[@[Sale Price]]/[@[Square Feet]],0)

This calculates price per square foot only when a true sale price exists.

4. Estimate the average price per square foot for comparable properties

Create a formula that calculates the average price per square foot for rows with the same:

Zip Code
Building Class
Sale Price greater than 0

Example approach:

=AVERAGEIFS([Price per Sq Ft],[Zip Code],[@[Zip Code]],[Building Class],[@[Building Class]],[Sale Price],">0")

This creates a comparable pricing benchmark for each property.

5. Create the Market Value column

Build a new column that:

Uses the actual sale price if it exists
Otherwise estimates value using:
average price per square foot × property square feet

Example formula:

=IF([@[Sale Price]]>0,[@[Sale Price]],[@[Square Feet]]*AVERAGEIFS([Price per Sq Ft],[Zip Code],[@[Zip Code]],[Building Class],[@[Building Class]],[Sale Price],">0"))
6. Format the calculated values
Format Sale Price and Market Value as currency
Check for rows that may still return errors or blanks
Validate that square footage values are present where estimates are needed
7. Create a Pivot Table for summary analysis

Build a pivot table from the Excel table to summarize the new Market Value field.

Suggested setup:

Rows: Neighborhood
Values: Sum of Market Value

This allows you to compare neighborhoods by total estimated market value.

8. Answer business questions with Pivot Table filters

Use pivot table filters or value filters to answer questions such as:

Which neighborhoods have total market value above $15 million?
Which neighborhoods contain the highest total value of properties?
9. Explore market value distribution by neighborhood

Create additional pivot table views to examine how values are distributed.

Examples:

Rows: Neighborhood
Values: Count of Market Value
Filters or groupings: Market Value ranges

This helps identify how property values vary across different Manhattan neighborhoods.

10. Turn the analysis into a dashboard-style layout


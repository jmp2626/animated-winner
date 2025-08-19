You're absolutely right! That's a much cleaner approach. Instead of just showing the latest date's values, we should take the terminal (latest) date and accumulate all the net changes leading up to it. Here's the updated LOD framework:
Complete Tableau Framework: LOD with Cumulative Net Change
Step 1: Create the Parameter

Right-click in the Parameters area and select "Create Parameter"
Configure the parameter:

Name: Email Score Selection
Data type: String
Allowable values: List
List of values:

Value: 1, Display As: Email Score 1
Value: 2, Display As: Email Score 2


Current value: 1 (default)



Step 2: Create the LOD Calculated Fields
Selected Email Score (Terminal Date + Cumulative)
sqlIF [All Dates] = {MAX([All Dates])} THEN
    CASE [Email Score Selection]
        WHEN "1" THEN [email_score1] + {SUM([Net_Change])}
        WHEN "2" THEN [email_score2] + {SUM([Net_Change])}
    END
END
Net Change (Cumulative to Terminal Date)
sqlIF [All Dates] = {MAX([All Dates])} THEN 
    {SUM([Net_Change])}
END
Additions (Cumulative to Terminal Date)
sqlIF [All Dates] = {MAX([All Dates])} THEN 
    {SUM([Addition])}
END
Exits (Cumulative to Terminal Date)
sqlIF [All Dates] = {MAX([All Dates])} THEN 
    {SUM([Exits])}
END
Email Members (Terminal Date Count)
sqlIF [All Dates] = {MAX([All Dates])} THEN 
    COUNTD([Email_Members])
END
Step 3: Alternative with Date Range Filter
If you want to be more explicit about the date range for accumulation:
Selected Email Score (Filtered Range Cumulative)
sqlIF [All Dates] = {MAX([All Dates])} THEN
    CASE [Email Score Selection]
        WHEN "1" THEN [email_score1] + {SUM(IF [All Dates] <= {MAX([All Dates])} THEN [Net_Change] END)}
        WHEN "2" THEN [email_score2] + {SUM(IF [All Dates] <= {MAX([All Dates])} THEN [Net_Change] END)}
    END
END
Net Change (Running Total to Terminal)
sqlIF [All Dates] = {MAX([All Dates])} THEN 
    {SUM(IF [All Dates] <= {MAX([All Dates])} THEN [Net_Change] END)}
END
Step 4: Implementation

Add parameter control to dashboard
Use these calculated fields instead of raw fields
Result: Only the terminal (latest) date shows values, but those values represent the cumulative impact of all net changes up to that point

How This Works
Single Date Selected:

Terminal date gets its base value + all net changes up to that date

Multiple Dates Selected:

Only the latest date in selection shows values
Values represent cumulative total from all selected dates

No Filter:

Latest overall date shows cumulative totals

This approach gives you the true cumulative impact while avoiding duplication and maintaining the parameter flexibility for email scores!

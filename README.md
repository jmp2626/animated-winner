-- Selected Email Score
IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN CASE [Email Score Selection] WHEN "1" THEN [email_score1] + {SUM([Net_Change])} - [Net_Change] WHEN "2" THEN [email_score2] + {SUM([Net_Change])} - [Net_Change] END END

-- Net Change  
IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN {SUM([Net_Change])} END

-- Additions
IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN {SUM([Addition])} END

-- Exits
IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN {SUM([Exits])} END

-- Email Members
IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN COUNTD([Email_Members]) END

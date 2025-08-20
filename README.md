-- Selected Email Score Total
IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN
    IF [Email Score Selection] = "1" THEN 
        [email_score1] + {SUM([Net_Change])}
    ELSE 
        [email_score2] + {SUM([Net_Change])}
    END
END

-- Net Change Total
IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN 
    {SUM([Net_Change])} 
END

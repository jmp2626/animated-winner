-- Selected Email Score Total
IF DATETIME([All Dates]) = ISNULL({MIN(DATETIME([All Dates]))}) THEN
    -- No dates selected, use latest date
    IF DATETIME([All Dates]) = {MAX(DATETIME([All Dates]))} THEN
        IF [Email Score Selection] = "1" THEN [email_score1] ELSE [email_score2] END
    END
ELSE
    -- Dates selected, use first date value only
    IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN
        IF [Email Score Selection] = "1" THEN [email_score1] ELSE [email_score2] END
    END
END

-- Net Change Total (sum of selected range)
IF DATETIME([All Dates]) = ISNULL({MIN(DATETIME([All Dates]))}) THEN
    -- No dates selected
    IF DATETIME([All Dates]) = {MAX(DATETIME([All Dates]))} THEN {SUM([Net_Change])} END
ELSE
    -- Dates selected
    IF DATETIME([All Dates]) = {MIN(DATETIME([All Dates]))} THEN {SUM([Net_Change])} END
END

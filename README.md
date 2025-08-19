IF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) = 0 THEN
    // Single date selected
    CASE [Email Score Selection]
        WHEN "1" THEN [email_score1]
        WHEN "2" THEN [email_score2]
    END
ELSEIF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) > 0 THEN
    // Multiple dates selected, show only latest to avoid duplication
    IF [All Dates] = MAX([All Dates]) THEN 
        CASE [Email Score Selection]
            WHEN "1" THEN [email_score1]
            WHEN "2" THEN [email_score2]
        END
    ELSE 0 END
ELSE
    // No filter applied, show most recent monthly snapshot
    IF [All Dates] = MAX([All Dates]) THEN 
        CASE [Email Score Selection]
            WHEN "1" THEN [email_score1]
            WHEN "2" THEN [email_score2]
        END
    ELSE 0 END
END

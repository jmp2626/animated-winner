# animated-winner


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
2. Net Change (Deduplicated)
IF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) = 0 THEN
    // Single date selected
    [Net_Change]
ELSEIF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) > 0 THEN
    // Multiple dates selected, show only latest
    IF [All Dates] = MAX([All Dates]) THEN [Net_Change] ELSE 0 END
ELSE
    // No filter applied, show most recent
    IF [All Dates] = MAX([All Dates]) THEN [Net_Change] ELSE 0 END
END
3. Additions (Deduplicated)
IF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) = 0 THEN
    [Addition]
ELSEIF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) > 0 THEN
    IF [All Dates] = MAX([All Dates]) THEN [Addition] ELSE 0 END
ELSE
    IF [All Dates] = MAX([All Dates]) THEN [Addition] ELSE 0 END
END
4. Exits (Deduplicated)
IF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) = 0 THEN
    [Exits]
ELSEIF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) > 0 THEN
    IF [All Dates] = MAX([All Dates]) THEN [Exits] ELSE 0 END
ELSE
    IF [All Dates] = MAX([All Dates]) THEN [Exits] ELSE 0 END
END
5. Email Members (Unique Count)
IF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) = 0 THEN
    COUNTD([Email_Members])
ELSEIF DATEDIFF('day', MIN([All Dates]), MAX([All Dates])) > 0 THEN
    IF [All Dates] = MAX([All Dates]) THEN COUNTD([Email_Members]) END
ELSE
    IF [All Dates] = MAX([All Dates]) THEN COUNTD([Email_Members]) END
END
Step 3: Alternative LOD Approach (Simpler)
If the above seems complex, here's a cleaner LOD approach:
Selected Email Score (LOD Version)
IF [All Dates] = {MAX([All Dates])} THEN
    CASE [Email Score Selection]
        WHEN "1" THEN [email_score1]
        WHEN "2" THEN [email_score2]
    END
END
Net Change (LOD Version)
IF [All Dates] = {MAX([All Dates])} THEN [Net_Change] END

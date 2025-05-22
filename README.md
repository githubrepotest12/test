85    proc sql;
86      update maic.bootstrapping_attrib A, werk.bootstrapping_attrib B
                                          -
                                          79
                                          76
ERROR 79-322: Expecting a SET.
ERROR 76-322: Syntax error, statement will be ignored.
87        set A.ALT      = B.ALT,
88            A.PLT      = B.PLT,
89            A.UnitCost = B.UnitCost
90      where A.NIIN = B.NIIN
91      ;
NOTE: PROC SQL set option NOEXEC and will continue to check the syntax of statements.
92    quit;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used (Total process time):
      real time           0.00 seconds
      cpu time            0.00 seconds
      

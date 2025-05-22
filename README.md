85    
86    proc sql;
87      update maic.bootstrapping_attrib as A
88        set A.ALT      = B.ALT,
               -
               73
               76
ERROR 73-322: Expecting an =.
ERROR 76-322: Syntax error, statement will be ignored.
89            A.PLT      = B.PLT,
90            A.UnitCost = B.UnitCost
91      from werk.bootstrapping_attrib as B
92      where A.NIIN = B.NIIN
93      ;
NOTE: PROC SQL set option NOEXEC and will continue to check the syntax of statements.
94    quit;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used (Total process time):
      real time           0.00 seconds
      cpu time            0.00 seconds
      
95    

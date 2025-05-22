/* 1. Sort both tables by NIIN */
proc sort data=maic.bootstrapping_attrib 
          out=werk._orig(rename=(NIIN=NIIN_orig));
  by NIIN;
run;

proc sort data=werk.bootstrapping_attrib 
          out=werk._imp(keep=NIIN ALT PLT UnitCost);
  by NIIN;
run;

/* 2. Merge, keeping all original NIINs and only overriding when edits exist */
data maic.bootstrapping_attrib;
  merge
    werk._orig(in=inOrig drop=ALT PLT UnitCost)  /* original fields minus the ones we’ll override */
    werk._imp (in=inImp);                         /* imported overrides */
  by NIIN;

  /* only keep those that existed originally */
  if not inOrig then delete;

  /* if user provided edits, round & assign them */
  if inImp then do;
    ALT      = round(ALT,      0.001);
    PLT      = round(PLT,      0.001);
    UnitCost = round(UnitCost, 0.001);
end;

NOTE: There were 1 observations read from the data set WERK.BOOTSTRAPPING_ATTRIB.
NOTE: The data set WERK._IMP has 1 observations and 4 variables.
NOTE: PROCEDURE SORT used (Total process time):
      real time           0.01 seconds
      cpu time            0.02 seconds
      
96    
97    /* 2. Merge, keeping all original NIINs and only overriding when edits exist */
98    data maic.bootstrapping_attrib;
99      merge
100       werk._orig(in=inOrig drop=ALT PLT UnitCost)  /* original fields minus the ones we’ll override */
101       werk._imp (in=inImp);                         /* imported overrides */
102     by NIIN;
103   
104     /* only keep those that existed originally */
105     if not inOrig then delete;
106   
107     /* if user provided edits, round & assign them */
108     if inImp then do;
109       ALT      = round(ALT,      0.001);
110       PLT      = round(PLT,      0.001);
111       UnitCost = round(UnitCost, 0.001);
112   end;
113   
114   %studio_hide_wrapper;
ERROR: BY variable NIIN is not on input data set WERK._ORIG.
WARNING: The data set MAIC.BOOTSTRAPPING_ATTRIB may be incomplete.  When this step was stopped there were 0 observations and 6 
         variables.
WARNING: Data set MAIC.BOOTSTRAPPING_ATTRIB was not replaced because this step was stopped.

/* 1. Sort both tables by NIIN */
proc sort data=maic.bootstrapping_attrib 
          out=_orig(rename=(NIIN=NIIN_orig));
  by NIIN;
run;

proc sort data=work.bootstrapping_attrib 
          out=_imp(keep=NIIN ALT PLT UnitCost);
  by NIIN;
run;

/* 2. Merge, keeping all original NIINs and only overriding when edits exist */
data maic.bootstrapping_attrib;
  merge
    _orig(in=inOrig drop=ALT PLT UnitCost)  /* original fields minus the ones we’ll override */
    _imp (in=inImp);                         /* imported overrides */
  by NIIN;

  /* only keep those that existed originally */
  if not inOrig then delete;

  /* if user provided edits, round & assign them */
  if inImp then do;
    ALT      = round(ALT,      0.001);
    PLT      = round(PLT,      0.001);
    UnitCost = round(UnitCost, 0.001);
  end;

  /* 3. Error checks (same as before) */
  if missing(RMC, ALT, PLT, UnitCost) then do;
    put 'ERROR: MISSING CRITICAL DATA: ' NIIN= RMC= ALT= PLT= UnitCost=/;
    abort cancel;
  end;
  if ALT < 0 or PLT < 0 or UnitCost < 0 then do;
    put 'ERROR: NEGATIVE DATA PRESENT: ' NIIN= ALT= PLT= UnitCost=/;
    abort cancel;
  end;
run;

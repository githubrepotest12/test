/* 1. Sort original MAIC table into your werk library WITHOUT renaming NIIN */
proc sort 
    data=maic.bootstrapping_attrib 
    out=werk._orig(drop=ALT PLT UnitCost);
  by NIIN;
run;

/* 2. Sort your imported edits (still in work) */
proc sort 
    data=work.bootstrapping_attrib      /* wherever your import landed */
    out=werk._imp(keep=NIIN ALT PLT UnitCost);
  by NIIN;
run;

/* 3. Merge back together */
data werk.bootstrapping_attrib;         /* test copy in werk */
  merge
    werk._orig(in=inOrig)
    werk._imp (in=inImp);
  by NIIN;

  /* only keep lines that existed originally */
  if not inOrig then delete;

  /* override only when edits exist */
  if inImp then do;
    ALT      = round(ALT,      0.001);
    PLT      = round(PLT,      0.001);
    UnitCost = round(UnitCost, 0.001);
  end;

  /* error checks */
  if missing(RMC, ALT, PLT, UnitCost) then do;
    put 'ERROR: MISSING CRITICAL DATA: ' NIIN= RMC= ALT= PLT= UnitCost=/;
    abort cancel;
  end;
  if ALT < 0 or PLT < 0 or UnitCost < 0 then do;
    put 'ERROR: NEGATIVE DATA PRESENT: ' NIIN= ALT= PLT= UnitCost=/;
    abort cancel;
  end;
run;

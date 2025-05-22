proc sql;
  update maic.bootstrapping_attrib as A
    set A.ALT      = B.ALT,
        A.PLT      = B.PLT,
        A.UnitCost = B.UnitCost
  from werk.bootstrapping_attrib as B
  where A.NIIN = B.NIIN
  ;
quit;

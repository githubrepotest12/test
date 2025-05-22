proc sql;
  update maic.bootstrapping_attrib A, werk.bootstrapping_attrib B
    set A.ALT      = B.ALT,
        A.PLT      = B.PLT,
        A.UnitCost = B.UnitCost
  where A.NIIN = B.NIIN
  ;
quit;

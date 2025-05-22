proc sql;
  update maic.bootstrapping_attrib A
    set ALT      = (select B.ALT
                    from werk.bootstrapping_attrib B
                    where B.NIIN = A.NIIN),
        PLT      = (select B.PLT
                    from werk.bootstrapping_attrib B
                    where B.NIIN = A.NIIN),
        UnitCost = (select B.UnitCost
                    from werk.bootstrapping_attrib B
                    where B.NIIN = A.NIIN)
  /* only touch rows where there *is* a matching edit */
  where exists (
    select 1 
      from werk.bootstrapping_attrib B
     where B.NIIN = A.NIIN
  )
  ;
quit;

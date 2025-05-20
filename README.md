	%if %upcase(&SIMTYPE.)=MAIC %then %do;
		*Import line item table table;
		proc import datafile="&outdir./Item_attribute_edits.xlsx"
		    out=maic.bootstrapping_attrib_export
		    dbms=XLSX
		    replace;
		    sheet=bootstrapping_attrib_export;
		    getnames=yes;
		run;

		*Error checks;
		data maic.bootstrapping_attrib_export;
			set maic.bootstrapping_attrib; *change to boostrapping_attrib when done;
				length NIIN $ 9 NIINFinal $ 9;
				
				*Delete row if NIIN does not exsist;
				if niin = '' then delete;
				
	 		    *Adjsut NIIN to 9 characters because excel autoformats csv files and drops the leading 0s;
				NIINFinal = reverse(substr(reverse(cats('00000000', strip(compress(NIIN, '-')))), 1,9));
			
				*Round import values; 
				ALT = round(ALT, .001); 
				PLT = round(PLT, .001); 
 				UnitCost = round(UnitCost, .001);
				
				*Error if missing critical data;
				if missing(RMC) or missing(ALT) or missing(PLT) or missing(UnitCost) then do; 
					put 'ERROR: MISSING CRITICAL DATA: '
					NIIN= RMC= ALT= PLT= UNITCOST= /;
					abort; 
				end;
				
	
				*Error if any numeric variable is negative;
				if ALT<0 or PLT<0 or UnitCost<0 then do;
					put 'ERROR: NEGATIVE OR NON-NUMERIC DATA PRESENT: '
					NIIN= ALT= PLT= UNITCOST=/;
					abort;
				end;
						
				drop NIIN;
				rename NIINFinal = NIIN;
		run;
	%end;

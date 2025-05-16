*Create fields for recalc flags;
		data work.bootstrapping_attrib_export;
			set maic.bootstrapping_attrib;
			Recalc_SS='N';
			Recalc_MaxOH='N';
			Recalc_CovDur='N';
		run;
		
		*Export IA table;
		ods excel options(sheet_name = "bootstrapping_attrib_export");
		
		proc print data=work.bootstrapping_attrib_export noobs;
			var NIIN / style(column)={background=lightgrey};
			var RMC ALT PLT UnitCost; 
		run;

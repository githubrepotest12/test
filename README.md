<body onload="defaultLoad();">
    <form action="/SASJobExecution/" target="_self" onsubmit="return cleanPopulationText()" id="myForm" novalidate>
        <input type="hidden" value="/Users/KJC0203/jeff_stage/jobs/SubmitStandard" name="_program">
        <input type="hidden" name="_action" value="execute">
        <input type="hidden" id="scencount" name="scencount" value="0">
        <input type="hidden" id="filePath" name="ui_prod_vs_dev_folder" value="&ui_prod_vs_dev_folder.">
        <input type="hidden" id="savelog" name="save_log" value="1">
        <input type="hidden" id="scendesc" name="scen_desc" value="">
        <input type="hidden" id="runFolderStamp" name="runFolderStamp" value="&runFolderStamp.">
        <input type="hidden" id="MSC" name="MSC" value="&MSC.">
<script>
    // Output Options: Simulation Analysis Type Function Call
    function simulationAnalysisType(){
            if ("&LOGIN_TYPE" == "AAA"){
                document.getElementById('simAnalysisType').style.display = 'none';
                document.getElementById('simAnalysisType2').style.display = 'block';
            }
            else {
                document.getElementById('simAnalysisType').style.display = 'block';
                document.getElementById('simAnalysisType2').style.display = 'none';
            }
        }

    function showCard(id) {
            document.getElementById(id).classList.toggle('show');
        }

    function editparamChange(){
        var paramCheck = document.getElementById("FlexInputType").checked;

        if (paramCheck == true){
            document.getElementById('editParamText').style.display = 'block';
        }

        else{
            document.getElementById('editParamText').style.display = 'none';
        }

    }
    function checkSS_SC_Cage(strategy) {
        var soleCheckbox = document.getElementById('sole');
        var sourceCheckbox = document.getElementById('source');

        var cage_sourcing_strat = document.getElementById('cage_sourcing_strat');

        var soleChecked = soleCheckbox.checked;
        var sourceChecked = sourceCheckbox.checked;

        if (soleChecked && sourceChecked) {
            cage_sourcing_strat.value = 'SS_SC';
        } else if (soleChecked) {
            cage_sourcing_strat.value = 'SS';
        } else if (sourceChecked) {
            cage_sourcing_strat.value = 'SC'
        } else{
            alert("You cannot Simulate Competitive Cages. Please select Source Controlled, Sole Sourced, or Both.");
        }
    }
    function forceAAAscenParams() {

        var PROC = document.getElementById('default_aaa_params').value;

        document.getElementById('include_icr_of_zero_y').checked = true;
        document.getElementById('inactive_toggle').style.display = "none";
        document.getElementById('supplyChain1').style.display = "none";
        document.getElementById('popSelection').style.display = "none";
        document.getElementById('popInput').style.display = "none";
        document.getElementById('fcst_type_rmcr_0').value = "DFUAVG";
        document.getElementById('partial_aaa').style.display = "flex";

        document.getElementById("att").checked = false;
        document.getElementById("pr").checked = false;
        document.getElementById("fin").checked = false;
        document.getElementById("tpipt").checked = false;
        document.getElementById("niin").checked = false;
        document.getElementById("usr").checked = false;
        document.getElementById("j8val").checked = false;
        document.getElementById("priceval").checked = false;
        document.getElementById("xlsohoo").checked = false;
        // document.getElementById("att").value = "0";
        // document.getElementById("pr").value = "0";
        // document.getElementById("fin").value = "0";
        // document.getElementById("tpipt").value = "0";
        // document.getElementById("niin").value = "0";
        // document.getElementById("usr").value = "0";
        // document.getElementById("j8val").value = "0";
        // document.getElementById("priceval").value = "0";


        if (PROC == "AAA_AVN") {
            
            alert("All parameters will be updated to default Aviation AAA Settings. \r\n \r\nPlease note that for this population option, BCA parameters cannot be changed. \r\n \r\nRefer to help documentation to view default settings and contact BCASimulatorSupport@dla.mil with any issues");
            
            //set SIMULATION level params by default for AVN
            document.getElementById("pen_CPS_buffer_all").value = 'AVNlvl';
            document.getElementById('pen_CPS_buffer_all').disabled  = true;
            document.getElementById('pen_CPS_buffer_all').classList.add('disabled');
            document.getElementById('simAnalysisType').value = "AVN_AAA_REPORT";
            document.getElementById("DefaultSCChoice").value = 'AVN';
            document.getElementById("ltc_data_source").value = 'OAExtract';
            document.getElementById('default_aaa_params').value = "AAA_AVN";
            document.getElementById("SSA_SC").value = 'AVN';
            document.getElementById("pen_CPS_buffer_all").value = 'AVNlvl';
            document.getElementById("accdb").value = '0';


            //need to add logic to delete scenarios that already exists so it doesnt keep compoudning as you change niin pop
            // TODO: Uncomment for full UP deployment

            // Setup DDTRANS Additional Scenario
            addScenario();
            // Setup DDLTC Additional Scenario
            addScenario();
            //Return autoscroll to the top
            window.scroll(0, 0);

            document.getElementById("scen_1").value = 'DDTRANS';
            document.getElementById("scen_2").value = 'DDLTC';
            document.getElementById("pen_CPS_buffer_0").value = '100';
            document.getElementById("pen_CPS_buffer_1").value = '100';
            document.getElementById("pen_CPS_buffer_2").value = '100';

            // document.getElementById("costEscOnOffC1").style.display = 'none';
            // document.getElementById("CostEscOnOffHeader1").style.display = 'none';
            // document.getElementById("costEscOnOffC2").style.display = 'none';
            // document.getElementById("CostEscOnOffHeader2").style.display = 'none';

            if ("&AdminUser." != "true"){
                
                document.getElementById('added_scenarios').style.display = 'none';
            }

            //set SCENARIO level params by default for AVN
            //note this really does nothing on the BE bc all scen values are overwritten on BE if default aaa param option is chosen. this is just for user view and continuity
            // TODO: Unomment for full UP deployment
            //hide extra cps proxy option for ddtrans
            //document.getElementById('cpsAAAalt1').style.display = "none";
            //show option set that doesnt have cps proxy option for ddtrans
            //document.getElementById('cps1').style.display = "flex";
            //show extra cps proxy option for ddltc
            //document.getElementById('cpsAAAalt2').style.display = "flex";
            //hide option set that doesnt have cps proxy option for ddltc
            //document.getElementById('cps2').style.display = "none";
            
            // document.getElementById("channel1").value = 'CDTODD';
            // document.getElementById("contract1").value = 'TRANS';
            // document.getElementById("cps1").value = 'OFFCPS';
            // document.getElementById("ALTVal1").value = 'SC_FSC_AVG';
            // showSimCalcALT(this, 1);
            // document.getElementById("covDurVal1").value = 'EOQ';
            // showSimCalcCov(this, 1);
            // document.getElementById("pen_CPS_buffer_1").value = '100';
            // updateSFpop(this, 1);
            
            // document.getElementById("channel2").value = 'CURRENT';
            // document.getElementById("contract2").value = 'LTC';
            // document.getElementById("cpsAAAalt2").value = 'CPSPROXY';
            // document.getElementById("ALTVal2").value = 'FIXED';
            // showSimCalcALT(this, 2);
            // document.getElementById("alt2").value = '15';
            // document.getElementById("covDurVal2").value = 'FIXED';
            // showSimCalcCov(this, 2);
            // document.getElementById("covDur2").value = '30';
            // document.getElementById("pen_CPS_buffer_2").value = '100';
            // updateSFpop(this, 2);    

        }
        else if (PROC == "AAA_LM") {
            
            alert("All parameters will be updated to default Land & Maritime AAA Settings. \r\n \r\nPlease note that for this population option, BCA parameters cannot be changed. \r\n \r\nRefer to help documentation to view default settings and contact BCASimulatorSupport@dla.mil with any issues");
            
            // set SIMULATION level params by default for LM
            document.getElementById("pen_CPS_buffer_all").value = 'LMlvl';
            document.getElementById('pen_CPS_buffer_all').disabled  = true;
            document.getElementById('pen_CPS_buffer_all').classList.add('disabled');
            document.getElementById('simAnalysisType').value = "LM_AAA_REPORT";
            document.getElementById("DefaultSCChoice").value = 'LM';
            document.getElementById("ltc_data_source").value = 'OAHeader'; 
            document.getElementById('default_aaa_params').value = "AAA_LM";
            document.getElementById("SSA_SC").value = 'LM';
            document.getElementById("pen_CPS_buffer_all").value = 'LMlvl';

            //need to add logic to delete scenarios that already exists so it doesnt keep compoudning as you change niin pop
            // Setup DDTRANS Additional Scenario
            addScenario();
            // Setup DDLTC Additional Scenario
            addScenario();
            //Return autoscroll to the top
            window.scroll(0, 0);

            document.getElementById("scen_1").value = 'DDTRANS';
            document.getElementById("scen_2").value = 'DDLTC';
            document.getElementById("pen_CPS_buffer_0").value = '85';
            // document.getElementById("costEscOnOffC1").style.display = 'none';
            // document.getElementById("CostEscOnOffHeader1").style.display = 'none';
            // document.getElementById("costEscOnOffC2").style.display = 'none';
            // document.getElementById("CostEscOnOffHeader2").style.display = 'none';
            if ("&AdminUser." != "true"){
                
                document.getElementById('added_scenarios').style.display = 'none';
            }

            //set SCENARIO level params by default for LM
            //note this really does nothing on the BE bc all scen values are overwritten on BE if default aaa param option is chosen. this is just for user view / continuity
            //hide extra unique option for ddtrans
            // document.getElementById('cpsAAAalt1').style.display = "none";
            //show option set that doesnt have unique option for ddtrans
            // document.getElementById('cps1').style.display = "flex";
            //show extra unique option for ddltc
            // document.getElementById('cpsAAAalt2').style.display = "flex";
            //hide option set that doesnt have unique option for ddltc
            // document.getElementById('cps2').style.display = "none";
            
            // document.getElementById("channel1").value = 'CDTODD';
            // document.getElementById("contract1").value = 'TRANS';
            // document.getElementById("cps1").value = 'OFFCPS';
            // document.getElementById("ALTVal1").value = 'SC_FSC_AVG';
            // showSimCalcALT(this, 1);
            // document.getElementById("covDurVal1").value = 'EOQ';
            // showSimCalcCov(this, 1);
            // document.getElementById("pen_CPS_buffer_1").value = '85';
            // updateSFpop(this, 1);
            
            // document.getElementById("channel2").value = 'CURRENT';
            // document.getElementById("contract2").value = 'LTC';
            // document.getElementById("cpsAAAalt2").value = 'LMAAADDLTC'; 
            // document.getElementById("ALTVal2").value = 'FIXED';
            // showSimCalcALT(this, 2);
            // document.getElementById("alt2").value = '15';
            // document.getElementById("covDurVal2").value = 'EOQ';
            // showSimCalcCov(this, 2);
            // document.getElementById("pen_CPS_buffer_2").value = '85';
            // updateSFpop(this, 2);  

        }
        else {
            document.getElementById('cpsAAAalt1').style.display = "none";
            document.getElementById('cpsAAAalt2').style.display = "none";
            document.getElementById('pen_CPS_buffer_all').disabled  = false;
            document.getElementById('pen_CPS_buffer_all').className = ('form-control');
        }
        }
    function ViewDefaultSCSettings() {
        var PROC = document.getElementById('DefaultSCSettingsYes').checked;

        if (PROC == true) {
            document.getElementById('DisplayDefaultSCOptions').style.display = "flex";
            
            //since disabling in JS will not generate a macro var, these are set on BE
            //if Default SC Settings is checked
            document.getElementById('ltc_data_source').disabled = true;
            document.getElementById('SSA_SC').disabled = true;
            document.getElementById('pen_CPS_buffer_all').disabled  = true;
            document.getElementById('pen_CPS_buffer_0').disabled  = true;
            //need to disable all pen_cps_buffer for every scenario dynamically

            // Add class to grey out options after disabling
            document.getElementById('ltc_data_source').classList.add('disabled');
            document.getElementById('SSA_SC').classList.add('disabled');
            document.getElementById('pen_CPS_buffer_all').classList.add('disabled');
            document.getElementById('pen_CPS_buffer_0').classList.add('disabled');
        }

        else { 
            document.getElementById('DefaultSCChoice').disabled = true;
            document.getElementById('DisplayDefaultSCOptions').style.display = "none"; 

            document.getElementById('ltc_data_source').disabled = false;
            document.getElementById('SSA_SC').disabled = false;
            document.getElementById('pen_CPS_buffer_all').disabled = false; 
            document.getElementById('pen_CPS_buffer_0').disabled = false;

            // Replace class with original to remove the greyed out one in the event the user clicks back and fourth
            document.getElementById('ltc_data_source').className = ('form-control');
            document.getElementById('SSA_SC').className = ('form-control');
            document.getElementById('pen_CPS_buffer_all').className = ('form-control');
            document.getElementById('pen_CPS_buffer_0').className = ('form-control');
        }
    }
    function showSimCalcRUC(that, scen) {
        
        var simCalcruc = document.getElementById('unit' + scen).value;

        if (simCalcruc === 'PERCENT') {
            document.getElementById('rucDays' + scen).style.display = 'none';
            document.getElementById('ruc' + scen).disabled = true;
            document.getElementById('rucPer' + scen).style.display = 'flex';
            document.getElementById('ucv' + scen).disabled = false;
            document.getElementById('rucNONE' + scen).style.display= 'none';
        }

        else if (simCalcruc === 'FIXED'){
            document.getElementById('rucDays' + scen).style.display= 'flex';
            document.getElementById('ruc' + scen).disabled = false;
            document.getElementById('rucPer' + scen).style.display = 'none';
            document.getElementById('ucv' + scen).disabled= true;
            document.getElementById('rucNONE' + scen).style.display= 'none';
            }
        else{
            document.getElementById('rucDays' + scen).style.display = 'none';
            document.getElementById('ruc' + scen).disabled = true;
            document.getElementById('rucPer' + scen).style.display = 'none';
            document.getElementById('ucv' + scen).disabled = true;
            document.getElementById('rucNONE' + scen).style.display= 'flex';
        }
    }
    function pathNumCheck(val) {

        document.getElementById('Refprevpath').value = val;

        if (val.length > 300 || val.length < 1) {
            alert("The path to the previously sourced data in SAS Grid must be between 1 and 300 characters");
            document.getElementById('Refprevpath').value = "";
        }
        else {
        }

    }

    function alphaNumCheckAS(val,id) {

        val = val.replace(/ /g, "_");


        document.getElementById(id).value = val;

        if (!(val.match(/^[a-zA-Z0-9_]*$/)) && (val.length > 6 || val.length < 1)) {
            alert("Your Scenario name can not contain special characters and its length must be between 1 and 6 characters");
            document.getElementById(id).value = id;
        }
        else if (!(val.match(/^[a-zA-Z0-9_]*$/))) {
            alert("Your Scenario name can not contain special characters");
            document.getElementById(id).value = id;
        }
        else if (val.length > 6 || val.length < 1) {
            alert("Your Scenario name length must be between 1 and 6 characters");
            document.getElementById(id).value = id;
        }
        else {
        }

        }
    function changeHidden2() {
        for (var i = 1; i < x; i++) {

            document.getElementById("ssType" + i).disabled = false;
            document.getElementById("ssType" + i).value = "PERCENT";


            document.getElementById('maxType' + i).disabled = false;
            document.getElementById('maxType' + i).value = "PERCENT";

            // document.getElementById('unEsc' + i).disabled = false;
            // document.getElementById('unEsc' + i).value = "COMPOUNDANNUAL";                    


            //Set these to whatever baseline was chosen as
            document.getElementById("fcst_type_rmcr_" + i).value = document.getElementById("fcst_type_rmcr_0").value;
            document.getElementById("dmd_type_rmcn_" + i).value = document.getElementById("dmd_type_rmcn_0").value;
            document.getElementById("dmd_type_rmcb_" + i).value = document.getElementById("dmd_type_rmcb_0").value;

            var rsoCheck = document.getElementById("Use_RSO_0").checked;

            if(rsoCheck == true){

            }
            else{
                document.getElementById("Use_RSO_" + i).value = 0;
            }

            // document.getElementById("Use_RSO_" + i).value = document.getElementById("Use_RSO_0").value;


            var v1 = document.getElementById("fcst_type_rmcr_0").value;
            var v2 = document.getElementById("dmd_type_rmcn_0").value;
            var v3 = document.getElementById("dmd_type_rmcb_0").value;

            if (v1 == "CUSTOM" || v2 == "CUSTOM" || v3 == "CUSTOM") {
                document.getElementById("custom_fcst_type_" + i).value = document.getElementById("custom_fcst_type_0").value;
                document.getElementById("custom_fcst_by_" + i).value = document.getElementById("custom_fcst_by_0").value;
            }

            if(document.getElementById("unit" + i).value == "NONE"){
            document.getElementById("ruc" + i).disabled = false;
                document.getElementById("ruc" + i).value = 0; 
            }
            if(document.getElementById("PLTVal" + i).value == "NONE"){
            document.getElementById("plt" + i).disabled = false;
                document.getElementById("plt" + i).value = 0; 
            }
            if(document.getElementById("ALTVal" + i).value == "NONE"){
            document.getElementById("alt" + i).disabled = false;
                document.getElementById("alt" + i).value = 0; 
            }
            if(document.getElementById("covDurVal" + i).value == "NONE"){
            document.getElementById("covDur" + i).disabled = false;
                document.getElementById("covDur" + i).value = 0; 
            }

            // var ucnum = (+document.getElementById("unitcostescalation" + i).value) / 100;
            // document.getElementById("unitcostescalation" + i).value = ucnum.toString();


            if(document.getElementById("unit"+ i).value == "PERCENT"){
                var rucNumber = (+document.getElementById("ucv" + i).value) / 100;
                document.getElementById("ucv" + i).value = rucNumber.toString();
            }
            
            }
            document.getElementById("topheader").style.display = "none";
            document.getElementById("accord1").style.display = "none";
            document.getElementById("accord2").style.display = "none";
            document.getElementById('displayadmin').style.display = "none";
            document.getElementById('DisplayExecSig').style.display = "none";
            document.getElementById("progbarhelp").style.display = "flex";
        }
    function customCheck(that, scen) {
        
        var num = scen;
        var v1 = document.getElementById("fcst_type_rmcr_" + scen).value;
        var v2 = document.getElementById("dmd_type_rmcn_" + scen).value;
        var v3 = document.getElementById("dmd_type_rmcb_" + scen).value;

        if (v1 == "CUSTOM" || v2 == "CUSTOM" || v3 == "CUSTOM") {
            document.getElementById("customMonthlyExtraQuestions" + scen).style.display = "flex";
        }
        else {
            document.getElementById("customMonthlyExtraQuestions" + scen).style.display = "none";
        }
    }
    function updateCostEsc(that, scen) {
        var PEChoiceNo = document.getElementById("costEscOff" + scen).checked;
        var DollarYes = document.getElementById("costEscD" + scen).checked;

        if(PEChoiceNo == true){
            document.getElementById("costEscOff" + scen).value = 'off';
            document.getElementById('CostEscFormat'+ scen).style.display = "none";
            document.getElementById('CostEscDollar'+ scen).style.display = "none";
            document.getElementById('CostEscPercent'+ scen).style.display = "none";
            document.getElementById('PercentChoice'+ scen).style.display = "none";
            document.getElementById('StaticPercentEsc'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc1'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc2'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc3'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc4'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc5'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
            document.getElementById('CompPercChoice'+ scen).style.display = "none";
            document.getElementById('StaticCompEsc'+ scen).style.display = "none";
            document.getElementById('PriceEscYear1'+ scen).style.display = "none";
            document.getElementById('PriceEscYear2'+ scen).style.display = "none";
            document.getElementById('PriceEscYear3'+ scen).style.display = "none";
            document.getElementById('PriceEscYear4'+ scen).style.display = "none";
            document.getElementById('PriceEscYear5'+ scen).style.display = "none";
            document.getElementById('PriceEscYear6'+ scen).style.display = "none";
            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
        }
        else{
            document.getElementById("costEscOff" + scen).value = 'on';
            document.getElementById('CostEscFormat'+ scen).style.display = "none";
            document.getElementById('CostEscDollar'+ scen).style.display = "none";
            document.getElementById('CostEscPercent'+ scen).style.display = "none";
            document.getElementById('PercentChoice'+ scen).style.display = "none";
            document.getElementById('StaticPercentEsc'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc1'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc2'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc3'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc4'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc5'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
            document.getElementById('CompPercChoice'+ scen).style.display = "none";
            document.getElementById('StaticCompEsc'+ scen).style.display = "none";
            document.getElementById('PriceEscYear1'+ scen).style.display = "none";
            document.getElementById('PriceEscYear2'+ scen).style.display = "none";
            document.getElementById('PriceEscYear3'+ scen).style.display = "none";
            document.getElementById('PriceEscYear4'+ scen).style.display = "none";
            document.getElementById('PriceEscYear5'+ scen).style.display = "none";
            document.getElementById('PriceEscYear6'+ scen).style.display = "none";
            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
            document.getElementById('PriceEscYear10'+ scen).style.display = "none";

            if(DollarYes == true){
                document.getElementById('CostEscDollar'+ scen).style.display = "flex";
                document.getElementById('CostEscPercent'+ scen).style.display = "none";
            }
            else{
                document.getElementById('CostEscDollar'+ scen).style.display = "none";
                document.getElementById('CostEscPercent'+ scen).style.display = "flex";
                
                var PEscType = document.getElementById('mySelectEscType'+ scen).value;

                if(PEscType == "Fixed"){
                    document.getElementById('PercentChoice'+ scen).style.display = "flex";
                    document.getElementById('CompPercChoice'+ scen).style.display = "none";

                    //static or yearly
                    var SFESC = document.getElementById('mySelectFixEscType'+ scen).value;

                    if(SFESC == "Static"){
                        document.getElementById('StaticPercentEsc'+ scen).style.display = "flex";
                        document.getElementById('CustPercentEsc1'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc2'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc3'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc4'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc5'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                        document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                    }
                    else{
                        //is yearly
                        var DUR = document.getElementById('duration').value;
                        document.getElementById('StaticPercentEsc'+ scen).style.display = "none";

                        if (DUR == '1') {
                                document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                                document.getElementById('CustPercentEsc2'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc3'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc4'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc5'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                                document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                            }

                        else if (DUR == '2') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '3') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '4') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '5') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '6') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '7') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '8') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "none";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '9') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "none";
                        }

                        else if (DUR == '10') {
                            document.getElementById('CustPercentEsc1'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc2'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc3'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc4'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc5'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc6'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc7'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc8'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc9'+ scen).style.display = "flex";
                            document.getElementById('CustPercentEsc10'+ scen).style.display = "flex";
                        }
                    }
                }
                else{
                    document.getElementById('CompPercChoice'+ scen).style.display = "flex";
                    // is compound
                    document.getElementById('PercentChoice'+ scen).style.display = "none";
                    var CStaticY = document.getElementById('mySelectCompEscType'+ scen).value;

                    if (CStaticY == "Static"){
                        document.getElementById('StaticCompEsc'+ scen).style.display = "flex";

                        document.getElementById('PriceEscYear1'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear2'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear3'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear4'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear5'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear6'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear7'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                        document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                    }
                    else if (CStaticY == "Yearly"){
                        //compound Yearly
                        var DUR = document.getElementById('duration').value;
                        document.getElementById('StaticCompEsc'+ scen).style.display = "none";

                        if (DUR == '1') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                            }

                        else if (DUR == '2') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '3') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '4') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '5') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '6') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '7') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '8') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "none";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '9') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "none";
                        }

                        else if (DUR == '10') {
                            document.getElementById('PriceEscYear1'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear2'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear3'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear4'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear5'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear6'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear7'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear8'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear9'+ scen).style.display = "flex";
                            document.getElementById('PriceEscYear10'+ scen).style.display = "flex";
                        }
                        
                    }
                }
                
            }
        }
    }
    function showSimCalcALT(that, scen) {
        
        var simCalc = document.getElementById('ALTVal' + scen).value;

        if (simCalc === 'SC_FSC_AVG') {
            document.getElementById('altOther' + scen).style.display= 'flex';
            document.getElementById('altDays' + scen).style.display= 'none';
            document.getElementById('alt' + scen).disabled= true;
            document.getElementById('altPer' + scen).style.display= 'none';	
            document.getElementById('altNONE' + scen).style.display= 'none';
        }
        else if (simCalc === 'PERCENT') {
            document.getElementById('altOther' + scen).style.display= 'none';
            document.getElementById('altDays' + scen).style.display= 'none';
            document.getElementById('alt' + scen).disabled= true;
            document.getElementById('altPer' + scen).style.display= 'flex';
            document.getElementById('altEnabled' + scen).disabled= false;
            document.getElementById('altNONE' + scen).style.display= 'none';
        }

        else if (simCalc === 'FIXED'){
            document.getElementById('altOther' + scen).style.display= 'none';
            document.getElementById('altDays' + scen).style.display= 'flex';
            document.getElementById('altPer' + scen).style.display= 'none';
            document.getElementById('alt' + scen).disabled= false;
            document.getElementById('altEnabled' + scen).disabled= true;
            document.getElementById('altNONE' + scen).style.display= 'none';
        }
        else{
            document.getElementById('altNONE' + scen).style.display= 'flex';
            document.getElementById('altOther' + scen).style.display= 'none';
            document.getElementById('altDays' + scen).style.display= 'none';
            document.getElementById('alt' + scen).disabled= true;
            document.getElementById('altPer' + scen).style.display= 'none';	
        }

        setAttributeMinMax('ALTVal' + scen, 'alt' + scen);
    }

    function showSimCalcPLT(that, scen) {
        
        var simCalcplt = document.getElementById('PLTVal' + scen).value;

        if (simCalcplt === 'SC_FSC_AVG') {
            document.getElementById('pltOther' + scen).style.display= 'flex';
            document.getElementById('pltOtherFSC' + scen).style.display= 'none';
            document.getElementById('pltDays' + scen).style.display= 'none';
            document.getElementById('plt' + scen).disabled= true;
            document.getElementById('pltPer' + scen).style.display= 'none';
            document.getElementById('pltNONE' + scen).style.display= 'none';
        }
        else if (simCalcplt === 'PERCENT') {
            document.getElementById('pltOther' + scen).style.display= 'none';
            document.getElementById('pltOtherFSC' + scen).style.display= 'none';
            document.getElementById('pltDays' + scen).style.display= 'none';
            document.getElementById('plt' + scen).disabled= true;
            document.getElementById('pltPer' + scen).style.display= 'flex';
            document.getElementById('pltEnabled' + scen).disabled= false;
            document.getElementById('pltNONE' + scen).style.display= 'none';
        }

        else if (simCalcplt === 'FIXED'){
            document.getElementById('pltOther' + scen).style.display= 'none';
            document.getElementById('pltOtherFSC' + scen).style.display= 'none';
            document.getElementById('pltDays' + scen).style.display= 'flex';
            document.getElementById('pltPer' + scen).style.display= 'none';
            document.getElementById('plt' + scen).disabled= false;
            document.getElementById('pltEnabled' + scen).disabled= true;
            document.getElementById('pltNONE' + scen).style.display= 'none';
        }
        else if (simCalcplt === 'FSC_AVG'){
            document.getElementById('pltOther' + scen).style.display= 'none';
            document.getElementById('pltOtherFSC' + scen).style.display= 'flex';
            document.getElementById('pltDays' + scen).style.display= 'none';
            document.getElementById('pltPer' + scen).style.display= 'none';
            document.getElementById('plt' + scen).disabled= false;
            document.getElementById('pltEnabled' + scen).disabled= true;
            document.getElementById('pltNONE' + scen).style.display= 'none';
        }
        else {
            document.getElementById('pltOther' + scen).style.display= 'none';
            document.getElementById('pltOtherFSC' + scen).style.display= 'none';
            document.getElementById('pltDays' + scen).style.display= 'none';
            document.getElementById('plt' + scen).disabled= true;
            document.getElementById('pltPer' + scen).style.display= 'none';
            document.getElementById('pltNONE' + scen).style.display= 'none';
        }
        setAttributeMinMax('PLTVal' + scen, 'plt' + scen);
    }
    function setAttributeMinMax(dropDownSelect, valueInput) {
        
        var dropDownValue = document.getElementById(dropDownSelect).value;

        if (dropDownValue == "PERCENT") {
            document.getElementById(valueInput).setAttribute("min", "1");
            document.getElementById(valueInput).setAttribute("max", "100");
        }

        // else if (dropDownValue == "FIXED") {
        //     document.getElementById(valueInput).setAttribute("min", "1");
        //     document.getElementById(valueInput).setAttribute("max", "1826");
        // }

        else {
            document.getElementById(valueInput).setAttribute("min", "0");
            document.getElementById(valueInput).setAttribute("max", "1826");
        }
    }
    function showSimCalcCov(that, scen) {
        
        var simCalc = document.getElementById('covDurVal' + scen).value;

        if (simCalc === 'EOQ') {
            document.getElementById('covDurOther' + scen).style.display= 'flex';
            document.getElementById('covDursc' + scen).style.display= 'none';
            document.getElementById("covDurOther" + scen).placeholder = "EOQ Calc Value";
            document.getElementById('covDurDays' + scen).style.display= 'none';
            document.getElementById('covDurDays' + scen).disabled= 'true';	
            document.getElementById('covPer' + scen).style.display= 'none';
            document.getElementById('covPer' + scen).disabled= 'true';	
            document.getElementById('covDurNONE' + scen).style.display= 'none';
            document.getElementById('covDurDisabled' + scen).value= 'EOQ Calc Value';
            document.getElementById('covDurDisabled' + scen).disabled= 'true';
        }
        else if (simCalc === 'SC_LTC') {
            document.getElementById('covDurOther' + scen).style.display= 'none';
            document.getElementById('covDursc' + scen).style.display= 'flex';
            document.getElementById('covDurDays' + scen).style.display= 'none';
            document.getElementById('covDurDays' + scen).disabled= 'true';
            document.getElementById('covPer' + scen).style.display= 'none';
            document.getElementById('covPer' + scen).disabled= 'true';	
            document.getElementById('covDurNONE' + scen).style.display= 'none';
        }
        else if (simCalc === 'PERCENT'){
            document.getElementById('covDurOther' + scen).style.display= 'none';
            document.getElementById('covDursc' + scen).style.display= 'none';
            document.getElementById('covDurOther' + scen).disabled= 'true';
            document.getElementById('covPer' + scen).style.display= 'flex';
            document.getElementById('covEnabled' + scen).disabled= false;
            document.getElementById('covDurDays' + scen).style.display= 'none';
            document.getElementById('covDur' + scen).disabled= true;
            document.getElementById('covDurNONE' + scen).style.display= 'none';
        }
        else if (simCalc === 'FIXED'){
            document.getElementById('covDurOther' + scen).style.display= 'none';
            document.getElementById('covDurOther' + scen).disabled= 'true';
            document.getElementById('covDursc' + scen).style.display= 'none';
            document.getElementById('covDurDays' + scen).style.display= 'flex';
            document.getElementById('covPer' + scen).style.display= 'none';
            document.getElementById('covPer' + scen).disabled= 'true';	
            document.getElementById('covDurNONE' + scen).style.display= 'none';
            document.getElementById('covDur' + scen).disabled= false;
            document.getElementById('covEnabled' + scen).disabled= true;
        }
        else{
            document.getElementById('covDurOther' + scen).style.display= 'none';
            document.getElementById('covDurOther' + scen).disabled= 'true';
            document.getElementById('covDursc' + scen).style.display= 'none';
            document.getElementById('covDurDays' + scen).style.display= 'none';
            document.getElementById('covDurDays' + scen).disabled= 'true';
            document.getElementById('covDurNONE' + scen).style.display= 'flex';
            document.getElementById('covPer' + scen).style.display= 'none';
            document.getElementById('covPer' + scen).disabled= 'true';
        }
        setAttributeMinMax('covDurVal' + scen, 'covDur' + scen);
    }
    
    function updateSFpop(that, scen, popTypeVal) {
        console.log("updateSFpop function called for scenario:", scen); // Debugging
    
        // Get the selected channel value
        var chanElement = document.getElementById("channel" + scen);
        if (!chanElement) {
            console.error("chan element not found for scenario:", scen);
            return;
        }
    
        var chan = chanElement.value.trim(); // Trimming to remove any extra spaces
        console.log("chan value (raw):", chan); // Log raw chan value
    
        // Debug if chan matches 'CDTODD'
        if (chan === 'CDTODD') {
            console.log("CDTODD condition met for scenario:", scen);
    
            // Additional logic
            var channelSFPop = document.getElementById("channel_SF_Pop" + scen);
            if (channelSFPop) {
                channelSFPop.value = '(RMC = B or SS_Calc = CPS)';
            } else {
                console.error("channel_SF_Pop element not found for scenario:", scen);
            }
    
            var pltVal = document.getElementById("PLTVal" + scen);
            if (pltVal) {
                pltVal.value = "FSC_AVG";
            }
    
            var plt = document.getElementById("plt" + scen);
            if (plt) {
                plt.value = "FSC Average";
            }
    
            var pltOther = document.getElementById('pltOther' + scen);
            if (pltOther) {
                pltOther.style.display = 'none';
            }
    
            var pltOtherFSC = document.getElementById('pltOtherFSC' + scen);
            if (pltOtherFSC) {
                pltOtherFSC.style.display = 'none';
            }
    
            var pltDays = document.getElementById('pltDays' + scen);
            if (pltDays) {
                pltDays.style.display = 'none';
            }

            var pltDisabled = document.getElementById('pltDisabled' + scen);
            if (pltDisabled) {
                pltDisabled.value = "FSC Avg Value";
            }

            var sfPop = document.getElementById('channel_SF_Pop' + scen);
            if (sfPop) {
                sfPop.value = "(RMC = B or (SS_Calc=CPS and Supply_Chain ne AVTN))";
            }
        } else {
            console.log("chan is not CDTODD, it's:", chan); // If the condition fails
        }
    
        // Handle CPS logic
        var cps = document.getElementById("cps" + scen)?.value;
        var cpsalt = document.getElementById("cpsAAAalt" + scen)?.value;
        if (cps === 'OFFCPS' || cpsalt === 'OFFCPS') {
            document.getElementById("cps_SF_Pop" + scen).value = 'All CPS items';
        } else {
            document.getElementById("cps_SF_Pop" + scen).value = 'N/A';
        }
    }    

    function yesnoCheck(that, scen) {
        
        var num = scen;
        if (that.value == "custom") {
            document.getElementById('pltOtherFSC' + scen).style.display= 'none';
            document.getElementById('pltDays' + scen).style.display= 'none';
            document.getElementById('pltNONE' + scen).style.display= 'flex';
            document.getElementById("covDur" + scen).value = "";
            document.getElementById("alt" + scen).value = "";
            document.getElementById("plt" + scen).value = "";
            document.getElementById("covDurVal" + scen).value = "FIXED";
            document.getElementById("ALTVal" + scen).value = "FIXED";
            document.getElementById("PLTVal" + scen).value = "FIXED";
            document.getElementById("channel" + scen).value = "CURRENT";
            updateSFpop(that, scen);
            /*make sure channel isnt greyd out*/
            document.getElementById("channel" + scen).readOnly = false;
            document.getElementById("channel_SF_Pop" + scen).readOnly = false;
            document.getElementById("channel" + scen).classList.remove("read_only_input");
            document.getElementById("channel_SF_Pop" + scen).classList.remove("read_only_input");
            document.getElementById('channel' + scen).className = ('fullWidth');
            document.getElementById('channel' + scen).classList.add('fullhover');
            document.getElementById('channel' + scen).classList.add('form-control');
            document.getElementById("lock" + scen).checked = true;
            document.getElementById("contract" + scen).value = "CURRENT";
            document.getElementById('covDur' + scen).style.display = 'flex';
            document.getElementById('alt' + scen).style.display = 'flex';
            document.getElementById('plt' + scen).style.display = 'flex';
            ltcchange(that, scen);
        }
        if (that.value == "on") {
            var cpsStatus = document.getElementById('cps' + scen);
            var stockForePop = document.getElementById('channel_SF_Pop' + scen);
            cpsStatus.value = "SC_RULES";
            stockForePop.value = "(RMC=B and On_LTC ne Y)";
            document.getElementById("covDurVal" + scen).value = "FIXED";
            document.getElementById("covDur" + scen).value = 90;
            document.getElementById("ALTVal" + scen).value = "FIXED";
            document.getElementById("alt" + scen).value = 15;
            document.getElementById("PLTVal" + scen).value = "FIXED";
            document.getElementById("plt" + scen).value = "";
            document.getElementById("channel" + scen).value = "CURRENT";
            showSimCalcCov(that, scen);
            showSimCalcALT(that, scen);
            showSimCalcPLT(that, scen);
            updateSFpop(that, scen);
            /*make sure channel isnt greyd out*/
            document.getElementById("channel" + scen).readOnly = false;
            document.getElementById("channel_SF_Pop" + scen).readOnly = false;
            document.getElementById("channel" + scen).classList.remove("read_only_input");
            document.getElementById("channel_SF_Pop" + scen).classList.remove("read_only_input");
            document.getElementById('channel' + scen).className = ('fullWidth');
            document.getElementById('channel' + scen).classList.add('fullhover');
            document.getElementById('channel' + scen).classList.add('form-control');
            document.getElementById("lock" + scen).checked = true;
            document.getElementById("contract" + scen).value = "LTC";
            var blankRevisedPltVal = document.getElementById("PLTVal" + scen);
            blankRevisedPltVal.value = 'NONE';
            var blankRevisedPlt = document.getElementById("plt" + scen);
            blankRevisedPlt.placeholder = ' ';
            ltcchange(that, scen);
        }
        else if (that.value == "off") {
            var cpsStatus = document.getElementById('cps' + scen);
            var stockForePop = document.getElementById('channel_SF_Pop' + scen);
            cpsStatus.value = "SC_RULES";
            stockForePop.value = "(RMC = B or (SS_Calc=CPS and Supply_Chain ne AVTN))";
            document.getElementById('pltDays' + scen).style.display= 'none';
            document.getElementById('pltNONE' + scen).style.display= 'none';
            document.getElementById("covDurVal" + scen).value = "EOQ";
            showSimCalcCov(that, scen);

            document.getElementById("ALTVal" + scen).value = "SC_FSC_AVG";
            document.getElementById("alt" + scen).value = "SC FSC Avg Value";
            showSimCalcALT(that, scen);

            document.getElementById("PLTVal" + scen).value = "FSC_AVG";
            document.getElementById("plt" + scen).value = "FSC Average";
            document.getElementById('pltOtherFSC' + scen).style.display= 'flex';
 
            document.getElementById("channel" + scen).value = "CURRENT";
            updateSFpop(that, scen);
            /*make sure channel isnt greyd out*/
            document.getElementById("channel" + scen).readOnly = false;
            document.getElementById("channel_SF_Pop" + scen).readOnly = false;
            document.getElementById("channel" + scen).classList.remove("read_only_input");
            document.getElementById("channel_SF_Pop" + scen).classList.remove("read_only_input");
            document.getElementById('channel' + scen).className = ('fullWidth');
            document.getElementById('channel' + scen).classList.add('fullhover');
            document.getElementById('channel' + scen).classList.add('form-control');
            document.getElementById("lock" + scen).checked = true;
            document.getElementById("contract" + scen).value = "TRANS";
            ltcchange(that, scen);
        }
        else if (that.value == "ddcd") {
            document.getElementById("covDurVal" + scen).value = "FIXED";
            // document.getElementById("covDur" + scen).value = "";
            document.getElementById("ALTVal" + scen).value = "FIXED";
            document.getElementById("alt" + scen).value = 1;
            document.getElementById("PLTVal" + scen).value = "FIXED";
            document.getElementById("plt" + scen).value = 2;
            document.getElementById("channel" + scen).value = "DDTOCD";
            document.getElementById('covDur' + scen).disabled = true;
            // showSimCalcCov(that, scen);
            showSimCalcALT(that, scen);
            showSimCalcPLT(that, scen);
            updateSFpop(that, scen);
            /*grey out channel*/
        
            document.getElementById("channel" + scen).readOnly = true;
            document.getElementById("channel_SF_Pop" + scen).readOnly = true;
            document.getElementById("channel" + scen).classList.add("read_only_input");
            document.getElementById("channel_SF_Pop" + scen).classList.add("read_only_input");
            document.getElementById("lock" + scen).checked = false;
            document.getElementById("contract" + scen).value = "LTC";
            document.getElementById('covDur' + scen).style.display = 'flex';
            document.getElementById('alt' + scen).style.display = 'flex';
            var blankcovDurVal = document.getElementById("covDurVal" + scen);
            blankcovDurVal.value = 'NONE';
            var blankRevisedCovDurVal = document.getElementById("covDur" + scen);
            blankRevisedCovDurVal.placeholder = ' ';
            document.getElementById("daysAppend").style.display = "none";
            ltcchange(that, scen);
        }
        else if (that.value == "cddd") {
            var cpsStatus = document.getElementById('cps' + scen);
            var stockForePop = document.getElementById('channel_SF_Pop' + scen);
            cpsStatus.value = "SC_RULES";
            stockForePop.value = "(RMC = B or (SS_Calc=CPS and Supply_Chain ne AVTN))";
            document.getElementById('pltDays' + scen).style.display= 'none';
            document.getElementById('pltNONE' + scen).style.display= 'none';
            document.getElementById("ALTVal" + scen).value = "FIXED";
            document.getElementById("alt" + scen).value = 120;
            document.getElementById("channel" + scen).value = "CDTODD";
            showSimCalcCov(that, scen);
            showSimCalcALT(that, scen);
            showSimCalcPLT(that, scen);
            updateSFpop(that, scen);
            /*grey out channel*/
            document.getElementById("channel" + scen).readOnly = true;
            document.getElementById("channel_SF_Pop" + scen).readOnly = true;
            document.getElementById("channel" + scen).classList.add("read_only_input");
            document.getElementById("channel_SF_Pop" + scen).classList.add("read_only_input");
            document.getElementById("lock" + scen).checked = true;
            document.getElementById("contract" + scen).value = "TRANS";
            document.getElementById('covDur' + scen).style.display = 'flex';
            document.getElementById('alt' + scen).style.display = 'flex';
            document.getElementById('plt' + scen).style.display = 'flex';
            document.getElementById('pltOtherFSC' + scen).style.display= 'flex';
            ltcchange(that, scen);
        }
    }
    
    var x = 1;
    function deleteScenario() {
        var scenarioLength = document.getElementsByClassName("section1").length;
        document.getElementsByClassName("section1")[scenarioLength - 1].outerHTML = '';
        scenarioLength--;

        document.getElementById('scencount').value = x - 2;
        x--;

        if (x > 1) {
            var scenx = x - 1;
            //var scenScroll = document.getElementById("scenario" + scenx).offsetTop - 150;
            //window.scroll(0, scenScroll);
        }
    }
    function costEscDefault() {
        document.getElementById('CostEscFormat'+x).style.display = "none";
        document.getElementById('CostEscDollar'+x).style.display = "none";
        document.getElementById('CostEscPercent'+x).style.display = "none";
        document.getElementById('PercentChoice'+x).style.display = "none";
        document.getElementById('StaticPercentEsc'+x).style.display = "none";
        document.getElementById('CustPercentEsc1'+x).style.display = "none";
        document.getElementById('CustPercentEsc2'+x).style.display = "none";
        document.getElementById('CustPercentEsc3'+x).style.display = "none";
        document.getElementById('CustPercentEsc4'+x).style.display = "none";
        document.getElementById('CustPercentEsc5'+x).style.display = "none";
        document.getElementById('CustPercentEsc6'+x).style.display = "none";
        document.getElementById('CustPercentEsc7'+x).style.display = "none";
        document.getElementById('CustPercentEsc8'+x).style.display = "none";
        document.getElementById('CustPercentEsc9'+x).style.display = "none";
        document.getElementById('CustPercentEsc10'+x).style.display = "none";
        document.getElementById('CompPercChoice'+x).style.display = "none";
        document.getElementById('StaticCompEsc'+x).style.display = "none";
        document.getElementById('PriceEscYear1'+x).style.display = "none";
        document.getElementById('PriceEscYear2'+x).style.display = "none";
        document.getElementById('PriceEscYear3'+x).style.display = "none";
        document.getElementById('PriceEscYear4'+x).style.display = "none";
        document.getElementById('PriceEscYear5'+x).style.display = "none";
        document.getElementById('PriceEscYear6'+x).style.display = "none";
        document.getElementById('PriceEscYear7'+x).style.display = "none";
        document.getElementById('PriceEscYear8'+x).style.display = "none";
        document.getElementById('PriceEscYear9'+x).style.display = "none";
        document.getElementById('PriceEscYear10'+x).style.display = "none";
    }
    function makeNextScen() {

        var strVar = "";

        strVar += "         <div class=\"container-fluid\">";
        strVar += "         <div class=\"accordion\">";
        strVar += "             <div class=\"section1\" id=\"scenario" + x + "\">";
        strVar += "               	<div class=\"card\">";
        strVar += "                 <div class=\"card-header astyle\" id=\"scenlooker" + x + "\">";
        strVar += "                         <button class=\"btn btn-link\" type=\"button\" data-toggle=\"collapse\" data-target=\"#collapse" + x + "\" aria-expanded=\"true\" aria-controls=\"collapse" + x + "\" onclick=\"showCard(\'collapse" + x + "\')\">";
        strVar += "                     <i class=\"fa fa-angle-down fa-lg\" style=\"font-weight:bolder\"></i>";
        strVar += "                     Scenario " + x + " Setup<\/button>";
        strVar += "                 <\/div>";
        strVar += "                 <div id=\"collapse" + x + "\" class=\"collapse show\" aria-labelledby=\"baselineoptions\">";
        strVar += "                     <div class=\"card-body\">";
        strVar += "                         <div class=\"row subheader\">"
        strVar += "                             <div class=\"col-sm-auto\">"
        strVar += "                                 Scenario Type";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row\">";
        strVar += "                             <label class=\"col-sm-5\">Enter a short name for your scenario. <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Provide an alphanumeric name for your scenario. (6 characters max).\"> <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"/></svg> </span><\/label>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                                 <input class=\"form-control\" id=\"scen_" + x + "\" type=\"text\" name=\"scen_name_" + x + "\" value=\"scen" + x + "\" maxlength=\"6\" onchange=\"alphaNumCheckAS(this.value,this.id)\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <label class=\"col-sm-5\" >Choose desired alternate scenario type.<\/label>";
        strVar += "                             <div class=\"col-sm-7 form-group\">";
        strVar += "                                 <select class=\"form-control\" id=\"ScenSelect" + x + "\" name=\"simType_" + x + "\" onchange=\"yesnoCheck(this, " + x + ");\">";
        strVar += "                                     <option value=\"custom\" selected>Custom<\/option>";
        strVar += "                                     <option value=\"on\">On LTC<\/option>";
        strVar += "                                     <option value=\"off\">Off LTC<\/option>";
        strVar += "                                     <option value=\"ddcd\">DD to CD LTC<\/option>";
        strVar += "                                     <option value=\"cddd\">CD to DD Transactional<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                        <\/div>";
        strVar += "                        <div class=\"genUnique\">"
        strVar += "                        <hr>";
        strVar += "                             <div class=\"row subheader\">"
        strVar += "                                 <div class=\"col-sm-auto\">"
        strVar += "                                     Demand &amp; Forecast Simulation Methods";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"row instructions\">";
        strVar += "                                 <span class=\"col-sm-auto\">Please select a forecast/demand method for each item type:<\/span>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"row\">";
        strVar += "                                 <label for=\"ScenSelect\" class=\"col-sm-5 col-form-label normalLabel\">Forecast Based Replenishment<\/label>";
        strVar += "                                 <div class=\"col-sm-7 form-group\">";
        strVar += "                                     <select class=\"form-control\" name=\"RMCR_FCST_DMD_TYPE_" + x + "\" id=\"fcst_type_rmcr_" + x + "\" onchange=\"customCheck(this, " + x + ");\">";
        strVar += "                                         <option value=\"ICR\">Item Consumption Rate (ICR)<\/option>";
        strVar += "                                         <option value=\"CONSUMPHIST\">Consumption History \/ 12<\/option>";
        strVar += "                                         <option value=\"ADQ\">ADQ \/ 12<\/option>";
        strVar += "                                         <option selected value=\"DFUAVG\">DFUtoSKU 12 Month Flatline Average<\/option>";
        // strVar += "                                         <option value=\"DFULOOP\">DFUtoSKU 12 Month Loop<\/option>";
        strVar += "                                         <option value=\"CUSTOM\">Custom Monthly Forecast<\/option>";
        strVar += "                                     <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"row\">";
        strVar += "                                 <label for=\"ScenSelect\" class=\"col-sm-5 normalLabel\">Minimum\/Maximum Replenishment<\/label>";
        strVar += "                                 <div class=\"col-sm-7 form-group\">";
        strVar += "                                     <select class=\"form-control\" name=\"RMCN_FCST_DMD_TYPE_" + x + "\" id=\"dmd_type_rmcn_" + x + "\" onchange=\"customCheck(this, " + x + ");\">";
        strVar += "                                         <option value=\"ICR\">Item Consumption Rate (ICR)<\/option>";
        strVar += "                                         <option value=\"CONSUMPHIST\">Consumption History \/ 12<\/option>";
        strVar += "                                         <option value=\"ADQ\">ADQ \/ 12<\/option>";
        strVar += "                                         <option selected value=\"TRAIL24\">Trailing 24 Month Demand Loop<\/option>";
        strVar += "                                         <option value=\"CUSTOM\">Custom Monthly Forecast<\/option>";
        strVar += "                                     <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        // Commented out until we determine if we're going to include in UP and build out in BE if so
        // strVar += "                         <div>";
        // strVar += "                             <div class=\"row\">";
        // strVar += "                                 <div class=\"col-sm-5\">";
        // strVar += "                                     <label class=\"normalLabel\" for=\"gdp" + x + "\">Include Navy Gross Demand Plan Input<\/label><\/div>";
        // strVar += "                                 <div class=\"col-sm-7\">";
        // strVar += "                                  <div class=\"form-check\">";
        // strVar += "                                     <input class=\"form-check-input\" name=\"Use_GDP_" + x + "\" value=\"1\" type=\"checkbox\" checked id=\"gdpholder" + x + "\">";
        // strVar += "                                 <\/div>";
        // strVar += "                             <\/div>";
        // strVar += "                             <\/div>";
        // strVar += "                         <\/div>";
        strVar += "                             <div class=\"row\">";
        strVar += "                                 <div class=\"col-sm-5\">";
        strVar += "                                     <label class=\"normalLabel\">Customer Direct Replenishment<\/label>";
        strVar += "                                 </div>";
        strVar += "                                 <div class=\"col-sm-7 form-group\">";
        strVar += "                                     <select class=\"form-control\" name=\"RMCB_FCST_DMD_TYPE_" + x + "\" id=\"dmd_type_rmcb_" + x + "\" onchange=\"customCheck(this, " + x + ");\">";
        strVar += "                                         <option selected value=\"ICR\">Item Consumption Rate (ICR)<\/option>";
        strVar += "                                         <option value=\"ADQ\">ADQ \/ 12<\/option>";
        strVar += "                                         <option value=\"CONSUMPHIST\">Consumption History \/ 12<\/option>";
        strVar += "                                         <option value=\"CUSTOM\">Custom Monthly Forecast<\/option>";
        strVar += "                                     <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <div>";
        strVar += "                             <div class=\"row\">";
        strVar += "                                 <div class=\"col-sm-10\">";
        strVar += "                                     <label class=\"normalLabel\" for=\"Use_RSO_" + x + "\">Ensure RMC B NIINs do not attrit below their Retail Protected Levels?<\/label><\/div>";
        strVar += "                                 <div class=\"col-sm-2\">";
        strVar += "                                  <div class=\"form-check\">";
        strVar += "                                     <input class=\"form-check-input\" id=\"Use_RSO_" + x + "\" name=\"Use_RSO_" + x + "\" value=\"1\" type=\"checkbox\" checked>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <div id=\"customMonthlyExtraQuestions" + x + "\" style=\"display:none;\" class=\"\">";
        strVar += "                             <div class=\"row\">";
        strVar += "                                 <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                     <label class=\"normalLabel\">Type of Custom Values Provided<\/label>";
        strVar += "                                 <\/div>";
        strVar += "                                 <div class=\"col-sm-4 form-group\">";
        strVar += "                                     <select class=\"form-control\" id=\"custom_fcst_type_" + x + "\" name=\"custom_fcst_type_" + x + "\" class=\"\">";
        strVar += "                                         <option value=\"FIXED\">Absolute Monthly Demand<\/option>";
        strVar += "                                         <option value=\"PERCENT\">Pct Change in Monthly Demand<\/option>";
        strVar += "                                     <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                                 <div class=\"col-sm-3 form-group\">";
        strVar += "                                     <select class=\"form-control\" id=\"custom_fcst_by_" + x + "\" class=\"mL\" name=\"custom_fcst_by_" + x + "\" class=\"\">";
        strVar += "                                         <option value=\"MONTH\">By Month<\/option>";
        strVar += "                                         <option value=\"YEAR\">By Year<\/option>";
        strVar += "                                     <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                        <hr>";
        strVar += "                         <div class=\"row subheader\">"
        strVar += "                             <div class=\"col-sm-auto\">"
        strVar += "                                 <span>Item Attributes<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row instructions\">";
        strVar += "                             <div class=\"col-sm-auto instructions\">";
        strVar += "                                 <span class=\"labelSmall\">Please specify the population-wide item attribute(s) you would like to change.<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row columnTitles\">";
        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                                 <label class=\"label1\">Change Type<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                                 <label class=\"label2\">Attribute<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                                 <label class=\"label3\">Value<\/label>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Coverage Duration<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <select class=\"form-control covdurhover\" id=\"covDurVal" + x + "\"  onchange=\"showSimCalcCov(this,  " + x + ")\" name=\"Revised_CovDur_Type_" + x + "\">";
        strVar += "                                     <option selected value=\"NONE\"><\/option>";
        strVar += "                                     <option value=\"FIXED\">Fixed Value<\/option>";
        strVar += "                                     <option value=\"SC_LTC\">Supply Chain LTC Calc Method<\/option>";
        strVar += "                                     <option value=\"EOQ\">EOQ Calc Method<\/option>";
        strVar += "                                     <option value=\"PERCENT\">Fixed Percent<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                                 <\/span>";
        strVar += "                             <\/div>";

        strVar += "                             <div class=\"col-sm-4\">";	
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"covDurDays" + x + "\">";	
        strVar += "                                 	<input class=\"form-control\" id=\"covDur" + x + "\" type=\"number\" min=\"0\" max=\"1826\" name=\"Revised_CovDur_Val_" + x + "\" placeholder=\"Enter Days...\" onblur=\"validateInput(this)\">";
        strVar += "						<div class=\"input-group-append\" id=\"daysAppend\">";
        strVar += "							<span class=\"input-group-text daysAppend\">days<\/span>";
        strVar += "						<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"covDurOther" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"covDurDisabled" + x + "\" type=\"text\" name=\"Revised_CovDur_Val_" + x + "\" placeholder=\"EOQ Calc Value\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"covDursc" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"covDurDisabled" + x + "\" type=\"text\" name=\"Revised_CovDur_Val_" + x + "\" placeholder=\"SC LTC Calc Value\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                             	<div class=\"input-group\" id=\"covDurNONE" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"covDurDisabled" + x + "\" type=\"text\" name=\"Revised_CovDur_Val_" + x + "\" placeholder=\"\" disabled>";    
        strVar += "					<\/div>";
        // strVar += "                              <\/div>";
        // strVar += "                         <\/div>";
        // strVar += "                             <div class=\"col-sm-4\">";	
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"covPer" + x + "\">";	
        strVar += "                                 	<input class=\"form-control\" id=\"covEnabled" + x + "\" type=\"number\" min=\"0\" max=\"100\" name=\"Revised_CovDur_Val_" + x + "\" placeholder=\"Enter Percent...\" disabled onblur=\"validateInput(this)\">";
        strVar += "						<div class=\"input-group-append\">";
        strVar += "							<span class=\"input-group-text\">%<\/span>";
        strVar += "						<\/div>";
        strVar += "						<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Administrative Lead Time<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <select class=\"form-control althover\" id=\"ALTVal" + x + "\" onchange=\"showSimCalcALT(this,  " + x + ")\" name=\"revised_ALT_Type_" + x + "\">";
        strVar += "                                     <option value=\"NONE\" selected><\/option>";
        strVar += "                                     <option value=\"PERCENT\">Percent Increase<\/option>";
        strVar += "                                     <option value=\"FIXED\">Fixed Value<\/option>";
        strVar += "                                     <option value=\"SC_FSC_AVG\">Supply Chain FSC Average<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"altDays" + x + "\">";	
        strVar += "                                 	<input class=\"form-control\" id=\"alt" + x + "\" type=\"number\" min=\"0\" max=\"1826\" name=\"revised_alt_val_" + x + "\" placeholder=\"Enter Days...\" onblur=\"validateInput(this)\">";
        strVar += "						<div class=\"input-group-append\">";
        strVar += "							<span class=\"input-group-text daysAppend\">days<\/span>";
        strVar += "						<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"altPer" + x + "\">";	
        strVar += "                                 	<input class=\"form-control\" id=\"altEnabled" + x + "\" type=\"number\" min=\"0\" max=\"100\" name=\"revised_alt_val_" + x + "\" placeholder=\"Enter Percent...\" disabled onblur=\"validateInput(this)\">";
        strVar += "						<div class=\"input-group-append\">";
        strVar += "							<span class=\"input-group-text\">%<\/span>";
        strVar += "						<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                             	<div class=\"input-group\" id=\"altNONE" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"altDisabled" + x + "\" type=\"text\" name=\"revised_alt_val_" + x + "\" placeholder=\"0\" value=\"0\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"altOther" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"altDisabled" + x + "\"  type=\"text\" name=\"revised_alt_val_" + x + "\" placeholder=\"SC FSC Avg Value\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                              <\/div>";
        strVar += "                         <\/div>";

        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Production Lead Time<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group plthover\">";
        strVar += "                                 <select class=\"form-control\" id=\"PLTVal" + x + "\" onchange=\"showSimCalcPLT(this,  " + x + ")\" name=\"revised_PLT_Type_" + x + "\">";
        strVar += "                                     <option value=\"NONE\" selected><\/option>";
        strVar += "                                     <option value=\"PERCENT\">Percent Increase<\/option>";
        strVar += "                                     <option value=\"FIXED\">Fixed Value<\/option>";
        strVar += "                                     <option value=\"SC_FSC_AVG\">Supply Chain FSC Average<\/option>";
        strVar += "                                     <option value=\"FSC_AVG\">FSC Average<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";

        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"pltDays" + x + "\">";	
        strVar += "                                 	<input class=\"form-control\" id=\"plt" + x + "\" type=\"number\" min=\"0\" max=\"1826\" name=\"REVISED_PLT_VAL_" + x + "\" placeholder=\"Enter Days...\" onblur=\"validateInput(this)\">";
        strVar += "						<div class=\"input-group-append\">";
        strVar += "							<span class=\"input-group-text daysAppend\">days<\/span>";
        strVar += "						<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"pltPer" + x + "\">";	
        strVar += "                                 	<input class=\"form-control\" id=\"pltEnabled" + x + "\" type=\"number\" min=\"0\" max=\"100\" name=\"REVISED_PLT_VAL_" + x + "\" placeholder=\"Enter Percent...\" disabled onblur=\"validateInput(this)\">";
        strVar += "						<div class=\"input-group-append\">";
        strVar += "							<span class=\"input-group-text\">%<\/span>";
        strVar += "						<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                             	<div class=\"input-group\" id=\"pltNONE" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"pltDisabled" + x + "\" type=\"text\" name=\"REVISED_PLT_VAL_" + x + "\" placeholder=\"0\" value=\"0\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"pltOther" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"pltDisabled" + x + "\"  type=\"text\" name=\"REVISED_PLT_VAL_" + x + "\" placeholder=\"SC FSC Avg Value\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"pltOtherFSC" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"pltDisabled" + x + "\"  type=\"text\" name=\"REVISED_PLT_VAL_" + x + "\" placeholder=\"FSC Avg Value\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                              <\/div>";
        strVar += "                         <\/div>";


        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Safety Stock Level <span data-toggle=\"tooltip\" data-placement=\"right\"</span><\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <input disabled class=\"form-control\" id=\"ssType" + x + "\" name=\"Revised_MinSS_Type_" + x + "\" value=\"Percent Increase\">";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                             	<div class=\"input-group\">";
        strVar += "                                 <input class=\"form-control\"  id=\"ssVal" + x + "\" type=\"number\" max=\"100.00\" min=\"0\" name=\"REVISED_MINSS_VAL_" + x + "\" value=\"0\" placeholder=\"Enter Percent...\" onblur=\"validateInput(this)\">";
        strVar += "					<div class=\"input-group-append\">";
        strVar += "						<span class=\"input-group-text\">%<\/span>";
        strVar += "					<\/div>";
        strVar += "                                <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Maximum OH Level <span data-toggle=\"tooltip\" data-placement=\"right\"</span><\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <input disabled class=\"form-control\" id=\"maxType" + x + "\" name=\"Revised_MaxOH_Type_" + x + "\" value=\"Percent Increase\">";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                             	<div class=\"input-group\">";
        strVar += "                                 <input class=\"form-control\" id=\"max" + x + "\" type=\"number\" max=\"100.00\" min=\"0\" name=\"REVISED_MAXOH_VAL_" + x + "\" value=\"0\" placeholder=\"Enter Percent...\" onblur=\"validateInput(this)\">";
        strVar += "					<div class=\"input-group-append\">";
        strVar += "						<span class=\"input-group-text\">%<\/span>";
        strVar += "					<\/div>";
        strVar += "                                 <\/div>";
        strVar += "                              <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Revised Unit Cost <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"The value entered will be interpreted as a percent or fixed value increase/decrease based on the attribute selection. The value is applied to each item's unit cost and rounded to one decimal place.\"> <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"/></svg> </span><\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group uchover\">";
        strVar += "                                 <select class=\"form-control ruchover\" id=\"unit" + x + "\" onchange=\"showSimCalcRUC(this,  " + x + ")\" name=\"Revised_Cost_Type_" + x + "\">";
        strVar += "                                     <option value=\"NONE\" selected><\/option>";
        strVar += "                                     <option value=\"PERCENT\">Percent Increase<\/option>";
        strVar += "                                     <option value=\"FIXED\">Fixed Value<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4\">";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"rucPer" + x + "\">";
        strVar += "                                 <input class=\"form-control\" id=\"ucv" + x + "\" type=\"number\" max=\"100.00\" min=\"0\" step=\"0.001\" name=\"REVISED_COST_VAL_" + x + "\" placeholder=\"Enter Percent...\" disabled onblur=\"validateInput(this)\">";
        strVar += "					<div class=\"input-group-append\">";
        strVar += "						<span class=\"input-group-text\">%<\/span>";
        strVar += "					<\/div>";
        strVar += "                                 <\/div>";
        strVar += "                             	<div class=\"input-group hideMetric\" id=\"rucDays" + x + "\">";	
        strVar += "                                 	<input class=\"form-control\" id=\"ruc" + x + "\" type=\"number\" min=\"0\" max=\"999999999\" name=\"REVISED_COST_VAL_" + x + "\" placeholder=\"Enter Amount...\" onblur=\"validateInput(this)\">";
        strVar += "						<div class=\"input-group-append\">";
        strVar += "							<span class=\"input-group-text\">$<\/span>";
        strVar += "						<\/div>";
        strVar += "                             	<\/div>";
        strVar += "                             	<div class=\"input-group\" id=\"rucNONE" + x + "\">";
        strVar += "						<input class=\"form-control\" id=\"rucDisabled" + x + "\" type=\"text\" name=\"REVISED_COST_VAL_" + x + "\" placeholder=\"0\" value=\"0\" disabled>";    
        strVar += "					<\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        // strVar += "                                 <label class=\"normalLabel\" data-toggle=\"tooltip\" data-placement=\"left\" title=\"The value entered will be interpreted as a percentage, rounded to the nearest whole number.\">Unit Cost Escalation<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        // strVar += "                                 <input disabled class=\"form-control\" id=\"unEsc" + x + "\" name=\"Cost_Escalation_Type_" + x + "\" value=\"COMPOUNDANNUAL\">";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4\">"
        strVar += "                             	<div class=\"input-group\">";
        // strVar += "                                 <input class=\"form-control\" value=\"0\" id=\"unitcostescalation" + x + "\" type=\"number\" min=\"0\" max=\"100\" step=\"0.001\" name=\"Cost_Escalation_Val_" + x + "\">";
        // strVar += "					<div class=\"input-group-append\">";
        // strVar += "						<span class=\"input-group-text\">%<\/span>";
        // strVar += "					<\/div>";
        strVar += "                                 <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">CPS Status<span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Current Setting: Uses current CPS Status. Off CPS: Update all items to be off CPS. Supply Chain Rules: Update CPS status based on rules set by supply chain.\"> <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"/></svg> </span><\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <select class=\"form-control\" name=\"revised_cps_" + x + "\" id=\"cps" + x + "\" onchange=\"updateSFpop(this, " + x + ");\">";
        strVar += "                                     <option selected value=\"CURRENT\">Current Setting<\/option>";
        strVar += "                                     <option value=\"OFFCPS\">Off CPS<\/option>";
        strVar += "                                     <option value=\"SC_RULES\">Supply Chain Rules<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Fulfillment Channel<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <select class=\"form-control fullhover\" id=\"channel" + x + "\" name=\"revised_channel_" + x + "\" onchange=\"updateSFpop(this, " + x + ");\">";
        strVar += "                                     <option selected value=\"CURRENT\">Current Setting<\/option>";
        strVar += "                                     <option value=\"DDTOCD\">DD to CD<\/option>";
        strVar += "                                     <option value=\"CDTODD\">CD to DD<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-4 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Stockability/Forecastability Population<span data-toggle=\"tooltip\" data-placement=\"right\" title=\"This option is used to specify the items that should be evaluated with Stockability and Forecastability tests to determine replenishment method under scenario settings (fulfillment channel).\"> <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"/></svg> </span><\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <select class=\"form-control\" id=\"channel_SF_Pop" + x + "\" name=\"SF_Pop_" + x + "\">";
        strVar += "                                     <option value=\"\">N/A<\/option>";
        strVar += "                                     <option value=\"(RMC = B or (SS_Calc=CPS and Supply_Chain ne AVTN))\">All RMC B items<\/option>";
        strVar += "                                     <option value=\"(RMC=B and On_LTC ne Y)\">Off LTC, RMC B items<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <br><div class=\"row\">";
        strVar += "                             <div class=\"col-sm-10\"><label for=\"lock" + x + "\">Use system MinSS &amp; MaxOH Values for Peak Policy and NextGen items.<span data-toggle=\"tooltip\" data-placement=\"right\" title=\"When selected, Safety Stock and MaxOH will not be recalculated for Peak/NextGen items, regardless of LTC or channel selections.\"> <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"/></svg> </span></label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-2 form-check pphover\">";
        strVar += "                                     <input class=\"form-check-input zero\" type=\"checkbox\" id=\"lock" + x + "\" value=\"1\" name=\"IGN_MXOH_SS_PRC_CHNG_4_PK_NG_" + x + "\" checked>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-10\"><label for=\"itemlevel" + x + "\">Make NIIN-Level Item Attribute changes in addition to the above.<span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Select this option to make attribute changes at the item-level. Once initialized, the simulation will pause and you will be prompted to complete an Excel spreadsheet with item-level updates. See the Standard BCA Line Item Changes User Guide in Help Documentation.\"> <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"/></svg> </span><\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-2 form-check itemhover\">";
        strVar += "                                     <input class=\"form-check-input zero\" type=\"checkbox\" id=\"itemlevel" + x + "\" value=\"0\" name=\"Line_Item_" + x + "\" onchange=\"itemAttributes(this, " + x + ");\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row itemAttributes\" id=\"itemAttributes" + x + "\">";
        // strVar += "                             <div class=\"col-sm-8 itemAttrIndent\"><label for=\"itemAttributes" + x + "\"  class=\"normalLabel\"data-toggle=\"tooltip\" title=\"Select how much time you will need to implement and upload line item changes.\">How long would you like the sim to pause for?</label><\/div>";
        // strVar += "                             <div class=\"col-sm-4\">";
        // strVar += "                         <div class=\"input-group\" id=\"licdur" + x + "\">";	
        // strVar += "                                 <input class=\"form-control\" value=\"10\" id=\"licdurshow" + x + "\" type=\"number\" min=\"1\" max=\"30\" name=\"Line_Item" + x + "\" placeholder=\"Enter Minutes...\">";
        // strVar += "						        <div class=\"input-group-append\">";
        // strVar += "							        <span class=\"input-group-text minAppend\">min<\/span>";
        // strVar += "						            <\/div>";
        // strVar += "                            <\/div>";    
        // strVar += "                                 <\/div>";    
        strVar += "                             <div class=\"col-sm-8 itemAttrIndent\" style=\"padding-left:33px;\"><label for=\"itemAttributes" + x + "\">Input unique Item Attribute values for each year?</label><\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group phasehover\" style=\"padding-left:15px;\">";
        strVar += "                                 <div class=\"form-check form-check-inline\">";
        strVar += "                                     <input class=\"form-check-input\" type=\"radio\" id=\"itemPropYes" + x + "\" name=\"Yearly_Line_Item_" + x + "\" value=\"1\" onchange=\"changeLIValue(this, " + x + ");\">";
        strVar += "                                     <label class=\"form-check-label\">Yes<\/label>"; 
        strVar += "                                 <\/div>";
        strVar += "                                 <div class=\"form-check form-check-inline\">";
        strVar += "                                     <input class=\"form-check-input\" type=\"radio\" id=\"itemPropNo" + x + "\" name=\"Yearly_Line_Item_" + x + "\" value=\"0\" onchange=\"changeLIValue(this, " + x + ");\" checked>";
        strVar += "                                     <label class=\"form-check-label\">No<\/label>"; 
        strVar += "                                 <\/div>";           
        strVar += "                             <\/div>";
        strVar += "                         <\/div>"; 
        // strVar += "                             <div class=\"col-sm-8 itemAttrIndent\"><label for=\"itemAttributes" + x + "\"  id=\"licdurcap" + x + "\" class=\"normalLabel\"data-toggle=\"tooltip\" title=\"Select how much time you will need to implement and upload line item changes.\">How long would you like the sim to pause for?</label><\/div>";
        // strVar += "                             <div class=\"col-sm-4\">";
        // strVar += "                         <div class=\"input-group\" id=\"licdur" + x + "\">";	
        // strVar += "                                 <input class=\"form-control\" value=\"10\" id=\"licdurshow" + x + "\" type=\"number\" min=\"1\" max=\"30\" name=\"simpausetime" + x + "\" placeholder=\"Enter Minutes...\">";
        // strVar += "						        <div class=\"input-group-append\">";
        // strVar += "							        <span class=\"input-group-text minAppend\">min<\/span>";
        // strVar += "						            <\/div>";
        // strVar += "                            <\/div>";    
        // strVar += "                                 <\/div>";     
        // strVar += "                         <\/div>";                                     
        strVar += "                         <hr>";
        strVar += "                         <div class=\"row subheader\">"
        strVar += "                             <div class=\"col-sm-auto\">"
        strVar += "                                 <span>Contract Status<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row instructions\">";
        strVar += "                             <div class=\"col-sm-auto instructions\">";
        strVar += "                                 <span class=\"labelSmall\">Please specify the desired settings for the contract status of each scenario.<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row contractStatus\">";
        strVar += "                             <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">LTC Status<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-7 form-group\">";
        strVar += "                                 <select class=\"form-control contracthover\" name=\"revised_contract_" + x + "\" onchange = \"ltcchange(this, " + x + ");\" class=\"contractClass\" id=\"contract" + x + "\">";
        strVar += "                                     <option selected value=\"CURRENT\">Current Setting<\/option>";
        strVar += "                                     <option value=\"LTC\">On LTC<\/option>";
        strVar += "                                     <option value=\"TRANS\">Off LTC<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
              //Lot Payment Start
        strVar += "                         <div class=\"row\" id=\"cocApp" + x + "\" style=\"margin-bottom: 15px; display:none;\">";
        strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        strVar += "                                 Material Cost Funding Type";
        strVar += "                                 <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Non-Lot Payment: Funds obligated at procurement award. Lot Payment: Funds obligated at beginning of each Period of Performance.\">";
        strVar += "                                     <svg xmlns=\"http:\/\/www.w3.org\/2000\/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https:\/\/fontawesome.com License - https:\/\/fontawesome.com\/license\/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"\/><\/svg>";
        strVar += "                                 <\/span>";
        strVar += "                             <\/label>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                                 <div class=\"form-check form-check-inline\">";
        strVar += "                                     <input class=\"form-check-input\" type=\"radio\" name=\"costofcapitalinput_" + x + "\" id=\"lotOff" + x + "\" onchange=\"enableCoc(this, " + x + ")\" value=\"nonlotpmt\" checked>";
        strVar += "                                     <label class=\"form-check-label\">Non-Lot Payment<\/label>";
        strVar += "                                 <\/div>";
        strVar += "                                 <div class=\"form-check form-check-inline\">";
        strVar += "                                     <input class=\"form-check-input\" type=\"radio\" name=\"costofcapitalinput_" + x + "\" id=\"lotOn" + x + "\" onchange=\"enableCoc(this, " + x + ")\" value=\"lotpmt\">";
        strVar += "                                     <label class=\"form-check-label\">Lot Payment<\/label>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\" id=\"lotInput" + x + "\" style=\"margin-bottom: 15px;\">";
        strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        strVar += "                                 Method";
        strVar += "                                 <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Simulated Spend: Contract value based on total PR value for the population. Actual Contract Spend: User input total contract value. Lot Payment Excel Input: Upload lot payment schedule.\">";
        strVar += "                                     <svg xmlns=\"http:\/\/www.w3.org\/2000\/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https:\/\/fontawesome.com License - https:\/\/fontawesome.com\/license\/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"\/><\/svg>";
        strVar += "                                 <\/span>";
        strVar += "                             <\/label>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                                 <div class=\"input-group\">";
        strVar += "                                     <select class=\"form-control\" name=\"lotpaymenttype_" + x + "\" id=\"lotInputSelect" + x + "\" onchange=\"lotPayInput(this, " + x + ")\">";
        strVar += "                                         <option value=\"simspend\" selected>Simulated Spend<\/option>";
        strVar += "                                         <option value=\"actctrspend\">Estimated Contract Spend<\/option>";
        strVar += "                                         <option value=\"excel\">Custom Input<\/option>";
        strVar += "                                     <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";

        strVar += "                         <div class=\"row\" id=\"totalConSpend" + x + "\" style=\"margin-bottom: 15px;\">";
        strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        strVar += "                                 Total Contract Spend";
        strVar += "                             <\/label>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                                 <div class=\"input-group\">";
        strVar += "                                     <div class=\"input-group-prepend\">";
        strVar += "                                         <span class=\"input-group-text minAppend\" data-placement=\"right\">$<\/span>";
        strVar += "                                     <\/div>";
        strVar += "                                     <input class=\"form-control auto-default-min\" type=\"number\" value=\"0\" min=\"0\" max=\"999999999999\" id=\"totalcontractspend" + x + "\" name=\"totalcontractspend_" + x + "\" onblur=\"validateInput(this)\">";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";

        strVar += "                         <div class=\"row\" id=\"nonFeePerc" + x + "\" style=\"margin-bottom: 15px;\">";
        strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        strVar += "                                 Non-Material Fee Percent";
        strVar += "                                 <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Specify the expected percentage of non-material fees in the contract.\">";
        strVar += "                                     <svg xmlns=\"http:\/\/www.w3.org\/2000\/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https:\/\/fontawesome.com License - https:\/\/fontawesome.com\/license\/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"\/><\/svg>";
        strVar += "                                 <\/span>";
        strVar += "                             <\/label>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                                 <div class=\"input-group\">";
        strVar += "                                     <input class=\"form-control\" type=\"number\" value=\"0\" step=\".1\" min=\"0\" max=\"100\" id=\"nonmaterialfeepct" + x + "\" name=\"nonmaterialfeepct_" + x + "\" onblur=\"validateInput(this)\">";
        strVar += "                                     <div class=\"input-group-append\">";
        strVar += "                                         <span class=\"input-group-text minAppend\">%<\/span>";
        strVar += "                                     <\/div>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";

        strVar += "                         <div class=\"row\" id=\"payFreq" + x + "\" style=\"margin-bottom: 15px;\">";
        strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        strVar += "                                 Payment Frequency";
        strVar += "                                 <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Select the frequency of lot payments for the contract. \">";
        strVar += "                                     <svg xmlns=\"http:\/\/www.w3.org\/2000\/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https:\/\/fontawesome.com License - https:\/\/fontawesome.com\/license\/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"\/><\/svg>";
        strVar += "                                 <\/span>";
        strVar += "                             <\/label>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                                 <div class=\"input-group\">";
        strVar += "                                     <select class=\"form-control\" name=\"paymentfreq_" + x + "\">";
        strVar += "                                         <option value=\"monthly\" selected>Monthly<\/option>";
        strVar += "                                         <option value=\"quarterly\">Rolling Quarterly<\/option>";
        strVar += "                                         <option value=\"annually\">Rolling Annually<\/option>";
        strVar += "                                     <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";

        // strVar += "                         <div class=\"row\" id=\"totalConSpend" + x + "\" style=\"margin-bottom: 15px;\">";
        // strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        // strVar += "                                 Total Contract Spend";
        // strVar += "                             <\/label>";
        // strVar += "                             <div class=\"col-sm-7\">";
        // strVar += "                                 <div class=\"input-group\">";
        // strVar += "                                     <span class=\"input-group-text minAppend\" data-placement=\"right\">$<\/span>";
        // strVar += "                                     <input class=\"form-control\" type=\"number\" onblur=\"checkTotalContractSpend(this, " + x + ")\"  id=\"totalcontractspend" + x + "\" name=\"totalcontractspend_" + x + "\">";
        // strVar += "                                 <\/div>";
        // strVar += "                             <\/div>";
        // strVar += "                         <\/div>";
        // strVar += "                         <div class=\"row\" id=\"nonFeePerc" + x + "\" style=\"margin-bottom: 15px;\">";
        // strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        // strVar += "                                 Non-Material Fee Percent";
        // strVar += "                                 <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"Specify the expected percentage of non-material fees in the contract.\">";
        // strVar += "                                     <svg xmlns=\"http:\/\/www.w3.org\/2000\/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https:\/\/fontawesome.com License - https:\/\/fontawesome.com\/license\/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"\/><\/svg>";
        // strVar += "                                 <\/span>";
        // strVar += "                             <\/label>";
        // strVar += "                             <div class=\"col-sm-7\">";
        // strVar += "                                 <div class=\"input-group\">";
        // strVar += "                                     <input class=\"form-control\" type=\"number\" value=\"0\" max=\"100\" onblur=\"checkFeePercent(this, " + x + ")\"  id=\"nonmaterialfeepct" + x + "\" name=\"nonmaterialfeepct_" + x + "\">";
        // strVar += "                                     <div class=\"input-group-append\">";
        // strVar += "                                         <span class=\"input-group-text minAppend\">%<\/span>";
        // strVar += "                                     <\/div>";
        // strVar += "                                 <\/div>";
        // strVar += "                             <\/div>";
        // strVar += "                         <\/div>";
        // strVar += "                         <div class=\"row\" id=\"payFreq" + x + "\" style=\"margin-bottom: 15px;\">";
        // strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        // strVar += "                                 Payment Frequency";
        // strVar += "                                 <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"TOOLTIP INPUT REQUIRED\">";
        // strVar += "                                     <svg xmlns=\"http:\/\/www.w3.org\/2000\/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https:\/\/fontawesome.com License - https:\/\/fontawesome.com\/license\/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"\/><\/svg>";
        // strVar += "                                 <\/span>";
        // strVar += "                             <\/label>";
        // strVar += "                             <div class=\"col-sm-7\">";
        // strVar += "                                 <div class=\"input-group\">";
        // strVar += "                                     <select class=\"form-control\" name=\"paymentfreq_" + x + "\">";
        // strVar += "                                         <option value=\"monthly\" selected>Monthly<\/option>";
        // strVar += "                                         <option value=\"quarterly\">Rolling Quarterly<\/option>";
        // strVar += "                                         <option value=\"annually\">Rolling Annually<\/option>";
        // strVar += "                                     <\/select>";
        // strVar += "                                 <\/div>";
        // strVar += "                             <\/div>";
        // strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\" id=\"lotExcel" + x + "\">";
        strVar += "                             <label class=\"col-form-label col-sm-5 pt-0\">";
        strVar += "                                 Excel Input Location";
        // strVar += "                                 <span data-toggle=\"tooltip\" data-placement=\"right\" title=\"TOOLTIP INPUT REQUIRED\">";
        // strVar += "                                     <svg xmlns=\"http:\/\/www.w3.org\/2000\/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https:\/\/fontawesome.com License - https:\/\/fontawesome.com\/license\/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"\/><\/svg>";
        // strVar += "                                 <\/span>";
        strVar += "                             <\/label>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                             <body style=\"display: flex; justify-content: center; align-items: center; min-height: 100vh;\">";
        strVar += "                                 <section class=\"loading\" style=\"max-width: 100%; line-height: 1.4; font-size: 1rem; font-weight: bold; text-align: left;\">";
        strVar += "                                     <span class=\"loading__author\" style=\"font-weight:normal; font-size: .9rem; color: rgba(0,0,0,5); margin: 0.6rem 0 2rem 0; display: block;\">";
        strVar += "                                         Please enter the complete path to your Excel file <strong>(the path should end in '.xlsx').</strong> <br> The Excel must have a sheet named <strong>'Lot_Payment'</strong> and two columns named <strong>'Date' and 'Obligated_Action'.</strong><br> <strong>'Date'</strong> should contain a list of schedule lot payment dates and <strong>'Obligated Action'</strong> the corresponding payment value.";
        strVar += "                                     <\/span>";
        strVar += "                                     <span class=\"loading__anim\"><\/span>";
        strVar += "                                 <\/section>";
        strVar += "                             <\/body>";
        strVar += "                                 <div class=\"input-group\">";
        strVar += "                                     <input class=\"form-control\" type=\"text\" value=\"/home/users/&sysuserid/sasviyadata/&msc/users/&sysuserid/My_Simulations/sBCA/inputs/NIIN_Population.xlsx\" name=\"lotpaymentfilepath_" + x + "\">";
        strVar += "                                 <\/div>";
        // strVar += "                             <body style=\"display: flex; justify-content: center; align-items: center; min-height: 100vh;\">";
        // strVar += "                                 <section class=\"loading\" style=\"max-width: 100%; line-height: 1.4; font-size: 1rem; font-weight: bold; text-align: left;\">";
        // strVar += "                                     <span class=\"loading__author\" style=\"font-weight:normal; font-size: .9rem; color: rgba(0,0,0,5); margin: 0.6rem 0 2rem 0; display: block;\">";
        // strVar += "                                         Lorem <strong>ipsum</strong> dolor sit amet, consectetur adipiscing elit. In pellentesque finibus tincidunt. Ut vehicula sem ultrices bibendum consectetur. Integer diam dolor, tincidunt eget molestie ut, aliquet vel neque. Phasellus ultrices erat mauris, nec euismod sem maximus sit amet. Phasellus sit amet semper velit. Donec ut erat eu libero vulputate dapibus. Donec rhoncus porta leo, eget vehicula neque mollis sed. Aenean quis lacinia urna, a tristique sapien.";
        // strVar += "                                     <\/span>";
        // strVar += "                                     <span class=\"loading__anim\"><\/span>";
        // strVar += "                                 <\/section>";
        // strVar += "                             <\/body>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        //Lot Payment End
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-5\" hidden><label for=\"phasedDays" + x + "\"  class=\"normalLabel\">Phased Delivery</label><\/div>";
        strVar += "                             <div class=\"col-sm-7 form-group phasehover\" hidden>";
        strVar += "                                 <div class=\"form-check form-check-inline\">";
        strVar += "                                     <input class=\"form-check-input\" type=\"radio\" id=\"phasedDaysYes" + x + "\" name=\"phased_delivery_" + x + "\" value=\"1\" onchange=\"showDaysBetween(this, " + x + ");\">";
        strVar += "                                     <label class=\"form-check-label\">Yes<\/label>"; 
        strVar += "                                 <\/div>";
        strVar += "                                 <div class=\"form-check form-check-inline\">";
        strVar += "                                     <input class=\"form-check-input\" type=\"radio\" id=\"phasedDaysNo" + x + "\" name=\"phased_delivery_" + x + "\" value=\"0\" onchange=\"showDaysBetween(this, " + x + ");\" checked>";
        strVar += "                                     <label class=\"form-check-label\">No<\/label>"; 
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\" id=\"daysBetween" + x + "\" style=\"display:none;\">";
        strVar += "                             <div class=\"col-sm-5 col-form-label\"><label class=\"normalLabel\" class=\"\">How many days between deliveries?<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-7\">";
        strVar += "                             <div class=\"input-group\">";
        strVar += "                                 <input class=\"form-control\" type=\"text\" id=\"inlineCheckbox" + x + "\" name=\"PHASED_DELIVERY_DAYS_" + x + "\" value=\"0\" placeholder=\"Enter Days...\"><\/td>";
        strVar += "                                 <div class=\"input-group-append\">";
        strVar += "                                     <span class=\"input-group-text\">days<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <\/div>";
        // strVar += "                         <hr>";
        strVar += "                         <div class=\"row subheader\" hidden>"
        strVar += "                             <div class=\"col-sm-auto\">"
        strVar += "                                 <span>CPS Behavior<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row instructions\" hidden>";
        strVar += "                             <div class=\"col-sm-auto instructions\">";
        strVar += "                                 <span class=\"labelSmall\">Please specify the desired settings for the CPS settings of each scenario.<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";

        strVar += "                         <div class=\"row\" hidden>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                  <label data-toggle=\"tooltip\" data-placement=\"left\">";
        strVar += "                                     CPS Buffer Penetration Threshold</label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-7 uctper\">";
        strVar += "                                 <div class=\"input-group\">";
        strVar += "                                     <input class=\"form-control\" value=100";
        strVar += "                                         type=\"number\" id=\"pen_CPS_buffer_" + x + "\" value=\"\" step=\"5\"";
        strVar += "                                         min=\"50\" max=\"100\" name=\"penetrate_CPS_buffer_" + x + "\"";
        strVar += "                                         placeholder=\"\" maxlength=\"3\" minlength=\"1\">";
        strVar += "                                     <div class=\"input-group-append\">";
        strVar += "                                         <span class=\"input-group-text\">\%</span>";
        strVar += "                                     <\/div>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        // strVar += "                         <br>";

        strVar += "                         <div class=\"row\" hidden>";
        strVar += "                             <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                 <label class=\"normalLabel\">Stockability/Forecastability Population<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-7 form-group\">";
        strVar += "                                 <select class=\"form-control disabled\" id=\"cps_SF_Pop" + x + "\" name=\"revised_cps_SF_Pop_" + x + "\" class=\"newWidth\" disabled >";
        strVar += "                                     <option value=\"N/A\">N/A<\/option>";
        strVar += "                                     <option value=\"All CPS items\">All CPS items<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";

        // strVar += "                         <hr>";
        // strVar += "                         <div id=\"forecast" + x + "\" class=\"forecast\">";
        strVar += "                         <hr>";
        strVar += "                         <div class=\"row subheader\"id=\"costEscOnOffHeader" + x + "\">"
        strVar += "                             <div class=\"col-sm-auto\">"
        strVar += "                                 <span>Price Escalation<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                            <div class=\"row\" id=\"costEscOnOffC" + x + "\">";
        strVar += "                              <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Apply Scenario Price Escalations<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7\">";
        strVar += "                                    <div class=\"form-check form-check-inline\">";
        strVar += "                                        <input class=\"form-check-input\" type=\"radio\" id=\"costEscOn" + x + "\" name=\"costEscOnOff_" + x + "\" value=\"on\" onchange=\"updateCostEsc(this, " + x + ");\">";
        strVar += "                                         <label class=\"form-check-label\">";
        strVar += "                                            Yes";
        strVar += "                                            <\/label>";
        strVar += "                                        <\/div>";
        strVar += "                                        <div class=\"form-check form-check-inline\">";
        strVar += "                                            <input class=\"form-check-input\" type=\"radio\" id=\"costEscOff" + x + "\" name=\"costEscOnOff_" + x + "\" value=\"off\" onchange=\"updateCostEsc(this, " + x + ");\" checked>";
        strVar += "                                            <label class=\"form-check-label\">";
        strVar += "                                                No";
        strVar += "                                            <\/label>";
        strVar += "                                        <\/div>";
        strVar += "                                   <\/div>";
        strVar += "                                <\/div>";

                                    // <!-- User Chooses Escalation Format -->
        strVar += "                                <div class=\"row\" id=\"CostEscFormat" + x + "\">";
        strVar += "                                    <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                        <label>Escalation Value<\/label>";
        strVar += "                                    <\/div>";
        strVar += "                                    <div class=\"col-sm-7\">";
        strVar += "                                        <div class=\"form-check form-check-inline\">";
        strVar += "                                            <input class=\"form-check-input\" type=\"radio\" id=\"costEscD" + x + "\" value=\"DOLLAR\" onchange=\"updateCostEsc(this, " + x + ");\">";
        strVar += "                                        <label class=\"form-check-label\">";
        strVar += "                                            Dollar";
        strVar += "                                        <\/label>";
        strVar += "                                    <\/div>";
        strVar += "                                    <div class=\"form-check form-check-inline\">";
        strVar += "                                        <input class=\"form-check-input\" type=\"radio\" id=\"costEscP" + x + "\" value=\"PERCENT\" onchange=\"updateCostEsc(this, " + x + ");\">";
        strVar += "                                        <label class=\"form-check-label\">";
        strVar += "                                            Percent";
        strVar += "                                        <\/label>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                             <\/div>";

                                    // <!-- If User Chooses Dollar Value, prompts user to enter a dollar escalation value -->
        strVar += "                            <div class=\"row\" id=\"CostEscDollar"+ x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Enter Amount<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7\">";
        strVar += "                                     <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control\" id=\"ruc1\" type=\"number\" min=\"0\" max=\"999999999\" name=\"dollar_esc_amount_"+ x + "\" value=\"0\" placeholder=\"0\">";
        strVar += "                                         <div class=\"input-group-append\">";
        strVar += "                                             <span class=\"input-group-text\">$<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <\/div>";
                                    
                                    
                                    //<!-- If User Chooses Percent Value, prompts user to choose fixed or compound-->
        strVar += "                            <div class=\"row\" id=\"CostEscPercent" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Escalation Method<\/label>";
        strVar += "                                <\/div>";
                                        
        // strVar += "                                <div class=\"col-sm-5\">";
        // strVar += "                                        <div class=\"input-group hideMetric\" id=\"mySelectEscType" + x + "\" name=\"cost_escalation_type_"+ x + "\" onchange=\"updateCostEsc(this, " + x + ");\"  disabled>";
        // // strVar += "                                            <option value=\"Fixed\" >Fixed<\/option>";
        // strVar += "                                            <input class=\"form-control\" type=\"text\" placeholder=\"COMPOUNDANNUAL\"><\/div>";

        // strVar += "                                <\/div>";
        strVar += "                             <div class=\"col-sm-4 form-group\">";
        strVar += "                                 <input disabled class=\"form-control\" id=\"mySelectEscType" + x + "\" name=\"comp_Type_" + x + "\" value=\"COMPOUNDANNUAL\">";
        strVar += "                             <\/div>";
        strVar += "                            <\/div>";
                                // <!-- If User Chooses Fixed Percent Value, prompts user to choose between Static or Custom Fixed Escalation -->
        strVar += "                            <div class=\"row\" id=\"PercentChoice" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                     <label>Select Type<\/label>";
        strVar += "                                   <\/div>";
        strVar += "                                <div class=\"col-sm-7 col-form-label\">";
        strVar += "                                    <select class=\"form-control\" id=\"mySelectFixEscType" + x + "\" name=\"fixed_esc_type_"+ x + "\" onchange=\"updateCostEsc(this, " + x + ");\">";
        strVar += "                                        <option value=\"Static\" selected >Fixed<\/option>";
        strVar += "                                         <option value=\"Yearly\">Yearly<\/option>";
        strVar += "                                      <\/select>";
        strVar += "                                 <\/div>";
        strVar += "                             <\/div>";
                                //  <!-- If User Chooses Static Fixed Percent Value -->
        strVar += "                            <div class=\"row\" id=\"StaticPercentEsc" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                      <label>Enter Percent<\/label>";
        strVar += "                                  <\/div>";
        strVar += "                                <div class=\"col-sm-7\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control\" id=\"ruc2\" type=\"number\" min=\"0\" max=\"100\" step=\"Any\" value=\"0\" placeholder=\"0.0\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
            strVar += "                                        <\/div>";
            strVar += "                                    <\/div>";
            strVar += "                            <\/div>";
            strVar += "                           <\/div>";
                                // <!-- If User Chooses Custom Fixed Percent Value -->
        strVar += "                           <div class=\"row\" id=\"CustPercentEsc1" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 1<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                     <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" id=\"PriceEscYear1Val\" name=\"CustPercentEsc1_" + x + "\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                             <\/div>";
        strVar += "                            <div class=\"row\" id=\"CustPercentEsc2" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 2<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc2_" + x + "\" id=\"PriceEscYear2Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                     <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <\/div>";
        strVar += "                            <div class=\"row\" id=\"CustPercentEsc3" + x + "\">";
        strVar += "                                 <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 3<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                         <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc3_" + x + "\" id=\"PriceEscYear3Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <\/div>";
        strVar += "                            <div class=\"row\" id=\"CustPercentEsc4" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 4<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc4_" + x + "\" id=\"PriceEscYear4Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                 <\/div>";
        strVar += "                            <\/div>";
        strVar += "                            <div class=\"row\" id=\"CustPercentEsc5" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 5<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc5_" + x + "\" id=\"PriceEscYear5Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                         <\/div>";
        strVar += "                                     <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <\/div><div class=\"row\" id=\"CustPercentEsc6" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                     <label>Price Escalation Year 6<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                     <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc6_" + x + "\" id=\"PriceEscYear6Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <\/div><div class=\"row\" id=\"CustPercentEsc7" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 7<\/label>";
        strVar += "                                 <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc7_" + x + "\" id=\"PriceEscYear7Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                         <\/div>";
        strVar += "                                   <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <\/div><div class=\"rowd\" id=\"CustPercentEsc8" + x + "\">";
        strVar += "                                 <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 8<\/label>";
        strVar += "                                  <\/div>";
        strVar += "                                 <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc8_" + x + "\" id=\"PriceEscYear8Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
            strVar += "                                        <\/div>";
            strVar += "                                <\/div>";
            strVar += "                            <\/div>";
            strVar += "                        <\/div>";
            strVar += "                        <div class=\"row\" id=\"CustPercentEsc9" + x + "\">";
        strVar += "                             <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 9<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc9_" + x + "\" id=\"PriceEscYear9Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                               <\/div>";
        strVar += "                            <\/div>";
        strVar += "                            <div class=\"row\" id=\"CustPercentEsc10" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 10<\/label>";
        strVar += "                               <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"CustPercentEsc10_" + x + "\" id=\"PriceEscYear10Val\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                             <\/div>";
                                    

                                    //<!-- If User Chooses Compound Percent Escalation, prompts user to choose between Compound Annual Static or Annual Compound Escalation -->
        strVar += "                            <div class=\"row\" id=\"CompPercChoice" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                 <label>Select Type<span data-toggle=\"tooltip\" data-placement=\"right\" title=\"FIXED: Cost escalation is applied annually at a fixed rate. YEARLY: Cost escalation is applied annually based on user specified value(s) for each year.\"> <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"12\" height=\"12\" viewBox=\"0 0 512 512\"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill=\"#bababa\" d=\"M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z\"/></svg> </span><\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 col-form-label\">";
        strVar += "                                    <select class=\"form-control\" id=\"mySelectCompEscType" + x + "\" name=\"compound_esc_type_" + x + "\" onchange=\"updateCostEsc(this, " + x + ");\">";
        // strVar += "                                         <option value=\"option0\" selected>Take Out<\/option>";
        strVar += "                                        <option value=\"Static\">Fixed<\/option>";
        strVar += "                                        <option value=\"Yearly\">Yearly<\/option>";
        strVar += "                                    <\/select>";
        strVar += "                                <\/div>";
        strVar += "                             <\/div>";
        //                            <!-- If User chooses Static Compound Escalation -->
        strVar += "                            <div class=\"row\" id=\"StaticCompEsc" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Enter Percent<\/label>";
        strVar += "                                 <\/div>";
        strVar += "                                 <div class=\"col-sm-7\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control\" id=\"ruc3\" type=\"number\" min=\"-100\" max=\"100\" step=\"Any\" name=\"cost_escalation_val_" + x + "\" value=\"0\" onblur=\"validateInput(this)\">";
        strVar += "                                        <div class=\"input-group-append\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <\/div>";
                            
        strVar += "                            <div class=\"row\" id=\"PriceEscYear1" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 1<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\" style=\"background-color: #f2f2f2;\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" max=\"100.00\" min=\"0\" step=\"Any\" name=\"PriceEscalationYr1_" + x + "\" id=\"PriceEscYear1Val\" disabled>";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear2" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 2<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr2_" + x + "\" id=\"PriceEscYear2Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear3" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 3<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr3_" + x + "\" id=\"PriceEscYear3Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear4" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 4<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr4_" + x + "\" id=\"PriceEscYear4Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear5" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 5<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr5_" + x + "\" id=\"PriceEscYear5Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear6" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 6<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr6_" + x + "\" id=\"PriceEscYear6Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear7" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 7<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr7_" + x + "\" id=\"PriceEscYear7Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear8" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 8<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr8_" + x + "\" id=\"PriceEscYear8Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear9" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 9<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr9_" + x + "\" id=\"PriceEscYear9Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        strVar += "                            <div class=\"row\" id=\"PriceEscYear10" + x + "\">";
        strVar += "                                <div class=\"col-sm-5 col-form-label\">";
        strVar += "                                    <label>Price Escalation Year 10<\/label>";
        strVar += "                                <\/div>";
        strVar += "                                <div class=\"col-sm-7 uctper\">";
        strVar += "                                    <div class=\"input-group\">";
        strVar += "                                        <input class=\"form-control yoytext\" type=\"number\" value=\"0.0\" min=\"-100.00\" max=\"100.00\" step=\"Any\" name=\"PriceEscalationYr10_" + x + "\" id=\"PriceEscYear10Val\" onblur=\"validateInput(this)\">";
        strVar += "                                            <span class=\"input-group-text\">%<\/span>";
        strVar += "                                        <\/div>";
        strVar += "                                    <\/div>";
        strVar += "                                <\/div>";
        //Price Escalation End

        strVar += "                         <div class=\"row subheader\" hidden>"
        strVar += "                             <div class=\"col-sm-auto\">"
        strVar += "                                 <span>Forecast\/Demand Revisions<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row instructions\" hidden>";
        strVar += "                             <div class=\"col-sm-auto instructions\">";
        strVar += "                                 <span class=\"labelSmall\">Please specify any population level forecast and demand revisions.<\/span>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"row\">";
        strVar += "                             <div class=\"col-sm-5 col-form-label\" hidden>";
        strVar += "                                 <label class=\"forecastLabel\">Forecast Revision Type<\/label>";
        strVar += "                             <\/div>";
        strVar += "                             <div class=\"col-sm-7 form-group forehover\" hidden>";
        strVar += "                                 <select class=\"form-control\" onchange=\"toggleFOPT();\" id=\"forecastOpt" + x + "\" name=\"Com_Delta_" + x + "\" class=\"fixedSelect\">";
        strVar += "                                     <option value=\"Fixed Annual Revision\">Fixed Annual Revision<\/option>";
        strVar += "                                     <option value=\"cmpnd_annual_revision\">Compound Annual Revision<\/option>";
        strVar += "                                     <option selected value=\"None\">No Forecast/Demand Revisions<\/option>";
        strVar += "                                 <\/select>";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";

        strVar += "                         <div class=\"col-sm-auto row instructions\" hidden>";
        strVar += "                             <span id=\"forecastText" + x + "\">Enter Forecast Revision values in the fields below for each year's forecast\/demand.<\/span>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year1\" id=\"year1" + x + "\";>";
        strVar += "                             <label id=\"txt1" + x + "\" class=\"col-sm-7\">Forecast Revision Year 1&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" id=\"yr1" + x + "\" step=\"1\" type=\"number\" value=\"0\" name=\"FCST_YR1_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year2\" id=\"year2" + x + "\";>";
        strVar += "                             <label id=\"txt2" + x + "\" class=\"col-sm-7\">Forecast Revision Year 2&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr2" + x + "\" type=\"number\" value=\"0\" name=\"FCST_YR2_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year3\" id=\"year3" + x + "\";>";
        strVar += "                             <label id=\"txt3" + x + "\"  class=\"col-sm-7\">Forecast Revision Year 3&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr3" + x + "\" type=\"number\" value=\"0\" name=\"FCST_YR3_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year4\" id=\"year4" + x + "\";>";
        strVar += "                             <label id=\"txt4" + x + "\" class=\"col-sm-7\">Forecast Revision Year 4&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr4" + x + "\" type=\"number\" value=\"0\" name=\"FCST_YR4_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year5\" id=\"year5" + x + "\";>";
        strVar += "                             <label id=\"txt5" + x + "\" class=\"col-sm-7\">Forecast Revision Year 5&nbsp;<\/label>";
        strVar += "                             <div id=\"year5\"class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr5" + x + "\"  type=\"number\" value=\"0\" name=\"FCST_YR5_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year6\" id=\"year6" + x + "\" style=\"display:none;\">";
        strVar += "                             <label id=\"txt6" + x + "\" class=\"col-sm-7 \">Forecast Revision Year 6&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr6" + x + "\"  type=\"number\" value=\"0\" name=\"FCST_YR6_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year7\" id=\"year7" + x + "\" style=\"display:none;\">";
        strVar += "                             <label id=\"txt7" + x + "\" class=\"col-sm-7 \">Forecast Revision Year 7&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr7" + x + "\"  type=\"number\" value=\"0\" name=\"FCST_YR7_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year8\" id=\"year8" + x + "\" style=\"display:none;\">";
        strVar += "                             <label id=\"txt8" + x + "\" class=\"col-sm-7 \">Forecast Revision Year 8&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr8" + x + "\"  type=\"number\" value=\"0\" name=\"FCST_YR8_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year9\" id=\"year9" + x + "\" style=\"display:none;\">";
        strVar += "                             <label id=\"txt9" + x + "\" class=\"col-sm-7 \">Forecast Revision Year 9&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr9" + x + "\"  type=\"number\" value=\"0\" name=\"FCST_YR9_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                         <div class=\"form-group row year10\" id=\"year10" + x + "\" style=\"display:none;\">";
        strVar += "                             <label id=\"txt10" + x + "\" class=\"col-sm-7 \">Forecast Revision Year 10&nbsp;<\/label>";
        strVar += "                             <div class=\"col-sm-5\">";
        strVar += "                                 <input class=\"form-control\" step=\"1\" id=\"yr10" + x + "\"  type=\"number\" value=\"0\" name=\"FCST_YR10_REV_" + x + "\">";
        strVar += "                             <\/div>";
        strVar += "                         <\/div>";
        strVar += "                        <\/div>";
        strVar += "            			<\/div>";
        strVar += "            		<\/div>";
        strVar += "            <\/div>";
        strVar += " 		<\/div>";
        strVar += " 	<\/div>";


        var this_div = document.getElementById('added_scenarios');
        this_div.insertAdjacentHTML('beforeend', strVar);            

        //Enable tool tip hover: Uncomment once Bootstrap version 5 is updated
        // var tooltipElement = document.getElementById('tooltip');
        // var tooltip = new bootstrap.Tooltip(tooltipElement);

        }
    function addScenario() {
        
        makeNextScen();
        costEscDefault();
        lotDefaults();
        var bool = true;
        toggleFOPT()

        var uniq = document.getElementById('uniqId').checked;
        var fore = document.getElementsByClassName("genUnique");
        var endfore = document.getElementsByClassName("forecast");
        if ("&AdminUser." == "true") {
            for (var i = 0; i < endfore.length; i++) {
                endfore.item(i).style.display = "block";
            }
        }
        else{
            for (var i = 0; i < endfore.length; i++) {
                endfore.item(i).style.display = "none";
            }
        }

        if (uniq) {
            for (var i = 0; i < fore.length; i++) {
                fore.item(i).style.display = "block";
            }
        }
        else {
            for (var i = 0; i < fore.length; i++) {
                fore.item(i).style.display = "none";
            }
        }

        document.getElementById('scencount').value = x;
        x++;

        var scenx = x - 1;
        
        if ("&AdminUser." == "true") {
            var scenScroll = document.getElementById("scenario" + scenx).offsetTop + 1525;
        } else {
            var scenScroll = document.getElementById("scenario" + scenx).offsetTop + 1125;
        }
        window.scroll(0, scenScroll);
    }
    function customCheck(that, scen) {
    
        var num = scen;
        var v1 = document.getElementById("fcst_type_rmcr_" + scen).value;
        var v2 = document.getElementById("dmd_type_rmcn_" + scen).value;
        var v3 = document.getElementById("dmd_type_rmcb_" + scen).value;

        if (v1 == "CUSTOM" || v2 == "CUSTOM" || v3 == "CUSTOM") {
            document.getElementById("customMonthlyExtraQuestions" + scen).style.display = "flex";
        }
        else {
            document.getElementById("customMonthlyExtraQuestions" + scen).style.display = "none";
        }
    }

    function ltcchange(that, scen){

        var val = document.getElementById("contract" + scen).value;
        if (val == "LTC"){
            document.getElementById("lotOff" + scen).checked = true;
            document.getElementById("cocApp" + scen).style.display = 'flex';
        }
        else{
            document.getElementById("lotOff" + scen).checked = true;
            document.getElementById("cocApp" + scen).style.display = 'none';
            document.getElementById("lotInput" + scen).style.display = 'none';
            document.getElementById("totalConSpend" + scen).style.display = 'none';
            document.getElementById("nonFeePerc" + scen).style.display = 'none';
            document.getElementById("payFreq" + scen).style.display = 'none';
            document.getElementById("lotExcel" + scen).style.display = 'none';
        }
    }
    function itemAttributes(that, scen) { 
   
        var ItemAttr = document.getElementById('itemlevel'+ scen).checked;
        var radiobtn = document.getElementById('itemPropNo'+ scen);

        if (ItemAttr == true) {
            document.getElementById('itemAttributes'+ scen).style.display = "flex";
            document.getElementById('itemlevel'+ scen).value =1;
        }

        else {
            document.getElementById('itemAttributes'+ scen).style.display = "none"; 
            radiobtn.checked = true;
            document.getElementById('itemlevel'+ scen).value =0;
        }
    }   
    function changeLIValue(that, scen) {
    
        var IAChecked = document.getElementById('itemPropYes'+ scen).checked;

        if (IAChecked == true) {
            document.getElementById('itemPropYes'+ scen).value =1;
            
            
        }
        else {
            document.getElementById('itemPropYes'+ scen).value =0; 
            
            
        }
    }
    function cleanPopulationText() {

        var simNameCheck = document.getElementById('run_name').value;

        if (simNameCheck == "_" || simNameCheck == "" || simNameCheck == " ") {
            // alert("Your Simulation name can not be blank.");
            return false;
        }

        else {
            if("&LOGIN_TYPE" == "AAA"){
                var val = document.getElementById('popTypeVal2').value;
            }
            else{
                var val = document.getElementById('popTypeVal').value;
            }
            var str_end = 0;

            if ((val == 'CUSTOM') || (val == 'WSDC') || (val == 'CAGELIST')) {

                var len = document.getElementById('poptext').value;
                var source = document.getElementById('sourceSAS').value;

                if (len.length < 2 && source === "") {
                    if (val == 'CUSTOM') {
                        var Type = "NIINs";
                    }
                    if (val == 'WSDC') {
                        var Type = "WSDCs";
                    }
                    if (val == 'CAGELIST') {
                        var Type = "Cages";
                    }

                    // alert("Please provide a list of " + Type + " to continue.");
                    return false;
                }

                else {

                    var val1 = document.getElementById('poptext').value;
                    var val2 = val1.replace(/(?:\r\n|\r|\n)/g, ",") + ',';
                    var stop = Math.ceil(val2.length / 190);
                    var i;

                    for (i = 0; i < Math.ceil(val2.length / 190); i++) {

                        str_start = Math.max(str_end - 2, 0);
                        str_end = Math.min(str_end + 189, val2.length);

                        do {
                            currentval = val2.substring(str_start, str_end);
                            str_end++;

                        }

                        while (!(currentval = val2.substring(str_end - 2, str_end - 1) == ','));

                        var element1 = document.createElement("input");
                        element1.type = "hidden";
                        element1.value = val2.substring(str_start, str_end - 1);
                        element1.name = "Population_Text" + i + "_Text";

                        document.getElementById("myForm").appendChild(element1);

                    }
                }
            }
        }
        }
    //Modal Code Start-----------------------------------------------
	
            // Get the modal
            var modal = document.getElementById("FlexInputModal");

            // Get the button that opens the modal
            var btn = document.getElementById("FlexInputType");

            // Get the <span> element that closes the modal
            var span = document.getElementsByClassName("close")[0];

            // When the user clicks the button, open the modal 
            // btn.onclick = function () {
            //     modal.style.display = "block";
                
            //     if (document.getElementById("ltc_data_source").value == 'ALL_LTC_NIIN_XLSX') {
            //         document.getElementById("LTCOption").innerHTML = 'Your current LTC Data Source is: ALL_LTC_NIIN.xlsx';
            //     }
            //     if (document.getElementById("ltc_data_source").value == 'OA_HEADER_LINE_EXTRACT') {
            //         document.getElementById("LTCOption").innerHTML = 'Your current LTC Data Source is: OA Header/Line Extract';
            //     }          
            //     // document.getElementById("LTCOption").innerHTML = document.getElementById("ltc_data_source").value;
            // }

            // When the user clicks on <span> (x), close the modal
            // span.onclick = function () {
            //     modal.style.display = "none";
            // }

            function LTCDataSourceChange() {
                document.getElementById("FlexInput").value = document.getElementById("ltc_data_source").value;
                console.log (document.getElementById("FlexInput").value );
            }

            function flexInSubmit() {
                modal.style.display = "none";
                document.getElementById('simParamVal').style.display = 'flex';
            }

            // When the user clicks anywhere outside of the modal, close it
            window.onclick = function (event) {
                if (event.target == modal) {
                    modal.style.display = "none";
                }
            }
        //Modal Code End-----------------------------------------------------
    function toggleRefPrevSource() {
        var PROC = document.getElementById('RefprevsourceYes').checked;

        if (PROC == true) {
            document.getElementById('hideRefprevpath').style.display = "flex";
            // document.getElementById('hidetablelevel').style.display = "flex";
            // document.getElementById('hidevarlevel').style.display = "flex";
        }

        else {
            document.getElementById('hideRefprevpath').style.display = "none"; 
            // document.getElementById('hidetablelevel').style.display = "none"; 
            // document.getElementById('hidevarlevel').style.display = "none"; 
        }
    }
    function popValCheck(val) {

        var upVal = val.toUpperCase();
        if("&LOGIN_TYPE" == "AAA"){
                var opt = document.getElementById('popTypeVal2').value;
            }
            else{
                var opt = document.getElementById('popTypeVal').value;
            }

        if ((opt == 'CAGELIST') && ((upVal.indexOf("O") != -1) || (upVal.indexOf("I") != -1))) {
            alert("Some/All of the CAGE values contain the letter O or I. Please review the CAGE values before submission.");
        }
        if(val.length > 8000){
            console.log(val.length);
            document.getElementById('poptext').value = "";
            alert("Your niin count exceeds the limit of 800. Please enter a smaller population size or use the 'Read from Excel' option.");
        }
    }
    function changeRadio1() {
        document.getElementById('sourceSAS').checked = false;
        document.getElementById('poptext').style.display = "flex";
        document.getElementById('customNIINText').style.display = "none";
//        document.getElementById('pastePopTooltip').style.display = "block";
        document.getElementById('sourceSAS').value = '';
        document.getElementById('poptext').required = true;
    }

    function changeRadio2() {
        document.getElementById('inputPop').checked = false;
        document.getElementById('poptext').style.display = "none";
        document.getElementById('poptext').value = "";
        document.getElementById('customNIINText').style.display = "block";
//        document.getElementById('pastePopTooltip').style.display = "none";
        document.getElementById('sourceSAS').value = 'SASPop';
        document.getElementById('poptext').required = false;
    }

    
    function alphaNumCheck(val) {

    val = val.replace(/ /g, "_");

    document.getElementById('run_name').value = val;

    if (!(val.match(/^[a-zA-Z0-9_]*$/)) && (val.length > 32 || val.length < 1)) {
        alert("Your Simulation name can not contain special characters and its length must be between 1 and 32 characters");
        document.getElementById('run_name').value = "";
    }
    else if (!(val.match(/^[a-zA-Z0-9_]*$/))) {
        alert("Your Simulation name can not contain special characters");
        document.getElementById('run_name').value = "";
    }
    else if (val.length > 32 || val.length < 1) {
        alert("Your Simulation name length must be between 1 and 32 characters");
        document.getElementById('run_name').value = "";
    }
    else {
    }
    }
    function toggleProcActiv() {
            var PROC = document.getElementById('auto_awd_hist_manual_wrkld_adj').checked;

            if (PROC == true) {
                    document.getElementById('histAdj').style.display = "flex";
            }

            else {
                    document.getElementById('histAdj').style.display = "none"; 
            }
    }
    
    function setPRPOLookbackDate(){
        var date = new Date();
        date.setDate(date.getDate() - 90)

        var dd = String(date.getDate()).padStart(2, '0');
        var mm = String(date.getMonth() + 1).padStart(2, '0');
        var yyyy = date.getFullYear();

        date = yyyy + '-' + mm +'-' +dd;

        var datePO = new Date();
        datePO.setDate(datePO.getDate() - 180)

        var ddPO = String(datePO.getDate()).padStart(2, '0');
        var mmPO = String(datePO.getMonth() + 1).padStart(2, '0');
        var yyyyPO = datePO.getFullYear();
        
        datePO = yyyyPO + '-' + mmPO +'-' +ddPO;

        document.getElementById("datepickerPO").value = datePO;
        document.getElementById("datepickerPR").value = date;
    }
   
    // function getDatePickedPO() {
    //     var inputDatePO = document.getElementById('datepickerPO').value;
    //     var enteredDatePO = new Date(inputDatePO);
    //     var minimumAllowedDatePO = new Date('January 1, 2003');

    //     var date = new Date();
    //     date.setDate(date.getDate() - 90)

    //     var dd = String(date.getDate()).padStart(2, '0');
    //     var mm = String(date.getMonth() + 1).padStart(2, '0');
    //     var yyyy = date.getFullYear();

    //     date = yyyy + '-' + mm +'-' +dd;

    //     if (isNaN(enteredDatePO.getTime())) {
    //         alert('Please enter a valid date');
    //         // document.getElementById('datepickerPO').value = date;
    //     } else if (enteredDatePO < minimumAllowedDatePO) {
    //         alert('Please enter a date on or after January 1, 2003');
    //         document.getElementById('datepickerPO').value = date;
    //     } else if (!/^\d{1,2}\/\d{1,2}\/\d{4}$/.test(inputDatePO)) {
    //         alert('Please enter date in a valid format (mm/dd/yyyy)');
    //         document.getElementById('datepickerPO').value = date;
    //     }
    // }

    function getDatePickedPO() {
        var inputDatePO = document.getElementById('datepickerPO').value;
        var enteredDatePO = new Date(inputDatePO);
        var minimumAllowedDatePO = new Date(Date.UTC(2003, 0, 1));

        var date = new Date();
        date.setDate(date.getDate() - 180)

        var dd = String(date.getDate()).padStart(2, '0');
        var mm = String(date.getMonth() + 1).padStart(2, '0');
        var yyyy = date.getFullYear();

        date = yyyy + '-' + mm +'-' +dd;

        if (isNaN(enteredDatePO.getTime()) || enteredDatePO < minimumAllowedDatePO || inputDatePO.split('-')[0].length > 4) {
            alert('Please enter a valid date that is on or after January 1, 2003');
            document.getElementById('datepickerPO').value = date;
        } else {
            console.log('This is a valid value and it should save this value off');
        }
    }

    function getDatePickedPR() {
        var inputDatePR = document.getElementById('datepickerPR').value;
        var enteredDatePR = new Date(inputDatePR);
        var minimumAllowedDatePR = new Date(Date.UTC(2003, 0, 1));

        var date = new Date();
        date.setDate(date.getDate() - 90)

        var dd = String(date.getDate()).padStart(2, '0');
        var mm = String(date.getMonth() + 1).padStart(2, '0');
        var yyyy = date.getFullYear();

        date = yyyy + '-' + mm +'-' +dd;

        if (isNaN(enteredDatePR.getTime()) || enteredDatePR < minimumAllowedDatePR || inputDatePR.split('-')[0].length > 4) {
            alert('Please enter a valid date that is on or after January 1, 2003');
            document.getElementById('datepickerPR').value = date;
        } else {
            console.log('This is a valid value and it should save this value off');
        }
    }    

    function togglecustomcodepath() {

        if (document.getElementById('codeBases').value == 'custom_path') {
            document.getElementById('hidecodepath').style.display = "flex";
        }

        else {
            document.getElementById('hidecodepath').style.display = "none"; 
        }
    }
    function toggleFOPT() {
        var DUR = document.getElementById('duration').value;
        if (x != 1) {
            for (var i = 1; i < x; i++) {
            
                var FOPT = document.getElementById('forecastOpt'+i).value;
                if (FOPT != 'None') {
                    if (DUR == '1') {
                        document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'none';
                                document.getElementById('year3' + i).style.display = 'none';
                                document.getElementById('year4' + i).style.display = 'none';
                                document.getElementById('year5' + i).style.display = 'none';
                                document.getElementById('year6' + i).style.display = 'none';
                                document.getElementById('year7' + i).style.display = 'none';
                                document.getElementById('year8' + i).style.display = 'none';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';
                            }
                            else if (DUR == '2') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'none';
                                document.getElementById('year4' + i).style.display = 'none';
                                document.getElementById('year5' + i).style.display = 'none';
                                document.getElementById('year6' + i).style.display = 'none';
                                document.getElementById('year7' + i).style.display = 'none';
                                document.getElementById('year8' + i).style.display = 'none';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';

                            }
                            else if (DUR == '3') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'none';
                                document.getElementById('year5' + i).style.display = 'none';
                                document.getElementById('year6' + i).style.display = 'none';
                                document.getElementById('year7' + i).style.display = 'none';
                                document.getElementById('year8' + i).style.display = 'none';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';
                            }
                            else if (DUR == '4') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'flex';
                                document.getElementById('year5' + i).style.display = 'none';
                                document.getElementById('year6' + i).style.display = 'none';
                                document.getElementById('year7' + i).style.display = 'none';
                                document.getElementById('year8' + i).style.display = 'none';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';
                            }
                            else if (DUR == '5') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'flex';
                                document.getElementById('year5' + i).style.display = 'flex';
                                document.getElementById('year6' + i).style.display = 'none';
                                document.getElementById('year7' + i).style.display = 'none';
                                document.getElementById('year8' + i).style.display = 'none';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';
                            }
                            else if (DUR == '6') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'flex';
                                document.getElementById('year5' + i).style.display = 'flex';
                                document.getElementById('year6' + i).style.display = 'flex';
                                document.getElementById('year7' + i).style.display = 'none';
                                document.getElementById('year8' + i).style.display = 'none';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';

                            }
                            else if (DUR == '7') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'flex';
                                document.getElementById('year5' + i).style.display = 'flex';
                                document.getElementById('year6' + i).style.display = 'flex';
                                document.getElementById('year7' + i).style.display = 'flex';
                                document.getElementById('year8' + i).style.display = 'none';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';
                            }
                            else if (DUR == '8') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'flex';
                                document.getElementById('year5' + i).style.display = 'flex';
                                document.getElementById('year6' + i).style.display = 'flex';
                                document.getElementById('year7' + i).style.display = 'flex';
                                document.getElementById('year8' + i).style.display = 'flex';
                                document.getElementById('year9' + i).style.display = 'none';
                                document.getElementById('year10' + i).style.display = 'none';
                            }
                            else if (DUR == '9') {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'flex';
                                document.getElementById('year5' + i).style.display = 'flex';
                                document.getElementById('year6' + i).style.display = 'flex';
                                document.getElementById('year7' + i).style.display = 'flex';
                                document.getElementById('year8' + i).style.display = 'flex';
                                document.getElementById('year9' + i).style.display = 'flex';
                                document.getElementById('year10' + i).style.display = 'none';
                            }
                            else {
                                document.getElementById('forecastText' + i).style.display = 'flex';
                                document.getElementById('year1' + i).style.display = 'flex';
                                document.getElementById('year2' + i).style.display = 'flex';
                                document.getElementById('year3' + i).style.display = 'flex';
                                document.getElementById('year4' + i).style.display = 'flex';
                                document.getElementById('year5' + i).style.display = 'flex';
                                document.getElementById('year6' + i).style.display = 'flex';
                                document.getElementById('year7' + i).style.display = 'flex';
                                document.getElementById('year8' + i).style.display = 'flex';
                                document.getElementById('year9' + i).style.display = 'flex';
                                document.getElementById('year10' + i).style.display = 'flex';
                            }
                    }
                    else {
                        document.getElementById('forecastText' + i).style.display = 'none';
                        document.getElementById('year1' + i).style.display = 'none';
                        document.getElementById('year2' + i).style.display = 'none';
                        document.getElementById('year3' + i).style.display = 'none';
                        document.getElementById('year4' + i).style.display = 'none';
                        document.getElementById('year5' + i).style.display = 'none';
                        document.getElementById('year6' + i).style.display = 'none';
                        document.getElementById('year7' + i).style.display = 'none';
                        document.getElementById('year8' + i).style.display = 'none';
                        document.getElementById('year9' + i).style.display = 'none';
                        document.getElementById('year10' + i).style.display = 'none';
                            }
                        }
                    }    
            }

    function toggleSIG() {
        var PROC = document.getElementById('ExecSIGYes').checked;

        if (PROC == true) {
            document.getElementById('DisplaySig0').style.display = "flex";
            document.getElementById('DisplaySig1').style.display = "flex";
            document.getElementById('DisplaySig2').style.display = "flex";
            document.getElementById('DisplaySig3').style.display = "flex";
            document.getElementById('DisplaySig4').style.display = "flex";
            document.getElementById('DisplaySig5').style.display = "flex";
            document.getElementById('DisplaySig6').style.display = "flex";
            document.getElementById('DisplaySig7').style.display = "flex";    
        }

        else {
            document.getElementById('DisplaySig0').style.display = "none";
            document.getElementById('DisplaySig1').style.display = "none";
            document.getElementById('DisplaySig2').style.display = "none";
            document.getElementById('DisplaySig3').style.display = "none";
            document.getElementById('DisplaySig4').style.display = "none";
            document.getElementById('DisplaySig5').style.display = "none";
            document.getElementById('DisplaySig6').style.display = "none";
            document.getElementById('DisplaySig7').style.display = "none";
        }
    }
    function reporttypedependecies() {
        
        var ReportType = document.getElementById('simAnalysisType').value;
        var PopType = document.getElementById('popTypeVal').value;
        var PopType2 = document.getElementById('popTypeVal2').value;
        var sc = document.getElementById('source').checked;

        console.log(ReportType);    
        simulationAnalysisType(true);
        //Output validation on the FRONT END

        if (PopType2 == "AAA_AVN" && ReportType == "VENDOR_FORECAST") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "AVN_AAA_REPORT";
            }
        if (PopType2 == "AAA_LM" && ReportType == "VENDOR_FORECAST") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "LM_AAA_REPORT";
            }
        if (PopType2 == "AAA_AVN" && ReportType == "LM_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "AVN_AAA_REPORT";
            }
        if (PopType2 == "AAA_LM" && ReportType == "AVN_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "LM_AAA_REPORT";
            }
        if (PopType == "CUSTOM" && ReportType == "VENDOR_FORECAST") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }

        if (PopType == "CUSTOM" && ReportType == "AVN_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        
        if (PopType == "CUSTOM" && ReportType == "LM_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
        }
        if (PopType == "CAGELIST" && ReportType == "AVN_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "CAGELIST" && sc && ReportType == "VENDOR_FORECAST") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "CAGELIST" && ReportType == "LM_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "SSA" && ReportType == "LM_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "SSA" && ReportType == "AVN_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "SC" && ReportType == "AVN_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "SC" && ReportType == "VENDOR_FORECAST") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "SC" && ReportType == "LM_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "WSDC" && ReportType == "AVN_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "WSDC" && ReportType == "VENDOR_FORECAST") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }
        if (PopType == "WSDC" && ReportType == "LM_AAA_REPORT") {
            window.alert("Your population type is not compatible with this report type. Please choose a different one.");
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            }

        if (ReportType == "AVN_AAA_REPORT" || ReportType == "LM_AAA_REPORT") {
            if(PopType != "CUSTOM" && PopType != "CAGELIST" && PopType != "SSA" && PopType != "SC" && PopType != "WSDC"){
                document.getElementById('DisplayExecSig').style.display = "flex";
                document.getElementById('ExecSIGYes').checked = true;

                //View all SIG options now that Run SIG is checked
                toggleSIG();
            
                if (ReportType == "AVN_AAA_REPORT") {
                    document.getElementById('default_aaa_params').value = "AAA_AVN";
                    document.getElementById('rank_order').value = "_FPI__,_A1_SB,_A1_SS,A1_NSB,__8A__,__SS__,SC_SDV,SC_HUB,SC_EDW,SC_WOS,_SC_SB,__SC__,OC_SDV,OC_HUB,OC_EDW,OC_WOS,_OC_SB,__OC__,_OC_SS";
                    document.getElementById('sig_scen_param_path').value = "/home/users/&sysuserid/sasviyadata/&msc/users/&sysuserid/My_Simulations/sBCA/inputs/sig_scen_params_avn_sop_def.xml";
                }
                else if (ReportType == "LM_AAA_REPORT") {
                    document.getElementById('default_aaa_params').value = "AAA_LM";
                    document.getElementById('rank_order').value = "SS,OC,OS,SC,SCS";
                    document.getElementById('sig_scen_param_path').value = "/home/users/&sysuserid/sasviyadata/&msc/users/&sysuserid/My_Simulations/sBCA/inputs/sig_scen_params_lm_sop_def.xml";
                }
            }
        }

        else {
            document.getElementById('default_aaa_params').value = "No";
            document.getElementById('DisplayExecSig').style.display = "none";
            document.getElementById('rank_order').value = "";

            //Remove all SIG options now that Run SIG is not checked
            toggleSIG();

        }    
    }
    function changedefaultniinoptions() {
        if("&LOGIN_TYPE" == "AAA"){
                var popTypeVal = document.getElementById('popTypeVal2').value;
            }
            else{
                var popTypeVal = document.getElementById('popTypeVal').value;
            }
        var fullAAAVal = document.getElementById('fullAAAYes').value;
        var AAATestVal = document.getElementById('AAATestModeYes').value;
        // Add so that SIG does not toggle on login;

        if (popTypeVal == "AAA_AVN" || popTypeVal == "AAA_LM" || popTypeVal == "SSA") {
            document.getElementById('simAnalysisType').style.display = "block";
            document.getElementById('trunc_pop').style.display = "none";

            if (popTypeVal == "AAA_AVN") {
                if ("&AdminUser." == "true") {

                }
                else{
                    document.getElementById('baselineoptions').style.display = 'none';
                    document.getElementById('collapseSeven').style.display = 'none';
                    document.getElementById('collapseFive').style.display = 'none';
                    document.getElementById('outputtitle').style.display = 'none';
                    document.getElementById('addtlsimtitle').style.display = 'none';
                    document.getElementById('collapseFour').style.display = 'none';
                    document.getElementById('scenariotitles').style.display = 'none';
                    document.getElementById('simdurshow').style.display = 'none';

                }
                // Delete any previous scenarios - This prevents user accidentally creating unintended scenarios 
                // when switching niin populations
                var scenarioLength = document.getElementsByClassName("section1").length;
                if (scenarioLength > 0){
                    for (var i = scenarioLength; i > 0; i--) {
                        deleteScenario();
                    }
                }
                
                //moved almost everything in here to forceAAAscenParams function
                document.getElementById('popTypeVal').value = "AAA_AVN";
                document.getElementById('DefaultSCSettingsYes').checked = true;  
                ViewDefaultSCSettings(); 
                document.getElementById('DefaultSCChoice').value = 'AVN';
                document.getElementById('default_aaa_params').value = "AAA_AVN";
                document.getElementById('popInput').style.display = "none";
                document.getElementById('testMode').style.display = "flex";
                document.getElementById('popSelection').style.display = "none";
                document.getElementById('fullAAAbox').style.display = "flex";
                document.getElementById('NIINRange').style.display = "flex";
                document.getElementById('aaasimparam').style.display = "flex";

                // if ("&AdminUser." == "true") {
                //     document.getElementById('indir').value = '/sasdata/nonfinance/users/' + "&userid." + '/shared_data/historical/avn/common/.acn_ss_files/reference/aaa_monthly';
                // }

                forceAAAscenParams();   
                reporttypedependecies()
            }

            else if (popTypeVal == "AAA_LM") {
                // Delete any previous scenarios - This prevents user accidentally creating unintended scenarios 
                // when switching niin populations
                var scenarioLength = document.getElementsByClassName("section1").length;
                if (scenarioLength > 0){
                    for (var i = scenarioLength; i > 0; i--) {
                        deleteScenario();
                    }
                }
                

                //moved almost everything in here to forceAAAscenParams function
                document.getElementById('popTypeVal').value = "AAA_LM";
                document.getElementById('DefaultSCSettingsYes').checked = true;  
                ViewDefaultSCSettings(); 
                document.getElementById('DefaultSCChoice').value = 'LM';
                document.getElementById('default_aaa_params').value = "AAA_LM";
                document.getElementById('popInput').style.display = "none";
                document.getElementById('testMode').style.display = "flex";
                document.getElementById('popSelection').style.display = "none";
                document.getElementById('fullAAAbox').style.display = "flex";
                document.getElementById('NIINRange').style.display = "flex";
                document.getElementById('aaasimparam').style.display = "flex";

                if ("&AdminUser." == "true") {
                    document.getElementById('indir').value = '/home/users/' + "&userid." + '/sasviyadata/' + "&msc." + '/users/' + "&userid." + '/My_Simulations/sBCA/inputs';
                }

                forceAAAscenParams();
                reporttypedependecies()          
            }

            else {
                document.getElementById('baselineoptions').style.display = 'flex';
                document.getElementById('collapseSeven').style.display = 'flex';
                document.getElementById('collapseFive').style.display = 'flex';
                document.getElementById('outputtitle').style.display = 'flex';
                document.getElementById('addtlsimtitle').style.display = 'flex';
                document.getElementById('collapseFour').style.display = 'flex';
                document.getElementById('scenariotitles').style.display = 'flex';

                document.getElementById('pen_CPS_buffer_all').className = ('form-control');
                document.getElementById('inactive_toggle').style.display = "flex";
                document.getElementById('include_icr_of_zero_n').checked = true;
                document.getElementById('simAnalysisType').value = "VENDOR_FORECAST";
                /*grey out channel*/
                //document.getElementById('simAnalysisType').classList.add('disabled');
                document.getElementById('fcst_type_rmcr_0').value = "ICR";
                document.getElementById('partial_aaa').style.display = "none";
                document.getElementById('testMode').style.display = "none";
                document.getElementById('fullAAAbox').style.display = "none";
                document.getElementById('NIINRange').style.display = "none";
                document.getElementById('aaasimparam').style.display = "none";
                document.getElementById('DisplayExecSig').style.display = "none";
                document.getElementById('DisplaySig0').style.display = "none";
                document.getElementById('DisplaySig1').style.display = "none";
                document.getElementById('DisplaySig2').style.display = "none";
                document.getElementById('DisplaySig3').style.display = "none";
                document.getElementById('DisplaySig4').style.display = "none";
                document.getElementById('DisplaySig5').style.display = "none";
                document.getElementById('DisplaySig6').style.display = "none";
                document.getElementById('DisplaySig7').style.display = "none";

            }

        }
        else {
            document.getElementById('baselineoptions').style.display = 'flex';
            document.getElementById('collapseSeven').style.display = 'flex';
            document.getElementById('collapseFive').style.display = 'flex';
            document.getElementById('outputtitle').style.display = 'flex';
            document.getElementById('addtlsimtitle').style.display = 'flex';
            document.getElementById('collapseFour').style.display = 'flex';
            document.getElementById('scenariotitles').style.display = 'flex';

            document.getElementById('DisplayExecSig').style.display = "none";
            document.getElementById('DisplaySig0').style.display = "none";
            document.getElementById('DisplaySig1').style.display = "none";
            document.getElementById('DisplaySig2').style.display = "none";
            document.getElementById('DisplaySig3').style.display = "none";
            document.getElementById('DisplaySig4').style.display = "none";
            document.getElementById('DisplaySig5').style.display = "none";
            document.getElementById('DisplaySig6').style.display = "none";
            document.getElementById('DisplaySig7').style.display = "none";
            document.getElementById('simAnalysisType').style.display = "block";
            document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
            document.getElementById('simAnalysisType').disabled = false;
            // document.getElementById('simAnalysisType' + scen).className = ('form-control');
            document.getElementById('partial_aaa').style.display = "none";
            document.getElementById('testMode').style.display = "none";
            document.getElementById('fullAAAbox').style.display = "none";
            document.getElementById('NIINRange').style.display = "none";
            document.getElementById('aaasimparam').style.display = "none";
            reporttypedependecies()
            
        }


        if (popTypeVal == "CAGELIST" || popTypeVal == "CUSTOM" || popTypeVal == "WSDC") {
            document.getElementById('popInput').style.display = "flex";
            document.getElementById('poptext').style.display = "flex";
            document.getElementById('sourceSAS').value = '';
        }
        else {
            document.getElementById('popInput').style.display = "none";
        }
        if (popTypeVal == "CUSTOM") {
            document.getElementById('popSelection').style.display = "flex";
            document.getElementById('popInput').style.display = "flex";
            document.getElementById('inputPop').checked = true;
            document.getElementById('sourceSAS').checked = false;
            document.getElementById('poptext').style.display = "flex";
            document.getElementById('customNIINText').style.display = "none";
        }
        else {
            document.getElementById('popSelection').style.display = "none";
            document.getElementById('customNIINText').style.display = "none";
        }
        if (popTypeVal == "CAGELIST"|| popTypeVal == "Vendor") {
            document.getElementById('sourcingStrat').style.display = "flex";
        }
        else {
            document.getElementById('sourcingStrat').style.display = "none";
        }

        if (popTypeVal == "SC") {
            for (var i = 1; i < 2; i++) {
                document.getElementById('supplyChain' + i).style.display = "flex";

            }
        }
        else {
            for (var i = 1; i < 2; i++) {
                document.getElementById('supplyChain' + i).style.display = "none";

            }
        }
        if (popTypeVal == "WSDC") {
            document.getElementById('WSDCopt').style.display = "flex";
        }
        else {
            document.getElementById('WSDCopt').style.display = "none";
        }
        if (popTypeVal == "Vendor") {
            document.getElementById('vendorSelect').style.display = "flex";
            document.getElementById('simAnalysisType').value = "VENDOR_FORECAST";
            document.getElementById('simAnalysisType').disabled = false;
        }
        else {
            document.getElementById('vendorSelect').style.display = "none";
        }

    }
    function showDate() {
        var PO = document.getElementById('exc_old_PO').checked;
        var PR = document.getElementById('exc_old_PR').checked;

        if (PR == false) {
            document.getElementById('ifExcludeCheckedPR').style.display = 'none';
            document.getElementById('ifExcludeCheckedPR1').style.display = 'none';
        } else {
            document.getElementById('ifExcludeCheckedPR').style.display = 'flex';
            document.getElementById('ifExcludeCheckedPR1').style.display = 'flex';
        }

        if (PO == false) {
            document.getElementById('ifExcludeCheckedPO').style.display = 'none';
            document.getElementById('ifExcludeCheckedPO1').style.display = 'none';
        } else {
            document.getElementById('ifExcludeCheckedPO').style.display = 'flex';
            document.getElementById('ifExcludeCheckedPO1').style.display = 'flex';
        }
    }
    function defaultLoad() {
        aaaTestToggle();
        costFacDefault();
        todaysDate();
        setPRPOLookbackDate();
        document.getElementById('popTypeVal').style.display = "none";
        document.getElementById('popTypeVal2').style.display = "none";
        document.getElementById('menuTitle2').style.display = "none";
        document.getElementById('menuTitle').style.display = "none";
        document.getElementById('progbarhelp').style.display = "none";
        if("&LOGIN_TYPE" == "AAA"){
            document.getElementById('popTypeVal').style.display = "none";
            document.getElementById('popTypeVal2').style.display = "flex";
            document.getElementById('menuTitle2').style.display = "none";
            document.getElementById('menuTitle').style.display = "flex";
            document.getElementById('popSelection').style.display = "none";
            document.getElementById('popInput').style.display = "none";
            if ("&AdminUser." != "true"){
                document.getElementById('baselineoptions').style.display = 'none';
                document.getElementById('collapseSeven').style.display = 'none';
                document.getElementById('collapseFive').style.display = 'none';
                document.getElementById('outputtitle').style.display = 'none';
                document.getElementById('addtlsimtitle').style.display = 'none';
                document.getElementById('collapseFour').style.display = 'none';
                document.getElementById('scenariotitles').style.display = 'none';
                document.getElementById('simdurshow').style.display = 'none';
            }
        }
        else{
            document.getElementById('popTypeVal').style.display = "flex";
            document.getElementById('popTypeVal2').style.display = "none";
            document.getElementById('menuTitle').style.display = "none";
            document.getElementById('menuTitle2').style.display = "flex";

        }
        if ("&AdminUser." != "true") {
            //hide entire admin advanced option section if not admin user
            // document.getElementById('displayadmin').style.display = 'none';
        }
        else {
            //value is set to 0 for all users (hidden - at top of page) and overwritten here if admin
            //so that log isn't output to clients personal run folder
            document.getElementById('savelog').value = '1';
            document.getElementById('displayadmin').style.display = "flex";
        }

        document.getElementById('run_name').value = '';
        document.getElementById('duration').value = '5';
        document.getElementById('year_type').value = 'ROLLING 12 MONTH';
        document.getElementById('popTypeVal').value = 'CUSTOM';
        document.getElementById('simAnalysisType').value = "STANDARD_ANALYSIS";
        document.getElementById('inactive_toggle').style.display = "none";
        document.getElementById('DisplayDefaultSCOptions').style.display = "none"; 
        document.getElementById('DisplayExecSig').style.display = "none"; //only display SIG once AAA is selected
        document.getElementById('hidecodepath').style.display = 'none';
        document.getElementById('run_var_lvl').style.display = "none"; 
        document.getElementById('run_var_lvl_opt').style.display = "none";
        document.getElementById('partial_aaa').style.display = "none";
        document.getElementById('trunc_pop').style.display = "none";

        showDate();
        var today = new Date();

        var pastdate = new Date(today - 90 * 86400000);
        dd = pastdate.getDate();
        mm = pastdate.getMonth() + 1;
        yyyy = pastdate.getFullYear();
        if (dd < 10) {
            dd = '0' + dd;
        }
        if (mm < 10) {
            mm = '0' + mm;
        }
    }

    function showDepDmd() {
        var depDmdChecked = document.getElementById('use_depdmd_0').checked;
        var extrapOptions = document.getElementById('extrap_demand_whole');

        // Shows the extrapolation options if dependent demand is checked & vice versa
        if (!depDmdChecked) {
            extrapOptions.style.display = 'none';
            // Set the value of demand extrapolation to blank if dependent demand is unchecked
            document.getElementById('extrap_depdmd').value = " ";
        } else {
            extrapOptions.style.display = 'flex';
            // Restores extrapolation defaults when re-checked
            document.getElementById('extrap_depdmd').value = "DEP_AVG";
            document.getElementById('extrapFrontOptionAVG').checked = true;
        }
    }

    // Set today's date and update input fields on page load
    function todaysDate() {
        const today = new Date();

        const formattedDate = today.toISOString().split('T')[0];

        document.getElementById('todaysbcadate').value = formattedDate;
        document.getElementById('todayssigdate').value = formattedDate;
    }

    // Lot Payment
    function lotDefaults() {
        document.getElementById('lotInput' + x).style.display = 'none';
        document.getElementById('totalConSpend' + x).style.display = 'none';
        document.getElementById('nonFeePerc' + x).style.display = 'none';
        document.getElementById('payFreq' + x).style.display = 'none';
        document.getElementById('lotExcel' + x).style.display = 'none';
    }

    function enableCoc(that, scen) {
        let lotOffChecked = document.getElementById('lotOff' + scen).checked;
        let lotOnChecked = document.getElementById('lotOn' + scen).checked;

        if (lotOffChecked == true) {
            document.getElementById('lotInput' + scen).style.display = 'none';
            document.getElementById('nonFeePerc' + scen).style.display = 'none';
            document.getElementById('payFreq' + scen).style.display = 'none';
            document.getElementById('totalConSpend' + scen).style.display = 'none';
            document.getElementById('lotExcel' + scen).style.display = 'none';
            console.log('Lot Payment is Off');
        } else if (lotOnChecked == true) {
            document.getElementById('lotInput' + scen).style.display = 'flex';
            document.getElementById('payFreq' + scen).style.display = 'flex';
            document.getElementById('lotInputSelect' + scen).value ='simspend';
            console.log('Lot Payment is On');
        }
    }

    function lotPayInput(that, scen) {
        let lotInputSelectVal = document.getElementById('lotInputSelect' + scen).value;

        if (lotInputSelectVal == 'simspend') {
            document.getElementById('nonFeePerc' + scen).style.display = 'none';
            // document.getElementById('payFreq' + scen).style.display = 'flex';
            console.log('Simulated Spend' + scen);
            document.getElementById('totalConSpend' + scen).style.display = 'none';
            document.getElementById('lotExcel' + scen).style.display = 'none';
            document.getElementById('payFreq' + scen).style.display = 'flex'
        } else if (lotInputSelectVal == 'actctrspend') {
            document.getElementById('totalConSpend' + scen).style.display = 'flex';
            document.getElementById('nonFeePerc' + scen).style.display = 'flex';
            // document.getElementById('payFreq' + scen).style.display = 'flex';
            console.log('Actual Contract Spend');
            document.getElementById('lotExcel' + scen).style.display = 'none';
            document.getElementById('payFreq' + scen).style.display = 'flex'
        } else if (lotInputSelectVal == 'excel') {
            document.getElementById('lotExcel' + scen).style.display = 'flex';
            console.log('Lot Payment Excel');
            // document.getElementById('payFreq' + scen).style.display = 'none';
            document.getElementById('nonFeePerc' + scen).style.display = 'none';
            document.getElementById('totalConSpend' + scen).style.display = 'none';
            document.getElementById('payFreq' + scen).style.display = 'none'
        } else {
            document.getElementById('nonFeePerc' + scen).style.display = 'none';
            // document.getElementById('payFreq' + scen).style.display = 'none';
            document.getElementById('totalConSpend' + scen).style.display = 'none';
            document.getElementById('lotExcel' + scen).style.display = 'none';
            console.log('No Option chosen for Lot Payment Input');
            document.getElementById('payFreq' + scen).style.display = 'flex'
        }
    }

    // Cost Factors
    function costFacDefault() {
        console.log("&MSC");
        var costFacRate = document.getElementById('costFactorRate');
        var storage = document.getElementById('storage');
        var costOfCap = document.getElementById('costOfCapital');

        if ("&MSC." === "MSC_AVIATION") {
            costFacRate.value = 'FY25';
            storage.value = 'CUBIC';
            costOfCap.value = 'OBL_INV_VAL';
            console.log('MSC Aviation works for costFacDefault function');
        } else {
            costFacRate.value = 'LEGACY';
            storage.value = 'OH_INV_VAL';
            costOfCap.value = 'OH_INV_VAL';
            console.log('MSC everything else works for costFacDefault function');
        }
    }

    function costFactChange() {
        var costFacRateDropdown = document.getElementById('costFactorRate').value;
        var storageDrop = document.getElementById('storage');
        var costOfCapDrop = document.getElementById('costOfCapital');

        if (costFacRateDropdown === "LEGACY") {
            storageDrop.value = 'OH_INV_VAL';
            costOfCapDrop.value = 'OH_INV_VAL';
            console.log('Legacy change works');
        } else {
            storageDrop.value = 'CUBIC';
            costOfCapDrop.value = 'OBL_INV_VAL';
            console.log('fy25 change works');
        }
    }

    function aaaTestToggle() {
        if ("&LOGIN_TYPE" == "AAA"){
            document.getElementById('runTripleATest').style.display = 'flex';
        }
        else {
            document.getElementById('runTripleATest').style.display = 'none';
        }
    }

    // Global flag to indicate if a toast notification is active
    let toastActive = false;

    function showInputToast(message, input) {
        // If a toast is already active for this input, exit early
        if (input._toastActive) return;
        input._toastActive = true;
    
        // Create the toast element
        let toast = document.createElement('div');
        toast.textContent = message;
    
        // Apply basic styling for the toast
        toast.style.position = 'absolute';
        toast.style.backgroundColor = 'rgba(255, 0, 0, 0.8)';
        toast.style.color = '#fff';
        toast.style.padding = '8px 12px';
        toast.style.borderRadius = '4px';
        toast.style.boxShadow = '0 2px 6px rgba(0, 0, 0, 0.3)';
        toast.style.zIndex = 1000;
        toast.style.opacity = '1';
        toast.style.transition = 'opacity 0.5s ease';
    
        // Calculate the input element's position on the page
        let rect = input.getBoundingClientRect();
        // Position the toast to the right of the input with a 10px gap:
        toast.style.top = rect.top + window.pageYOffset + "px";
        toast.style.left = rect.right + window.pageXOffset + 10 + "px";
    
        // Append the toast to the body
        document.body.appendChild(toast);
    
        // Start fade out after 2.5 seconds
        setTimeout(() => {
            toast.style.opacity = '0';
        }, 1000000);
    
        // Remove the toast from the DOM after 3 seconds, then reset the flag
        setTimeout(() => {
            if (toast.parentElement) {
                toast.parentElement.removeChild(toast);
            }
            input._toastActive = false;
        }, 3000);
    }
    
    function validateInput(input) {
        // Parse the input value and min/max values as integers
        let min = parseInt(input.min, 10);
        let max = parseInt(input.max, 10);
        let value = parseInt(input.value, 10);
        
        if (value < min || value > max || isNaN(value)) {
            showInputToast("The value must be between " + min + " and " + max + ".", input);
        }
    }
    document.addEventListener('DOMContentLoaded', () => {
        const form = document.getElementById('myForm');
        const runBtn = document.getElementById('runSim');

        form.addEventListener('input', () => {
            runBtn.disabled = !form.checkValidity();
        });
    
        form.addEventListener('submit', e => {
            if (!form.checkValidity()) {
                e.preventDefault();
                form.reportValidity();
            }
        });

    });

    document.addEventListener('DOMContentLoaded', () => {
        const autoFields = document.querySelectorAll('input.auto-default-min');
        console.log('Found auto-default fields:', autoFields);
      
        autoFields.forEach(input => {
          console.log('Binding blur handler to:', input);
          let timer;
      
          input.addEventListener('blur', () => {
            console.log('Blur fired on:', input);
            if (input.value.trim() === '') {
              console.log('Starting 3s timer for blank field…');
              timer = setTimeout(() => {
                const minVal = parseFloat(input.min) || 0;
                console.log(`Timer done → autofilling ${minVal}`);
                input.value = minVal;
                showInputToast(
                  `No value entered — defaulting to minimum of ${minVal}.`,
                  input
                );
                runBtn.disabled = !isFormValid();
              }, 3000);
            }
          });
      
          ['focus', 'input'].forEach(evt => {
            input.addEventListener(evt, () => {
              console.log(`${evt} on ${input.id} → clearing timer`);
              clearTimeout(timer);
            });
          });
        });
      });
      
      

</script>
        <div class="sticky">
            <div class="header">
                <div class="container-fluid">
                    <ul class="float-left">
                        <li>
                            <b>
                                <img src="https://www.dla.mil/Portals/104/DLA-logo-w-blueback-Web.png?ver=2015-04-02-091859-267"
                                     alt="DLA Icon" class="logo">Defense Logistics Agency
                            </b>
                        </li>
                    </ul>
                    <ul class="float-right">
                        <li id="menuTitle">AAA Interface</li>
                        <li id="menuTitle2">Standard BCA Simulator</li>
                    </ul>
                </div>
            </div>

            <div class="header2" id= "topheader">
                <div class="container-fluid">
                    <div class="float-left" id="scenariotitles">
                        <a class="btn btn-add" id="addScenario" style="color: #2C4B81;" onclick="addScenario();">
                            <i class="fa fa-plus-square-o"></i> Add Scenario
                        </a>
                        <a class="btn btn-remove" id="deleteScenario" style="color: #2C4B81;" onclick="deleteScenario();">
                            <i class="fa fa-minus-square-o" id="aClick"></i> Remove Last Scenario
                        </a>
                    </div>
                    <div class="float-right">
                        <button id="runSim" class="btn btn-run" type="submit" onclick="changeHidden2()" disabled> Run Simulation</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="body container-fluid">
            <div id="container2">
                <div class="accordion" id="accord1">
                    <div class="card">
                        <div class="card-header" id="section">
                            <button class="btn btn-link" type="button" data-toggle="collapse"
                            data-target="#collapseOne" aria-controls="collapseOne" aria-expanded="true" onclick="showCard('collapseOne')">
                            <i class="fa fa-chevron-down"></i>
                                General Population Options
                            </button>
                        </div>

                        <div id="collapseOne" class="collapse show" aria-labelledby="headingOne">
                            <div class="card-body">
                            <div class="form-group row">
                                <label for="run_name" class="col-sm-5 col-form-label">
                                    Simulation Name
                                    <span style="color:red;">*</span>
                                </label>
                                <div class="col-sm-7">
                                    <input type="text" class="form-control" id="run_name" name="run_name" value="" maxlength="23" minlength="1"
                                         aria-describedby="runNameTooltip" required>
                                    <small id="runNameTooltip" class="form-text text-muted">
                                        Provide an alphanumeric name (23 chars max).
                                    </small>
                                </div>
                            </div>

                                <div class="form-group row" id = "simdurshow">
                                        <label for="inputTwo" class="col-sm-5 col-form-label">
                                            Duration & Year Type
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Duration: Determines the number of years the simulator will execute.
                                                Year Type: For DLA Ficsal Year and Calendar Year selections, Year 1 encompasses only the remaining months of the current calendar or fiscal year, as defined by the selection. For Rolling 12 Months, the simulation run date is month 1 of Year 1.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    <div class="col-sm-3">
                                        <div class="form-group">
                                            <select class="form-control inputDate" name="sim_dur" id="duration"
                                                    onchange="toggleFOPT()">
                                                <option value="1">1 year</option>
                                                <option value="2">2 years</option>
                                                <option value="3">3 years</option>
                                                <option value="4">4 years</option>
                                                <option value="5" selected>5 years</option>
                                                <option value="6">6 years</option>
                                                <option value="7">7 years</option>
                                                <option value="8">8 years</option>
                                                <option value="9">9 years</option>
                                                <option value="10">10 years</option>
                                            </select>
                                        </div>
                                    </div>
                                    <div class="col-sm-4">
                                        <div class="form-group">
                                            <select class="form-control" name="year_type" id="year_type">
                                                <option value="DLA FISCAL YEAR">DLA Fiscal Year</option>
                                                <option value="CALENDAR YEAR">Calendar Year</option>
                                                <option value="ROLLING 12 MONTH" selected>Rolling 12 Month</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>

                                <div class="row">
                                    <div class="col-sm-5 col-form-label">
                                        <label> 
                                            Population Type
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="The BCA Simulator uses the following population options to initialize a simulation's item population:

                                                Aviation AAA: Auto-source monthly Aviation AAA population (See AAA Playbook for specific criteria).
                                                LM AAA: Auto-source monthly Land & Maritime AAA population (See AAA Playbook for specific criteria).
                                                CUSTOM NIIN Population: User-specified list of NIINs or NSNs.
                                                CAGE Provided: Auto-source NIINs supplied by user-provided CAGE(s).
                                                WSDC Provided: Auto-source NIINs from provided weapon systems designator code(s).
                                                SSA Vendors: Auto-source active items from DLA Aviation's current Strategic Sourcing Alliance vendor list.
                                                Supply Chains: Simulate all active items in the user-selected supply chain.
                                                    
                                                Note: AAA populations are only able to be used in AAA runs. All other populations are sBCA only.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class="input-group">
                                            <select class="form-control" name="niin_pop" id="popTypeVal"
                                                    onchange="changedefaultniinoptions()">
                                                <option value="CUSTOM" selected>Custom NIIN Population</option>
                                                <option value="CAGELIST" >CAGE Provided</option>
                                                <option value="WSDC"  >WSDC Provided</option>
                                                <option value="Vendor" hidden>Vendor Provided</option>             
                                                <option value="SSA" >SSA Vendors</option>
                                                <option value="SC" >Supply Chains</option>
                                                <option value="AAA_AVN" hidden>Aviation AAA Monthly</option>
                                                <option value="AAA_LM" hidden>Land and Maritime AAA Monthly</option>
                                                
                                            </select>
                                        </div>
                                    
                                    
                                        <div class="input-group">
                                            <select class="form-control" name="niin_pop" id="popTypeVal2"
                                                    onchange="changedefaultniinoptions()">
                                                <option value="" hidden></option>
                                                <option value="AAA_AVN">Aviation AAA Monthly</option>
                                                <option value="AAA_LM">Land and Maritime AAA Monthly</option>
                                                
                                            </select>
                                        </div>
                                    </div>
                                </div>															
                                
                                <div class="row" id="popSelection">
                                    <label class="col-form-label col-sm-5 pt-0" data-toggle="tooltip" data-placement="left" data-html="true">
                                        Population Selection
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="Paste Values Below: Type or paste in a NIIN or NSN. Each entry must be on its own line or seperated by a comma. The field cannot include spaces or special characters.

                                            Read From File: Follow the instructions to create a valid Excel or SAS dataset and specify the complete SAS grid filepath. Note that the file meet all naming convention requirements.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                        <span style="color:red;">*</span>
                                    </label>
                                    <div class="col-sm-7" id="customNIINRadio">
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="inputPop" id="inputPop"
                                                   onclick="changeRadio1();" checked>
                                            <label class="form-check-label">
                                                Paste Values Below
                                            </label>
                                        </div>
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="sourcePop"
                                                   id="sourceSAS" onclick="changeRadio2();" value="">
                                            <label class="form-check-label">
                                                Read from File
                                            </label>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="form-group row" id="popInput">
                                    <label class="col-form-label col-sm-5 pt-0"></label>
                                    <div class="col-sm-7 popTextMargin">
                                        <div id="customNIINText">
                                           Please enter the complete path to your Excel file or SAS dataset (the path should end in "<b>.xlsx</b>" or "<b>.sas7bdat</b>") 
                                           <br></br>
                                           <u>If the file is a SAS dataset</u>, it must have <b>at least a column named "NIIN" </b> with at least one valid NIIN.
                                           <br></br>
                                           <u>If the file is an Excel</u>, it must have a <b>sheet named
                                            "NIINs" and a column named "NIIN" </b>with at least one valid NIIN.
                                            
                                            <input type="text" class="form-control" id="pathtofile" name="cust_path"
                                            value="/home/users/&sysuserid/sasviyadata/&msc./users/&sysuserid/niin_list.sas7bdat" maxlength="300" minlength="30">
                                        </div>
                                        <textarea class="form-control" id="poptext" name="Population_text"
                                                  onchange="popValCheck(this.value)" value=""
                                                  placeholder="Paste your population here (one observation per line, maximum: 800 NIINs)"
                                                  rows="3" 
                                                  required>
                                        </textarea>
                                    </div>
                                </div>
                                <div class="row" id="WSDCopt">
                                    <div class="col-sm-5">
                                        <label for="WSDCopt" data-toggle="tooltip" data-placement="left">
                                            WSDC Options
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Selecting this option removes any items supporting multiple Weapon Systems.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7 wsdchover">
                                        <div class="form-check">
                                            <input class="form-check-input" type="checkbox" name="unique_wsdc" id="simi"
                                                    value="1">
                                            <label class="form-check-label" for="simi">
                                                Simulate only items supporting single WSDCs
                                            </label>
                                        </div>
                                    </div>
                                </div>
                                <div id="vendorSelect">
                                    <div class="form-group row">
                                        <label for="vendorSelect" class="col-sm-5 col-form-label" data-toggle="tooltip"
                                        data-placement="left" title="Provide vendor name to simulate only items sourced from the specified vendor.">
                                        Vendor Name</label>
                                        <div class="col-sm-7 wsdchover">
                                            <input type="text" class="form-control" name="save_VName"
                                                   placeholder="Type a Vendor Name">
                                        </div>
                                    </div>
                                </div>
                                <div class="row" id="supplyChain1">
                                    <legend class="col-form-label col-sm-5 pt-0" data-toggle="tooltip"
                                    data-placement="left" title="The Simulator will only simulate items assigned to the selected Supply Chain. Only RMC R & N items will be included.">
                                        Supply Chain Selection</legend>
                                    <div class="col-sm-7">
                                        <div class="input-group">
                                            <select class="form-control" name="supply_chain_pop">
                                                    <option value="AVIATION" id="av" selected>Aviation</option>
                                                    <option value="CANDE" id="const">Construction &amp; Equipment</option>
                                                    <option value="IH" id="indust">Industrial Hardware</option>
                                                    <option value="LAND" id="land">Land</option>
                                                    <option value="MARITIME" id="mar">Maritime</option>
                                                    <option value="MEDICAL" id="med">Medical</option>
                                                    <option value="SUBSISTENCE" id="sub">Subsistence</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>
                                <div class="row" id="inactive_toggle" hidden>
                                    <div class="col-sm-5">
                                        <label data-toggle="tooltip" data-placement="left"
                                                        title="By default, the BCA Simulator defines active items as those with ICR > 0. Choose Yes to classify items with ICR ≥ 0 as active.">
                                                Include inactive items (ICR=0)? </label>
                                    </div>
                                    <div class="col-sm-7 form-group">
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="icr_include_zero" id="include_icr_of_zero_y" value="1" checked>
                                            <label class="form-check-label">
                                                Yes
                                            </label>
                                        </div>
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="icr_include_zero" id="include_icr_of_zero_n" value="0">
                                            <label class="form-check-label">
                                                No
                                            </label>
                                        </div>
                                    </div>										
                                </div>	
                                <div id="sourcingStrat" class="row">
                                        <label class="col-sm-5 col-form-label">
                                            Sourcing Strategy
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Toggle for a single or one to multi-source strategy.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                        <div class="col-sm-7">
                                            <div class="form-check form-check-inline">
                                                <input class="form-check-input" type="checkbox" checked name="checkStrat" id="sole" onchange="checkSS_SC_Cage('sole')">
                                                <label class="form-check-label" id="checkedPadding" for="sole">
                                                    Sole Sourced
                                                </label>
                                            </div>
                                            <div class="form-check form-check-inline">
                                                <input class="form-check-input" type="checkbox" name="checkStrat" id="source" onchange="checkSS_SC_Cage('source')">
                                                <label class="form-check-label" for="source">
                                                    Source Controlled
                                                </label>
                                            </div>
                                            <!-- Backend Variable -->
                                            <input type="hidden" name="cage_sourcing_strat" id="cage_sourcing_strat" value="SS">
                                        </div>
                                </div>
                                <div class="row">
                                    <div class="col-sm-5">
                                        <label>
                                            Use previously sourced data
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Execute your simulation using source data tables that have been previously sourced to reduce runtime and/or align inputs. Note that item populations and simulation parameters / setup must be identical to the original Simulation.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                            </div>
                                                <div class="col-sm-7 form-group">
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="ref_prev_src_data" id="RefprevsourceYes" onchange="toggleRefPrevSource()" value="1">
                                                        <label class="form-check-label">
                                                            Yes
                                                        </label>
                                                    </div>
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="ref_prev_src_data" id="RefprevsourceNo" onchange="toggleRefPrevSource()" value="0" checked>
                                                        <label class="form-check-label">
                                                            No
                                                        </label>
                                                    </div>
                                        </div>										
                                </div>
                                <div class="row" id="hideRefprevpath">
                                    <div class="col-sm-5 col-form-label">
                                        <label>
                                        Path to previously sourced data
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="Please enter the complete SAS grid filepath directly to the source folder of the Simulation you'd like to reference.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <input type="text" class="form-control" name="prev_src_path"
                                            onchange="pathNumCheck(this.value)" value="/home/users/&sysuserid/sasviyadata/&msc/users/&sysuserid/My_Simulations/sBCA/results/[prev_simultion_name]/source" maxlength="300" minlength="30">
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="card" hidden>
                        <div class="card-header">
                            <button class="btn btn-link" type="button" data-toggle="collapse"
                                    data-target="#collapseTwo" aria-expanded="true" aria-controls="collapseTwo" onclick="showCard('collapseTwo')">
                                <i class="fa fa-chevron-down"></i>
                                MSC Settings
                            </button>
                        </div>

                        <div id="collapseTwo" class="collapse show" aria-labelledby="headingTwo">
                            <div class="card-body">                              

                                <div class="row">
                                    <div class="col-sm-5">
                                        <label for="DefaultSCSettings" data-toggle="tooltip" data-placement="left" 
                                                        title="need to fill out.">
                                                Use MSC Default Settings? </label>
                                    </div>
                                    <div class="col-sm-7 form-group" id="DefaultSCSettings">
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="DefaultSCSettings" id="DefaultSCSettingsYes" onchange="ViewDefaultSCSettings()" value="1">
                                            <label class="form-check-label">
                                                Yes
                                            </label>
                                        </div>
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="DefaultSCSettings" onchange="ViewDefaultSCSettings()" value="0" checked>
                                            <label class="form-check-label">
                                                No
                                            </label>
                                        </div>
                                    </div>										
                                </div>
                                            
                                <div class="row" id="DisplayDefaultSCOptions">
                                    <div class="col-sm-5 col-form-label">
                                        <label data-toggle="tooltip" data-placement="left" title="need to fill in.">
                                        MSC </label>
                                    </div>

                                    <div class="col-sm-7">
                                        <div class="form-group">
                                            <select class="form-control" name="default_SC" id="DefaultSCChoice" onchange="toggleDefaultSCSettings()">
                                                <option value="AVN" selected>Aviation</option>
                                                <option value="LM" >Land and Maritime</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>

                                <div class="row subheader">
                                    <div class="col-sm-auto">
                                        <span>Simulation Level</span>
                                    </div>
                                </div>  

                                <div class="row">
                                    <div class="col-sm-5 col-form-label">
                                        <label for="SSA_SC" data-toggle="tooltip" data-placement="left" title="Would you like to use the Aviation or LM SSA Cage Mapping to determine SSA NIINs?.">
                                        SSA Cage Mapping </label>
                                    </div>

                                    <div class="col-sm-7">
                                        <div class="form-group">
                                            <select class="form-control" name="ssa_sc_cage_mapping" id="SSA_SC">
                                                <option value="AVN" selected>Aviation</option>
                                                <option value="LM" >Land and Maritime</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>
                                

                                <div class="row subheader">
                                    <div class="col-sm-auto">
                                        <span>Scenario Level</span>
                                    </div>
                                </div>

                                <div class="row">
                                    <div class="col-sm-5 col-form-label">
                                        <label for="default_aaa_params" data-toggle="tooltip" data-placement="left" data-html="true" data-placement="left" title="fill out.">
                                            Default AAA Scenario Parameters </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class="form-group">
                                            <select class="form-control" name="default_aaa_params" id="default_aaa_params" onchange=forceAAAscenParams()>                                              
                                                <option value="AAA_AVN">Aviation</option>
                                                <option value="AAA_LM">Land and Maritime</option>
                                                <option value="No" selected>Custom Scenario Values</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>

                                <div class="row">
                                    <div class="col-sm-5">
                                        <label for="pen_CPS_buffer_all" data-toggle="tooltip" data-placement="left"
                                        title="This threshold controls the release of PRs for CPS items by waiting to order until the 
                                               Effective OH quantity equals a given percentage of the CPS Buffer (i.e., MaxOH).
                                               To simulate Aviation's current strategy, which is to NOT wait, enter '100' in the box.
                                               To simulate LM's current strategy, which is to wait until EffOH = 85% of MaxOH, enter '85'.">
                                        CPS Buffer Penetration Threshold</label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class="form-group">
                                            <select class="form-control" name="penetrate_CPS_buffer_all" id="pen_CPS_buffer_all" onchange=UpdateMasterCPSthresh()>                                              
                                                <option value="AVNlvl" selected>Aviation: 100%</option>
                                                <option value="LMlvl">Land and Maritime: 85%</option>
                                                <option value="Customlvl">Custom Scenario Values</option>
                                            </select>
                                        </div>
                                    </div>
                                </div> 

                            </div>
                        </div>
                    </div>

                    <div class="card" id=displayadmin style="display:none">
                        <div class="card-header">
                            <button class="btn btn-link" type="button" data-toggle="collapse"
                                    data-target="#collapseThree" aria-expanded="true" aria-controls="collapseThree" onclick="showCard('collapseThree')">
                                <i class="fa fa-chevron-down"></i>
                                Admin: Advanced Options
                            </button>
                        </div>

                        <div id="collapseThree" class="collapse show" aria-labelledby="headingThree">
                            <div class="card-body">

                            <div class="form-group row">
                                    <label class="col-sm-5 col-form-label">
                                        Default BCA Run Date
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="This is your BCA run date.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                    </label>
                                    <div class="col-sm-7 input-group">
                                        <input class="form-control non-input" name="run_date"
                                            style="background-color: #f5f5f5;"
                                            autocomplete="off" type="date" id="todaysbcadate" readonly>
                                    </div>
                                </div>

                                <div class="form-group row">
                                    <label class="col-sm-5 col-form-label">
                                        Default SIG Run Date
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="This is your SIG run date.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                    </label>
                                    <div class="col-sm-7 input-group">
                                        <input class="form-control non-input" name="sig_rundate"
                                            style="background-color: #f5f5f5;"
                                            autocomplete="off" type="date" id="todayssigdate" readonly>
                                    </div>
                                </div>
                                
                                <div class="form-group row">
                                    <label class="col-sm-5 col-form-label">
                                        Input Location
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="Enter the path to the parent directory where you'd like to input.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                    </label>
                                    <div class="col-sm-7 input-group">
                                        <input type="text" class="form-control" id="indir" name="indir"
                                               value="/home/users/&sysuserid/sasviyadata/&msc/users/&sysuserid/My_Simulations/sBCA/inputs" maxlength="320" minlength="35">
                                    </div>
                                </div>

                                <div class="form-group row">
                                    <label class="col-sm-5 col-form-label">
                                        Output Location
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="Enter the path to the parent directory where you'd like to output your results.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                    </label>
                                    <div class="col-sm-7 input-group">
                                        <input type="text" class="form-control" id="outdir" name="outdir"
                                               value="/home/users/&sysuserid/sasviyadata/&msc/users/&sysuserid/My_Simulations/sBCA/results" maxlength="320" minlength="35">
                                    </div>
                                </div>

                                <div class="row">
                                    <div class="col-sm-5 col-form-label">
                                        <label for="codeBases">Code Base
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="Choose your codebase.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class="form-group">
                                            <select class="form-control" id="codeBases" name="SAS_CODE_BASE" onchange="togglecustomcodepath()">
                                                <option value="production" selected>Production</option>
                                                <option value="personal" hidden>Personal</option>
                                                <option value="custom_path">Custom Path</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>

                                <div class="row" id="hidecodepath" >
                                    <div class="col-sm-5 col-form-label">
                                        <label>
                                            Code Base Path
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Provide your codebase path.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <input type="text" class="form-control" name="custom_path"
                                            value="/home/users/&sysuserid/sasviyadata/&msc/users/&sysuserid/My_Simulations/code/aaa" maxlength="300" minlength="30">
                                    </div>
                                </div>
                                
                                <!-- <div class="row">
                                    <div class="col-sm-5">
                                        <label data-toggle="tooltip" data-placement="left" 
                                                        title="Run your Simulation using previously sourced data. Be sure to use Simulation parameters that are identical to the parameters of the original Simulation.">
                                                Use previously sourced data</label>
                                            </div>
                                                <div class="col-sm-7 form-group">
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="ref_prev_src_data" id="RefprevsourceYes" onchange="toggleRefPrevSource()" value="1">
                                                        <label class="form-check-label">
                                                            Yes
                                                        </label>
                                                    </div>
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="ref_prev_src_data" id="RefprevsourceNo" onchange="toggleRefPrevSource()" value="0" checked>
                                                        <label class="form-check-label">
                                                            No
                                                        </label>
                                                    </div>
                                                </div>										
                                            </div>	 -->
                                            
                                            <div class="row" id="hideRefprevpath1" hidden>
                                                <div class="col-sm-5 col-form-label">
                                                    <label for="pathtodata" data-toggle="tooltip"
                                                    data-placement="left" title="Please enter the path directly to the bca_source folder of the Simulation you'd like to reference.">
                                                    Path to previously sourced data</label>
                                                </div>
                                                <div class="col-sm-7">
                                                    <input type="text" class="form-control" name="prev_src_path"
                                                        onchange="pathNumCheck(this.value)" value="/sasdata/nonfinance/users/&userid./my_aaa_files/results/[prev_simultion_name]/source" maxlength="300" minlength="30">
                                                </div>
                                                <div class="col-sm-5" id="run_tbl_lvl"> 
                                                    <label data-toggle="tooltip" data-placement="left" 
                                                                        title="need to fill out tooltip.">
                                                                Run <i>table</i> level comparisons?</label>
                                                </div>
                                                <div class="col-sm-7 form-group">
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="run_table_lvl_comp" id="run_tbl_lvl_y" value="1" onchange="forcetablecomp()">
                                                        <label class="form-check-label">
                                                            Yes
                                                        </label>
                                                    </div>
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="run_table_lvl_comp" value="0" onchange="forcetablecomp()" checked>  
                                                        <label class="form-check-label">
                                                            No
                                                        </label>
                                                    </div>
                                                </div> 
                                                <div class="col-sm-5" id="run_var_lvl">
                                                    <label data-toggle="tooltip" data-placement="left" 
                                                                        title="need to fill out tooltip.">
                                                                Run <i>variable</i> level comparisons?</label>
                                                </div>
                                                <div class="col-sm-7 form-group" id="run_var_lvl_opt">
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="run_var_lvl_comp" value="1" onchange="forcetablecomp()">
                                                        <label class="form-check-label">
                                                            Yes
                                                        </label>
                                                    </div>
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="run_var_lvl_comp" value="0" onchange="forcetablecomp()" checked>  
                                                        <label class="form-check-label">
                                                            No
                                                        </label>
                                                    </div>
                                                </div>
                                            </div>

                                            <div class="row">
                                                <div class="col-sm-5">
                                                    <label>
                                                        Output bca_temp tables
                                                        <span data-toggle="tooltip" data-placement="right"
                                                            title="Would you like to print tables to your bca_temp folder or would you like to save space by writing the tables to work?">
                                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                        </span>
                                                    </label>
                                                    </div>
                                                    <div class="col-sm-7 form-group">
                                                        <div class="form-check form-check-inline">
                                                            <input class="form-check-input" type="radio" name="keep_temp_tables" value="1" checked>
                                                            <label class="form-check-label">
                                                                Yes
                                                            </label>
                                                        </div>
                                                        <div class="form-check form-check-inline">
                                                            <input class="form-check-input" type="radio" name="keep_temp_tables" value="0">
                                                            <label class="form-check-label">
                                                                No
                                                            </label>
                                                        </div>
                                                    </div>										
                                            </div>

                                            <div class="row" id="runTripleATest">
                                                <div class="col-sm-5">
                                                    <label>
                                                        Run AAA Tests
                                                        <span data-toggle="tooltip" data-placement="right"
                                                            title="Would you like to run Automated AAA Tests? (Gut Check / Integration Test)">
                                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                        </span>
                                                    </label>
                                                </div>
                                                <div class="col-sm-7 form-group">
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="run_aaa_tests" value="1">
                                                        <label class="form-check-label">
                                                            Yes
                                                        </label>
                                                    </div>
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="run_aaa_tests" value="0" checked>
                                                        <label class="form-check-label">
                                                            No
                                                        </label>
                                                    </div>
                                                </div>										
                                            </div>

                                            <div class="row" id="partial_aaa" hidden>
                                                <div class="col-sm-5">
                                                    <label for="full_or_partial_aaa" data-toggle="tooltip" data-placement="left" 
                                                                        title="Would you like to print tables to your bca_temp folder or would you like to save space by writing the tables to work?">
                                                                Would you like to run a full or partial AAA run?</label>
                                                    </div>
                                                    <div class="col-sm-7 form-group">
                                                        <div class="form-check form-check-inline">
                                                            <input class="form-check-input" type="radio" name="full_or_partial_aaa" value="FULL" onchange="toggleaaaniinpopsize()" checked>
                                                            <label class="form-check-label">
                                                                Full
                                                            </label>
                                                        </div>
                                                        <div class="form-check form-check-inline">
                                                            <input class="form-check-input" type="radio" name="full_or_partial_aaa" id="run_a_partial_aaa" onchange="toggleaaaniinpopsize()" value="PARTIAL">
                                                            <label class="form-check-label">
                                                                Partial
                                                            </label>
                                                        </div>
                                                    </div>										
                                            </div>
                                            <div class="row" id="testMode" hidden>
                                                <div class="col-sm-5 col-form-label">
                                                    <label for="AAATestMode">Test Mode</label>
                                                </div>
                                                <div class="col-sm-7">
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="SAVE_Test_mode"
                                                               onchange="changeAAATestMode()" id="AAATestModeYes" value="yes" checked>
                                                        <label class="form-check-label">
                                                            Yes
                                                        </label>
                                                    </div>
                                                    <div class="form-check form-check-inline">
                                                        <input class="form-check-input" type="radio" name="SAVE_Test_mode"
                                                               onchange="changeAAATestMode()" id="AAATestModeNo" value="no">
                                                        <label class="form-check-label">
                                                            No
                                                        </label>
                                                    </div>
                                                </div>
                                            </div>
            
                                                <div class="row checkBoxMargin" id="fullAAAbox" hidden>
                                                    <div class="col-sm-5">
                                                        <label for="fullAAA">Full AAA Test</label>
                                                    </div>
                                                    <div class="col-sm-7">
                                                        <div class="form-check form-check-inline">
                                                            <input class="form-check-input" type="radio" name="SAVE_Full_AAA"
                                                                   onchange="changeAAATestPop()" id="fullAAAYes" value="yes">
                                                            <label class="form-check-label">
                                                                Yes
                                                            </label>
                                                        </div>
                                                        <div class="form-check form-check-inline">
                                                            <input class="form-check-input" type="radio" name="SAVE_Full_AAA"
                                                                   onchange="changeAAATestPop()" id="fullAAANo" value="no" checked>
                                                            <label class="form-check-label">
                                                                No
                                                            </label>
                                                        </div>
                                                    </div>
                                            </div>
                                            <div class="form-group row checkBoxMargin" id="NIINRange" hidden>
                                                <label for="NIINRange" class="col-sm-5 col-form-label">NIIN Range</label>
                                                <div class="col-sm-7">
                                                    <input type="number" class="form-control" name="SAVE_NIINRange" value="20"
                                                           >
                                                </div>
                                            </div>
                                            <div class="row" id="aaasimparam">
                                                <div class="col-sm-5">
                                                    <label for="aaasimparam">Alternate Scenarios</label>
                                                </div>
                                                <div class="col-sm-7">
                                                    <div class="form-check">
                                                        <input class="form-check-input" type="checkbox" name="AAA_Simparam"
                                                               id="simp" value="yes" checked>
                                                        <label class="form-check-label" for="simp">
                                                            Use the AAA Default
                                                        </label>
                                                    </div>
                                                </div>
                                            </div>
                                            <div class="row checkboxMargin" hidden>
                                                <div class="col-sm-10">
                                                    <label for="uniqId" data-toggle="tooltip" data-placement="left"
                                                           title="Check to simulate alternate scenario(s) demand/forecast using methods different than those of the baseline scenario. Options appear in each alternate scenario on next page.">
                                                        Simulate Unique Scenario Forecast/Demand in Alternate Scenarios
                                                    </label>
                                                </div>
                                                <div class="col-sm-2 simLeft uni">
                                                    <div class="form-check">
                                                        <input class="form-check-input" type="checkbox" id="uniqId"
                                                               onclick="showHideForecast()" name="scen_uniq_fcst" value="1">
                                                    </div>
                                                </div>
                                            </div>
            
                                            <div class="row" id="trunc_pop" >
                                                <div class="col-sm-5">
                                                    <label data-toggle="tooltip" data-placement="left"
                                                    title="need to fill in.">
                                                    Truncated AAA Pop Size</label>
                                                </div>
                                                <div class="col-sm-7 uctper">
                                                    <div class="input-group">
                                                        <input class="form-control"
                                                                type="number" placeholder="50" step="5" id="truncated_value"
                                                                min="50" max="400000" name="truncated_aaa_pop" 
                                                                maxlength="6" minlength="1">
                                                        <div class="input-group-append">
                                                            <span class="input-group-text"></span>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div> 

                                        </div>
																
                            </div>
                        </div>


                    <div class="card">
                        <div class="card-header" id= "addtlsimtitle">
                            <button class="btn btn-link" type="button" data-toggle="collapse"
                                    data-target="#collapseFour" data-toggle="collapse" aria-expanded="true" aria-controls="collapseFour" onclick="showCard('collapseFour')">
                                <i class="fa fa-chevron-down"></i>
                                Additional Simulation Options
                            </button>
                        </div>
                        <div id="collapseFour" class="collapse show" aria-labelledby="headingFour">
                            <div class="card-body">
 
                                <div class="row">
                                    <div class="col-sm-5 col-form-label">
                                        <label>
                                            LTC Data Source
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Select an LTC Data Source: 
                                                OA Extract: Aviation LTC Source. 
                                                OA Header/OA Line: L&M LTC Source.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class="form-group">
                                            <select class="form-control" name="LTC_Source" id="ltc_data_source"
                                                    onchange="LTCDataSourceChange()">
                                                <option value="OAExtract" selected>OA Extract</option>
                                                <option value="OAHeader">OA Header/OA Line</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>

                                <div class="row">
                                    <div class="col-sm-5 col-form-label">
                                        <label>
                                            Default Simulation Parameters
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Default Simulation parameters, such as inventory holding costs and delivery order costs, can be manually edited via the downloadable Excel workbook.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class = "form-check form-check-inline">
                                        <input class="form-check-input zero" type= "checkbox" id="FlexInputType" onchange="editparamChange()" value="0" unchecked>
                                        <label class="form-check-label">
                                            Edit Parameters
                                        </label>
                                    </div>
                                    </div>
                                </div>

                                <div class="row">
                                    <div class="col-sm-5 col-form-label">
                                        <label>
                                            Cost Factor Rate
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Selecting this option will apply the appropriate Cost of Capital and Storage inventory types based on the current or legacy fiscal year.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class="form-group">
                                            <select 
                                            class="form-control" 
                                            name="Cost_Factor_Rate" 
                                            id="costFactorRate"
                                            onchange="costFactChange();"
                                            >
                                            <option value="FY25">FY25</option>
                                            <option value="LEGACY">Legacy</option>
                                            </select>
                                            <input type="hidden" name="COC_Inv_Type" id="costOfCapital" value="OBL_INV_VAL">
                                            <input type="hidden" name="Stor_Inv_Type" id="storage" value="CUBIC">
                                        </div>
                                    </div>
                                </div>

                                <div class="row" id ="editParamText" style="display:none;">
                                    <div class="col-sm-auto">
                                    <label>
                                        To update the Default Simulation Parameters:
                                    </label>
                                    <br>
                                    <p> 1. Log into SAS Studio </p>
                                    <p></p>
                                    <p> 2. Download the following file: <br><b>/home/users/&userid./sasviyadata/&msc./users/&userid.<br>/My_Simulations/sBCA/inputs/Flexible_Inputs_Default.xlsx </b></p>
                                    <p></p>
                                    <p> 3. Apply desired parameter changes </p>
                                    <p></p>
                                    <p> 4. Re-upload edited file to: <br><b>/home/users/&userid./sasviyadata/&msc./users/&userid.<br>/My_Simulations/sBCA/inputs</b></p>
                                    <p> (Replacing existing Flexible_Inputs_Default.xlsx) </p>
                                    <p></p>
                                </div>
                                </div>
                                <div class="row" id="simParamVal">
                                    <div class="col-sm-auto">
                                        <label class="uploadSpacing">
                                            To update the Default Simulation Parameters, log into SAS Studio, and upload your updated Simulation Parameters to this (case-sensitive!) path:
                                        </label>
                                        <p>my_aaa_files/inputs/Flexible_Inputs_Default.xlsx</p> <br>
                                    </div>
                                </div>
                                <div class="row" hidden>
                                    <div class="col-sm-5">
                                        <label for="unit" data-toggle="tooltip" data-placement="left"
                                               title="Select which unit cost type the Simulator should use to assess inventory and procurement costs.">
                                            Unit Cost Type</label>
                                    </div>
                                    <div class="col-sm-7">
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" id="unit" onchange="showShouldCost()"
                                                   name="SAVE_unit_cost" value="Cost Basis" checked>
                                            <label class="form-check-label">
                                                Cost Basis Price
                                            </label>
                                        </div>
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" id="unit" onchange="showShouldCost()"
                                                   name="SAVE_unit_cost" value="Custom">
                                            <label class="form-check-label">
                                                Custom
                                            </label>
                                        </div>
                                    </div>
                                </div>
                                <div class="form-group row">
                                    <div class="col-sm-5"></div>
                                    <div class="col-sm-7">
                                        <div id="shouldCostMessage">
                                            To provide Custom Prices, log into SASStudio and edit
                                            the ShouldCost.xlsx located at: <i>Save_SCPath</i>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="row" hidden>
                                    <div class="col-sm-5 col-form-label yoy">
                                        <label for="pernum" data-toggle="tooltip" data-placement="left"
                                        title="The Simulator will increase the unit cost by the given percent compounded annually.">
                                        Increase Unit Cost YoY by (%)</label>
                                    </div>
                                    <div class="col-sm-7 uctper">
                                        <div class="input-group">
                                            <input class="form-control" type="number" id="pernum"
                                                   value="0" step="0.1" name="pct_yoy_cost_inf_0">
                                            <div class="input-group-append">
                                                <span class="input-group-text">%</span>
                                            </div>
                                        </div>
                                    </div>
                                </div>

                                
                                <div class="row">                                
                                    <div class="col-sm-5"> 
                                        <label>
                                            Exclude delinquent POs from on hand inventory
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="By default, the simulation excludes all delinquent POs great than 180 days delinqent from OH inventory to align with Planning Policy. This option can be adjusted to include all deliquent POs or can be adjusted to set a custom delinquent date.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7 form-group">
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="exclude_old_POs" id="exc_old_PO" value="1" onchange="showDate()" checked>
                                            <label class="form-check-label">
                                                Yes, exclude delinquent POs with planned delivery dates before selected date below
                                            </label>
                                        </div>
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="exclude_old_POs" value="inc_old_PO" onchange="showDate()">  
                                            <label class="form-check-label">
                                                No, include all delinquent POs
                                            </label>
                                        </div>
                                    </div>                               
                                </div>

                                <div class="form-group row" id="ifExcludeCheckedPO">
                                    <label class="col-sm-5 col-form-label">
                                        Exclude delinquent POs scheduled to deliver before
                                    </label>
                                    <div class="col-sm-7 input-group" id="ifExcludeCheckedPO1">
                                        <input class="form-control" onblur="getDatePickedPO()" 
                                            name="exclude_POs_before_date" type="date" id="datepickerPO">
                                    </div>
                                </div>
                                
                                <div class="row">                                                                                            
                                    <div class="col-sm-5"> 
                                        <label>
                                            Exclude delinquent PRs from on hand inventory?
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="By default, the simulation includes all delinquent PRs to align with Planning Policy. This option can be adjusted to exclude deliquent PRs based on a custom delinquent date.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7 form-group">
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="exclude_old_PRs" id="exc_old_PR" value="1" onchange="showDate()">
                                            <label class="form-check-label">
                                                Yes, exclude delinquent PRs with delivery dates before selected date below
                                            </label>
                                        </div>
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="exclude_old_PRs" value="0" onchange="showDate()" checked>  
                                            <label class="form-check-label">
                                                No, include all delinquent PRs
                                            </label>
                                        </div>
                                    </div>                                    
                                </div>          

                                <div class="form-group row" id="ifExcludeCheckedPR">
                                    <label for="ifExcludeChecked" class="col-sm-5 col-form-label" data-toggle="tooltip" data-placement="left"
                                    data-toggle="tooltip" data-placement="left" title="By default, the simulation will exclude all PRs that were scheduled to be received over 90 days ago.">
                                        Exclude delinquent PRs scheduled to deliver before</label>
                                    <div class="col-sm-7 input-group" id="ifExcludeCheckedPR1">
                                        <input class="form-control" onblur="getDatePickedPR()" 
                                            name="exclude_PRs_before_date" type="date" id="datepickerPR">
                                    </div>
                                </div>

                                <div class="row checkBoxMargin">
                                    <div class="col-sm-5">
                                        <label>
                                            Exclude Manual Workload Costs for items that have historically been Auto Awarded?
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="Selecting this option excludes manual workload costs for transactional PRs that are generated for items with historical auto-award history over a specified percentage.">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </label>
                                    </div>
                                    <div class="col-sm-7 form-group" id="procActivity">
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="auto_awd_hist_manual_wrkld_adj"  id="auto_awd_hist_manual_wrkld_adj" value="1" onchange="toggleProcActiv()" checked>
                                            <label class="form-check-label">
                                                Yes
                                            </label>
                                        </div>
                                        <div class="form-check form-check-inline">
                                            <input class="form-check-input" type="radio" name="auto_awd_hist_manual_wrkld_adj"  id="ProcActivNo" value="0" onchange="toggleProcActiv()" checked>

                                            <label class="form-check-label">
                                                No
                                            </label>
                                        </div>
                                    </div>
			            </div>
                            <div class="row" id="histAdj">
                                <div class="col-sm-5  col-form-label histAdjMargin">
                                    <label style=padding-left:33px;>
                                    Auto Award Procurements Threshold</label>
                                </div>
                                <div class="col-sm-5 uctper">
                                    <div class="input-group">
                                        <input class="form-control" type="number" id="perThreshold"
                                               value="0" step="1.0" min="0" max="100.00" name="auto_po_threshold" onblur="validateInput(this)">
                                        <div class="input-group-append">
                                            <span class="input-group-text">%</span>                                           
                                    	</div>
                                    </div>
                           	</div>
                            	</div>
                                
                                
                            <div class="row checkBoxMargin">
                                <div class="col-sm-5">
                                    <label id="licdurcap" class="normalLabel">
                                        Upload window for Custom Forecast/Item Attribute Changes
                                        <span data-toggle="tooltip" data-placement="right"
                                            title="This option is only used when executing a custom monthly forecast or custom item attribute change and defines how long the simulation will pause for to allow time to upload files. See Standard BCA Custom Forecast and Line Item Changes User Guides in Help Documentation.">
                                            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                        </span>
                                    </label>
                                </div>
                            <div class="col-sm-7">
                                <div class="input-group" id="licdur">	
                                    <input class="form-control auto-default-min" value="10" id="licdurshow" type="number" min="1" max="240" name="simpausetime" placeholder="Enter Minutes..." onblur="validateInput(this)">
                                    <div class="input-group-append">
                                        <span class="input-group-text minAppend">min</span>
                                    </div>
                                </div>   
                            </div>   
                            </div>  
                            </div>


</div>
                            </div>
                        </div>        
                        </div>

                        <div class="card" id="accord2" >
                            <div class="card-header" id="outputtitle">
                                <button class="btn btn-link" type="button" data-toggle="collapse"
                                        data-target="#collapseFive" aria-expanded="true" aria-controls="collapseFive" onclick="showCard('collapseFive')">
                                    <i class="fa fa-chevron-down"></i>
                                    Output Options
                                </button>
                            </div>
                            <div id="collapseFive" class="collapse show" aria-labelledby="headingFive">
                                <div class="card-body">
                                    <div class="row">
                                        <div class="col-sm-5 col-form-label">
                                            <label>
                                                Simulation Analysis Type
                                                <span data-toggle="tooltip" data-placement="right"
                                                    title="
                                                    Aviation AAA Report: Standard AAA output reports by NIIN and Month for each scenario.
                                                    L&M AAA Report: Standard AAA output reports by NIIN and Month for each scenario.
                                                    Standard Analysis: Generates simulation output reports by NIIN and Month. 
                                                    Pipeline Report: Generates an inventory / net asset summary by NIIN (Schedrcpts, Backorders, etc).
                                                    Vendor Forecast Report: Generates simulation outputs by Vendor.

                                                    Note: AAA reports are only available for AAA Simulations.">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                </span>
                                            </label>
                                        </div>

                                        <!-- Output Options: Simulation Analysis Type -->
                                        <div class="col-sm-7">
                                            <div id="outBCA" class="form-group">
                                                <select class="form-control" id="simAnalysisType" name="output_report"
                                                        onchange="reporttypedependecies();">
                                                    <option value="STANDARD_ANALYSIS">Standard Analysis</option>
                                                    <!-- <option value="BAU_Report">Business as Usual Report</option> -->
                                                    <option value="LM_PIPELINE_REPORT">Pipeline Report</option>
                                                    <option value="VENDOR_FORECAST">Vendor Forecast Report</option>
                                                    <option value="AVN_AAA_REPORT" hidden>Aviation AAA Report</option>
                                                    <option value="LM_AAA_REPORT" hidden>L&M AAA Report</option>                                                
                                                </select>
                                                <select class="form-control" id="simAnalysisType2" name="save_Type"
                                                    >
                                                    <option value="AVN_AAA_REPORT">Aviation AAA Report</option>
                                                    <option value="LM_AAA_REPORT">L&M AAA Report</option>
                                                </select>
                                            </div>
                                                
                                        </div>

                                    </div>

                                    <!-- Output Options: Simulation Analysis Type Function Call -->
                                    <!-- <script>
                                        simulationAnalysisType(true);
                                    </script> -->

                                    <div class="row">
                                        <div class="col-sm-5 col-form-label">
                                            <label>
                                                PR Table Cutoff
                                                <span data-toggle="tooltip" data-placement="right"
                                                    title="
                                                    This option filters all scenario PR Tables based on the date selected:

                                                    PR Generation Date: Any PRs generated within the simulation duration are included in the PR table even in cases where the OA Consumption Date is beyond the simulation horizon.
                                                    OA Consumption Date: Any PRs with OA Consumption Dates beyond the end of simulation duration are excluded from the PR Table.

                                                    Note: This option does not impact total OA spend in final output reports. 
                                                    ">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                </span>
                                            </label>
                                        </div>
                                        <div class="col-sm-7">
                                            <div class="form-group">
                                                <select class="form-control" id="PRTableCutoff" name="PRTableCutoff">
                                                    <option value="PRGENDATE_MO">PR Generation Date</option>
                                                    <option value="OACONSDATE_MO">OA Consumption Date</option>
                                                </select>
                                            </div>
                                        </div>
                                    </div>

                                    <div class="row">
                                        <div class="col-sm-5">
                                            <label>
                                                Output Unit of Measure
                                                <span data-toggle="tooltip" data-placement="right"
                                                    title="The selected unit of measure determines the units for final output reports.">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                </span>
                                            </label>
                                        </div>
                                        <div class="col-sm-7">
                                            <div class="form-check form-check-inline">
                                                <input class="form-check-input" type="radio" name="Output_UOM" value="SALES" checked>
                                                <label class="form-check-label">
                                                    Sales Unit
                                                </label>
                                            </div>
                                            <div class="form-check form-check-inline">
                                                <input class="form-check-input" type="radio" name="Output_UOM" value="BASE">
                                                <label class="form-check-label">
                                                    Base Unit
                                                </label>
                                            </div>
                                        </div>
                                    </div>

                                    <!-- Savings Calc --><!--  
                                    <div class="row">
                                        <div class="col-sm-5">
                                            <label for="underAAA" data-toggle="tooltip" data-placement="left"
                                                   title="Select which savings calculation the Simulator should use. This defaults to OA Consumption Date.">
                                                Savings Calculation</label>
                                        </div>
                                        <div class="col-sm-7">
                                            <div class="form-check form-check-inline">
                                                <input class="form-check-input" type="radio" name="output_date" value="OACONSDATE" checked>
                                                <label class="form-check-label">
                                                    OA Consumption Date
                                                </label>
                                            </div>
                                            <div class="form-check form-check-inline">
                                                <input class="form-check-input" type="radio" name="output_date" value="PRGENDATE_MO">
                                                <label class="form-check-label">
                                                    PR Generation Date
                                                </label>
                                            </div>
                                        </div>
                                    </div>-->

                                    <div class="row subheader subheaderMargin2">
                                        <div class="col-sm-auto">
                                            <span> Additional Outputs & Analyses </span>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <legend class="col-form-label col-sm-5 pt-0">
                                            Check to create the desired additional outputs and/or analyses in Excel.
                                            <span data-toggle="tooltip" data-placement="right"
                                                title="
                                                Aggregate TPIP: Select to produce a PDF summary of population-level TPIPs for each scenario.
                                                Supply Chain Breakout: Select to produce outputs (Spend, IHC, Manual Workload, etc.) for each scenario by supply chain.
                                                NIIN Month PR Breakout: Select to produce PR reports at the NIIN-Month level for each scenario.
                                                ">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                            </span>
                                        </legend>
                                        <div class="col-sm-7 agg">
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="Agg_TPIP"
                                                       value="1" id="tpip" unchecked>
                                                <label class="form-check-label" for="tpip">
                                                    Aggregate TPIP
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="SCBREAKOUT"
                                                       value="1" id="scb" unchecked>
                                                <label class="form-check-label" for="scb">
                                                    Supply Chain Breakout
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="PRBREAKOUT"
                                                       value="1" id="prbo" unchecked>
                                                <label class="form-check-label" for="prbo">
                                                    NIIN Month PR Breakout
                                                </label>
                                                <br>
                                            </div>
                                        </div>
                                    </div>
                                    <hr>
                                    <div class="row subheader">
                                        <div class="col-sm-auto">
                                            <span> Excel Outputs </span>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <legend class="col-form-label col-sm-5 pt-0">
                                            Check to create the desired additional outputs in Excel Format.
                                        </legend>
                                        <div class="col-sm-7">
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsATTables"
                                                       value="1" id="att" checked>
                                                <label for="att" class="form-check-label">
                                                    Attributes Table
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsPRTables"
                                                       value="1" id="pr" checked>
                                                <label for="pr" class="form-check-label">
                                                    PR Tables
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsoutput"
                                                       value="1" id="fin" checked>
                                                <label for="fin" class="form-check-label">
                                                    Final Output
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsTPIPs"
                                                       value="1" id="tpipt" checked>
                                                <label for="tpipt" class="form-check-label">
                                                    TPIP Tables
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsnosim"
                                                       value="1" id="niin" checked>
                                                <label for="niin" class="form-check-label">
                                                    NIINs not Simulated
                                                </label>
                                                <br>
                                            </div>

                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsoptions"
                                                       value="1" id="usr" checked>
                                                <label for="usr" class="form-check-label">
                                                    User Options
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsj8fin"
                                                       value="1" id="j8val" checked>
                                                <label for="J8R" class="form-check-label">
                                                    J8 Financial Analysis Input Data
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlspricing"
                                                       value="1" id="priceval" checked>
                                                <label for="xPrice" class="form-check-label">
                                                    Pricing Output
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check">
                                                <input class="form-check-input" type="checkbox" name="xlsohoo"
                                                       value="1" id="xlsohoo" checked>
                                                <label for="xlsohoo" class="form-check-label">
                                                    On Hand/On-Order Report
                                                </label>
                                                <br>
                                            </div>
                                            <div class="form-check bauhover">
                                                <input class="form-check-input" type="checkbox"
                                                       name="SAVE_Hist_BAU_Analysis" value="Yes" id="bau">
                                                <label for="bau" id="bauText">Historical BAU</label>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="card" id="DisplayExecSig" style="display:none">
                                <div class="card-header">
                                    <button class="btn btn-link" type="button" data-toggle="collapse"
                                            data-target="#collapseSix" aria-expanded="true" aria-controls="collapseSix" onclick="showCard('collapseSix')">
                                        <i class="fa fa-chevron-down"></i>
                                        SIG Output Options
                                    </button>
                                </div>
        
                                <div id="collapseSix" class="collapse show" aria-labelledby="headingSix">
                                    <div class="card-body">

                                        <div class="row checkBoxMargin">
                                            <div class="col-sm-5">
                                                <label for="execSIG" data-toggle="tooltip" data-placement="left" title="need to fill out.">
                                                Execute SIG?</label>
                                            </div>
                                            <div class="col-sm-7 form-group" id="execSIG">
                                                <div class="form-check form-check-inline">
                                                    <input class="form-check-input" type="radio" name="run_sig" id="ExecSIGYes" onchange="toggleSIG()" value="1">
                                                    <label class="form-check-label">
                                                        Yes
                                                    </label>
                                                </div>
                                                <div class="form-check form-check-inline">
                                                    <input class="form-check-input" type="radio" name="run_sig" onchange="toggleSIG()" value="0" checked>
                                                    <label class="form-check-label">
                                                        No
                                                    </label>
                                                </div>
                                            </div>
                                        </div> 
                                        <hr id="DisplaySig0">
                                        <div class="row subheader" id="DisplaySig1">
                                            <div class="col-sm-auto">
                                                <span>SIG Simulation Level Parameters</span>
                                            </div>
                                        </div>  
        
                                        <div class="form-group row" id="DisplaySig2">
                                            <label for="run_name" class="col-sm-5 col-form-label">
                                                Rank Order
                                            </label>
                                            <div class="col-sm-7">
                                                <input type="text" class="form-control" id="rank_order" name="rank_order"
                                                    value="" placeholder="" maxlength="200" minlength="1">
                                            </div>
                                        </div>

                                        <div class="row checkBoxMargin" id="DisplaySig3">
                                            <div class="col-sm-5">
                                                <label for="execSIG" data-toggle="tooltip" data-placement="left" title="Refresh active project data with current simulation data.">
                                                    Refresh Active Projects</label>
                                            </div>
                                            <div class="col-sm-7 form-group" id="execSIG">
                                                <div class="form-check form-check-inline">
                                                    <input class="form-check-input" type="radio" name="refresh_active_projects" value="1" checked>
                                                    <label class="form-check-label">
                                                        Yes
                                                    </label>
                                                </div>
                                                <div class="form-check form-check-inline">
                                                    <input class="form-check-input" type="radio" name="refresh_active_projects" value="0">
                                                    <label class="form-check-label">
                                                        No
                                                    </label>
                                                </div>
                                            </div>
                                        </div> 

                                        <div class="row checkBoxMargin" id="DisplaySig4">
                                            <div class="col-sm-5">
                                                <label for="execSIG" data-toggle="tooltip" data-placement="left" title="Generate outputs used to generate Access DB for SSS (Default for LM runs).">
                                                Create SSS SIG Outputs</label>
                                            </div>
                                            <div class="col-sm-7 form-group" id="execSIG">
                                                <div class="form-check form-check-inline">
                                                    <input class="form-check-input" type="radio" name="aaa_data_outputs" id="accdb" value="1" checked>
                                                    <label class="form-check-label">
                                                        Yes
                                                    </label>
                                                </div>
                                                <div class="form-check form-check-inline">
                                                    <input class="form-check-input" type="radio" name="aaa_data_outputs" id="accdb" value="0">
                                                    <label class="form-check-label">
                                                        No
                                                    </label>
                                                </div>
                                            </div>
                                        </div> 
                                        <hr id="DisplaySig5">
                                        <div class="row subheader" id="DisplaySig6">
                                            <div class="col-sm-auto">
                                                <span>SIG Scenario Level Parameters</span>
                                            </div>
                                        </div>  
                                        
                                        <div class="form-group row" id="DisplaySig7">
                                            <div class="col-sm-5  col-form-label">
                                                <label data-toggle="tooltip"
                                                data-placement="left" title="Need to fill out.">
                                                Path to SIG scenario XML</label>
                                            </div>
                                            <div class="col-sm-7">
                                                    <input type="text" class="form-control" name="sig_scen_params" id="sig_scen_param_path"
                                                        value="" maxlength="320" minlength="35">
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>

                            <div class="card">
                                <div class="card-header" id="baselineoptions">
                                    <button class="btn btn-link" type="button" data-toggle="collapse"
                                            data-target="#collapseSeven" data-target="#collapseSeven" aria-expanded="true" aria-controls="collapseSeven" onclick="showCard('collapseSeven')">
                                        <i class="fa fa-chevron-down"></i>
                                        Baseline Scenario
                                    </button>
                                </div>
                                <div id="collapseSeven" class="collapse show" aria-labelledby="baselineoptions">
                                    <div class="card-body">
                                        <div class="row subheader">
                                            <div class="col-sm-auto">
                                                <span>Demand & Forecast Simulation Methods</span>
                                            </div>
                                        </div>
                                        <div class="row instructions">
                                            <div class="col-sm-auto">
                                                <span>
                                                    Please select a forecast/demand simulation method for each item
                                                    type:
                                                </span>
                                            </div>
                                        </div>
                                        <div class="row">
                                            <div class="col-sm-5 col-form-label">
                                                <label>
                                                    Forecast Based Replenishment
                                                    <span data-toggle="tooltip" data-placement="right"
                                                        title="
                                                        DFUtoSKU Forecast + 12 Month Fixed Avg: Leverages available DFUtoSKU forecast and extrapolates the forecast to the out
                                                        years by averaging the last 12 months of the DFUtoSKU forecast and applying that fixed monthly rate to all remaining
                                                        simulation months.
                                                        DFUtoSKU 12 Month Loop: Leverages available DFUtoSKU forecast and extrapolates the forecast to the out years by looping over the last 12 months of the DFUtoSKU forecast and applying to all remaining months.
                                                        Item Consumption Rate (ICR): An item's system ICR is used as the demand forecast.
                                                        Consumption History / 12: Item's consumption history as a monthly average is used as the demand forecast.
                                                        ADQ / 12: an item's Annual Demand Quantity as a monthly average is used as the demand forecast.
                                                        Custom Forecast: User can enter a custom forecast by item. See the Standard BCA Custom Forecast User Guide in Help Documentation.
                                                        ">
                                                        <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                    </span>
                                                </label>
                                            </div>
                                            <div class="col-sm-7">
                                                <div class="input-group">
                                                    <select class="form-control" id="fcst_type_rmcr_0" name="RMCR_FCST_DMD_TYPE_0" onchange="customCheck(this, 0);">
                                                        <option value="DFUAVG" selected>DFUtoSKU Forecast + 12 Month Fixed Avg</option>
                                                        <option value="DFULOOP">DFUtoSKU 12 Month Loop</option>
                                                        <option value="ICR">Item Consumption Rate (ICR)</option>
                                                        <option value="CONSUMPHIST">Consumption History / 12</option>
                                                        <option value="ADQ">ADQ / 12</option>
                                                        <option value="CUSTOM">Custom Forecast</option>
                                                    </select> 
                                                </div>
                                            </div>
                                        </div>
                                        <div class="row checkboxMargin">
                                            <div class="col-sm-5 col-form-label">
                                                <label>
                                                    Min/Max Replenishment
                                                    <span data-toggle="tooltip" data-placement="right"
                                                        title="
                                                        Item Consumption Rate (ICR): An item's system ICR is used as the demand forecast.
                                                        ADQ / 12: An item's Annual Demand Quantity as a monthly average is used as the demand forecast.
                                                        Consumption History / 12: Item's consumption history as a monthly average is used as the demand forecast.
                                                        Trailing 24 Month Demand Loop: Loops through the prior 24 months of demand for each month of the Simulation. Month 1 leverages historical demand.
                                                        Custom Forecast: User can enter a custom forecast by item. See the Standard BCA Custom Forecast User Guide in Help Documentation.    
                                                        ">
                                                        <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                    </span>
                                                </label>
                                            </div>
                                            <div class="col-sm-7">
                                                <div class="input-group">
                                                    <select class="form-control" id="dmd_type_rmcn_0" name="RMCN_FCST_DMD_TYPE_0" onchange="customCheck(this, 0);">
                                                        <option value="ICR">Item Consumption Rate (ICR)</option>
                                                        <option value="ADQ">ADQ / 12</option>
                                                        <option value="CONSUMPHIST">Consumption History / 12</option>
                                                        <option selected value="TRAIL24">Trailing 24 Month Demand Loop</option>
                                                        <option value="CUSTOM">Custom Forecast</option>
                                                    </select>
                                                </div>
                                            </div>
                                        </div>

                                        <div class="row checkboxMargin">
                                            <div class="col-sm-5 col-form-label">
                                                <label>
                                                    Customer Direct Replenishment
                                                    <span data-toggle="tooltip" data-placement="right"
                                                        title="
                                                        Item Consumption Rate (ICR): An item's system ICR is used as the demand forecast.
                                                        ADQ / 12: An item's Annual Demand Quantity as a monthly average is used as the demand forecast.
                                                        Consumption History / 12: Item's consumption history as a monthly average is used as the demand forecast.
                                                        Custom Forecast: User can enter a custom forecast by item. See the Standard BCA Custom Forecast User Guide in Help Documentation.
                                                        ">
                                                        <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                    </span>
                                                </label>
                                            </div>
                                            <div class="col-sm-7 gdphover">
                                                <div class="input-group">
                                                    <select class="form-control" id="dmd_type_rmcb_0" name="RMCB_FCST_DMD_TYPE_0" onchange="customCheck(this, 0);">
                                                        <option value="ICR">Item Consumption Rate (ICR)</option>
                                                        <option value="ADQ">ADQ / 12</option>
                                                        <option value="CONSUMPHIST">Consumption History / 12</option>
                                                        <option value="CUSTOM">Custom Forecast</option>
                                                    </select>
                                                </div>
                                            </div>
                                        </div>
                                        <!-- Commented out until we determine if we're going to include in UP and build out in BE if so -->
                                        <!--<div class="row checkboxMargin">
                                            <div class="col-sm-10">
                                                <label for="gdp" class="normalLabel" data-toggle="tooltip" data-placement="left"
                                                       title="Check to include Navy Gross Demand Plan as a portion of the simulated demand for nonforecastable items, where applicable.">
                                                    Include Navy Gross Demand Plan Input for Nonforecastable Items
                                                </label>
                                            </div>
                                            <div class="col-sm-2 gdphover">
                                                <div class="form-check">
                                                    <input class="form-check-input" type="checkbox" checked
                                                           name="Use_GDP_0" value="1" type="checkbox" id="gdp">
                                                </div>
                                                <br>
                                            </div>
                                        </div>-->
                                        <div class="row checkboxMargin">
                                            <div class="col-sm-10">
                                                <label class="normalLabel">
                                                    Ensure RMC B NIINs do not attrit below their Retail Protected Levels?
                                                 </label>
                                            </div>
                                            <div class="col-sm-2 simLeft uni">
                                                <div class="form-check">
                                                    <input class="form-check-input" type="checkbox" id="Use_RSO_0" name="Use_RSO_0"
                                                           value="1" checked>
                                                </div>
                                            </div>
                                        </div>

                                        <div class="row checkboxMargin">
                                            <div class="col-sm-10">
                                                <label class="normalLabel">
                                                    Include Dependent Demand?
                                                    <span data-toggle="tooltip" data-placement="right"
                                                        title="Selecting this option will include MTS kitting demand for component items.">
                                                        <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                    </span>
                                                 </label>
                                            </div>
                                            <div class="col-sm-2 simLeft uni">
                                                <div class="form-check">
                                                    <input class="form-check-input" type="checkbox" id="use_depdmd_0" name="use_depdmd_0" onchange="showDepDmd();"
                                                           value="1" checked>
                                                </div>
                                            </div>
                                        </div>

                                        <div class="row" id="extrap_demand_whole">
                                            <label class="col-form-label col-sm-5 pt-0">
                                                Dependent Demand Extrapolation Method
                                                <span data-toggle="tooltip" data-placement="right"
                                                    title="
                                                    Select a method to extrapolate dependent demand to component items beyond the available forecast for MTS kits:
                                                    
                                                    Fixed Average Forecast: Applies the monthly average of the last 24 months to all remaining simulation months.
                                                    Loop Forecast: Repeats the last 24 months of the forecast to all remaining simulation months.
                                                    ">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#bababa" d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM216 336h24V272H216c-13.3 0-24-10.7-24-24s10.7-24 24-24h48c13.3 0 24 10.7 24 24v88h8c13.3 0 24 10.7 24 24s-10.7 24-24 24H216c-13.3 0-24-10.7-24-24s10.7-24 24-24zm40-208a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"/></svg>
                                                </span>
                                            </label>
                                            <div class="col-sm-7" id="extrap_demand_methods">
                                                <div class="input-group">
                                                    <select class="form-control" id="extrap_depdmd_0" name="EXTRAP_DEPDMD_0">
                                                        <option value="DEP_AVG">Fixed Average Forecast</option>
                                                        <option value="DEP_LOOP">Loop Forecast</option>
                                                    </select>
                                                </div>
                                            </div>
                                        </div>


                                            <div class="row checkboxMargin" id="customMonthlyExtraQuestions0">
                                                <div class="col-sm-5 col-form-label">
                                                    <label class="customVal" data-toggle="tooltip" data-placement="left"
                                                    title="Provide Absolute or Percent Increase custom values by Month or by Year for selected Custom Monthly Forecast.">
                                                        Type of Custom Values Provided</label>
                                                </div>
                                                <div class="col-sm-4">
                                                    <div class="form-group">
                                                        <select class="form-control extraQuestion inputDate" id="custom_fcst_type_0" name="custom_fcst_type_0"
                                                                class="extraQuestion">
                                                            <option value="FIXED" selected>
                                                                Absolute
                                                                Monthly Demand
                                                            </option>
                                                            <option value="PERCENT">
                                                                Pct Change in
                                                                Monthly Demand
                                                            </option>
                                                        </select>
                                                    </div>
                                                </div>
                                                <div class="col-sm-2.5">
                                                    <div class="form-group">
                                                        <select class="form-control" id="custom_fcst_by_0" name="custom_fcst_by_0">
                                                            <option value="MONTH"selected>By Month</option>
                                                            <option value="YEAR">By Year</option>
                                                        </select>
                                                    </div>
                                                </div>
                                        </div>
                                        <!-- <hr> -->
                                        <div class="row subheader" hidden>
                                            <div class="col-sm-auto">
                                                <span>CPS Behavior</span>
                                            </div>
                                        </div>

                                        <div class="row" hidden>
                                            <div class="col-sm-5">
                                                <label for="pen_CPS_buffer_0" data-toggle="tooltip" data-placement="left"
                                                title="This threshold controls the release of PRs for CPS items by waiting to order until the 
                                                       Effective OH quantity equals a given percentage of the CPS Buffer (i.e., MaxOH).
                                                       To simulate Aviation's current strategy, which is to NOT wait, enter '100' in the box.
                                                       To simulate LM's current strategy, which is to wait until EffOH = 85% of MaxOH, enter '85'.">
                                                CPS Buffer Penetration Threshold</label>
                                            </div>
                                            <div class="col-sm-7 uctper">
                                                <div class="input-group">
                                                    <input class="form-control" value="100"
                                                            type="number" id="pen_CPS_buffer_0" value="" step="5" 
                                                            min="50" max="100" name="penetrate_CPS_buffer_0" 
                                                            placeholder="" maxlength="3" minlength="1">
                                                    <div class="input-group-append">
                                                        <span class="input-group-text">%</span>
                                                    </div>
                                                </div>
                                            </div>
                                        </div> 

                                    </div>
                                </div>
                            </div>
                        <div class="field_wrapper" id="added_scenarios" > </div>
                    </div>
                </div>
   				</form>
                    <div id="progbarhelp" class="bodyText">
                        <p class="intro">Your &LOGIN_TYPE simulation is <b>In Progress</b></p>
                        <p>When your simulation is complete, an email will be sent to <u>&Email.</u>. </p>
                        <p>If you selected Custom Forecast / Line Item Change options, an additional email will be sent with further instructions. </p>
                        <p class="intro"> You may now close this window </p>
                    </div>
                <div id="FlexInputModal" class="modal">
                    <div class="modal-content">
                        <p><span class="close">&times;</span></p>
                        <p class="modal-title">Download and Edit Input Parameters</p>
                        <br>
                        <p class="modal-text">Simulation parameters can be edited within the Flexible Input Excel file. </p>
                        <b><p id="LTCOption" class="modal-text"></p></b>
                        <!-- <p class="modal-text">To change your data source, close this message and use the LTC Data Source pulldown to make a selection.</p> -->
                        <br>
    
                        <form action="&_URL" method="POST" enctype="multipart/form-data" id="DownloadFlex">
                                <input type="hidden" id="FlexInput" value="ALL_LTC_NIIN_XLSX" name="Save_LTC_Source">
                                <input type="hidden" id="filePath2" name="save_FilePath" value="&save_FilePath.">
                                <input type="hidden" id="runMultiple2" name="save_run_multiple" value="&save_run_multiple.">
                                <input type="hidden" value="/Non Finance/Aviation/UP_UI/Production/Utility/downloadFlexInputs" name="_program">
                                <button class="btn btn-secondary" onclick="flexInSubmit()" type="submit">Download</button>
                        </form>
    
                        <p class="modal-text">
                        <br>Note: This download will occur in the background and may take a few minutes. 
                        </p>      
                    </div>
    
                 </div>


</body>
</html>

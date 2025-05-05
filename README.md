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

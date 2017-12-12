# koha-palci-loginas
Adds a "Login to PALCI as" button to the staff client patron view

## What is PALCI?
The Pennsylvania Academic Library Consortium, Inc.—better known as PALCI—formed in 1996 as a grassroots federation of 35 academic libraries in the Commonwealth of Pennsylvania.

Today, the PALCI membership consists of nearly 70 academic and research libraries, private and public, in Pennsylvania, New Jersey, West Virginia, and New York. Member institutions range from small liberal arts colleges to publicly funded universities to ARL institutions to the State Library of Pennsylvania. Libraries in PALCI have holdings in excess of 144 million and a combined FTE of more than 500,000 students.

PALCI’s mission is to build access through collaboration among academic libraries in Pennsylvania and the neighboring states. To do so, PALCI
* Coordinates resource-sharing through services such as E-ZBorrow and RapidILL
* Provides opportunities for cooperative purchasing of electronic resources from major vendors, such as Gale, ProQuest, Wiley, and many scholarly societies
* Leverages economy of scale to expand access to shared eBook collections through consortial DDA, EBA, subscription and bulk purchasing programs
* Collaborates on collection development and management initiatives, such as remote storage, a shared serials archive, digital collections, and disaster planning
* Fosters a program of free reciprocal faculty borrowing privileges among select member libraries
* Facilitates PA Digital, the state-wide initiative of cultural heritage institutions making Pennsylvania's extraordinary digital assets available to the world through the Digital Public Library of America 
* Promotes networking and professional development among academic library colleagues throughout the region

For more information about PALCI visit [the official PALCI site here](http://www.palci.org)

## What is the purpose of this repository?

This repository is to provide PALCI memberlibraries who use the [Koha ILS platform](https://koha-community.org/) with a way to authenticate as a patron into PALCI's E-ZBorrow interface (i.e. to instruct the patron on how to use the E-ZBorrow service) from the patron record screen of Koha's staff interface.

![PALCI as this user button](koha-palci-loginas-button.png?raw=true)

Initially, this button was created as a hard-coded patch  but thanks to [Kyle Hall](https://github.com/kylemhall), it is now much simpler to use pure JavaScript to add the button to every patron record!

    $(document).ready(function() {
    var data = $("div.patroninfo h5").html();
    var regExp = /\(([^)]+)\)/;
    var matches = regExp.exec(data);
    var cardnumber = matches[1];

    /* Replace 'INST-CODE' below with your PALCI institution code */
    $('<a id="palciLoginAs" target="_blank" class="btn btn-default btn-sm" href="https://e-zborrow.relaisd2d.com/service-proxy/?command=mkauth&LS=INST-CODE&PI=' + cardnumber + '"><i class="fa fa-search"></i> PALCI as this user</a>').insertAfter($('#addnewmessageLabel'));
    });

\<\!DOCTYPE html\>

\<html lang="en"\>

\<head\>

    \<meta charset="UTF-8"\>

    \<meta name="viewport" content="width=device-width, initial-scale=1.0"\>

    \<title\>Property Lock Box Management\</title\>

    \<script src="https://cdn.tailwindcss.com"\>\</script\>

    \<style\>

        /\* Custom styles if needed, though Tailwind is preferred \*/

        body {

            font-family: 'Inter', sans-serif;

            background-color: \#f4f7f6; /\* Light gray background \*/

        }

        .input-field {

            @apply mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm;

        }

        .btn {

            @apply py-2 px-4 rounded-md shadow-sm text-sm font-medium focus:outline-none focus:ring-2 focus:ring-offset-2 transition-colors duration-150 ease-in-out;

        }

        .btn-primary {

            @apply text-white bg-indigo-600 hover:bg-indigo-700 focus:ring-indigo-500;

        }

        .btn-secondary {

            @apply text-gray-700 bg-gray-200 hover:bg-gray-300 focus:ring-gray-400;

        }

        .th-cell {

            @apply px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider bg-gray-50 sticky top-0 z-10; /\* Added sticky for header \*/

        }

        .td-cell {

            @apply px-4 py-3 whitespace-nowrap text-sm text-gray-700 border-b border-gray-200;

        }

        /\* Modal styles \*/

        .modal-backdrop {

            @apply fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full flex items-center justify-center z-50;

        }

        .modal-content {

            @apply bg-white p-6 rounded-lg shadow-xl w-11/12 md:w-1/3 max-w-md mx-auto;

        }

        .modal-title {

            @apply text-xl font-semibold text-gray-700;

        }

        .modal-body {

            @apply text-gray-600 my-4;

        }

        .modal-close-button {

             @apply text-gray-400 hover:text-gray-600 transition-colors duration-150 ease-in-out;

        }

        .table-container { /\* Added for potentially scrollable table body \*/

            @apply max-h-\[60vh\] overflow-y-auto; /\* Adjust max-height as needed \*/

        }

    \</style\>

    \<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700\&display=swap" rel="stylesheet"\>

\</head\>

\<body class="bg-gray-100"\>

    \<div class="container mx-auto p-4 sm:p-6 lg:p-8"\>

        \<header class="mb-8 text-center"\>

            \<h1 class="text-3xl font-bold text-gray-800"\>Property Lock Box Management\</h1\>

            \<p class="text-sm text-gray-500 mt-1"\>Your User ID: \<span id="userIdDisplay" class="font-semibold"\>Loading...\</span\>\</p\>

        \</header\>

        \<\!-- Interactive Form for Data Entry (Conceptually the "First Table") \--\>

        \<section class="bg-white shadow-xl rounded-lg p-6 mb-8"\>

            \<h2 class="text-2xl font-semibold mb-6 text-gray-700 border-b pb-3"\>Enter New Lock Box Information\</h2\>

            \<\!-- Changed div to form \--\>

            \<form id="entryForm" class="space-y-6"\>

                \<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-x-6 gap-y-4"\>

                    \<div\>

                        \<label for="property" class="block text-sm font-medium text-gray-700"\>Property Name \<span class="text-red-500"\>\*\</span\>\</label\>

                        \<input type="text" id="property" class="input-field" placeholder="e.g., Main Street Complex" list="propertyDatalist"\>

                        \<datalist id="propertyDatalist"\>\</datalist\>

                    \</div\>

                    \<div\>

                        \<label for="unitNumber" class="block text-sm font-medium text-gray-700"\>Unit Number \<span class="text-red-500"\>\*\</span\>\</label\>

                        \<input type="text" id="unitNumber" class="input-field" placeholder="e.g., Apt 101 or SFP" list="unitDatalist"\>

                        \<datalist id="unitDatalist"\>\</datalist\>

                    \</div\>

                    \<div\>

                        \<label for="propertyLockBoxLocation" class="block text-sm font-medium text-gray-700"\>Property Lock Box Location\</label\>

                        \<input type="text" id="propertyLockBoxLocation" class="input-field" placeholder="e.g., Main Gate"\>

                    \</div\>

                    \<div\>

                        \<label for="propertyLockBoxCode" class="block text-sm font-medium text-gray-700"\>Property Lock Box Code\</label\>

                        \<input type="text" id="propertyLockBoxCode" class="input-field" placeholder="e.g., 1234"\>

                    \</div\>

                    \<div\>

                        \<label for="unitLockBoxLocation" class="block text-sm font-medium text-gray-700"\>Unit Lock Box Location\</label\>

                        \<input type="text" id="unitLockBoxLocation" class="input-field" placeholder="e.g., Unit Front Door"\>

                    \</div\>

                    \<div\>

                        \<label for="unitLockBoxCode" class="block text-sm font-medium text-gray-700"\>Unit Lock Box Code\</label\>

                        \<input type="text" id="unitLockBoxCode" class="input-field" placeholder="e.g., 5678"\>

                    \</div\>

                    \<div\>

                        \<label for="lastVisitedDate" class="block text-sm font-medium text-gray-700"\>Last Visited Date\</label\>

                        \<input type="date" id="lastVisitedDate" class="input-field"\>

                    \</div\>

                    \<div\>

                        \<label for="lastVisitedBy" class="block text-sm font-medium text-gray-700"\>Last Visited By\</label\>

                        \<input type="text" id="lastVisitedBy" class="input-field" placeholder="e.g., John Doe"\>

                    \</div\>

                    \<div\>

                        \<label for="lastKnownLBCode" class="block text-sm font-medium text-gray-700"\>Last Known-LB Code\</label\>

                        \<input type="text" id="lastKnownLBCode" class="input-field" placeholder="e.g., PREV999"\>

                    \</div\>

                \</div\>

                \<div class="flex flex-col sm:flex-row justify-end space-y-2 sm:space-y-0 sm:space-x-3 pt-4"\>

                    \<\!-- Added type="button" to buttons \--\>

                    \<button type="button" id="resetButton" class="btn btn-secondary w-full sm:w-auto"\>Reset Fields\</button\>

                    \<button type="button" id="saveButton" class="btn btn-primary w-full sm:w-auto" disabled\>Save Information\</button\>

                \</div\>

            \</form\> \<\!-- Corresponding closing form tag \--\>

        \</section\>

        \<\!-- Saved Data Table (The "Second Table") \--\>

        \<section class="bg-white shadow-xl rounded-lg p-6"\>

            \<h2 class="text-2xl font-semibold mb-6 text-gray-700 border-b pb-3"\>Lock Box Information Overview\</h2\>

             \<div class="overflow-x-auto table-container"\>

                \<table id="savedDataTable" class="min-w-full divide-y divide-gray-200"\>

                    \<thead class="bg-gray-50"\>

                        \<tr\>

                            \<th class="th-cell"\>Property\</th\>

                            \<th class="th-cell"\>Unit \#\</th\>

                            \<th class="th-cell"\>Prop LB Loc\</th\>

                            \<th class="th-cell"\>Prop LB Code\</th\>

                            \<th class="th-cell"\>Unit LB Loc\</th\>

                            \<th class="th-cell"\>Unit LB Code\</th\>

                            \<th class="th-cell"\>Visited Date\</th\>

                            \<th class="th-cell"\>Visited By\</th\>

                            \<th class="th-cell"\>Last Known LBC\</th\>

                        \</tr\>

                    \</thead\>

                    \<tbody id="savedDataTableBody" class="bg-white divide-y divide-gray-200"\>

                        \<tr\>

                            \<td colspan="9" class="td-cell text-center text-gray-500"\>Loading data...\</td\>

                        \</tr\>

                    \</tbody\>

                \</table\>

            \</div\>

        \</section\>

    \</div\>

    \<\!-- Message Modal \--\>

    \<div id="messageModal" class="modal-backdrop hidden"\>

        \<div class="modal-content"\>

            \<div class="flex justify-between items-center mb-1"\>

                \<h3 id="messageModalTitle" class="modal-title"\>Message\</h3\>

                \<button id="messageModalCloseButton" class="modal-close-button"\>

                    \<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"\>\<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"\>\</path\>\</svg\>

                \</button\>

            \</div\>

            \<p id="messageModalText" class="modal-body"\>\</p\>

            \<div class="text-right mt-6"\>

                \<button id="messageModalConfirmButton" class="btn btn-primary"\>OK\</button\>

            \</div\>

        \</div\>

    \</div\>

    \<script type="module"\>

        // Firebase Imports

        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";

        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";

        import { getFirestore, collection, addDoc, query, onSnapshot, orderBy, serverTimestamp, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // \--- Embedded CSV Data \---

        const csvData \= \`

,,,,,,,,,

\#,ACTIVE PROPERTIES,OWNER ACCOUNT NAME,,OCCUPIED,LISTED,VACANT,,,

,,,UNIT NUMBER,,,,,,

,,,,,,,VACANCY REASON,TARGET LISTING DATE,

1,11916 Tarragon Rd Unit H,MVSM Properties LLC,SFP,/,,,OCCUPIED,,

2,4522 Curtis Ave,Weijun Wang,4522C-1F,/,,,OCCUPIED,,

,,,4522C-1R,/,,,OCCUPIED,,

,,,4522C-2,/,,,OCCUPIED,,

5,6023 Gwynn Oak Ave,6023 Gwynn Oak Ave LLC,6023G-101,,,/,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-102,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-103,,,/,appoval email sent T2B5T5W,,

,,,6023G-104,,/ ,,LISTED,,

,,,6023G-201,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-202,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-203,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-204,,,/,"unit turn long ovedue

TL4VB3EB",,

,,,6023G-B1,,,/,unit turn pending TWBAEYIB,,

,,,6023G-B2,,,/,"long overdue

TJRPX0KB",,

15,130 Hammershire Road,MVSM Properties LLC,SFP,,,/,unit turn client TUTLPHBB,,

17,1891 Grempler Way,1891 Grempler LLC,SFP,/,,,OCCUPIED,,

18,1922 Eloise Lane,MVSM Properties LLC,SFP,,,/,property is for sale client \#241536,,

19,203 Hammershire Road,Amarish Pathak,SFP,/,,,OCCUPIED,,

20,21 S Castle Street,Elizabeth Cheever,SFP,/,,,OCCUPIED,,

21,3413 Esther Place,Terry Gene Pricer JR,SFP,/,,,OCCUPIED,,

22,5904 Falkirk Road,Monsurat Shittu,SFP,/,,,OCCUPIED,,

23,27 Tallow Court,Mohammad Khan,SFP,/,,,OCCUPIED,,

24,45 Tallow Court ,Mohammad Khan,SFP,/,,,OCCUPIED,,

25,1727 Park Avenue,Gary Anderson,SFP,/,,,OCCUPIED,,

31,1615 Cole St,Weijun Wang,SFP,,,/,this property is for sale.,,

32,1239 Glyndon Ave,Donald Panda,SFP,/,,,OCCUPIED,,

33,611 E 37th St,Deyo Johnson,611e37-1F,,,/,unit turn for approval T4VMIRW,,

,,,611e37-2F,,,/,client lives here,,

 ,610 Kingfisher Rd,Jennifer & Kevin Gladden,SFP,/,,,OCCUPIED,,

36,23 S Calhoun St,Ray Christopher Brewer,23sCal-1,/,,,OCCUPIED,,

,,,23sCal-2,/,,,OCCUPIED,,

,,,23sCal-3,/,,,OCCUPIED,,unit turn completed T5QLF6HB

40,1450 Broening Hwy,Dariusz & Hanna Czubacki,SFP,/,,,OCCUPIED,,

41,527 S. Decker,Dariusz & Hanna Czubacki,SFP,/,,,OCCUPIED,,

42,3533 Reisterstown Rd,3533 REISTERSTOWN ROAD LLC,SFP,,,/,client took over Move out insp/replace locks & unit turn,,

43,220 S Augusta Ave,Michmar LLC,220sAug-1F,/,,,OCCUPIED,,

,,,220sAug-2F,,,/,NOT LISTED \- NO UPDATED RENTAL LICENSE,,

,,,220sAug-1&2R,/,,,evicted 06/4/24 \- client did the drill nd replace,,

44,203 S Augusta Ave,Michmar LLC,203sAug-1,,,/,never been tenanted,,

,,,203sAug-2,,,/,NO license- Client will take care of the License TENANT MOVED TO MCKEAN,,

,,,203sAug-3,/,,,OCCUPIED,,

47,234 S Loudon Ave,Michmar LLC,SFP,/,,,OCCUPIED,,

48,42 S Morley St,Michmar LLC,SFP,/,,,OCCUPIED,,

49,85 S Morley St,Michmar LLC,SFP,/,,,OCCUPIED,,

50,42 S Kossuth St,Michmar LLC,SFP,,,/,NO license- Client will take care of the License,,

51,48 S Kossuth St,Michmar LLC,SFP,/,,,OCCUPIED,,

52,40 S Kossuth St,Michmar LLC,SFP,,,/,home rental inspection cancelled. client will handle TNT5YIHB,,

53,44 S Kossuth St,Michmar LLC,SFP,/,,,OCCUPIED,,

54,46 S Kossuth St,Michmar LLC,SFP,/,,,OCCUPIED,,

55,347 Martingale Ave,Letoya Fields Ogallo,SFP,,,/,Tenant just moved out 02/04/2025-Coordinated with clyde about the lead cert,,

56,3012 W Garrison Ave,Gladys Ononjobi,SFP,/,,,OCCUPIED,,

57,136 Coralwood Rd,Helen M. Moan,SFP,/,,,OCCUPIED,,

58,2152 Hollins St,Melanie Turner,SFP,/,,,OCCUPIED,,

59,2005 N Wolfe Street,Triple J Noble Investments,SFP,,,/,TENANTS EVICTED ,,

60,1111 Hollins St,Anthony Corradetti,SFP,,,/,unit turn approval pending T8FWR8X,,

61,10547 Twin Rivers Rd Unit F-2,Josephine Tao Saba,SFP,/,,,OCCUPIED,,

62,701 Venable,Vinh Quoc Diep,SFP,/,,,OCCUPIED,,

63,2736 Kinsey Ave,2736 Kinsey LLC,SFP,,,/,unit turn handled client TA6W3ZV,,

65,3800 Meghan Dr \#3A,Raymond McRae,SFP,/,,,OCCUPIED,,

66,802 Corktree Rd ,Fanuel Chirombo,SFP,/,,,OCCUPIED,,

71,1116 W Hamburg St,Hassen H. Mender,SFP,/,,,OCCUPIED,,

73,2703 White Ave,Anthony Alicea,SFP,/,,,OCCUPIED,,

74,1113 Hollins St,Anthony Corradetti,SFP,,,/,unit turn approval email sent TMEFB6Q,,

77,2506 McHenry St,Taylor Estate 2 LLC,SFP,/,,,OCCUPIED,,

78,1903 Grinnalds,Taylor Estate 2 LLC,SFP,/,,,OCCUPIED,,

80,2510 Lauretta Ave,2510 LAURETTA AVE LLC,SFP,,,/,Tenant move out; 11/13/2024- For lead inspection,,

81,4012 Clarks Ln,Jixu Xiao,SFP,/,,,OCCUPIED,,

82,4246 Nicholas Ave,4246 Nicholas LLC,SFP,/,,,tenant placement,,

85,4109 Morrison Ct,Barry Leathers Jr,SFP,/,,,OCCUPIED,,

86,115 Cross Keys Rd Unit R115E,Bryan Mckay,SFP,/,,,OCCUPIED,,

87,437 S Pulaski St,Erinc Emer,SFP,,/,,LISTED,,

91,10108 Blansford Way ,Jenell Ellis,SFP,/,,,OCCUPIED,,

92,4014 Clarks Ln,Jixu Xiao,SFP,/,,,OCCUPIED,,

94,414 Water St,Michael Brown,SFP,,,/,OCCUPIED,,

95,3744 Elmley Ave ,Michael Akinbaleye,SFP,/,,,OCCUPIED,,

98,9746 Harvester Cir,Amit Bhusal,SFP,/,,,OCCUPIED,,

101,414 Water St,Kristofer O Bryant,SFP,,,/,CLIENT TERM,,

105,7941 Saint Gregory Dr,Zheng Ling Bin,SFP,/,,,OCCUPIED,,

106,1226 E Chase St,Carla Colson,SFP,/,,,OCCUPIED,,

107,748 E 36th St,Joel Brown,SFP,/,,,inspection fail list completed TJLFV8V,,

108,2733 Ellicott Dr,Joel Brown,SFP,/,,,OCCUPIED,,

109,3406 Woodbine Ave,Joel Brown,3406Woo-1,/,,,OCCUPIED,,

,,,3406Woo-2,,,/,OCCUPIED,,

112,5 S Conkling St,Luciana E Holdings LLC,SFP,/,,,OCCUPIED,,

113,2558 Aisquith St,Erin Langley,SFP,/,,,OCCUPIED,,

114,2139 Whistler Ave,Erin Langley,SFP,/,,,OCCUPIED,,

115,3232 Elmley Ave,Erin Langley,SFP,/,,,OCCUPIED,,

116,1218 Bentalou St,Erin Langley,SFP,/,,,OCCUPIED,,

117,3200 Carlisle  Ave,Erin Langley,3200Car-1,/,,,OCCUPIED,,

,,,3200Car-2,/,,,OCCUPIED,,

119,1639 N Warwick Ave,Erin Langley,SFP,/,,,OCCUPIED,,

120,2526 Cecil Ave,Erin Langley,SFP,/,,,OCCUPIED,,

128,805 McKean Ave,Nicholas Noll,SFP,/,,,OCCUPIED,,

131,2758 Wilkens Ave,Palmetto State Enterprise LLC,SFP,/,,,OCCUPIED,,

132,3520 Ellamont Rd,Attallah Banks,SFP,,,/,no updates,,

136,1024 N Carey St ,Adewale Adeleye,1024nCar-1,/,,,OCCUPIED,,

,,,1024nCar-2,/,,,OCCUPIED,,

,45 S Morley Street,michmar LLC,SFP,,,/,RENTAL LICENSE UPDATED. NOT LISTED,,

,133 Denison Street ,Nick Daurio(VCAP),133Den-1,,,/,TENANT MOVED OUT UNIT TURN TVE4PD3,,

,,,133Den-2,,,/,Unit Turn,,

,144 Palormo Ave ,Nick Daurio(VCAP),SFP,,,/,No license,,

,214 N Fulton Ave,Nick Daurio(BRF1),SFP,,,/,No license,,

,2114 Vine Street,Nick Daurio(BRF1),SFP,,,/,No license,,

,236 S Clinton St ,Danielle Duckett,SFP,,,/,CLIENT TERM,,

,402 S Calhoun,Nick Daurio(BRF1),SFP,,,/,No lead cert,,

,512 N Glover Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,526 N Clover ,Nick Daurio(BRF1),SFP,,,/,NOT LISTED NO RENTAL LICENSE,,

,542 Brunswick St ,Nick Daurio(VCAP),SFP,,,/,"TENANT MOVED OUT UNIT TURN

TUG3B9Y",,

,616 N WOODINGTON,Ganiyat Lawal,616 N WOODINGTON Unit 1,/,,,OCCUPIED,,

,,,616 N WOODINGTON Unit 2,/,,,OCCUPIED,,

,,,616 N WOODINGTON Unit 3,,/,,LISTED,,

,625 McCollough Cir,Gail Rearden,SFP,,,/,NO LICENSE,,

,1123 N Mount St.,,SFP,,,/,UPDATED LICENSE NOT LISTED,,

,637 E 29th St,Rodney Mason,SFP,,,/,UPDATE LICENSE NOT LISTED,,

,721 Appleton Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1108 N MOUNT ST,Adaobi Herlich,1108 N MOUNT ST Unit 1,,,/,OCCUPIED,,

,,,1108 N MOUNT ST Unit 2,,,/,OCCUPIED,,

,1203 N Milton Ave,Nick Daurio(BRF1),SFP,,,/,UNIT TURN TGY041V,,

,1239 N Decker Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1323 N Milton Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1339 Ramsay Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1402 Mosher Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1420 Aisquith Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1424 Aisquith St ,Nick Daurio(VCAP),SFP,,,/,NO LICENSE NOT LISTED,,

,1516 Cliftview Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1523 W FAIRMOUNT AVE,Marquell Scott,SFP,,/,,LISTED,,

,1612 Eastern Ave ,John Childress,1612 Eastern Ave  Apt 1,/,,,OCCUPIED,,

,,,1612 Eastern Ave Apt 2,,,/,NOT LISTED,,

,1616 PLUM ST ,Edmundo Safdie,1616 PLUM ST Unit 2,,,/,NO LICENSE NO UPDATES,,

,1706 N Monroe Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NO UPDATES,,

,1710 E 28TH ST,Erick Garski,SFP,,,/,EXPIRED IICENSE,,

,1710 Ramsay Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1713 E 30TH,Amit Shenoy,SFP,,,/,UPDATED LICENSE NOT LISTED,,

,1715 N Washington St,Nick Daurio(VCAP),SFP,,,/,NO LICENSE NOT LISTED,,

,1733 N Bond St ,Nick Daurio(VCAP),SFP,,,/,NO LICENSE NOT LISTED,,

,1755 Abbotston St ,Raymond Mends,SFP,,,/,TPA,,

,1807 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1811 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1813 N Collington Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1823 N Chapel,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1824 N Collington Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1827 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1831 N Dallas Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1833 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1909 E Oliver Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1910 Wilhelm Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1912 Wilhelm Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1924 Wilhelm Street ,Nick Daurio(BRF1),SFP,,,/,NO LICENSE  NOT LISTED,,

,1944 Harlem Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,2005 N Wolfe Street ,Tierra Joseph- Triple J Noble Investments,SFP,,,/,Unit Turn,,

,2012 E Lafayette Ave ,Nick Daurio(VCAP),SFP,,,/,NO LICENSE,,

,2013 N Longwood Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,2114 Vine Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,2243 E Biddle Street,Nick Daurio(BRF1),SFP,,,/,NOLICENSE,,

,2304 W NORTH AVE,Ashley Kansinally,2304 W NORTH AVE. Unit 1,/,,,OCCUPIED,,

,,,2304 W NORTH AVE. Unit 2,,/,/,LISTED,,

,,,2304 W NORTH AVE B|Booth-1,/,,,OCCUPIED,,

,,,2304 W NORTH AVE B|Booth-2,,/,/,LISTED,,

,,,2304 W NORTH AVE B|Booth-3,,,/,No Lead cert,,

,,,2304 W NORTH AVE B|Booth-4,,,/,No Lead cert,,

,2332 W Baltimore Street,Nick Daurio(BRF1),SFP,,,/,No Lead cert,,

,2409 E Oliver St ,Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,2416 E Oliver Street,Nick Daurio(BRF1),SFP,,,/,On going home inspection and Lead inspection,,

,2440 CALLOW AVE ,Renika Ramsay,2440 CALLOW AVE UNIT 1,/,,,OCCUPIED,,

,,,2440 CALLOW AVE UNIT 2,,/,/,LISTED,,

,,,2440 CALLOW AVE UNIT 3,,/,/,LISTED,,

,2515 W Fairmount Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,"2520 Mosher St,",Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,2520 W Franklin St,Nick Daurio(VCAP),SFP,,,/,On going home inspection and Lead inspection,,

,2556 W Fairmount Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2616 Orleans Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2627 Hafer Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2629 Llewelyn Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2640 Lauretta Ave,Anwar Minni \-2640Lau,SFP,,,/,License is soon to expire( task created) and no Lead cert,,

,2692 Dulany Street,Nick Daurio(BRF1),SFP,,,/,No License,,

,2730 Winchester Street,Nick Daurio(BRF1),SFP,,,/,No License,,

,"2731 The Alameda,",Joel Brown,SFP,,,/,OCCUPIED,,

,2736 Kinsey Ave,Anwar Minni \- 2736Kin,SFP,,,/,Tenant move Out 04/29/2024 \- For Lead inspection,,

\-,2737 Prospect Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2752 Mosher Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2812 WOODBROOK AVE,Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,2815 Kennedy Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2906 Oakford Ave,Kimberly Aiken/Oakford Ave LLC,SFP,,,/,No lead cert and Unit turn,,

,2918 E Federal St Unit ,Linda Mays,2918 E Federal St Unit  1,,,/,No Lead cert,,

,,,2918 E Federal St Unit 2,,,/,No Lead cert,,

,2919 Belmont Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3001 Kenyon Ave,Vinh Quoc Diep,SFP,/,,,OCCUPIED,,

,3027 Harlem Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3200 Elmora Ave,Raymond Mends,SFP,,,/,Lead cert and Unit turn,,

,3409 Ravenwood Ave,Francis Kamara,SFP,,,/,Lead Inspection fail list,,

,3416 Gwynns Falls Pkwy,Sabina Yasmin,3416 Gwynns Falls Pkwy Room 1,,,/,No license and Lead cert,,

,,,3416 Gwynns Falls Pkwy Room 2,,,/,No license and Lead cert,,

,,,3416 Gwynns Falls Pkwy Room 3,,,/,No license and Lead cert,,

,3428 Hilldale Place,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3434 Edmondson Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3520 ELLAMONT ROAD,Attallah Banks,SFP,,,/,Unit Turn,,

,3641 Park Heights Ave,Nick Daurio(BRF1),SFP,,,/,UPDATED LICENSE NOT LISTED,,

,4628 REISTERSTOWN ROAD,Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,4814 Curtis Ave,Nick Daurio(BRF1),SFP,,,/,No lead cert,,

,4816 Curtis Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,4818 Curtis Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE UNDER VCAP,,

,5421 Denmore Ave,Amit Shenoy,SFP,,,/,NO LICENSE UNDER VCAP,,

,2435 E Hoffman Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2646 Beryl Ave,Rafael Brown \- Magis,SFP,,/,,LISTED,,

,,,,,,,,,

,,,,,,,,,

,,,,,9,123,,,

\`;

        // \--- Module-scoped variable for parsed CSV property/unit pairs \---

        let parsedCsvItems \= \[\];

        // \--- Firebase Configuration \---

        const firebaseConfig \= typeof \_\_firebase\_config \!== 'undefined' ? JSON.parse(\_\_firebase\_config) : {

            apiKey: "YOUR\_API\_KEY", authDomain: "YOUR\_AUTH\_DOMAIN", projectId: "YOUR\_PROJECT\_ID",

            storageBucket: "YOUR\_STORAGE\_BUCKET", messagingSenderId: "YOUR\_MESSAGING\_SENDER\_ID", appId: "YOUR\_APP\_ID"

        };

        // \--- App Configuration \---

        const appId \= typeof \_\_app\_id \!== 'undefined' ? \_\_app\_id : 'default-lockbox-app';

        const COLLECTION\_NAME \= 'property\_records';

        // \--- Firebase Initialization \---

        let app;

        let db;

        let auth;

        let userId \= null;

        let unsubscribeSnapshot \= null;

        try {

            app \= initializeApp(firebaseConfig);

            db \= getFirestore(app);

            auth \= getAuth(app);

            setLogLevel('debug');

            console.log("Firebase initialized.");

        } catch (error) {

            console.error("Firebase initialization error:", error);

            showMessage("Initialization Error", "Could not initialize the application. Please refresh.");

            const saveBtn \= document.getElementById('saveButton');

            if (saveBtn) saveBtn.disabled \= true;

            const userIdDisp \= document.getElementById('userIdDisplay');

            if (userIdDisp) userIdDisp.textContent \= 'Error';

        }

        // \--- DOM Elements \---

        // Note: entryForm is now a \<form\> element

        const entryForm \= document.getElementById('entryForm');

        const propertyInput \= document.getElementById('property');

        const unitNumberInput \= document.getElementById('unitNumber');

        const propertyLockBoxLocationInput \= document.getElementById('propertyLockBoxLocation');

        const propertyLockBoxCodeInput \= document.getElementById('propertyLockBoxCode');

        const unitLockBoxLocationInput \= document.getElementById('unitLockBoxLocation');

        const unitLockBoxCodeInput \= document.getElementById('unitLockBoxCode');

        const lastVisitedDateInput \= document.getElementById('lastVisitedDate');

        const lastVisitedByInput \= document.getElementById('lastVisitedBy');

        const lastKnownLBCodeInput \= document.getElementById('lastKnownLBCode');

        const resetButton \= document.getElementById('resetButton');

        const saveButton \= document.getElementById('saveButton');

        const savedDataTableBody \= document.getElementById('savedDataTableBody');

        const userIdDisplay \= document.getElementById('userIdDisplay');

        const propertyDatalist \= document.getElementById('propertyDatalist');

        const unitDatalist \= document.getElementById('unitDatalist');

        // Modal elements

        const messageModal \= document.getElementById('messageModal');

        const messageModalTitle \= document.getElementById('messageModalTitle');

        const messageModalText \= document.getElementById('messageModalText');

        const messageModalCloseButton \= document.getElementById('messageModalCloseButton');

        const messageModalConfirmButton \= document.getElementById('messageModalConfirmButton');

        // \--- Modal Functions \---

        function showMessage(title, text) {

            if (messageModalTitle) messageModalTitle.textContent \= title;

            if (messageModalText) messageModalText.textContent \= text;

            if (messageModal) messageModal.classList.remove('hidden');

        }

        if (messageModalCloseButton) messageModalCloseButton.onclick \= () \=\> messageModal.classList.add('hidden');

        if (messageModalConfirmButton) messageModalConfirmButton.onclick \= () \=\> messageModal.classList.add('hidden');

        if (messageModal) {

            messageModal.onclick \= (event) \=\> {

                if (event.target \=== messageModal) {

                    messageModal.classList.add('hidden');

                }

            };

        }

        // \--- CSV Parsing and Datalist/Property List Population \---

        function parseCSVAndPopulateDatalistsAndProperties(csvString) {

            const lines \= csvString.trim().split('\\n');

            const uniquePropertiesForDatalist \= new Set();

            const uniqueUnitsForDatalist \= new Set();

           

            const tempParsedItems \= \[\]; // For collecting property/unit pairs for the table

            let currentPropertyContext \= "";

            // Column indices from CSV structure

            const dataStartIndex \= 4; // Estimated start of actual data

            const propertyColIndex \= 1; // "ACTIVE PROPERTIES"

            const unitColIndex \= 3;     // "UNIT NUMBER"

            for (let i \= dataStartIndex; i \< lines.length; i++) {

                const line \= lines\[i\].trim();

                if (\!line) continue;

                const columns \= line.split(',');

                const propertyName \= columns.length \> propertyColIndex ? columns\[propertyColIndex\].trim() : "";

                const unitName \= columns.length \> unitColIndex ? columns\[unitColIndex\].trim() : "";

                // For Datalists

                if (propertyName && propertyName \!== "\#" && propertyName \!== "ACTIVE PROPERTIES") {

                    uniquePropertiesForDatalist.add(propertyName);

                    currentPropertyContext \= propertyName; // Update context for property/unit pairs

                }

                if (unitName && unitName \!== "UNIT NUMBER" && unitName.toUpperCase() \!== "SFP") {

                    uniqueUnitsForDatalist.add(unitName);

                }

                 if (unitName && unitName \!== "UNIT NUMBER" && unitName.toUpperCase() \=== "SFP") { // Also add SFP to unit datalist

                    uniqueUnitsForDatalist.add("SFP");

                }

                // For Property/Unit pairs table (parsedCsvItems)

                if (propertyName && propertyName \!== "\#" && propertyName \!== "ACTIVE PROPERTIES") {

                    // This line defines a new property (or re-defines one)

                    if (unitName && unitName \!== "UNIT NUMBER") {

                        tempParsedItems.push({ property: propertyName, unit: unitName });

                    } else { // Property listed, but unit is SFP or effectively blank for this specific line's unit col

                        tempParsedItems.push({ property: propertyName, unit: "SFP" }); // Default to SFP if no specific unit on property line

                    }

                } else if (unitName && unitName \!== "UNIT NUMBER" && currentPropertyContext) {

                    // This line has no property, but has a unit, so it belongs to currentPropertyContext

                    tempParsedItems.push({ property: currentPropertyContext, unit: unitName });

                }

            }

           

            // Populate Datalists

            if (propertyDatalist) {

                propertyDatalist.innerHTML \= '';

                uniquePropertiesForDatalist.forEach(prop \=\> {

                    if (prop) {

                        const option \= document.createElement('option');

                        option.value \= prop;

                        propertyDatalist.appendChild(option);

                    }

                });

            }

            if (unitDatalist) {

                unitDatalist.innerHTML \= '';

                uniqueUnitsForDatalist.forEach(unit \=\> {

                     if (unit) {

                        const option \= document.createElement('option');

                        option.value \= unit;

                        unitDatalist.appendChild(option);

                    }

                });

            }

            console.log("Datalists populated:", { numProperties: uniquePropertiesForDatalist.size, numUnits: uniqueUnitsForDatalist.size });

            // Deduplicate and finalize parsedCsvItems for the table

            const uniqueCsvItemsMap \= new Map();

            tempParsedItems.forEach(item \=\> {

                if (item.property) { // Ensure property is not empty

                     uniqueCsvItemsMap.set(\`${item.property}|${item.unit}\`, item);

                }

            });

            parsedCsvItems \= Array.from(uniqueCsvItemsMap.values());

            console.log("Parsed CSV items for table:", parsedCsvItems.length, parsedCsvItems.slice(0,5)); // Log count and a few items

        }

        // \--- Authentication \---

        onAuthStateChanged(auth, async (user) \=\> {

            if (user) {

                userId \= user.uid;

                console.log("User authenticated. UID:", userId);

                if (userIdDisplay) userIdDisplay.textContent \= userId;

                if (saveButton) saveButton.disabled \= false;

                loadAndDisplaySavedData(); // This will trigger renderSavedDataTable

            } else {

                console.log("User not authenticated. Attempting sign-in.");

                if (userIdDisplay) userIdDisplay.textContent \= "Authenticating...";

                if (saveButton) saveButton.disabled \= true;

                // Attempt to render table with CSV data even if auth fails, then show auth error

                renderSavedDataTable(\[\]); // Show CSV structure initially

                if (typeof \_\_initial\_auth\_token \=== 'undefined' || \!\_\_initial\_auth\_token) {

                    try {

                        await signInAnonymously(auth);

                    } catch (error) {

                        console.error("Error signing in anonymously:", error);

                        userId \= \`error-anon-${crypto.randomUUID().slice(0,8)}\`;

                        if (userIdDisplay) userIdDisplay.textContent \= \`Error (Session ID: ${userId})\`;

                        showMessage("Authentication Error", "Could not sign in anonymously. Saved data cannot be loaded or new data saved reliably.");

                    }

                } else {

                    userId \= \`error-custom-${crypto.randomUUID().slice(0,8)}\`;

                    if (userIdDisplay) userIdDisplay.textContent \= \`Auth Failed (ID: ${userId})\`;

                }

            }

        });

        async function initializeAuth() {

            if (\!auth) {

                console.error("Auth service not available for initializeAuth.");

                if (userIdDisplay) userIdDisplay.textContent \= 'Auth Error';

                renderSavedDataTable(\[\]); // Show CSV structure initially

                return;

            }

            if (typeof \_\_initial\_auth\_token \!== 'undefined' && \_\_initial\_auth\_token) {

                try {

                    await signInWithCustomToken(auth, \_\_initial\_auth\_token);

                } catch (error) {

                    console.error("Error with signInWithCustomToken:", error);

                    showMessage("Authentication Error", \`Failed to sign in with token: ${error.message}. Attempting anonymous sign-in.\`);

                    try {

                        await signInAnonymously(auth);

                    } catch (anonError) {

                        console.error("Fallback anonymous sign-in error:", anonError);

                        userId \= \`error-fallback-${crypto.randomUUID().slice(0,8)}\`;

                        if (userIdDisplay) userIdDisplay.textContent \= \`Critical Auth Error (ID: ${userId})\`;

                        showMessage("Critical Auth Error", "Could not sign in. App functionality is severely limited.");

                        renderSavedDataTable(\[\]); // Show CSV structure

                    }

                }

            } else {

                if (\!auth.currentUser) {

                    try {

                        await signInAnonymously(auth);

                    } catch (error) {

                        console.error("Error signing in anonymously (initial attempt):", error);

                         userId \= \`error-init-anon-${crypto.randomUUID().slice(0,8)}\`;

                        if (userIdDisplay) userIdDisplay.textContent \= \`Init Auth Error (ID: ${userId})\`;

                        renderSavedDataTable(\[\]); // Show CSV structure

                    }

                } else {

                    // Already authenticated (e.g. existing session), onAuthStateChanged will handle it.

                    // loadAndDisplaySavedData will be called by onAuthStateChanged.

                }

            }

        }

       

        if (auth) {

            initializeAuth();

        } else {

            // If auth itself failed to init, still try to show CSV data

            document.addEventListener('DOMContentLoaded', () \=\> {

                 parseCSVAndPopulateDatalistsAndProperties(csvData);

                 renderSavedDataTable(\[\]);

                 if (propertyInput) propertyInput.focus();

            });

        }

        // \--- Form Handling \---

        function resetForm() {

            // entryForm is now guaranteed to be a \<form\> element

            if (entryForm && typeof entryForm.reset \=== 'function') {

                 entryForm.reset();

            } else if (entryForm) {

                // Fallback for manual reset if entryForm is not a form or reset is missing

                // (should not happen with the HTML change, but good for robustness)

                console.warn("entryForm.reset() is not available. Manually resetting fields.");

                propertyInput.value \= '';

                unitNumberInput.value \= '';

                propertyLockBoxLocationInput.value \= '';

                propertyLockBoxCodeInput.value \= '';

                unitLockBoxLocationInput.value \= '';

                unitLockBoxCodeInput.value \= '';

                lastVisitedDateInput.value \= '';

                lastVisitedByInput.value \= '';

                lastKnownLBCodeInput.value \= '';

            }

            if (propertyInput) propertyInput.focus();

        }

        async function handleSave() {

            if (\!userId || userId.startsWith('error-')) { // Check for actual userId

                showMessage("Error", "User not properly authenticated. Cannot save data.");

                if (saveButton) saveButton.disabled \= true;

                return;

            }

            if (\!db) {

                showMessage("Error", "Database not available. Cannot save data.");

                return;

            }

            const property \= propertyInput.value.trim();

            const unitNumber \= unitNumberInput.value.trim();

            if (\!property || \!unitNumber) {

                showMessage("Validation Error", "Property Name and Unit Number are required.");

                return;

            }

            const dataToSave \= {

                property: property,

                unitNumber: unitNumber,

                propertyLockBoxLocation: propertyLockBoxLocationInput.value.trim(),

                propertyLockBoxCode: propertyLockBoxCodeInput.value.trim(),

                unitLockBoxLocation: unitLockBoxLocationInput.value.trim(),

                unitLockBoxCode: unitLockBoxCodeInput.value.trim(),

                lastVisitedDate: lastVisitedDateInput.value,

                lastVisitedBy: lastVisitedByInput.value.trim(),

                lastKnownLBCode: lastKnownLBCodeInput.value.trim(),

                timestamp: serverTimestamp(),

                savedByUserId: userId

            };

            try {

                if (saveButton) saveButton.disabled \= true;

                if (saveButton) saveButton.textContent \= 'Saving...';

                const collectionPath \= \`/artifacts/${appId}/users/${userId}/${COLLECTION\_NAME}\`;

                const docRef \= await addDoc(collection(db, collectionPath), dataToSave);

                console.log("Document written with ID: ", docRef.id);

                showMessage("Success", "Information saved successfully\!");

                resetForm(); // This should now work correctly

                // onSnapshot will automatically update the table

            } catch (error) {

                console.error("Error adding document: ", error);

                showMessage("Error", \`Could not save information: ${error.message}\`);

            } finally {

                 if (saveButton) saveButton.disabled \= false;

                 if (saveButton) saveButton.textContent \= 'Save Information';

            }

        }

        if (resetButton) resetButton.addEventListener('click', resetForm);

        if (saveButton) saveButton.addEventListener('click', handleSave);

        // \--- Data Display Logic for the Second Table \---

        function renderSavedDataTable(firestoreDocsArray \= \[\]) {

            if (\!savedDataTableBody) {

                console.error("Target table body 'savedDataTableBody' not found in DOM.");

                return;

            }

            savedDataTableBody.innerHTML \= ''; // Clear existing content

            const firestoreDataMap \= new Map();

            firestoreDocsArray.forEach(docData \=\> {

                // Assuming docData contains property and unitNumber fields

                // Since Firestore query is ordered by timestamp desc,

                // this will keep the latest entry for a given property-unit pair.

                if(docData.property && docData.unitNumber) {

                    firestoreDataMap.set(\`${docData.property}-${docData.unitNumber}\`, docData);

                }

            });

            const displayedItems \= new Set(); // To track property-unit pairs already rendered from CSV \+ Firestore

            // 1\. Iterate through CSV items and merge with Firestore data

            parsedCsvItems.forEach(csvItem \=\> {

                const key \= \`${csvItem.property}-${csvItem.unit}\`;

                const savedData \= firestoreDataMap.get(key);

                const dataToDisplay \= savedData || csvItem; // Use Firestore data if available, else CSV structure

                const row \= savedDataTableBody.insertRow();

                const addCell \= (text) \=\> {

                    const cell \= row.insertCell();

                    cell.textContent \= text || '-';

                    cell.className \= 'td-cell';

                };

                addCell(dataToDisplay.property);

                addCell(dataToDisplay.unit); // unit from CSV or unitNumber from Firestore

                addCell(savedData ? savedData.propertyLockBoxLocation : '-');

                addCell(savedData ? savedData.propertyLockBoxCode : '-');

                addCell(savedData ? savedData.unitLockBoxLocation : '-');

                addCell(savedData ? savedData.unitLockBoxCode : '-');

                addCell(savedData ? savedData.lastVisitedDate : '-');

                addCell(savedData ? savedData.lastVisitedBy : '-');

                addCell(savedData ? savedData.lastKnownLBCode : '-');

               

                displayedItems.add(key);

            });

            // 2\. Add any Firestore items that were not in the CSV list

            firestoreDocsArray.forEach(docData \=\> {

                if (docData.property && docData.unitNumber) {

                    const key \= \`${docData.property}-${docData.unitNumber}\`;

                    if (\!displayedItems.has(key)) {

                        const row \= savedDataTableBody.insertRow();

                        const addCell \= (text) \=\> {

                            const cell \= row.insertCell();

                            cell.textContent \= text || '-';

                            cell.className \= 'td-cell';

                        };

                        addCell(docData.property);

                        addCell(docData.unitNumber);

                        addCell(docData.propertyLockBoxLocation);

                        addCell(docData.propertyLockBoxCode);

                        addCell(docData.unitLockBoxLocation);

                        addCell(docData.unitLockBoxCode);

                        addCell(docData.lastVisitedDate);

                        addCell(docData.lastVisitedBy);

                        addCell(docData.lastKnownLBCode);

                    }

                }

            });

            if (savedDataTableBody.rows.length \=== 0\) {

                const tr \= savedDataTableBody.insertRow();

                const td \= tr.insertCell();

                td.colSpan \= 9;

                td.textContent \= 'No property data found in CSV or no saved records.';

                td.className \= 'td-cell text-center text-gray-500 py-4';

            }

        }

        async function loadAndDisplaySavedData() {

            if (\!userId || userId.startsWith('error-') || \!db) {

                const reason \= \!userId || userId.startsWith('error-') ? "User not authenticated properly." : "Database not available.";

                console.log(\`Cannot load saved data: ${reason}\`);

                // Render table with CSV data only if auth/db issues prevent Firestore fetch

                // This is now handled by onAuthStateChanged calling renderSavedDataTable(\[\]) on failure.

                // Or if parsedCsvItems is ready, call it:

                if(parsedCsvItems.length \> 0\) {

                    renderSavedDataTable(\[\]);

                } else {

                     if (savedDataTableBody) savedDataTableBody.innerHTML \= \`\<tr\>\<td colspan="9" class="td-cell text-center text-gray-500"\>${reason} Cannot load saved data.\</td\>\</tr\>\`;

                }

                return;

            }

            if (unsubscribeSnapshot) {

                unsubscribeSnapshot();

                unsubscribeSnapshot \= null;

            }

            const collectionPath \= \`/artifacts/${appId}/users/${userId}/${COLLECTION\_NAME}\`;

            console.log(\`Listening for saved data from: ${collectionPath}\`);

            const q \= query(collection(db, collectionPath), orderBy("timestamp", "desc"));

            unsubscribeSnapshot \= onSnapshot(q, (querySnapshot) \=\> {

                console.log(\`Received snapshot. Empty: ${querySnapshot.empty}, Size: ${querySnapshot.size}\`);

                const firestoreDocsArray \= querySnapshot.docs.map(doc \=\> ({ id: doc.id, ...doc.data() }));

                renderSavedDataTable(firestoreDocsArray);

            }, (error) \=\> {

                console.error("Error fetching saved data with onSnapshot:", error);

                if (savedDataTableBody) {

                     savedDataTableBody.innerHTML \= \`\<tr\>\<td colspan="9" class="td-cell text-center text-red-500"\>Error loading saved data: ${error.message}\</td\>\</tr\>\`;

                }

                showMessage("Data Error", \`Could not load saved records: ${error.message}\`);

            });

        }

       

        // \--- Initial Page Load Actions \---

        document.addEventListener('DOMContentLoaded', () \=\> {

            // Parse CSV for datalists and for the initial table structure

            parseCSVAndPopulateDatalistsAndProperties(csvData);

           

            // Initial render of the table with CSV data.

            // Firestore listener will update it once connected & data is fetched.

            renderSavedDataTable(\[\]); // Render with empty Firestore data initially

                                     // This shows CSV structure.

           

            if (propertyInput) propertyInput.focus();

           

            // initializeAuth is called after Firebase services are confirmed to be available.

            // If auth is not available, a fallback in initializeAuth also calls renderSavedDataTable(\[\]).

        });

    \</script\>

\</body\>

\</html\>

\<\!DOCTYPE html\>

\<html lang="en"\>

\<head\>

    \<meta charset="UTF-8"\>

    \<meta name="viewport" content="width=device-width, initial-scale=1.0"\>

    \<title\>Property Lock Box Management\</title\>

    \<script src="https://cdn.tailwindcss.com"\>\</script\>

    \<style\>

        /\* Custom styles if needed, though Tailwind is preferred \*/

        body {

            font-family: 'Inter', sans-serif;

            background-color: \#f4f7f6; /\* Light gray background \*/

        }

        .input-field {

            @apply mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm;

        }

        .btn {

            @apply py-2 px-4 rounded-md shadow-sm text-sm font-medium focus:outline-none focus:ring-2 focus:ring-offset-2 transition-colors duration-150 ease-in-out;

        }

        .btn-primary {

            @apply text-white bg-indigo-600 hover:bg-indigo-700 focus:ring-indigo-500;

        }

        .btn-secondary {

            @apply text-gray-700 bg-gray-200 hover:bg-gray-300 focus:ring-gray-400;

        }

        .th-cell {

            @apply px-4 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider bg-gray-50 sticky top-0 z-10; /\* Added sticky for header \*/

        }

        .td-cell {

            @apply px-4 py-3 whitespace-nowrap text-sm text-gray-700 border-b border-gray-200;

        }

        /\* Modal styles \*/

        .modal-backdrop {

            @apply fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full flex items-center justify-center z-50;

        }

        .modal-content {

            @apply bg-white p-6 rounded-lg shadow-xl w-11/12 md:w-1/3 max-w-md mx-auto;

        }

        .modal-title {

            @apply text-xl font-semibold text-gray-700;

        }

        .modal-body {

            @apply text-gray-600 my-4;

        }

        .modal-close-button {

             @apply text-gray-400 hover:text-gray-600 transition-colors duration-150 ease-in-out;

        }

        .table-container { /\* Added for potentially scrollable table body \*/

            @apply max-h-\[60vh\] overflow-y-auto; /\* Adjust max-height as needed \*/

        }

    \</style\>

    \<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700\&display=swap" rel="stylesheet"\>

\</head\>

\<body class="bg-gray-100"\>

    \<div class="container mx-auto p-4 sm:p-6 lg:p-8"\>

        \<header class="mb-8 text-center"\>

            \<h1 class="text-3xl font-bold text-gray-800"\>Property Lock Box Management\</h1\>

            \<p class="text-sm text-gray-500 mt-1"\>Your User ID: \<span id="userIdDisplay" class="font-semibold"\>Loading...\</span\>\</p\>

        \</header\>

        \<\!-- Interactive Form for Data Entry (Conceptually the "First Table") \--\>

        \<section class="bg-white shadow-xl rounded-lg p-6 mb-8"\>

            \<h2 class="text-2xl font-semibold mb-6 text-gray-700 border-b pb-3"\>Enter New Lock Box Information\</h2\>

            \<\!-- Changed div to form \--\>

            \<form id="entryForm" class="space-y-6"\>

                \<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-x-6 gap-y-4"\>

                    \<div\>

                        \<label for="property" class="block text-sm font-medium text-gray-700"\>Property Name \<span class="text-red-500"\>\*\</span\>\</label\>

                        \<input type="text" id="property" class="input-field" placeholder="e.g., Main Street Complex" list="propertyDatalist"\>

                        \<datalist id="propertyDatalist"\>\</datalist\>

                    \</div\>

                    \<div\>

                        \<label for="unitNumber" class="block text-sm font-medium text-gray-700"\>Unit Number \<span class="text-red-500"\>\*\</span\>\</label\>

                        \<input type="text" id="unitNumber" class="input-field" placeholder="e.g., Apt 101 or SFP" list="unitDatalist"\>

                        \<datalist id="unitDatalist"\>\</datalist\>

                    \</div\>

                    \<div\>

                        \<label for="propertyLockBoxLocation" class="block text-sm font-medium text-gray-700"\>Property Lock Box Location\</label\>

                        \<input type="text" id="propertyLockBoxLocation" class="input-field" placeholder="e.g., Main Gate"\>

                    \</div\>

                    \<div\>

                        \<label for="propertyLockBoxCode" class="block text-sm font-medium text-gray-700"\>Property Lock Box Code\</label\>

                        \<input type="text" id="propertyLockBoxCode" class="input-field" placeholder="e.g., 1234"\>

                    \</div\>

                    \<div\>

                        \<label for="unitLockBoxLocation" class="block text-sm font-medium text-gray-700"\>Unit Lock Box Location\</label\>

                        \<input type="text" id="unitLockBoxLocation" class="input-field" placeholder="e.g., Unit Front Door"\>

                    \</div\>

                    \<div\>

                        \<label for="unitLockBoxCode" class="block text-sm font-medium text-gray-700"\>Unit Lock Box Code\</label\>

                        \<input type="text" id="unitLockBoxCode" class="input-field" placeholder="e.g., 5678"\>

                    \</div\>

                    \<div\>

                        \<label for="lastVisitedDate" class="block text-sm font-medium text-gray-700"\>Last Visited Date\</label\>

                        \<input type="date" id="lastVisitedDate" class="input-field"\>

                    \</div\>

                    \<div\>

                        \<label for="lastVisitedBy" class="block text-sm font-medium text-gray-700"\>Last Visited By\</label\>

                        \<input type="text" id="lastVisitedBy" class="input-field" placeholder="e.g., John Doe"\>

                    \</div\>

                    \<div\>

                        \<label for="lastKnownLBCode" class="block text-sm font-medium text-gray-700"\>Last Known-LB Code\</label\>

                        \<input type="text" id="lastKnownLBCode" class="input-field" placeholder="e.g., PREV999"\>

                    \</div\>

                \</div\>

                \<div class="flex flex-col sm:flex-row justify-end space-y-2 sm:space-y-0 sm:space-x-3 pt-4"\>

                    \<\!-- Added type="button" to buttons \--\>

                    \<button type="button" id="resetButton" class="btn btn-secondary w-full sm:w-auto"\>Reset Fields\</button\>

                    \<button type="button" id="saveButton" class="btn btn-primary w-full sm:w-auto" disabled\>Save Information\</button\>

                \</div\>

            \</form\> \<\!-- Corresponding closing form tag \--\>

        \</section\>

        \<\!-- Saved Data Table (The "Second Table") \--\>

        \<section class="bg-white shadow-xl rounded-lg p-6"\>

            \<h2 class="text-2xl font-semibold mb-6 text-gray-700 border-b pb-3"\>Lock Box Information Overview\</h2\>

             \<div class="overflow-x-auto table-container"\>

                \<table id="savedDataTable" class="min-w-full divide-y divide-gray-200"\>

                    \<thead class="bg-gray-50"\>

                        \<tr\>

                            \<th class="th-cell"\>Property\</th\>

                            \<th class="th-cell"\>Unit \#\</th\>

                            \<th class="th-cell"\>Prop LB Loc\</th\>

                            \<th class="th-cell"\>Prop LB Code\</th\>

                            \<th class="th-cell"\>Unit LB Loc\</th\>

                            \<th class="th-cell"\>Unit LB Code\</th\>

                            \<th class="th-cell"\>Visited Date\</th\>

                            \<th class="th-cell"\>Visited By\</th\>

                            \<th class="th-cell"\>Last Known LBC\</th\>

                        \</tr\>

                    \</thead\>

                    \<tbody id="savedDataTableBody" class="bg-white divide-y divide-gray-200"\>

                        \<tr\>

                            \<td colspan="9" class="td-cell text-center text-gray-500"\>Loading data...\</td\>

                        \</tr\>

                    \</tbody\>

                \</table\>

            \</div\>

        \</section\>

    \</div\>

    \<\!-- Message Modal \--\>

    \<div id="messageModal" class="modal-backdrop hidden"\>

        \<div class="modal-content"\>

            \<div class="flex justify-between items-center mb-1"\>

                \<h3 id="messageModalTitle" class="modal-title"\>Message\</h3\>

                \<button id="messageModalCloseButton" class="modal-close-button"\>

                    \<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"\>\<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"\>\</path\>\</svg\>

                \</button\>

            \</div\>

            \<p id="messageModalText" class="modal-body"\>\</p\>

            \<div class="text-right mt-6"\>

                \<button id="messageModalConfirmButton" class="btn btn-primary"\>OK\</button\>

            \</div\>

        \</div\>

    \</div\>

    \<script type="module"\>

        // Firebase Imports

        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";

        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";

        import { getFirestore, collection, addDoc, query, onSnapshot, orderBy, serverTimestamp, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // \--- Embedded CSV Data \---

        const csvData \= \`

,,,,,,,,,

\#,ACTIVE PROPERTIES,OWNER ACCOUNT NAME,,OCCUPIED,LISTED,VACANT,,,

,,,UNIT NUMBER,,,,,,

,,,,,,,VACANCY REASON,TARGET LISTING DATE,

1,11916 Tarragon Rd Unit H,MVSM Properties LLC,SFP,/,,,OCCUPIED,,

2,4522 Curtis Ave,Weijun Wang,4522C-1F,/,,,OCCUPIED,,

,,,4522C-1R,/,,,OCCUPIED,,

,,,4522C-2,/,,,OCCUPIED,,

5,6023 Gwynn Oak Ave,6023 Gwynn Oak Ave LLC,6023G-101,,,/,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-102,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-103,,,/,appoval email sent T2B5T5W,,

,,,6023G-104,,/ ,,LISTED,,

,,,6023G-201,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-202,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-203,/,,,"No lead cert, no license (Will discussed it with zap)",,

,,,6023G-204,,,/,"unit turn long ovedue

TL4VB3EB",,

,,,6023G-B1,,,/,unit turn pending TWBAEYIB,,

,,,6023G-B2,,,/,"long overdue

TJRPX0KB",,

15,130 Hammershire Road,MVSM Properties LLC,SFP,,,/,unit turn client TUTLPHBB,,

17,1891 Grempler Way,1891 Grempler LLC,SFP,/,,,OCCUPIED,,

18,1922 Eloise Lane,MVSM Properties LLC,SFP,,,/,property is for sale client \#241536,,

19,203 Hammershire Road,Amarish Pathak,SFP,/,,,OCCUPIED,,

20,21 S Castle Street,Elizabeth Cheever,SFP,/,,,OCCUPIED,,

21,3413 Esther Place,Terry Gene Pricer JR,SFP,/,,,OCCUPIED,,

22,5904 Falkirk Road,Monsurat Shittu,SFP,/,,,OCCUPIED,,

23,27 Tallow Court,Mohammad Khan,SFP,/,,,OCCUPIED,,

24,45 Tallow Court ,Mohammad Khan,SFP,/,,,OCCUPIED,,

25,1727 Park Avenue,Gary Anderson,SFP,/,,,OCCUPIED,,

31,1615 Cole St,Weijun Wang,SFP,,,/,this property is for sale.,,

32,1239 Glyndon Ave,Donald Panda,SFP,/,,,OCCUPIED,,

33,611 E 37th St,Deyo Johnson,611e37-1F,,,/,unit turn for approval T4VMIRW,,

,,,611e37-2F,,,/,client lives here,,

 ,610 Kingfisher Rd,Jennifer & Kevin Gladden,SFP,/,,,OCCUPIED,,

36,23 S Calhoun St,Ray Christopher Brewer,23sCal-1,/,,,OCCUPIED,,

,,,23sCal-2,/,,,OCCUPIED,,

,,,23sCal-3,/,,,OCCUPIED,,unit turn completed T5QLF6HB

40,1450 Broening Hwy,Dariusz & Hanna Czubacki,SFP,/,,,OCCUPIED,,

41,527 S. Decker,Dariusz & Hanna Czubacki,SFP,/,,,OCCUPIED,,

42,3533 Reisterstown Rd,3533 REISTERSTOWN ROAD LLC,SFP,,,/,client took over Move out insp/replace locks & unit turn,,

43,220 S Augusta Ave,Michmar LLC,220sAug-1F,/,,,OCCUPIED,,

,,,220sAug-2F,,,/,NOT LISTED \- NO UPDATED RENTAL LICENSE,,

,,,220sAug-1&2R,/,,,evicted 06/4/24 \- client did the drill nd replace,,

44,203 S Augusta Ave,Michmar LLC,203sAug-1,,,/,never been tenanted,,

,,,203sAug-2,,,/,NO license- Client will take care of the License TENANT MOVED TO MCKEAN,,

,,,203sAug-3,/,,,OCCUPIED,,

47,234 S Loudon Ave,Michmar LLC,SFP,/,,,OCCUPIED,,

48,42 S Morley St,Michmar LLC,SFP,/,,,OCCUPIED,,

49,85 S Morley St,Michmar LLC,SFP,/,,,OCCUPIED,,

50,42 S Kossuth St,Michmar LLC,SFP,,,/,NO license- Client will take care of the License,,

51,48 S Kossuth St,Michmar LLC,SFP,/,,,OCCUPIED,,

52,40 S Kossuth St,Michmar LLC,SFP,,,/,home rental inspection cancelled. client will handle TNT5YIHB,,

53,44 S Kossuth St,Michmar LLC,SFP,/,,,OCCUPIED,,

54,46 S Kossuth St,Michmar LLC,SFP,/,,,OCCUPIED,,

55,347 Martingale Ave,Letoya Fields Ogallo,SFP,,,/,Tenant just moved out 02/04/2025-Coordinated with clyde about the lead cert,,

56,3012 W Garrison Ave,Gladys Ononjobi,SFP,/,,,OCCUPIED,,

57,136 Coralwood Rd,Helen M. Moan,SFP,/,,,OCCUPIED,,

58,2152 Hollins St,Melanie Turner,SFP,/,,,OCCUPIED,,

59,2005 N Wolfe Street,Triple J Noble Investments,SFP,,,/,TENANTS EVICTED ,,

60,1111 Hollins St,Anthony Corradetti,SFP,,,/,unit turn approval pending T8FWR8X,,

61,10547 Twin Rivers Rd Unit F-2,Josephine Tao Saba,SFP,/,,,OCCUPIED,,

62,701 Venable,Vinh Quoc Diep,SFP,/,,,OCCUPIED,,

63,2736 Kinsey Ave,2736 Kinsey LLC,SFP,,,/,unit turn handled client TA6W3ZV,,

65,3800 Meghan Dr \#3A,Raymond McRae,SFP,/,,,OCCUPIED,,

66,802 Corktree Rd ,Fanuel Chirombo,SFP,/,,,OCCUPIED,,

71,1116 W Hamburg St,Hassen H. Mender,SFP,/,,,OCCUPIED,,

73,2703 White Ave,Anthony Alicea,SFP,/,,,OCCUPIED,,

74,1113 Hollins St,Anthony Corradetti,SFP,,,/,unit turn approval email sent TMEFB6Q,,

77,2506 McHenry St,Taylor Estate 2 LLC,SFP,/,,,OCCUPIED,,

78,1903 Grinnalds,Taylor Estate 2 LLC,SFP,/,,,OCCUPIED,,

80,2510 Lauretta Ave,2510 LAURETTA AVE LLC,SFP,,,/,Tenant move out; 11/13/2024- For lead inspection,,

81,4012 Clarks Ln,Jixu Xiao,SFP,/,,,OCCUPIED,,

82,4246 Nicholas Ave,4246 Nicholas LLC,SFP,/,,,tenant placement,,

85,4109 Morrison Ct,Barry Leathers Jr,SFP,/,,,OCCUPIED,,

86,115 Cross Keys Rd Unit R115E,Bryan Mckay,SFP,/,,,OCCUPIED,,

87,437 S Pulaski St,Erinc Emer,SFP,,/,,LISTED,,

91,10108 Blansford Way ,Jenell Ellis,SFP,/,,,OCCUPIED,,

92,4014 Clarks Ln,Jixu Xiao,SFP,/,,,OCCUPIED,,

94,414 Water St,Michael Brown,SFP,,,/,OCCUPIED,,

95,3744 Elmley Ave ,Michael Akinbaleye,SFP,/,,,OCCUPIED,,

98,9746 Harvester Cir,Amit Bhusal,SFP,/,,,OCCUPIED,,

101,414 Water St,Kristofer O Bryant,SFP,,,/,CLIENT TERM,,

105,7941 Saint Gregory Dr,Zheng Ling Bin,SFP,/,,,OCCUPIED,,

106,1226 E Chase St,Carla Colson,SFP,/,,,OCCUPIED,,

107,748 E 36th St,Joel Brown,SFP,/,,,inspection fail list completed TJLFV8V,,

108,2733 Ellicott Dr,Joel Brown,SFP,/,,,OCCUPIED,,

109,3406 Woodbine Ave,Joel Brown,3406Woo-1,/,,,OCCUPIED,,

,,,3406Woo-2,,,/,OCCUPIED,,

112,5 S Conkling St,Luciana E Holdings LLC,SFP,/,,,OCCUPIED,,

113,2558 Aisquith St,Erin Langley,SFP,/,,,OCCUPIED,,

114,2139 Whistler Ave,Erin Langley,SFP,/,,,OCCUPIED,,

115,3232 Elmley Ave,Erin Langley,SFP,/,,,OCCUPIED,,

116,1218 Bentalou St,Erin Langley,SFP,/,,,OCCUPIED,,

117,3200 Carlisle  Ave,Erin Langley,3200Car-1,/,,,OCCUPIED,,

,,,3200Car-2,/,,,OCCUPIED,,

119,1639 N Warwick Ave,Erin Langley,SFP,/,,,OCCUPIED,,

120,2526 Cecil Ave,Erin Langley,SFP,/,,,OCCUPIED,,

128,805 McKean Ave,Nicholas Noll,SFP,/,,,OCCUPIED,,

131,2758 Wilkens Ave,Palmetto State Enterprise LLC,SFP,/,,,OCCUPIED,,

132,3520 Ellamont Rd,Attallah Banks,SFP,,,/,no updates,,

136,1024 N Carey St ,Adewale Adeleye,1024nCar-1,/,,,OCCUPIED,,

,,,1024nCar-2,/,,,OCCUPIED,,

,45 S Morley Street,michmar LLC,SFP,,,/,RENTAL LICENSE UPDATED. NOT LISTED,,

,133 Denison Street ,Nick Daurio(VCAP),133Den-1,,,/,TENANT MOVED OUT UNIT TURN TVE4PD3,,

,,,133Den-2,,,/,Unit Turn,,

,144 Palormo Ave ,Nick Daurio(VCAP),SFP,,,/,No license,,

,214 N Fulton Ave,Nick Daurio(BRF1),SFP,,,/,No license,,

,2114 Vine Street,Nick Daurio(BRF1),SFP,,,/,No license,,

,236 S Clinton St ,Danielle Duckett,SFP,,,/,CLIENT TERM,,

,402 S Calhoun,Nick Daurio(BRF1),SFP,,,/,No lead cert,,

,512 N Glover Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,526 N Clover ,Nick Daurio(BRF1),SFP,,,/,NOT LISTED NO RENTAL LICENSE,,

,542 Brunswick St ,Nick Daurio(VCAP),SFP,,,/,"TENANT MOVED OUT UNIT TURN

TUG3B9Y",,

,616 N WOODINGTON,Ganiyat Lawal,616 N WOODINGTON Unit 1,/,,,OCCUPIED,,

,,,616 N WOODINGTON Unit 2,/,,,OCCUPIED,,

,,,616 N WOODINGTON Unit 3,,/,,LISTED,,

,625 McCollough Cir,Gail Rearden,SFP,,,/,NO LICENSE,,

,1123 N Mount St.,,SFP,,,/,UPDATED LICENSE NOT LISTED,,

,637 E 29th St,Rodney Mason,SFP,,,/,UPDATE LICENSE NOT LISTED,,

,721 Appleton Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1108 N MOUNT ST,Adaobi Herlich,1108 N MOUNT ST Unit 1,,,/,OCCUPIED,,

,,,1108 N MOUNT ST Unit 2,,,/,OCCUPIED,,

,1203 N Milton Ave,Nick Daurio(BRF1),SFP,,,/,UNIT TURN TGY041V,,

,1239 N Decker Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1323 N Milton Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1339 Ramsay Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1402 Mosher Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1420 Aisquith Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1424 Aisquith St ,Nick Daurio(VCAP),SFP,,,/,NO LICENSE NOT LISTED,,

,1516 Cliftview Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1523 W FAIRMOUNT AVE,Marquell Scott,SFP,,/,,LISTED,,

,1612 Eastern Ave ,John Childress,1612 Eastern Ave  Apt 1,/,,,OCCUPIED,,

,,,1612 Eastern Ave Apt 2,,,/,NOT LISTED,,

,1616 PLUM ST ,Edmundo Safdie,1616 PLUM ST Unit 2,,,/,NO LICENSE NO UPDATES,,

,1706 N Monroe Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NO UPDATES,,

,1710 E 28TH ST,Erick Garski,SFP,,,/,EXPIRED IICENSE,,

,1710 Ramsay Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1713 E 30TH,Amit Shenoy,SFP,,,/,UPDATED LICENSE NOT LISTED,,

,1715 N Washington St,Nick Daurio(VCAP),SFP,,,/,NO LICENSE NOT LISTED,,

,1733 N Bond St ,Nick Daurio(VCAP),SFP,,,/,NO LICENSE NOT LISTED,,

,1755 Abbotston St ,Raymond Mends,SFP,,,/,TPA,,

,1807 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1811 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1813 N Collington Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1823 N Chapel,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1824 N Collington Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE NOT LISTED,,

,1827 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1831 N Dallas Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1833 N Chapel Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1909 E Oliver Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1910 Wilhelm Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1912 Wilhelm Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,1924 Wilhelm Street ,Nick Daurio(BRF1),SFP,,,/,NO LICENSE  NOT LISTED,,

,1944 Harlem Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,2005 N Wolfe Street ,Tierra Joseph- Triple J Noble Investments,SFP,,,/,Unit Turn,,

,2012 E Lafayette Ave ,Nick Daurio(VCAP),SFP,,,/,NO LICENSE,,

,2013 N Longwood Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,2114 Vine Street,Nick Daurio(BRF1),SFP,,,/,NO LICENSE,,

,2243 E Biddle Street,Nick Daurio(BRF1),SFP,,,/,NOLICENSE,,

,2304 W NORTH AVE,Ashley Kansinally,2304 W NORTH AVE. Unit 1,/,,,OCCUPIED,,

,,,2304 W NORTH AVE. Unit 2,,/,/,LISTED,,

,,,2304 W NORTH AVE B|Booth-1,/,,,OCCUPIED,,

,,,2304 W NORTH AVE B|Booth-2,,/,/,LISTED,,

,,,2304 W NORTH AVE B|Booth-3,,,/,No Lead cert,,

,,,2304 W NORTH AVE B|Booth-4,,,/,No Lead cert,,

,2332 W Baltimore Street,Nick Daurio(BRF1),SFP,,,/,No Lead cert,,

,2409 E Oliver St ,Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,2416 E Oliver Street,Nick Daurio(BRF1),SFP,,,/,On going home inspection and Lead inspection,,

,2440 CALLOW AVE ,Renika Ramsay,2440 CALLOW AVE UNIT 1,/,,,OCCUPIED,,

,,,2440 CALLOW AVE UNIT 2,,/,/,LISTED,,

,,,2440 CALLOW AVE UNIT 3,,/,/,LISTED,,

,2515 W Fairmount Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,"2520 Mosher St,",Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,2520 W Franklin St,Nick Daurio(VCAP),SFP,,,/,On going home inspection and Lead inspection,,

,2556 W Fairmount Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2616 Orleans Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2627 Hafer Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2629 Llewelyn Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2640 Lauretta Ave,Anwar Minni \-2640Lau,SFP,,,/,License is soon to expire( task created) and no Lead cert,,

,2692 Dulany Street,Nick Daurio(BRF1),SFP,,,/,No License,,

,2730 Winchester Street,Nick Daurio(BRF1),SFP,,,/,No License,,

,"2731 The Alameda,",Joel Brown,SFP,,,/,OCCUPIED,,

,2736 Kinsey Ave,Anwar Minni \- 2736Kin,SFP,,,/,Tenant move Out 04/29/2024 \- For Lead inspection,,

\-,2737 Prospect Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2752 Mosher Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2812 WOODBROOK AVE,Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,2815 Kennedy Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2906 Oakford Ave,Kimberly Aiken/Oakford Ave LLC,SFP,,,/,No lead cert and Unit turn,,

,2918 E Federal St Unit ,Linda Mays,2918 E Federal St Unit  1,,,/,No Lead cert,,

,,,2918 E Federal St Unit 2,,,/,No Lead cert,,

,2919 Belmont Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3001 Kenyon Ave,Vinh Quoc Diep,SFP,/,,,OCCUPIED,,

,3027 Harlem Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3200 Elmora Ave,Raymond Mends,SFP,,,/,Lead cert and Unit turn,,

,3409 Ravenwood Ave,Francis Kamara,SFP,,,/,Lead Inspection fail list,,

,3416 Gwynns Falls Pkwy,Sabina Yasmin,3416 Gwynns Falls Pkwy Room 1,,,/,No license and Lead cert,,

,,,3416 Gwynns Falls Pkwy Room 2,,,/,No license and Lead cert,,

,,,3416 Gwynns Falls Pkwy Room 3,,,/,No license and Lead cert,,

,3428 Hilldale Place,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3434 Edmondson Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,3520 ELLAMONT ROAD,Attallah Banks,SFP,,,/,Unit Turn,,

,3641 Park Heights Ave,Nick Daurio(BRF1),SFP,,,/,UPDATED LICENSE NOT LISTED,,

,4628 REISTERSTOWN ROAD,Nick Daurio(VCAP),SFP,,,/,No license and Lead cert,,

,4814 Curtis Ave,Nick Daurio(BRF1),SFP,,,/,No lead cert,,

,4816 Curtis Ave,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,4818 Curtis Ave,Nick Daurio(BRF1),SFP,,,/,NO LICENSE UNDER VCAP,,

,5421 Denmore Ave,Amit Shenoy,SFP,,,/,NO LICENSE UNDER VCAP,,

,2435 E Hoffman Street,Nick Daurio(BRF1),SFP,,,/,No license and Lead cert,,

,2646 Beryl Ave,Rafael Brown \- Magis,SFP,,/,,LISTED,,

,,,,,,,,,

,,,,,,,,,

,,,,,9,123,,,

\`;

        // \--- Module-scoped variable for parsed CSV property/unit pairs \---

        let parsedCsvItems \= \[\];

        // \--- Firebase Configuration \---

        const firebaseConfig \= typeof \_\_firebase\_config \!== 'undefined' ? JSON.parse(\_\_firebase\_config) : {

            apiKey: "YOUR\_API\_KEY", authDomain: "YOUR\_AUTH\_DOMAIN", projectId: "YOUR\_PROJECT\_ID",

            storageBucket: "YOUR\_STORAGE\_BUCKET", messagingSenderId: "YOUR\_MESSAGING\_SENDER\_ID", appId: "YOUR\_APP\_ID"

        };

        // \--- App Configuration \---

        const appId \= typeof \_\_app\_id \!== 'undefined' ? \_\_app\_id : 'default-lockbox-app';

        const COLLECTION\_NAME \= 'property\_records';

        // \--- Firebase Initialization \---

        let app;

        let db;

        let auth;

        let userId \= null;

        let unsubscribeSnapshot \= null;

        try {

            app \= initializeApp(firebaseConfig);

            db \= getFirestore(app);

            auth \= getAuth(app);

            setLogLevel('debug');

            console.log("Firebase initialized.");

        } catch (error) {

            console.error("Firebase initialization error:", error);

            showMessage("Initialization Error", "Could not initialize the application. Please refresh.");

            const saveBtn \= document.getElementById('saveButton');

            if (saveBtn) saveBtn.disabled \= true;

            const userIdDisp \= document.getElementById('userIdDisplay');

            if (userIdDisp) userIdDisp.textContent \= 'Error';

        }

        // \--- DOM Elements \---

        // Note: entryForm is now a \<form\> element

        const entryForm \= document.getElementById('entryForm'); 

        const propertyInput \= document.getElementById('property');

        const unitNumberInput \= document.getElementById('unitNumber');

        const propertyLockBoxLocationInput \= document.getElementById('propertyLockBoxLocation');

        const propertyLockBoxCodeInput \= document.getElementById('propertyLockBoxCode');

        const unitLockBoxLocationInput \= document.getElementById('unitLockBoxLocation');

        const unitLockBoxCodeInput \= document.getElementById('unitLockBoxCode');

        const lastVisitedDateInput \= document.getElementById('lastVisitedDate');

        const lastVisitedByInput \= document.getElementById('lastVisitedBy');

        const lastKnownLBCodeInput \= document.getElementById('lastKnownLBCode');

        const resetButton \= document.getElementById('resetButton');

        const saveButton \= document.getElementById('saveButton');

        const savedDataTableBody \= document.getElementById('savedDataTableBody');

        const userIdDisplay \= document.getElementById('userIdDisplay');

        const propertyDatalist \= document.getElementById('propertyDatalist');

        const unitDatalist \= document.getElementById('unitDatalist');

        // Modal elements

        const messageModal \= document.getElementById('messageModal');

        const messageModalTitle \= document.getElementById('messageModalTitle');

        const messageModalText \= document.getElementById('messageModalText');

        const messageModalCloseButton \= document.getElementById('messageModalCloseButton');

        const messageModalConfirmButton \= document.getElementById('messageModalConfirmButton');

        // \--- Modal Functions \---

        function showMessage(title, text) {

            if (messageModalTitle) messageModalTitle.textContent \= title;

            if (messageModalText) messageModalText.textContent \= text;

            if (messageModal) messageModal.classList.remove('hidden');

        }

        if (messageModalCloseButton) messageModalCloseButton.onclick \= () \=\> messageModal.classList.add('hidden');

        if (messageModalConfirmButton) messageModalConfirmButton.onclick \= () \=\> messageModal.classList.add('hidden');

        if (messageModal) {

            messageModal.onclick \= (event) \=\> {

                if (event.target \=== messageModal) {

                    messageModal.classList.add('hidden');

                }

            };

        }

        // \--- CSV Parsing and Datalist/Property List Population \---

        function parseCSVAndPopulateDatalistsAndProperties(csvString) {

            const lines \= csvString.trim().split('\\n');

            const uniquePropertiesForDatalist \= new Set();

            const uniqueUnitsForDatalist \= new Set();

            

            const tempParsedItems \= \[\]; // For collecting property/unit pairs for the table

            let currentPropertyContext \= "";

            // Column indices from CSV structure

            const dataStartIndex \= 4; // Estimated start of actual data

            const propertyColIndex \= 1; // "ACTIVE PROPERTIES"

            const unitColIndex \= 3;     // "UNIT NUMBER"

            for (let i \= dataStartIndex; i \< lines.length; i++) {

                const line \= lines\[i\].trim();

                if (\!line) continue; 

                const columns \= line.split(','); 

                const propertyName \= columns.length \> propertyColIndex ? columns\[propertyColIndex\].trim() : "";

                const unitName \= columns.length \> unitColIndex ? columns\[unitColIndex\].trim() : "";

                // For Datalists

                if (propertyName && propertyName \!== "\#" && propertyName \!== "ACTIVE PROPERTIES") {

                    uniquePropertiesForDatalist.add(propertyName);

                    currentPropertyContext \= propertyName; // Update context for property/unit pairs

                }

                if (unitName && unitName \!== "UNIT NUMBER" && unitName.toUpperCase() \!== "SFP") {

                    uniqueUnitsForDatalist.add(unitName);

                }

                 if (unitName && unitName \!== "UNIT NUMBER" && unitName.toUpperCase() \=== "SFP") { // Also add SFP to unit datalist

                    uniqueUnitsForDatalist.add("SFP");

                }

                // For Property/Unit pairs table (parsedCsvItems)

                if (propertyName && propertyName \!== "\#" && propertyName \!== "ACTIVE PROPERTIES") {

                    // This line defines a new property (or re-defines one)

                    if (unitName && unitName \!== "UNIT NUMBER") {

                        tempParsedItems.push({ property: propertyName, unit: unitName });

                    } else { // Property listed, but unit is SFP or effectively blank for this specific line's unit col

                        tempParsedItems.push({ property: propertyName, unit: "SFP" }); // Default to SFP if no specific unit on property line

                    }

                } else if (unitName && unitName \!== "UNIT NUMBER" && currentPropertyContext) {

                    // This line has no property, but has a unit, so it belongs to currentPropertyContext

                    tempParsedItems.push({ property: currentPropertyContext, unit: unitName });

                }

            }

            

            // Populate Datalists

            if (propertyDatalist) {

                propertyDatalist.innerHTML \= ''; 

                uniquePropertiesForDatalist.forEach(prop \=\> {

                    if (prop) { 

                        const option \= document.createElement('option');

                        option.value \= prop;

                        propertyDatalist.appendChild(option);

                    }

                });

            }

            if (unitDatalist) {

                unitDatalist.innerHTML \= ''; 

                uniqueUnitsForDatalist.forEach(unit \=\> {

                     if (unit) { 

                        const option \= document.createElement('option');

                        option.value \= unit;

                        unitDatalist.appendChild(option);

                    }

                });

            }

            console.log("Datalists populated:", { numProperties: uniquePropertiesForDatalist.size, numUnits: uniqueUnitsForDatalist.size });

            // Deduplicate and finalize parsedCsvItems for the table

            const uniqueCsvItemsMap \= new Map();

            tempParsedItems.forEach(item \=\> {

                if (item.property) { // Ensure property is not empty

                     uniqueCsvItemsMap.set(\`${item.property}|${item.unit}\`, item);

                }

            });

            parsedCsvItems \= Array.from(uniqueCsvItemsMap.values());

            console.log("Parsed CSV items for table:", parsedCsvItems.length, parsedCsvItems.slice(0,5)); // Log count and a few items

        }

        // \--- Authentication \---

        onAuthStateChanged(auth, async (user) \=\> {

            if (user) {

                userId \= user.uid;

                console.log("User authenticated. UID:", userId);

                if (userIdDisplay) userIdDisplay.textContent \= userId;

                if (saveButton) saveButton.disabled \= false;

                loadAndDisplaySavedData(); // This will trigger renderSavedDataTable

            } else {

                console.log("User not authenticated. Attempting sign-in.");

                if (userIdDisplay) userIdDisplay.textContent \= "Authenticating...";

                if (saveButton) saveButton.disabled \= true;

                // Attempt to render table with CSV data even if auth fails, then show auth error

                renderSavedDataTable(\[\]); // Show CSV structure initially

                if (typeof \_\_initial\_auth\_token \=== 'undefined' || \!\_\_initial\_auth\_token) {

                    try {

                        await signInAnonymously(auth);

                    } catch (error) {

                        console.error("Error signing in anonymously:", error);

                        userId \= \`error-anon-${crypto.randomUUID().slice(0,8)}\`;

                        if (userIdDisplay) userIdDisplay.textContent \= \`Error (Session ID: ${userId})\`;

                        showMessage("Authentication Error", "Could not sign in anonymously. Saved data cannot be loaded or new data saved reliably.");

                    }

                } else {

                    userId \= \`error-custom-${crypto.randomUUID().slice(0,8)}\`;

                    if (userIdDisplay) userIdDisplay.textContent \= \`Auth Failed (ID: ${userId})\`;

                }

            }

        });

        async function initializeAuth() {

            if (\!auth) {

                console.error("Auth service not available for initializeAuth.");

                if (userIdDisplay) userIdDisplay.textContent \= 'Auth Error';

                renderSavedDataTable(\[\]); // Show CSV structure initially

                return;

            }

            if (typeof \_\_initial\_auth\_token \!== 'undefined' && \_\_initial\_auth\_token) {

                try {

                    await signInWithCustomToken(auth, \_\_initial\_auth\_token);

                } catch (error) {

                    console.error("Error with signInWithCustomToken:", error);

                    showMessage("Authentication Error", \`Failed to sign in with token: ${error.message}. Attempting anonymous sign-in.\`);

                    try {

                        await signInAnonymously(auth);

                    } catch (anonError) {

                        console.error("Fallback anonymous sign-in error:", anonError);

                        userId \= \`error-fallback-${crypto.randomUUID().slice(0,8)}\`;

                        if (userIdDisplay) userIdDisplay.textContent \= \`Critical Auth Error (ID: ${userId})\`;

                        showMessage("Critical Auth Error", "Could not sign in. App functionality is severely limited.");

                        renderSavedDataTable(\[\]); // Show CSV structure

                    }

                }

            } else {

                if (\!auth.currentUser) {

                    try {

                        await signInAnonymously(auth);

                    } catch (error) {

                        console.error("Error signing in anonymously (initial attempt):", error);

                         userId \= \`error-init-anon-${crypto.randomUUID().slice(0,8)}\`;

                        if (userIdDisplay) userIdDisplay.textContent \= \`Init Auth Error (ID: ${userId})\`;

                        renderSavedDataTable(\[\]); // Show CSV structure

                    }

                } else {

                    // Already authenticated (e.g. existing session), onAuthStateChanged will handle it.

                    // loadAndDisplaySavedData will be called by onAuthStateChanged.

                }

            }

        }

        

        if (auth) {

            initializeAuth();

        } else {

            // If auth itself failed to init, still try to show CSV data

            document.addEventListener('DOMContentLoaded', () \=\> {

                 parseCSVAndPopulateDatalistsAndProperties(csvData);

                 renderSavedDataTable(\[\]);

                 if (propertyInput) propertyInput.focus();

            });

        }

        // \--- Form Handling \---

        function resetForm() {

            // entryForm is now guaranteed to be a \<form\> element

            if (entryForm && typeof entryForm.reset \=== 'function') {

                 entryForm.reset();

            } else if (entryForm) {

                // Fallback for manual reset if entryForm is not a form or reset is missing

                // (should not happen with the HTML change, but good for robustness)

                console.warn("entryForm.reset() is not available. Manually resetting fields.");

                propertyInput.value \= '';

                unitNumberInput.value \= '';

                propertyLockBoxLocationInput.value \= '';

                propertyLockBoxCodeInput.value \= '';

                unitLockBoxLocationInput.value \= '';

                unitLockBoxCodeInput.value \= '';

                lastVisitedDateInput.value \= '';

                lastVisitedByInput.value \= '';

                lastKnownLBCodeInput.value \= '';

            }

            if (propertyInput) propertyInput.focus();

        }

        async function handleSave() {

            if (\!userId || userId.startsWith('error-')) { // Check for actual userId

                showMessage("Error", "User not properly authenticated. Cannot save data.");

                if (saveButton) saveButton.disabled \= true;

                return;

            }

            if (\!db) {

                showMessage("Error", "Database not available. Cannot save data.");

                return;

            }

            const property \= propertyInput.value.trim();

            const unitNumber \= unitNumberInput.value.trim();

            if (\!property || \!unitNumber) {

                showMessage("Validation Error", "Property Name and Unit Number are required.");

                return;

            }

            const dataToSave \= {

                property: property,

                unitNumber: unitNumber,

                propertyLockBoxLocation: propertyLockBoxLocationInput.value.trim(),

                propertyLockBoxCode: propertyLockBoxCodeInput.value.trim(),

                unitLockBoxLocation: unitLockBoxLocationInput.value.trim(),

                unitLockBoxCode: unitLockBoxCodeInput.value.trim(),

                lastVisitedDate: lastVisitedDateInput.value,

                lastVisitedBy: lastVisitedByInput.value.trim(),

                lastKnownLBCode: lastKnownLBCodeInput.value.trim(),

                timestamp: serverTimestamp(),

                savedByUserId: userId

            };

            try {

                if (saveButton) saveButton.disabled \= true;

                if (saveButton) saveButton.textContent \= 'Saving...';

                const collectionPath \= \`/artifacts/${appId}/users/${userId}/${COLLECTION\_NAME}\`;

                const docRef \= await addDoc(collection(db, collectionPath), dataToSave);

                console.log("Document written with ID: ", docRef.id);

                showMessage("Success", "Information saved successfully\!");

                resetForm(); // This should now work correctly

                // onSnapshot will automatically update the table

            } catch (error) {

                console.error("Error adding document: ", error);

                showMessage("Error", \`Could not save information: ${error.message}\`);

            } finally {

                 if (saveButton) saveButton.disabled \= false;

                 if (saveButton) saveButton.textContent \= 'Save Information';

            }

        }

        if (resetButton) resetButton.addEventListener('click', resetForm);

        if (saveButton) saveButton.addEventListener('click', handleSave);

        // \--- Data Display Logic for the Second Table \---

        function renderSavedDataTable(firestoreDocsArray \= \[\]) {

            if (\!savedDataTableBody) {

                console.error("Target table body 'savedDataTableBody' not found in DOM.");

                return;

            }

            savedDataTableBody.innerHTML \= ''; // Clear existing content

            const firestoreDataMap \= new Map();

            firestoreDocsArray.forEach(docData \=\> {

                // Assuming docData contains property and unitNumber fields

                // Since Firestore query is ordered by timestamp desc,

                // this will keep the latest entry for a given property-unit pair.

                if(docData.property && docData.unitNumber) {

                    firestoreDataMap.set(\`${docData.property}-${docData.unitNumber}\`, docData);

                }

            });

            const displayedItems \= new Set(); // To track property-unit pairs already rendered from CSV \+ Firestore

            // 1\. Iterate through CSV items and merge with Firestore data

            parsedCsvItems.forEach(csvItem \=\> {

                const key \= \`${csvItem.property}-${csvItem.unit}\`;

                const savedData \= firestoreDataMap.get(key);

                const dataToDisplay \= savedData || csvItem; // Use Firestore data if available, else CSV structure

                const row \= savedDataTableBody.insertRow();

                const addCell \= (text) \=\> {

                    const cell \= row.insertCell();

                    cell.textContent \= text || '-';

                    cell.className \= 'td-cell';

                };

                addCell(dataToDisplay.property);

                addCell(dataToDisplay.unit); // unit from CSV or unitNumber from Firestore

                addCell(savedData ? savedData.propertyLockBoxLocation : '-');

                addCell(savedData ? savedData.propertyLockBoxCode : '-');

                addCell(savedData ? savedData.unitLockBoxLocation : '-');

                addCell(savedData ? savedData.unitLockBoxCode : '-');

                addCell(savedData ? savedData.lastVisitedDate : '-');

                addCell(savedData ? savedData.lastVisitedBy : '-');

                addCell(savedData ? savedData.lastKnownLBCode : '-');

                

                displayedItems.add(key);

            });

            // 2\. Add any Firestore items that were not in the CSV list

            firestoreDocsArray.forEach(docData \=\> {

                if (docData.property && docData.unitNumber) {

                    const key \= \`${docData.property}-${docData.unitNumber}\`;

                    if (\!displayedItems.has(key)) {

                        const row \= savedDataTableBody.insertRow();

                        const addCell \= (text) \=\> {

                            const cell \= row.insertCell();

                            cell.textContent \= text || '-';

                            cell.className \= 'td-cell';

                        };

                        addCell(docData.property);

                        addCell(docData.unitNumber);

                        addCell(docData.propertyLockBoxLocation);

                        addCell(docData.propertyLockBoxCode);

                        addCell(docData.unitLockBoxLocation);

                        addCell(docData.unitLockBoxCode);

                        addCell(docData.lastVisitedDate);

                        addCell(docData.lastVisitedBy);

                        addCell(docData.lastKnownLBCode);

                    }

                }

            });

            if (savedDataTableBody.rows.length \=== 0\) {

                const tr \= savedDataTableBody.insertRow();

                const td \= tr.insertCell();

                td.colSpan \= 9;

                td.textContent \= 'No property data found in CSV or no saved records.';

                td.className \= 'td-cell text-center text-gray-500 py-4';

            }

        }

        async function loadAndDisplaySavedData() {

            if (\!userId || userId.startsWith('error-') || \!db) {

                const reason \= \!userId || userId.startsWith('error-') ? "User not authenticated properly." : "Database not available.";

                console.log(\`Cannot load saved data: ${reason}\`);

                // Render table with CSV data only if auth/db issues prevent Firestore fetch

                // This is now handled by onAuthStateChanged calling renderSavedDataTable(\[\]) on failure.

                // Or if parsedCsvItems is ready, call it:

                if(parsedCsvItems.length \> 0\) {

                    renderSavedDataTable(\[\]);

                } else {

                     if (savedDataTableBody) savedDataTableBody.innerHTML \= \`\<tr\>\<td colspan="9" class="td-cell text-center text-gray-500"\>${reason} Cannot load saved data.\</td\>\</tr\>\`;

                }

                return;

            }

            if (unsubscribeSnapshot) {

                unsubscribeSnapshot(); 

                unsubscribeSnapshot \= null;

            }

            const collectionPath \= \`/artifacts/${appId}/users/${userId}/${COLLECTION\_NAME}\`;

            console.log(\`Listening for saved data from: ${collectionPath}\`);

            const q \= query(collection(db, collectionPath), orderBy("timestamp", "desc"));

            unsubscribeSnapshot \= onSnapshot(q, (querySnapshot) \=\> {

                console.log(\`Received snapshot. Empty: ${querySnapshot.empty}, Size: ${querySnapshot.size}\`);

                const firestoreDocsArray \= querySnapshot.docs.map(doc \=\> ({ id: doc.id, ...doc.data() }));

                renderSavedDataTable(firestoreDocsArray);

            }, (error) \=\> {

                console.error("Error fetching saved data with onSnapshot:", error);

                if (savedDataTableBody) {

                     savedDataTableBody.innerHTML \= \`\<tr\>\<td colspan="9" class="td-cell text-center text-red-500"\>Error loading saved data: ${error.message}\</td\>\</tr\>\`;

                }

                showMessage("Data Error", \`Could not load saved records: ${error.message}\`);

            });

        }

        

        // \--- Initial Page Load Actions \---

        document.addEventListener('DOMContentLoaded', () \=\> {

            // Parse CSV for datalists and for the initial table structure

            parseCSVAndPopulateDatalistsAndProperties(csvData);

            

            // Initial render of the table with CSV data.

            // Firestore listener will update it once connected & data is fetched.

            renderSavedDataTable(\[\]); // Render with empty Firestore data initially

                                     // This shows CSV structure.

            

            if (propertyInput) propertyInput.focus();

            

            // initializeAuth is called after Firebase services are confirmed to be available.

            // If auth is not available, a fallback in initializeAuth also calls renderSavedDataTable(\[\]).

        });

    \</script\>

\</body\>

\</html\>


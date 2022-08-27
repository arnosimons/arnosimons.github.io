---
layout: default
type: project
recent: true
date: 2022
title: ScratchBook
themes: 
    - Turntablism
permalink: /scratchbook
---

<head>
    <title>ScratchBook</title>
    <!-- Standard stuff -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- PyScript -->
    <script defer src="https://pyscript.net/alpha/pyscript.js"></script>
    <link rel="stylesheet" href="https://pyscript.net/alpha/pyscript.css"/>
    <py-env>
      - matplotlib
    </py-env>
    <!-- Bootstrap 5.1.3 -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/5.1.3/css/bootstrap.min.css">
    <!-- JQuery -->
    <script src="https://code.jquery.com/jquery-3.5.1.js"></script>
    <!-- Datatables -->
    <script src="https://cdn.datatables.net/1.12.1/js/jquery.dataTables.min.js"></script>
    <script src="https://cdn.datatables.net/1.12.1/js/dataTables.bootstrap5.min.js"></script>
    <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.12.1/css/dataTables.bootstrap5.min.css">
    <!-- Global Styling -->
    <style>
      :root {
          /* --hover-color: rgba(135, 206, 250, 0.124); */
          --hover-color: rgba(0, 0, 0, 0.09);

          /* --blue-light: rgba(135, 206, 250, 0.33); */
          --blue-light: lightskyblue;
          /* --blue-light: #2196F3; */

          --blue-dark: #069;
          --blue-dark: rgb(0, 102, 153);

          --grey-light: #F8F8F8;
          /* --grey-light: #61dd7e; */

          /* --grey-dark: #d8d8d8;
          --grey-dark: #ccc; */
          --grey-dark: rgba(0, 0, 0, 0.125);
          /* --grey-dark: #61dd7e; */

          --black: rgb(33, 37, 41);

          --red:#d13108;
          
      }
      p {
        font-size: 14px;
      }
      a, a.page-link {
        color:var(--blue-dark); 
        font-weight: 300;
        text-decoration:none;
      }  
      a:hover {
        color:var(--blue-dark);
        font-weight: 500;
        text-decoration:none;
      }
      .dark-link {
        color:var(--blue-light); 
        font-weight: 200;
        text-decoration:none;
      }  
      .dark-link:hover  {
        color:var(--blue-light);
        font-weight: 400;
      }
      .dataTables_wrapper { /* Show Entries, Search, Pagination*/
        font-size: 12px;
      }      
      .pagination .page-item.active .page-link { 
        background-color: var(--blue-dark);
        border-color: var(--blue-dark); 
      }
      .pagination .page-link:hover { 
        background-color: var(--hover-color);
      }
      .pagination .page-link:focus { 
        box-shadow: 0 0 3px 3px var(--blue-light)
      }
      .switch {
        position: relative;
        display: inline-block;
        width: 40px;
        height: 22px;
      }
      .switch input { 
        opacity: 0;
        width: 0;
        height: 0;
      }
      .slider {
        position: absolute;
        cursor: pointer;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: var(--grey-dark);
        -webkit-transition: .4s;
        transition: .4s;
        border-radius: 22px;
      }
      .slider:before {
        position: absolute;
        content: "";
        height: 18px;
        width: 18px;
        left: 2px;
        bottom: 2px;
        background-color: white;
        -webkit-transition: .4s;
        transition: .4s;
        border-radius: 50%;
      }
      input:checked + .slider {
        background-color: var(--blue-light);
      }
      input:focus + .slider {
        box-shadow: 0 0 1px var(--blue-light);
      }
      input:checked + .slider:before {
        -webkit-transform: translateX(18px);
        -ms-transform: translateX(18px);
        transform: translateX(18px);
      }
      input.form-control{
        font-size: 14px; 
        font-family: Menlo; 
        color: var(--blue-dark); 
        border-color: var(--blue-light);
        border-radius: 4px;
        border-width: 2px;
        /* box-shadow: 0 0 3px 3px var(--blue-light) */
      }
      input.form-control:focus{
        color: var(--blue-dark);
        border-color: var(--blue-light);
        box-shadow: 0 0 5px 1px var(--blue-light)
      }
      .mybuttons {
        border: solid;
        border-width: 1px;
        border-radius: 3px;
        border-color: var(--grey-dark);
        padding: 3px;
        box-shadow: 0px 2px 0px -1px var(--grey-dark);
        background-color: var(--grey-light);
        font-size: 12px;
        font-weight: 370;
        color:rgb(33, 37, 41);
        text-align: center;
      }
      .mybuttons:hover {
        background-color: var(--hover-color);
      }
      .mybuttons:active {
        transform: scale(.95);
      }
      .card-header:hover{
        background-color: var(--hover-color);
      }
      .card-header {
        background-color: var(--grey-light);
      }
      .btn[data-bs-toggle="collapse"]:focus {
        outline: none !important;
        box-shadow: none;
      }
      .btn[data-bs-toggle="collapse"]:after {
        content: '+'; 
        font-size: 16px;
        font-weight: 50;
        color: var(--black);
        float: right;
      }
      .btn[aria-expanded="true"]:after {
        content: '-'; 
      }
      .btn[aria-expanded="false"]:after {
        content: '+'; 
      }
      .column {
        float: left;
        padding: 0px;
        width: 75px;
      }
      /* Clear floats after the columns */
      /* .row:after {
        content: "";
        display: table;
        clear: both;
      } */
      .switch-row {
        font-size: 12px;
        text-align: center;
        width: auto; 
        margin-left: 0px; 
        margin-right: 1px; 
        margin-bottom: 0px;
      }
      .expert-heading {
        font-size: 13px; 
        font-weight: 500; 
        margin-left: 0px; 
        margin-top:5px; 
        margin-bottom:5px;
      }
      
      
    </style>
  </head>
  <body style="background-color:var(--grey-light);">
    <header style="background-color:rgb(33, 37, 41);box-shadow:0px 4px 3px -1px var(--grey-dark)">
      <div class="container-md p-2.5 bg-dark text-white">
        <h1>ScratchBook &#128221;&#127926;</h1>
        <p style="color: white; font-size: 16px;">A platform for browsing, composing and visualizing scratches in <a class="dark-link" href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>TTM-like notation.</a></p>
        <p style="color: var(--red); font-size: 18px">&#9888; Loading the page takes time. Please be patient until you see the scratch plot.</p>
      </div>
    </header>
    <br/>
    <!-- Visualizer -->
    <div class="container-md pt-3 border rounded" style="background-color: white; box-shadow:0px 2px 0px -1px var(--grey-dark)">
      <div class="panel-group" id="Visualizer">
        <div class="panel panel-default">
          <div class="panel-heading"><h4>Visualizer</h4></div>
          <div class="panel-body">
            <p>Type and visualize your scratch formula...</p>
            <p id="TEST"></p>
            <input 
              id="scratch_input"
              class="form-control" 
              type="text" 
              
              placeholder="Type formula and press ENTER"/>
            <p style="margin-top: 5px;">
              <button 
                id="copy_button" 
                class="mybuttons"
                title="Copy url+formula and share it with your friends.">
                Copy
              </button>
              <button 
                id="download_button"
                class="mybuttons"
                title="Download png image.">
                Download
              </button> 
              <button 
                id="clear_button"
                class="mybuttons"
                title="Clear the input field.">
                Clear
              </button>
              <button 
                id="default_button"
                class="mybuttons"
                title="Reset to default scratch formula.">
                Default
              </button>  
              <button 
                id="surprise_button"
                class="mybuttons"
                title="Pick a scratch at random (currently limited to the Combos collection).">
                Surprise!
              </button>            
              <button 
                id="scratch_button" 
                type="submit" 
                style="border: none; background-color:rgba(255, 255, 255, 0);"
                pys-onClick="plot" >
              </button> 
            </p>
            <div 
              id="session_output" 
              style="padding-bottom: 10px">
            </div>
            <p id="session_message" style="font-size: 14px; color: var(--red)"></p>
            <script>
              $(document).ready(function () {       
                // tooltips for mybuttons
                $('.mybuttons[title]').tooltip({
                  trigger: "hover",
                  "container": 'body',
                });
                // get handlers for key elements
                var default_url = 'https://arnosimons.github.io/scratchbook';
                var default_formula = "kermit + prizm + (chirp / 0.25) * 4";
                var scratch_input = document.getElementById("scratch_input");
                var scratch_button = document.getElementById("scratch_button");
                var session_output = document.getElementById("session_output");
                var session_message = document.getElementById("session_message");
                var urlParams = new URLSearchParams(window.location.search);
                if (urlParams.has("formula")) {scratch_input.value = urlParams.get('formula')} 
                else {scratch_input.value = default_formula}
                // updateURL function
                function updateURL(formula) {
                  formula = formula.trim()
                  if (formula) {window.history.replaceState({}, 'ScratchBook', default_url + '?formula=' + encodeURIComponent(formula))} 
                  else {window.history.replaceState({}, 'ScratchBook', default_url)}
                }
                // Initiate url params
                updateURL(scratch_input.value.trim())
                // Function for scratch_input
                scratch_input.addEventListener("keypress", function(event) {
                  if (event.key === "Enter") {
                    updateURL(scratch_input.value)
                    event.preventDefault();
                    if (scratch_input.value.trim()) {scratch_button.click()}
                    else {session_output.innerHTML = ""}
                  }
                });
                // Function for copy_button
                $("#copy_button").click(function(){
                  session_message.innerHTML = "";
                  if (scratch_input.value.trim()) {
                    navigator.clipboard.writeText(window.location);
                    session_message.innerHTML = "Copied formula to clipboard"
                  }
                  else {session_message.innerHTML = "Nothing to copy"}
                  ;
                });
                // Function for download_button
                $("#download_button").click(function(){
                  session_message.innerHTML = "";
                  if ($("#session_output").children('img').length){
                    let img_src = $("#session_output").find('img').attr('src');
                    var a_temp = document.createElement('a');
                    a_temp.setAttribute('href', img_src);
                    a_temp.setAttribute('download',  "scratchbook_output");
                    document.body.appendChild(a_temp);
                    a_temp.click();
                    document.body.removeChild(a_temp);
                  } 
                  else {session_message.innerHTML = "Nothing to download"}
                });
                // Function for clear_button
                $("#clear_button").click(function(){
                  session_message.innerHTML = "";
                  scratch_input.value = "";
                  session_output.innerHTML = ""
                  updateURL("")
                });
                // Function for default_button
                $("#default_button").click(function(){
                  session_message.innerHTML = "";
                  scratch_input.value = default_formula;
                  session_output.innerHTML = "";
                  updateURL("");
                  scratch_button.click();
                });
                // Function for surprise_button
                $("#surprise_button").click(function(){
                  session_message.innerHTML = "";
                  scratches = [
                    'autobahn',
                    'babyorbit',
                    'boomerang',
                    'boomerang_roll',
                    'brbhippopotamus',
                    'chirp',
                    'chirpboomerang',
                    'chirpflare1',
                    'chirpflare2',
                    'chirpogflare',
                    'chirpogflare_roll',
                    'diceorbit',
                    'drills',
                    'enneagon',
                    'enneagon_roll',
                    'hendecagon',
                    'hendecagon_roll',
                    'hippopotamus',
                    'hippopotamus_roll',
                    'internet',
                    'kermit',
                    'military',
                    'ogflare',
                    'oneclickflare',
                    'prizm',
                    'prizm_roll',
                    'rawhippopotamus',
                    'royalline',
                    'scribble',
                    'seesaw',
                    'slice',
                    'slicecombo1',
                    'slicecombo2',
                    'stab',
                    'stabcrab',
                    'stabcrabmarch',
                    'swingflare',
                    'tazer1',
                    'tazer2',
                    'turnaroundtransform',
                    'twoclickflare',
                  ]
                  scratch_input.value = scratches[Math.floor(Math.random() * scratches.length)];
                  scratch_button.click();
                  updateURL(scratch_input.value)
                });
              });
            </script>
          </div>
        </div>
      </div>
    </div>
    <br/>
    <!-- Library and Logic -->
    <div class="container-md pt-3 border rounded" style="background-color: white; box-shadow:0px 2px 0px -1px var(--grey-dark)">
      <div class="panel-group" id="Rules">
        <div class="panel panel-default">
          <div class="panel-heading"><h4>Library and Logic</h4></div>
          <div class="panel-body">
            <p style="margin-bottom: 5px;">ScratchBook lets you write TTM-notation just like math. Combine <strong>scratches</strong> and <strong>operators</strong> into formulas, such as: <code style="color: var(--blue-dark)">autobahn + prizm + (slice / 0.25) * 4</code></p>
            <p>Open the cards to learn more...</p>
          </div>
          <!-- Scratches -->
          <div class="card" style="margin-bottom: 10px;">
            <div class="card-header">
              <a class="btn" data-bs-toggle="collapse" href="#ScratchCard" style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">Scratches</a>
            </div>
            <div id="ScratchCard" class="collapse in">
              <div class="card-body" style="overflow-x:auto;">
                <div class="card" style="margin-bottom: 10px;">
                  <div class="card-header">
                    <a class="btn btn-sm" data-bs-toggle="collapse" href="#ExpertCard" title="Show expert controls." style="width: 100%; text-align: left; font-size: 14px; font-weight: 500;">Expert Mode</a>
                  </div>
                  <script>
                    $(document).ready(function () {
                      $('a[title]').tooltip({
                        trigger: "hover",
                        "container": 'body',
                      });
                    });
                  </script>
                  <div id="ExpertCard" class="collapse in">
                    <!-- Switches for collections -->
                    <div class="container" style="width:95%; padding:0px; background-color: var(--grey-light); margin-top: 10px">
                      <div class="row" style="margin-left: 0px;">
                        <p class="expert-heading">Collections</p>
                      </div>
                      <div class="row switch-row">
                        <div class="column" 
                          title="The CORE collection contains 41 scratches and is loaded on default when opening the page.">
                          <label class="switch"><input id="CORE" type="checkbox" checked/><span class="slider"></span></label>
                        </div>
                        <div class="column" 
                          title="The ELEMENTS collection contains 242 unidirectional scratches with various modifications that form the ELEMENTS for all other scratches.">
                          <label class="switch"><input id="ELEMENTS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="The TEARS collection contains 54 unidirectional tear variations.">
                          <label class="switch"><input id="TEARS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Core</div>
                        <div class="column">Elements</div>
                        <div class="column">Tears</div>
                      </div>
                      <div class="row switch-row">
                        <div class="column" title="The ORBITS1 collection contains 57,025 orbits, generated from pairwise combinations of elements and tears. Most orbits you will ever need are in here.">
                          <label class="switch"><input id="ORBITS1" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="The ORBITS2 collection contains another 45,620 orbits, generated from pairwise combinations of elements and tears. These orbits are less common and you might not be interested in them.">
                          <label class="switch"><input id="ORBITS2" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="The COMBOS collection contains 32 popular scratch combos, most of which you want to use at some point. All of these combos are also included in the CORE collection.">
                          <label class="switch"><input id="COMBOS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Orbits1</div>
                        <div class="column">Orbits2</div>
                        <div class="column">Combos</div>
                      </div>
                    </div>
                    <!-- Switches for Curves -->
                    <div class="container" style="width:95%; padding:0px; background-color: var(--grey-light); margin-top: 10px">
                      <div class="row" style="margin-left: 0px;">
                        <p class="expert-heading">Curves</p>
                      </div>
                      <div class="row switch-row">
                        <div class="column" title="Only show scratches with REGULAR CURVES.">
                          <label class="switch"><input id="RegularCurves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Only show scratches with IRREGULAR CURVES (i.e. Log or Ex).">
                          <label class="switch"><input id="IrregularCurves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Regular</div>
                        <div class="column">Irregular</div>
                      </div>                  
                    </div>
                    <!-- Switches Clicks -->
                    <div class="container" style="width:95%; padding:0px; background-color: var(--grey-light); margin-top: 10px">
                      <div class="row" style="margin-left: 0px;">
                        <p class="expert-heading">Clicks</p>
                      </div>
                      <div class="row switch-row">
                        <div class="column" title="Only show scratches with REGULAR CLICK PATTERNS.">
                          <label class="switch"><input id="RegularClicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Only show scratches with IRREGULAR CLICK PATTERNS (i.e. D, A, S, or Q).">
                          <label class="switch"><input id="IrregularClicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Regular</div>
                        <div class="column">Irregular</div>
                      </div>                  
                    </div>
                    <!-- Switches for columns -->
                    <div class="container" style="width:95%; padding:0px; background-color: var(--grey-light); margin-top: 10px; margin-bottom: 10px">
                      <div class="row" style="margin-left: 0px;">
                        <p class="expert-heading">Columns</p>
                      </div>
                      <div class="row switch-row">
                        <div class="column" title="Show CURVE types.">
                          <label class="switch"><input id="Curves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Show CLICK types">
                          <label class="switch"><input id="Clicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Show SCRATCH types">
                          <label class="switch"><input id="Scratches" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Show FORMULA">
                          <label class="switch"><input id="Composition" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Curves</div>
                        <div class="column">Clicks</div>
                        <div class="column">Scratches</div>
                        <div class="column">Formula</div>
                      </div>                  
                    </div>
                  </div>
                </div>
                <!-- Style tooltips for all switches: -->
                <script>
                  $(document).ready(function () {
                    $('.column[title]').tooltip({
                      trigger: "hover",
                      "container": 'body',
                    });
                  });
                </script>
                <!-- DataTable -->
                <table class="table" id="scratch-table" style="font-size: 12px; background-color: var(--grey-light)"></table>
                <script type="text/javascript">
                  // Define table
                  $(document).ready(function () {
                    var table = $('#scratch-table').DataTable({
                      ajax: "https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_CORE.json",
                      columns: [
                        // Basic
                        { data: 'Name(s)',     title: 'Name(s)',     }, // 0
                        { data: 'Tutorial',    title: 'Tutorial',    }, // 1
                        { data: '#Sounds',     title: '#Sounds',     }, // 2
                        // Curves
                        { data: 'Ex',          title: 'Ex',          }, // 3
                        { data: 'Log',         title: 'Log',         }, // 4
                        { data: 'OrbCurve',    title: 'OrbCurve',    }, // 5
                        // Clicks
                        { data: '#FO',         title: '#FO',         }, // 6
                        { data: '#FC',         title: '#FC',         }, // 7
                        { data: '#PO',         title: '#PO',         }, // 8
                        { data: '#PC',         title: '#PC',         }, // 9
                        { data: 'D',           title: 'D',           }, // 10
                        { data: 'A',           title: 'A',           }, // 11
                        { data: 'S',           title: 'S',           }, // 12
                        { data: 'Q',           title: 'Q',           }, // 13
                        // Scratches
                        { data: 'Baby',        title: 'Baby',        }, // 14
                        { data: 'In',          title: 'In',          }, // 15
                        { data: 'Out',         title: 'Out',         }, // 16
                        { data: 'Dice',        title: 'Dice',        }, // 17
                        { data: 'Flare',       title: 'Flare',       }, // 18
                        { data: 'Transformer', title: 'Transformer', }, // 19
                        { data: 'Tear',        title: 'Tear',        }, // 20
                        { data: 'Orbit',       title: 'Orbit',       }, // 21
                        { data: 'Slice',       title: 'Slice',       }, // 22
                        { data: 'Chirp',       title: 'Chirp',       }, // 23
                        { data: 'Stab',        title: 'Stab',        }, // 24
                        { data: 'OCF',         title: 'OCF',         }, // 25
                        { data: 'TCF',         title: 'TCF',         }, // 26
                        { data: 'OGF',         title: 'OGF',         }, // 27
                        // Composition
                        { data: '#Els',        title: '#Els',        }, // 28
                        { data: 'Formula',     title: 'Formula',     }, // 29
                        // Libraries
                        { data: 'CORE',        title: 'CORE',        }, // 30
                        { data: 'ELEMENTS',    title: 'ELEMENTS',    }, // 31
                        { data: 'TEARS',       title: 'TEARS',       }, // 32
                        { data: 'ORBITS1',     title: 'ORBITS1',     }, // 33
                        { data: 'ORBITS2',     title: 'ORBITS2',     }, // 34
                        { data: 'COMBOS',      title: 'COMBOS',      }, // 35
                      ],
                      order: [
                        [ 0, "asc" ], 
                      ],
                      "searching": true,  
                      "lengthChange": true,
                      // scrollY: '50vh',
                      // scrollCollapse: true,
                      // fixedHeader: {
                      //   header: true,
                      // },
                      "initComplete": function(settings){
                        $('#scratch-table thead th').each(function () {
                          var $td = $(this);
                          var headerText = $td.text(); 
                          var headerTitle=$td.text(); 
                          // Basic
                          if ( headerText == "Name(s)" )
                            headerTitle =  "Available NAMES for the scratch, to be used in the VISUALIZER. Synonymous names are seperated by a comma.";
                          else if (headerText == "Tutorial" )
                            headerTitle = "A link to a VIDEO-TUTORIAL for the scratch (if available).";
                          else if (headerText == "#Sounds" )
                            headerTitle = "The number of SOUNDS the scratch makes.";
                          // Curves
                          else if (headerText == "Ex" )
                            headerTitle = "Whether or not the scratch contains at least one EXPONENTIAL curve.";
                          else if (headerText == "Log" )
                            headerTitle = "Whether or not the scratch contains at least one LOGARITHMIC curve.";
                          else if (headerText == "OrbCurve" )
                            headerTitle = "(Only applies to orbits) Names the CURVE-SHAPE of the orbit, e.g. S-CURVED, TAZER or PHANTAZM.";
                          // Clicks
                          else if (headerText == "#FO" )
                            headerTitle = "The Number of times the FADER is OPENED in the scratch.";
                          else if (headerText == "#FC" )
                            headerTitle = "The Number of times the FADER is CLOSED in the scratch.";
                          else if (headerText == "#PO" )
                            headerTitle = "The Number of times the PHANTOMFADER is OPENED in the scratch, i.e. one starts holding the record still.";
                          else if (headerText == "#PC" )
                            headerTitle = "The Number of times the PHANTOMFADER is CLOSED in the scratch, i.e. one stops holding the record still.";
                          else if (headerText == "D" )
                            headerTitle = "Whether or not the scratch contains at least one DIMINISHED click pattern.";
                          else if (headerText == "A" )
                            headerTitle = "Whether or not the scratch contains at least one AUGMENTED click pattern.";
                          else if (headerText == "S" )
                            headerTitle = "Whether or not the scratch contains at least one STRECHED click pattern.";
                          else if (headerText == "Q" )
                            headerTitle = "Whether or not the scratch contains at least one SQUEEZED click pattern.";
                          // Scratches
                          else if (headerText == "Baby" )
                            headerTitle = "Whether or not the scratch contains at least one BABY scratch.";
                          else if (headerText == "In" )
                            headerTitle = "Whether or not the scratch contains at least one IN scratch";
                          else if (headerText == "Out" )
                            headerTitle = "Whether or not the scratch contains at least one OUT scratch.";
                          else if (headerText == "Dice" )
                            headerTitle = "Whether or not the scratch contains at least one DICE scratch.";
                          else if (headerText == "Flare" )
                            headerTitle = "Whether or not the scratch contains at least one FLARE scratch.";
                          else if (headerText == "Transformer" )
                            headerTitle = "Whether or not the scratch contains at least one TRANSFORMER scratch.";
                          else if (headerText == "Tear" )
                            headerTitle = "Whether or not the scratch contains at least one TEAR scratch.";
                          else if (headerText == "Orbit" )
                            headerTitle = "Whether or not the scratch contains at least one ORBIT scratch.";
                          else if (headerText == "Slice" )
                            headerTitle = "Whether or not the scratch contains at least one SLICE scratch.";
                          else if (headerText == "Chirp" )
                            headerTitle = "Whether or not the scratch contains at least one CHIRP scratch.";
                          else if (headerText == "Stab" )
                            headerTitle = "Whether or not the scratch contains at least one STAB scratch.";
                          else if (headerText == "OCF" )
                            headerTitle = "Whether or not the scratch contains at least one OC-FLARE scratch.";
                          else if (headerText == "TCF" )
                            headerTitle = "Whether or not the scratch contains at least one TC-FLARE scratch.";
                          else if (headerText == "OGF" )
                            headerTitle = "Whether or not the scratch contains at least one OG-FLARE scratch.";                          
                          // Composition
                          else if (headerText == "#Els" )
                            headerTitle = "The number of ELEMENTS the scratch is composed of.";
                          else if (headerText == "Formula" )
                            headerTitle = "The FORMULA for composing the scratch. Copy-n-paste formulas into the VISUALIZER to make your own modifications! ";
                          // Set the attribute...
                          $td.attr('title', headerTitle);
                        });
                        /* Style header tooltips */
                        $('#scratch-table thead th[title]').tooltip({
                          trigger: "hover",
                          "container": 'body',
                        });
                        // Visibility of columns
                        var cols = [3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,]
                        table.columns( cols ).visible(false, false);
                        table.columns( cols ).searchable(false);
                      },
                    });
                    
                    // Functions for row-filtering switches  
                    function activeLibs() {
                        let active_switches = [];
                        for (let libinfo of [
                          ["CORE", 30],
                          ["ELEMENTS", 31],
                          ["TEARS", 32],
                          ["ORBITS1", 33],
                          ["ORBITS2", 34],
                          ["COMBOS", 35],
                        ]) {
                          if (document.getElementById(libinfo[0]).checked) {
                              active_switches.push("data['" + libinfo[1] + "'] == 1")
                            }
                        }
                        return active_switches.join(" || ")
                    };
                    function curvesAndClicks() {
                        let active_switches = [];
                        if (document.getElementById("RegularCurves").checked) {
                          active_switches.push("data['3'] == 0 && data['4'] == 0")
                        } else if (document.getElementById("IrregularCurves").checked) {
                          active_switches.push("data['3'] == 1 || data['4'] == 1")
                        }
                        if (document.getElementById("RegularClicks").checked) {
                          active_switches.push("data['10'] == 0 && data['11'] == 0 && data['12'] == 0 && data['13'] == 0")
                        } else if (document.getElementById("IrregularClicks").checked) {
                          active_switches.push("data['10'] == 1 || data['11'] == 1 || data['12'] == 1 || data['13'] == 1")
                        }
                        return active_switches.join(" && ")
                        
                    };
                    function filterRows() {
                      let query = []
                      if (activeLibs()) {
                        query.push("(" + activeLibs() + ")");
                        if (curvesAndClicks()) { // only relevant if some lib is active, hence nested here
                          query.push("(" + curvesAndClicks() + ")");
                        }
                      }
                      return query.join(" && ")
                    }
                    function removeDuplicates(table) {
                      var names = table.column( 0 ).data().toArray();
                      session_message.innerHTML = names[0]
                      var rowsToRemove = [];
                      table.rows().every(function(rowIdx, tableLoop, rowLoop) {
                        var data = this.data();
                        // Find number of times name is in names array
                        var numOccurances = names.filter(x => x === data["Name(s)"]).length;
                        // If only once remove the row
                        if (! numOccurances > 1 ) {
                          rowsToRemove.push( this.index() );
                        }
                      });
                      table.rows( rowsToRemove ).remove().draw();
                    };
                    
                    function addNewRows(table, json) {
                      var existing_names = table.column( 0 ).data().toArray();
                      rowsToAdd = []
                      for (let row of json.data) {
                        // session_message.innerHTML = row["Name(s)"];
                        if (!existing_names.includes(row["Name(s)"])) {
                          rowsToAdd.push(row)
                        }
                      }
                      session_message.innerHTML = "Added " + rowsToAdd.length + " rows";
                      table.rows.add(rowsToAdd).draw(false);
                    }
                    ///////////////////////////////////////////////////////////////////////
                    // CORE switch
                    $("#CORE").change(function() {
                        $.fn.dataTable.ext.search.push(
                          function(settings, data, dataIndex) {
                            return eval(filterRows())
                          }
                        );
                        table.draw();
                    });
                    // ELEMENTS switch
                    var load_ELEMENTS = true
                    $("#ELEMENTS").change(function() {
                      if(this.checked && load_ELEMENTS === true) {
                        load_ELEMENTS = false;
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_ELEMENTS.json', function(json) {
                          addNewRows(table, json);
                        });
                      }
                      $.fn.dataTable.ext.search.push(
                          function(settings, data, dataIndex) {
                            return eval(filterRows())
                          }
                      );
                      table.draw();
                    });
                    // TEARS switch
                    var load_TEARS = true
                    $("#TEARS").change(function() {
                      if(this.checked && load_TEARS === true) {
                        load_TEARS = false;
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_TEARS.json', function(json) {
                          addNewRows(table, json);
                        });
                      }
                      $.fn.dataTable.ext.search.push(
                          function(settings, data, dataIndex) {
                          return eval(filterRows())
                          }
                      );
                      table.draw();
                    });
                    // ORBITS1 switch
                    var load_ORBITS1 = true
                    $("#ORBITS1").change(function() {
                      if(this.checked && load_ORBITS1 === true) {
                        load_ORBITS1 = false;
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_ORBITS1.json', function(json) {
                          // table.rows.add(json.data).draw(false);
                          addNewRows(table, json);
                        });
                      }
                      $.fn.dataTable.ext.search.push(
                          function(settings, data, dataIndex) {
                          return eval(filterRows())
                          }
                      );
                      table.draw();
                    });
                    // ORBITS2 switch
                    var load_ORBITS2 = true
                    $("#ORBITS2").change(function() {
                      if(this.checked && load_ORBITS2 === true) {
                        load_ORBITS2 = false;
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_ORBITS2.json', function(json) {
                          addNewRows(table, json);
                        });
                      }
                      $.fn.dataTable.ext.search.push(
                          function(settings, data, dataIndex) {
                          return eval(filterRows())
                          }
                      );
                      table.draw();
                    });
                    // COMBOS switch
                    var COMBOS = true
                    $("#COMBOS").change(function() {
                      if(this.checked && COMBOS === true) {
                        COMBOS = false;
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_COMBOS.json', function(json) {
                          addNewRows(table, json);
                        });
                      }
                      $.fn.dataTable.ext.search.push(
                          function(settings, data, dataIndex) {
                          return eval(filterRows())
                          }
                      );
                      table.draw();
                    });
                    ///////////////////////////////////////////////////////////////////////
                    // Regular Curves Switch
                    $("#RegularCurves").change(function() {
                      if (document.getElementById("RegularCurves").checked) {
                        document.getElementById("IrregularCurves").checked = false
                      }
                      $.fn.dataTable.ext.search.push(
                        function(settings, data, dataIndex) {
                          return eval(filterRows())
                        }
                      );
                      table.draw();
                    });
                    $("#IrregularCurves").change(function() {
                      if (document.getElementById("IrregularCurves").checked) {
                        document.getElementById("RegularCurves").checked = false
                      }
                      $.fn.dataTable.ext.search.push(
                        function(settings, data, dataIndex) {
                          return eval(filterRows())
                        }
                      );
                      table.draw();
                    });
                    // Regular Clicks Switch
                    $("#RegularClicks").change(function() {
                      if (document.getElementById("RegularClicks").checked) {
                        document.getElementById("IrregularClicks").checked = false
                      }
                      $.fn.dataTable.ext.search.push(
                        function(settings, data, dataIndex) {
                          return eval(filterRows())
                        }
                      );
                      table.draw();
                    });
                    $("#IrregularClicks").change(function() {
                      if (document.getElementById("IrregularClicks").checked) {
                        document.getElementById("RegularClicks").checked = false
                      }
                      $.fn.dataTable.ext.search.push(
                        function(settings, data, dataIndex) {
                          return eval(filterRows())
                        }
                      );
                      table.draw();
                    });
                    // Column Switches
                    $('#Curves').change(function() {
                      var cols = [3,4,5]
                      if(this.checked) {
                        table.columns( cols ).visible(true, false);
                        table.columns( cols ).searchable(true);
                      }
                      else {
                        table.columns( cols ).visible(false, false);
                        table.columns( cols ).searchable(false);
                      }
                    });
                    $('#Clicks').change(function() {
                      var cols = [6,7,8,9,10,11,12,13,]
                      if(this.checked) {
                        table.columns( cols ).visible(true, false);
                        table.columns( cols ).searchable(true);
                      }
                      else {
                        table.columns( cols ).visible(false, false);
                        table.columns( cols ).searchable(false);
                      }
                    });
                    $('#Scratches').change(function() {
                      var cols = [14,15,16,17,18,19,20,21,22,23,24,25,26,27]
                      if(this.checked) {
                        table.columns( cols ).visible(true, false);
                        table.columns( cols ).searchable(true);
                      }
                      else {
                        table.columns( cols ).visible(false, false);
                        table.columns( cols ).searchable(false);
                      }
                    });
                    $('#Composition').change(function() {
                      var cols = [28,29]
                      if(this.checked) {
                        table.columns( cols ).visible(true, false);
                        table.columns( cols ).searchable(true);
                      }
                      else {
                        table.columns( cols ).visible(false, false);
                        table.columns( cols ).searchable(false);
                      }
                    });
                  });
                </script>
              </div>
            </div>
          </div>
          <!-- Operators -->
          <div class="card" style="margin-bottom: 10px;">
            <div class="card-header">
              <a class="btn" data-bs-toggle="collapse" href="#OperatorCard" style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">Operators</a>
            </div>
            <div id="OperatorCard" class="collapse in">
              <div class="card-body" style="overflow-x:auto;">
                <p>Operators can be used to modify and combine scratches. The following table lists and explains all available operators.
                </p>
                <table class="table" id="OperatorTable" style="font-size: 12px">
                  <thead>
                    <tr>
                        <th>Operator</th>
                        <th>Purpose</th>
                        <th>Grammar</th>
                        <th>Example</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                        <td>~</td>
                        <td>"Reverse" or "backwards" scratching (Flip a scratch on the y-axis)</td>
                        <td>~scratch</td>
                        <td>~autobahn</td>
                    </tr>
                    <tr>
                        <td>-</td>
                        <td>"Mirror" scratching (Flip a scratch on the x-axis)</td>
                        <td>-scratch</td>
                        <td>-autobahn</td>
                    </tr>
                    <tr>
                        <td>*</td>
                        <td>Repeat a scratch <em>n</em> times (<em>n</em> must be an integer number)</td>
                        <td>scratch * <em>n</em></td>
                        <td>chirp * 4</td>
                    </tr>
                    <tr>
                        <td>+</td>
                        <td>Chain scratches from left to right</td>
                        <td>scratch + scratch</td>
                        <td>chirp + flob2 + steps</td>
                    </tr>
                    <tr>
                        <td>/</td>
                        <td>Set the length <em>n</em> of a scratch in 1/4 notes (aka beats)</td>
                        <td>scratch / <em>n</em></td>
                        <td>baby / 2</td>
                    </tr>
                    <tr>
                        <td>//</td>
                        <td>Decide how much of sample is used (<em>n</em> must be between 0 and 1)</td>
                        <td>scratch // <em>n</em></td>
                        <td>swingflare // 0.2</td>
                    </tr>
                    <tr>
                        <td>**</td>
                        <td>Move a scratch or expression up on the Y-axis. Typically used in connection with the "//" Operator". Use brackets wisely! For example, "chirp // 0.5 ** 0.5" is not the same as "(chirp // 0.5) ** 0.5".</td>
                        <td>expression ** <em>n</em></td>
                        <td>(chirp // 0.5) ** 0.5</td>
                    </tr>
                    <tr>
                        <td>%</td>
                        <td>Shift the "phase" of a scratch by rotating its parts from right to left. (<em>n</em> must be an integer number)</td>
                        <td>scratch % <em>n</em></td>
                        <td>prizm % 0.25</td>
                    </tr>
                    <tr>
                        <td>[<em>n</em>]</td>
                        <td>Show the <em>n</em>-ths part of a composed scratch (<em>n</em> must be an integer number. <span style="color: var(--red)">&#9888;</span> Counting starts at 0 not at 1!)</td>
                        <td>scratch[<em>n</em>]</td>
                        <td>autobahn[3]</td>
                    </tr>
                    <tr>
                        <td>[<em>n</em>:<em>m</em>]</td>
                        <td>Show all parts between the <em>n</em>-ths (included) and <em>m</em>-ths (excluded) part of a composed scratch (<em>n</em> and <em>m</em> must be integer numbers. <span style="color: var(--red)">&#9888;</span> Counting starts at 0 not at 1!)</td>
                        <td>scratch[<em>n</em>:<em>m</em>]</td>
                        <td>autobahn[3:7]</td>
                    </tr>
                    <tr>
                        <td>(<em>expression</em>)</td>
                        <td>Use (nested) brackets to logically "shield off" expressions from each other. For example, "chirp / 1/3" is not the same as "chirp / (1/3)". Brackets are essential for many complex expressions.</td>
                        <td>(<em>expression</em>)</td>
                        <td>(chirp // (1/3)) ** (2/3)</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
          <!-- The Idea -->
          <div class="card" style="width: auto">
            <div class="card-header">
              <a class="btn" data-bs-toggle="collapse" href="#IdeaCard" style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">Notation</a>
            </div>
            <div id="IdeaCard" class="collapse in">
              <div class="card-body" style="overflow-x:auto;">
                <p> 
                  The <a href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>turntablist transcription methodology (TTM)</a> was created and published by John Carluccio, Ithan Imboden, and Raymond Pirtle in the late 1990s. According to the original <a href="https://www.ttm-dj.com/TTMv1.1_Eng.pdf" target='_blank'>TTM-booklet</a>, TTM is emphatically <em>"an open source effort...Fight it, defend it, tweak it, trash it - all will assist its evolution"</em> (p.10).
                </p>
                <p> 
                  In this spirit, <b>ScratchBook modifies the original TTM</b> in the following way: 
                </p>
                <ol style="font-size:14px">
                  <li>1) The <b>color white</b> generally indicates that the <b>fader is closed</b>.</li>
                  <li>2) <b>Regular fader clicks</b> are sybolized as <b>white cirlces</b> (not as black circles)</li>
                  <li>3) <b>Silent record motions</b>, such as during a stab scratch, are symbolized by <b>white curves</b>.</li>
                  <li>4) <b>No "phantom clicks"</b> are shown, but they can always be inferred from near-zero slopes of the scratch curves.</li>
                </ol>
              </div>
            </div>
          </div>
        </div>
      </div>
      <br/>
    </div>
    <br/>
    <footer class="bg-dark text-center text-white">
      <!-- Grid container -->
      <div class="container p-4">
        <section class="mb-4">
          <!-- Twitter -->
          <a class="btn btn-outline-light btn-floating m-1" href="https://twitter.com/arno_simons" target='_blank' role="button"
            ><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-twitter" viewBox="0 0 16 16"><path d="M5.026 15c6.038 0 9.341-5.003 9.341-9.334 0-.14 0-.282-.006-.422A6.685 6.685 0 0 0 16 3.542a6.658 6.658 0 0 1-1.889.518 3.301 3.301 0 0 0 1.447-1.817 6.533 6.533 0 0 1-2.087.793A3.286 3.286 0 0 0 7.875 6.03a9.325 9.325 0 0 1-6.767-3.429 3.289 3.289 0 0 0 1.018 4.382A3.323 3.323 0 0 1 .64 6.575v.045a3.288 3.288 0 0 0 2.632 3.218 3.203 3.203 0 0 1-.865.115 3.23 3.23 0 0 1-.614-.057 3.283 3.283 0 0 0 3.067 2.277A6.588 6.588 0 0 1 .78 13.58a6.32 6.32 0 0 1-.78-.045A9.344 9.344 0 0 0 5.026 15z"/></svg></a>
          <!-- Instagram -->
          <a class="btn btn-outline-light btn-floating m-1" href="https://www.instagram.com/dj_hdrs/" target='_blank' role="button"
            ><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-instagram" viewBox="0 0 16 16"><path d="M8 0C5.829 0 5.556.01 4.703.048 3.85.088 3.269.222 2.76.42a3.917 3.917 0 0 0-1.417.923A3.927 3.927 0 0 0 .42 2.76C.222 3.268.087 3.85.048 4.7.01 5.555 0 5.827 0 8.001c0 2.172.01 2.444.048 3.297.04.852.174 1.433.372 1.942.205.526.478.972.923 1.417.444.445.89.719 1.416.923.51.198 1.09.333 1.942.372C5.555 15.99 5.827 16 8 16s2.444-.01 3.298-.048c.851-.04 1.434-.174 1.943-.372a3.916 3.916 0 0 0 1.416-.923c.445-.445.718-.891.923-1.417.197-.509.332-1.09.372-1.942C15.99 10.445 16 10.173 16 8s-.01-2.445-.048-3.299c-.04-.851-.175-1.433-.372-1.941a3.926 3.926 0 0 0-.923-1.417A3.911 3.911 0 0 0 13.24.42c-.51-.198-1.092-.333-1.943-.372C10.443.01 10.172 0 7.998 0h.003zm-.717 1.442h.718c2.136 0 2.389.007 3.232.046.78.035 1.204.166 1.486.275.373.145.64.319.92.599.28.28.453.546.598.92.11.281.24.705.275 1.485.039.843.047 1.096.047 3.231s-.008 2.389-.047 3.232c-.035.78-.166 1.203-.275 1.485a2.47 2.47 0 0 1-.599.919c-.28.28-.546.453-.92.598-.28.11-.704.24-1.485.276-.843.038-1.096.047-3.232.047s-2.39-.009-3.233-.047c-.78-.036-1.203-.166-1.485-.276a2.478 2.478 0 0 1-.92-.598 2.48 2.48 0 0 1-.6-.92c-.109-.281-.24-.705-.275-1.485-.038-.843-.046-1.096-.046-3.233 0-2.136.008-2.388.046-3.231.036-.78.166-1.204.276-1.486.145-.373.319-.64.599-.92.28-.28.546-.453.92-.598.282-.11.705-.24 1.485-.276.738-.034 1.024-.044 2.515-.045v.002zm4.988 1.328a.96.96 0 1 0 0 1.92.96.96 0 0 0 0-1.92zm-4.27 1.122a4.109 4.109 0 1 0 0 8.217 4.109 4.109 0 0 0 0-8.217zm0 1.441a2.667 2.667 0 1 1 0 5.334 2.667 2.667 0 0 1 0-5.334z"/></svg></a>
          <!-- Linkedin -->
          <a class="btn btn-outline-light btn-floating m-1" href="" target='_blank' role="button"
            ><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-linkedin" viewBox="0 0 16 16"><path d="M0 1.146C0 .513.526 0 1.175 0h13.65C15.474 0 16 .513 16 1.146v13.708c0 .633-.526 1.146-1.175 1.146H1.175C.526 16 0 15.487 0 14.854V1.146zm4.943 12.248V6.169H2.542v7.225h2.401zm-1.2-8.212c.837 0 1.358-.554 1.358-1.248-.015-.709-.52-1.248-1.342-1.248-.822 0-1.359.54-1.359 1.248 0 .694.521 1.248 1.327 1.248h.016zm4.908 8.212V9.359c0-.216.016-.432.08-.586.173-.431.568-.878 1.232-.878.869 0 1.216.662 1.216 1.634v3.865h2.401V9.25c0-2.22-1.184-3.252-2.764-3.252-1.274 0-1.845.7-2.165 1.193v.025h-.016a5.54 5.54 0 0 1 .016-.025V6.169h-2.4c.03.678 0 7.225 0 7.225h2.4z"/></svg></a>
          <!-- Github -->
          <a class="btn btn-outline-light btn-floating m-1" href="https://github.com/arnosimons" target='_blank' role="button"
            ><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-github" viewBox="0 0 16 16"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg></a>
        </section>
        <section class="mb-4">
          <p>ScratchBook is an educational and non-commercial project. The <a class="dark-link" href="https://github.com/arnosimons/scratchbook" target='_blank'>underlying code</a> is free freely available and reusable under the GPL-3.0 license.</p>
          <p> The <a class="dark-link" href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>turntablist transcription methodology (TTM)</a> ScratchBook uses was created and <a class="dark-link" href="https://www.ttm-dj.com/TTMv1.1_Eng.pdf" target='_blank'>published</a> by John Carluccio, Ithan Imboden, and Raymond Pirtle in the late 1990s. I am deeply indebted to their work.
          <p> © 2022 by Arno Simons, a Berlin-based turntablist and researcher.</p>
        </section>
      </div>
    </footer>
    



  </body>
  <py-script>
    import re
    from js import XMLHttpRequest
    req = XMLHttpRequest.new()
    req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/classes_and_functions.py", False)
    req.send()
    exec(str(req.response))
    req = XMLHttpRequest.new()
    req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/codebook.json", False)
    req.send()
    exec(f"codebook = {req.response}")
    def getCodeNames(text):
        if "Scratch" in text:
            return
        text = re.sub(r"[-+*/%~\[\]\(\).:]|yshift|ys", " ", text)
        for code_name in re.sub(r"\b\d*\b", " ", text).split():
            if not code_name in codebook:
                message = f'Sorry, but "{code_name}" is not in the codebook. Browse the library to see what scratches are available!'
                pyscript.write("session_output", message)
                raise ValueError(message)
            try:
                exec(code_name)
            except NameError:
                yield code_name
                for i in getCodeNames(codebook[code_name]):
                    yield i
    def plot(x=None):
        text = Element("scratch_input").element.value
        if not text:
          pyscript.write("session_output", "plot() requires a formula as input.")
          return
        for code_name in list(getCodeNames(text))[::-1]:
            exec(f"{code_name} = {codebook[code_name]}")
        try:
            session = Session(eval(text), fontsize=11, w_pad=2)
            pyscript.write("session_output", session.fig)
        except Exception as e:
            pyscript.write("session_output", str(e))  
    for code_name in ["i", "o", "slice"]: # workaround for handling "slice" in python's namespace... 
        exec(f"{code_name} = {codebook[code_name]}")
    plot()
  </py-script>
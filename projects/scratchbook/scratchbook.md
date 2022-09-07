---
layout: default
type: project
recent: false
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
          --hover-color: rgba(0, 0, 0, 0.09);
          --blue-light: lightskyblue;
          --blue-dark: #069;
          --blue-dark: rgb(0, 102, 153);
          --grey-light: #F8F8F8;
          --grey-dark: rgba(0, 0, 0, 0.125);
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
      .card{
        margin-bottom: 10px;
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
      .scratch_table {
        font-size: 12px; 
        background-color: var(--grey-light);
      }
      /* .scratch_table thead th[class="sorting"] {
        line-height: 18px;
        color: yellow;
      }
      .scratch_table thead th[class="sorting sorting_asc"] {
        line-height: 18px;
        color: green;
      }
      .scratch_table thead th[class="sorting sorting_desc"] {
        line-height: 18px;
        color: red;
      } */
      .info_table {
        font-size: 12px;
        display: block;
        overflow-x: auto;
        white-space: nowrap;
      }
      .info_table_title{
        font-size: 14px;
        font-weight: 600;
        padding: 7px;
      }
      .info_container{
        width:100%; 
        padding:0px; 
        background-color: var(--grey-light); 
        margin-top: 10px;
      }
      ul {
        list-style-type: circle;
      }
      li {
        font-size: 14px;
      }
      .center {
        display: block;
        margin-left: auto;
        margin-right: auto;
        width: 50%;
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
      <div class="panel-group">
        <div class="panel panel-default">
          <div class="panel-heading"><h4>Visualizer</h4></div>
          <div class="panel-body">
            <p>Type and visualize your scratch formula...</p>
            <input 
              id="scratch_input"
              class="form-control" 
              type="text" 
              placeholder="Type formula and press ENTER"/>
            <p style="margin-top: 5px;">
              <button 
                id="copy_button" 
                class="mybuttons"
                title="Copy url+formula and share it with your friends">
                Copy
              </button>
              <button 
                id="download_button"
                class="mybuttons"
                title="Download png image">
                Download
              </button> 
              <button 
                id="clear_button"
                class="mybuttons"
                title="Clear the input field">
                Clear
              </button>
              <button 
                id="default_button"
                class="mybuttons"
                title="Reset to default scratch formula">
                Default
              </button>  
              <button 
                id="surprise_button"
                class="mybuttons"
                title="Pick a scratch at random (currently limited to the Combos collection)">
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
            <div class="container" id="session_info">
              <div class="card" >
                <div class="card-header">
                  <a 
                    class="btn btn-sm" 
                    data-bs-toggle="collapse" 
                    href="#InfoCard" 
                    title="Show detailed stats about your composition" 
                    style="width: 100%; text-align: left; font-size: 16px; font-weight: 500;">
                    Analyze your composition...
                  </a>
                </div>
                <div id="InfoCard" class="collapse in">
                  <div class="card-body" style="overflow-x:auto;">
                    <p>
                      The following tables tell you how many sounds your composition makes, how many elements and popular scratches it contains, which types of clicks and curves are involved, and much more.
                    </p>
                    <div class="info_container">
                      <p class="info_table_title">Basic Info</p>
                      <table id="info_basic" class="table info_table">
                        <thead><tr id="info_basic_thead">                          
                          <td title="Number of DISTINCT SOUNDS the composition makes">Sounds</td>
                          <td title="Number of ELEMENTARY SCRATCHES in the composition">Elements</td>
                          <td title="Number of TEARS in the composition">Tears</td>
                          <td title="Number of ORBITS in the composition">Orbits</td>
                        </tr></thead>
                        <tbody id="info_basic_tbody"></tbody>
                      </table>
                    </div>
                    <div class="info_container">
                      <p class="info_table_title">Clicks and Curves</p>
                      <table id="info_curves_clicks" class="table info_table">
                        <thead><tr id="info_curves_clicks_thead">
                          <td title="Number of times the FADER is OPENED in the composition">FO</td>
                          <td title="Number of times the FADER is CLOSED in the composition">FC</td>
                          <td title="Number of times the PHANTOM-FADER is OPENED in the composition">PO</td>
                          <td title="Number of times the PHANTOM-FADER is CLOSED in the composition">PC</td>
                          <td title="Number of DIMINISHED click patterns in the composition">D</td>
                          <td title="Number of AUGMENTED click patterns in the composition">A</td>
                          <td title="Number of STRETCHED click patterns in the composition">S</td>
                          <td title="Number of SQUEEZED click patterns in the composition">Q</td>
                          <td title="Number of EXPONENTIAL curves in the composition">Ex</td>
                          <td title="Number of LOGARITHMIC curves in the scratch">Log</td>
                        </tr></thead>
                        <tbody id="info_curves_clicks_tbody"></tbody>
                      </table>
                    </div>
                    <div class="info_container">
                      <p class="info_table_title">Elements</p>
                      <table id="info_elements" class="table info_table">
                        <thead><tr id="info_elements_thead">                          
                          <td title="Number of BABIES in the composition">Babies</td>
                          <td title="Number of INS in the composition">Ins</td>
                          <td title="Number of OUTS in the composition">Outs</td>
                          <td title="Number of DICES in the composition">Dices</td>
                          <td title="Number of FLARES in the composition">Flares</td>
                          <td title="Number of iFLARES in the composition">iFlares</td>
                          <td title="Number of oFLARES in the composition">oFlares</td>
                          <td title="Number of TRANSFORMERS in the composition">Transformers</td>
                          <td title="Number of GHOSTS in the composition">Ghosts</td>
                          <td title="Number of HOLDS in the composition">Holds</td>
                          <td title="Number of G-HOLDS in the composition">G-Holds</td>
                        </tr></thead>
                        <tbody id="info_elements_tbody"></tbody>
                      </table>
                    </div>
                    <div class="info_container">
                      <p class="info_table_title">Orbits</p>
                      <table id="info_orbits" class="table info_table">
                        <thead><tr id="info_orbits_thead">
                          <td title="Number of CHIRPS in the composition">Chirps</td>
                          <td title="Number of SLICES in the composition">Slices</td>
                          <td title="Number of STABS in the composition">Stabs</td>
                          <td title="Number of FLARE-ORBITS in the composition">Flare-Orbits</td>
                          <td title="Number of OG-FLARES in the composition">OG-Flares</td>
                          <td title="Number of BABY-ORBITS in the composition">Baby-Orbits</td>
                          <td title="Number of DICE-ORBITS in the composition">Dice-Orbits</td>
                          <td title="Number of OFF-STABS in the composition">Off-Stabs</td>
                        </tr></thead>
                        <tbody id="info_orbits_tbody"></tbody>
                      </table>
                    </div>
                    <div class="info_container">
                      <p class="info_table_title">Orbit Types</p>
                      <table id="info_orbit_types" class="table info_table">
                        <thead><tr id="info_orbit_types_thead">
                          <td title="Number of S-CURVED ORBITS in the composition">S-Curved</td>
                          <td title="Number of TAZER ORBITS in the composition">Tazers</td>
                          <td title="Number of PHANTAZM ORBITS in the composition">Phantazms</td>
                          <td title="Number of EX-TAZER ORBITS in the composition">Ex-Tazers</td>
                          <td title="Number of EX-PHANTAZM ORBITS in the composition">Ex-Phantazms</td>
                        </tr></thead>
                        <tbody id="info_orbit_types_tbody"></tbody>
                      </table>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <script>
              $(document).ready(function () { 
                $('.mybuttons[title]').tooltip({
                  trigger: "hover",
                  "container": 'body',
                });
                $('.table [title]').tooltip({
                  trigger: "hover",
                  "container": 'body',
                });
                // get handlers for key elements
                var default_url = 'https://arnosimons.github.io/scratchbooknew';
                var default_formula = "autobahn + chirp / 0.25 * 4";
                var scratch_input = document.getElementById("scratch_input");
                var scratch_button = document.getElementById("scratch_button");
                var session_output = document.getElementById("session_output");
                var session_message = document.getElementById("session_message");
                var session_info = document.getElementById("session_info");
                session_info.style.display = "none";
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
                    if (scratch_input.value.trim()) {
                      scratch_button.click();
                    }
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
                  session_info.style.display = "none";
                  updateURL("")
                });
                // Function for default_button
                $("#default_button").click(function(){
                  session_message.innerHTML = "";
                  scratch_input.value = default_formula;
                  session_output.innerHTML = "";
                  updateURL(scratch_input.value);
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
                    'flareorbit1',
                    'flareorbit2',
                    'flareorbit3',
                    'hendecagon',
                    'hendecagon_roll',
                    'hippopotamus',
                    'hippopotamus_roll',
                    'internet',
                    'kermit',
                    'military',
                    'ogflare',
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
      <br/>
    </div>
    <br/>
    <!-- Library -->
    <div class="container-md pt-3 border rounded" style="background-color: white; box-shadow:0px 2px 0px -1px var(--grey-dark)">
      <div class="panel-group">
        <div class="panel panel-default">
          <div class="panel-heading">
            <h4>Library</h4>
          </div>
          <div class="panel-body">
            <p style="margin-bottom: 5px;">ScratchBook lets you write TTM-notation just like math. Combine <strong>scratches</strong> and <strong>operators</strong> into formulas, such as: <code style="color: var(--blue-dark)">autobahn + prizm + (slice / 0.25) * 4</code></p>
            <p>Open the cards to learn more...</p>
          </div>
          <!-- Scratches -->
          <div class="card">
            <div class="card-header">
              <a 
                class="btn" 
                data-bs-toggle="collapse" 
                href="#ScratchCard" 
                title="Show ScratchBook's LIBRARY OF SCRATCHES"
                style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">
                Scratches
              </a>
            </div>
            <div id="ScratchCard" class="collapse in">
              <div class="card-body" style="overflow-x:auto;">
                <p>
                  In principle, <strong>you can compose almost any scratch</strong> out of ScratchBook's <strong>elements</strong> and <strong>operators</strong> and with the help of ScratchBook's special <strong>tear and orbit sub-languages</strong>.
                </p>
                <p>
                  But ScratchBook also provides a <strong>library of pre-composed scratches</strong>, which you can browse here.
                </p>
                <p>
                  Use the <strong>"Expert Mode"</strong> to show more geeky colums, to filter scratches, and to switch additional collections on and off.
                </p>
                <div class="card">
                  <div class="card-header">
                    <a 
                      class="btn btn-sm" 
                      data-bs-toggle="collapse" 
                      href="#ExpertCard" 
                      title="Show EXPERT CONTROLS" 
                      style="width: 100%; text-align: left; font-size: 14px; font-weight: 500;">
                      Expert Mode
                    </a>
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
                          title="The CORE collection contains 43 scratches and is loaded on default when opening the page">
                          <label class="switch"><input id="CORE" type="checkbox" checked/><span class="slider"></span></label>
                        </div>
                        <div class="column" 
                          title="The ELEMENTS collection contains 171 unidirectional scratches with various modifications that form the ELEMENTS for all other scratches">
                          <label class="switch"><input id="ELEMENTS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="The TEARS collection contains 42 unidirectional tear variations">
                          <label class="switch"><input id="TEARS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="The ORBITS collection contains 594 orbits, generated from pairwise combinations of elements. Most orbits you will ever need are in here">
                          <label class="switch"><input id="ORBITS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="The COMBOS collection contains 33 popular scratch combos, most of which you want to use at some point. All of these combos are also included in the CORE collection">
                          <label class="switch"><input id="COMBOS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Core</div>
                        <div class="column">Elements</div>
                        <div class="column">Tears</div>
                        <div class="column">Orbits</div>
                        <div class="column">Combos</div>
                      </div>
                    </div>
                    <!-- Switches Clicks -->
                    <div class="container" style="width:95%; padding:0px; background-color: var(--grey-light); margin-top: 10px">
                      <div class="row" style="margin-left: 0px;">
                        <p class="expert-heading">Clicks</p>
                      </div>
                      <div class="row switch-row">
                        <div class="column" title="Only show scratches with REGULAR CLICK PATTERNS">
                          <label class="switch"><input id="RegularClicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Only show scratches with IRREGULAR CLICK PATTERNS (D, A, S, or Q)">
                          <label class="switch"><input id="IrregularClicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Regular</div>
                        <div class="column">Irregular</div>
                      </div>                  
                    </div>
                    <!-- Switches for Curves -->
                    <div class="container" style="width:95%; padding:0px; background-color: var(--grey-light); margin-top: 10px">
                      <div class="row" style="margin-left: 0px;">
                        <p class="expert-heading">Curves</p>
                      </div>
                      <div class="row switch-row">
                        <div class="column" title="Only show scratches with REGULAR CURVES">
                          <label class="switch"><input id="RegularCurves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Only show scratches with IRREGULAR CURVES (Ex or Log)">
                          <label class="switch"><input id="IrregularCurves" type="checkbox"/><span class="slider"></span></label>
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
                        <div class="column" title="Show CLICK TYPES">
                          <label class="switch"><input id="Clicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Show CURVE TYPES">
                          <label class="switch"><input id="Curves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="column" title="Show SCRATCH TYPES">
                          <label class="switch"><input id="Scratches" type="checkbox"/><span class="slider"></span></label>
                        </div>
                      </div>
                      <div class="row switch-row">
                        <div class="column">Clicks</div>
                        <div class="column">Curves</div>
                        <div class="column">Scratches</div>
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
                <!-- <table class="table scratch_table" id="scratch_table" style="font-size: 12px; background-color: var(--grey-light)"></table> -->
                <table class="table scratch_table" id="scratch_table"></table>
                <script type="text/javascript">
                  // Define table
                  $(document).ready(function () {
                    var table = $('#scratch_table').DataTable({
                      ajax: "https://raw.githubusercontent.com/arnosimons/scratchbook/main/CORE.json",
                      columns: [
                      {data:"Name(s)", title: "Name(s)"}, // 0
                      {data:"Tutorial", title: "Tutorial"}, // 1
                      {data:"Sounds", title: "Sounds"}, // 2
                      {data:"Elements", title: "Elements"}, // 3
                      {data:"Tears", title: "Tears"}, // 4
                      {data:"Orbits", title: "Orbits"}, // 5

                      {data:"FO", title: "FO"}, // 6
                      {data:"FC", title: "FC"}, // 7
                      {data:"PO", title: "PO"}, // 8
                      {data:"PC", title: "PC"}, // 9
                      {data:"D", title: "D"}, // 10
                      {data:"A", title: "A"}, // 11
                      {data:"S", title: "S"}, // 12
                      {data:"Q", title: "Q"}, // 13

                      {data:"Ex", title: "Ex"}, // 14
                      {data:"Log", title: "Log"}, // 15

                      {data:"Babies", title: "Babies"}, // 16
                      {data:"Ins", title: "Ins"}, // 17
                      {data:"Outs", title: "Outs"}, // 18
                      {data:"Dices", title: "Dices"}, // 19
                      {data:"Flares", title: "Flares"}, // 20
                      {data:"iFlares", title: "iFlares"}, // 21
                      {data:"oFlares", title: "oFlares"}, // 22
                      {data:"Transformers", title: "Transformers"}, // 23
                      {data:"Ghosts", title: "Ghosts"}, // 24
                      {data:"Holds", title: "Holds"}, // 25
                      {data:"G-Holds", title: "G-Holds"}, // 26

                      {data:"Chirps", title: "Chirps"}, // 27
                      {data:"Slices", title: "Slices"}, // 28
                      {data:"Stabs", title: "Stabs"}, // 29
                      {data:"Flare-Orbits", title: "Flare-Orbits"}, // 30
                      {data:"OG-Flares", title: "OG-Flares"}, // 31
                      {data:"Baby-Orbits", title: "Baby-Orbits"}, // 32
                      {data:"Dice-Orbits", title: "Dice-Orbits"}, // 33
                      {data:"Off-Stabs", title: "Off-Stabs"}, // 34

                      {data:"S-Curved", title: "S-Curved"}, // 35
                      {data:"Tazers", title: "Tazers"}, // 36
                      {data:"Phantazms", title: "Phantazms"}, // 37
                      {data:"Ex-Tazers", title: "Ex-Tazers"}, // 38
                      {data:"Ex-Phantazms", title: "Ex-Phantazms"}, // 39

                      {data:"Formula", title: "Formula"}, // 40

                      {data:"Search", title: "Search"}, // 41
                      
                      {data:"CORE", title: "CORE"}, // 42
                      {data:"ELEMENTS", title: "ELEMENTS"}, // 43
                      {data:"TEARS", title: "TEARS"}, // 44
                      {data:"ORBITS", title: "ORBITS"}, // 45
                      {data:"COMBOS", title: "COMBOS"}, // 46
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
                        $('#scratch_table thead th').each(function () {
                          var $td = $(this);
                          var headerText = $td.text(); 
                          var headerTitle=$td.text(); 
                          // Basic 6
                          if ( headerText == "Name(s)" )
                            headerTitle =  "Available NAMES for the scratch, to be used in the VISUALIZER. Synonymous names are seperated by a comma";
                          else if (headerText == "Tutorial" )
                            headerTitle = "A link to a VIDEO-TUTORIAL for the scratch (if available)";
                          else if (headerText == "Sounds" )
                            headerTitle = "Number of DISTINCT SOUNDS the scratch makes";
                          else if (headerText == "Elements" )
                            headerTitle = "Number of ELEMENTS in the scratch";
                          else if (headerText == "Tears" )
                            headerTitle = "Number of TEARS the scratch";
                          else if (headerText == "Orbits" )
                            headerTitle = "Number of ORBITS in the scratch";
                          // Clicks 8
                          else if (headerText == "FO" )
                            headerTitle = "Number of times the FADER is OPENED in the scratch";
                          else if (headerText == "FC" )
                            headerTitle = "Number of times the FADER is CLOSED in the scratch";
                          else if (headerText == "PO" )
                            headerTitle = "Number of times the PHANTOM-FADER is OPENED in the scratch";
                          else if (headerText == "PC" )
                            headerTitle = "Number of times the PHANTOM-FADER is OPENED in the scratch";
                          else if (headerText == "D" )
                            headerTitle = "Number of DIMINISHED click patterns in the scratch";
                          else if (headerText == "A" )
                            headerTitle = "Number of AUGMENTED click patterns in the scratch";
                          else if (headerText == "S" )
                            headerTitle = "Number of STRECHED click patterns in the scratch";
                          else if (headerText == "Q" )
                            headerTitle = "Number of SQUEEZED click patterns in the scratch";
                          // Curves 2
                          else if (headerText == "Ex" )
                            headerTitle = "Number of EXPONENTIAL curves in the scratch";
                          else if (headerText == "Log" )
                            headerTitle = "Number of LOGARITHMIC curves in the scratch";
                          // Elements 9
                          else if (headerText == "Babies" )
                            headerTitle = "Number of BABIES in the scratch";
                          else if (headerText == "Ins" )
                            headerTitle = "Number of INS in the scratch";
                          else if (headerText == "Outs" )
                            headerTitle = "Number of OUTS in the scratch";
                          else if (headerText == "Dices" )
                            headerTitle = "Number of DICES in the scratch";
                          else if (headerText == "Flares" )
                            headerTitle = "Number of FLARES in the scratch";
                          else if (headerText == "iFlares" )
                            headerTitle = "Number of iFLARES in the scratch";
                          else if (headerText == "oFlares" )
                            headerTitle = "Number of oFLARES in the scratch";
                          else if (headerText == "Transformers" )
                            headerTitle = "Number of TRANSFORMERS in the scratch";
                          else if (headerText == "Ghosts" )
                            headerTitle = "Number of GHOSTS in the scratch";
                          else if (headerText == "Holds" )
                            headerTitle = "Number of HOLDS in the scratch";
                          else if (headerText == "G-Holds" )
                            headerTitle = "Number of G-HOLDS in the scratch";
                          // Orbits
                          else if (headerText == "Chirps" )
                            headerTitle = "Number of CHIRPS in the scratch";
                          else if (headerText == "Slices" )
                            headerTitle = "Number of SLICES in the scratch";
                          else if (headerText == "Stabs" )
                            headerTitle = "Number of STABS in the scratch";
                          else if (headerText == "Flare-Orbits" )
                            headerTitle = "Number of FLARE-ORBITS in the scratch";
                          else if (headerText == "OG-Flares" )
                            headerTitle = "Number of OG-FLARES in the scratch";
                          else if (headerText == "Baby-Orbits" )
                            headerTitle = "Number of BABY-ORBITS in the scratch";
                          else if (headerText == "Dice-Orbits" )
                            headerTitle = "Number of DICE-ORBITS in the scratch";
                          else if (headerText == "Off-Stabs" )
                            headerTitle = "Number of OFF-STABS in the scratch";
                          // Orbit-Types
                          else if (headerText == "S-Curved" )
                            headerTitle = "Number of S-CURVED ORBITS in the scratch";
                          else if (headerText == "Tazers" )
                            headerTitle = "Number of TAZER ORBITS in the scratch";
                          else if (headerText == "Phantazms" )
                            headerTitle = "Number of PHANTAZM ORBITS in the scratch";
                          else if (headerText == "Ex-Tazers" )
                            headerTitle = "Number of EX-TAZER ORBITS in the scratch";
                          else if (headerText == "Ex-Phantazms" )
                            headerTitle = "Number of EX-PHANTAZM ORBITS in the scratch";
                          // Formula 1
                          else if (headerText == "Formula" )
                            headerTitle = "The FORMULA for composing the scratch. Copy-and-paste formulas into the VISUALIZER to make your own modifications!";
                          // Set the attribute...
                          $td.attr('title', headerTitle);
                        });
                        /* Style header tooltips */
                        $('#scratch_table [title]').tooltip({
                          trigger: "hover",
                          "container": 'body',
                        });
                        // Visibility of columns (the once skipped are the ones always visible)
                        var cols = [
                          // 0,1,2, // Name(s), Tutorial, Sounds
                          // 3,4,5, // Elements, Tears, Orbits
                          6,7,8,9, // clicks
                          10,11,12,13, // click patterns
                          14,15, // curves
                          16,17,18,19,20,21,22,23,24,25,26, // elements
                          27,28,29,30,31,32,33,34, // orbits
                          35, 36,37,38,39, // orbit-types
                          // 40, // formula
                          41, // search
                          42,43,44,45,46 // libraries
                        ]
                        table.columns( cols ).visible(false, false);
                        table.columns( cols ).searchable(false);
                        // Search column extra:
                        // table.columns( [41] ).visible(false, false);
                        table.columns( [41] ).searchable(true);
                      },
                    });
                    // Functions for row-filtering switches  
                    function activeLibs() {
                        let active_switches = [];
                        for (let libinfo of [
                          ["CORE", 42],
                          ["ELEMENTS", 43],
                          ["TEARS", 44],
                          ["ORBITS", 45],
                          ["COMBOS", 46],
                        ]) {
                          if (document.getElementById(libinfo[0]).checked) {
                              active_switches.push("data['" + libinfo[1] + "'] == 1")
                            }
                        }
                        return active_switches.join(" || ")
                    };
                    function crossFilters() {
                        let active_switches = [];
                        if (document.getElementById("RegularCurves").checked) {
                          active_switches.push("data['14'] == 0 && data['15'] == 0")
                        } else if (document.getElementById("IrregularCurves").checked) {
                          active_switches.push("data['14'] == 1 || data['15'] == 1")
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
                        if (crossFilters()) { // only relevant if some lib is active, hence nested here
                          query.push("(" + crossFilters() + ")");
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
                        var numOccurances = names.filter(x => x === data["Name(s)"]).length;
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
                        if (!existing_names.includes(row["Name(s)"])) {
                          rowsToAdd.push(row)
                        }
                      }
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
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/ELEMENTS.json', function(json) {
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
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/TEARS.json', function(json) {
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
                    // ORBITS switch
                    var load_ORBITS = true
                    $("#ORBITS").change(function() {
                      if(this.checked && load_ORBITS === true) {
                        load_ORBITS = false;
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/ORBITS.json', function(json) {
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
                    // COMBOS switch
                    var COMBOS = true
                    $("#COMBOS").change(function() {
                      if(this.checked && COMBOS === true) {
                        COMBOS = false;
                        $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/COMBOS.json', function(json) {
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
                      var cols = [14,15]
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
                      var cols = [6,7,8,9,10,11,12,13]
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
                      var cols = [
                        16,17,18,19,20,21,22,23,24,25,26, // elements
                        27,28,29,30,31,32,33,34, // orbits
                        35, 36,37,38,39, // orbit-types
                      ]
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
          <div class="card">
            <div class="card-header">
              <a 
                class="btn" 
                data-bs-toggle="collapse" 
                href="#OperatorCard" 
                title="Show ScratchBook's OPERATORS"
                style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">
                Operators
              </a>
            </div>
            <div id="OperatorCard" class="collapse in">
              <div class="card-body" style="overflow-x:auto;">
                <p><strong>Operators</strong> can be used <strong>to modify and combine scratches</strong>. The following table lists and explains all available operators.
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
                        <td>Add scratches from left to right</td>
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
                        <td>Decide how much of the sample is used (<em>n</em> must be between 0 and 1)</td>
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
                        <td>Shift the "phase" of a scratch by rotating its elements from right to left. (<em>n</em> must be an integer number)</td>
                        <td>scratch % <em>n</em></td>
                        <td>prizm % 0.25</td>
                    </tr>
                    <tr>
                        <td>[<em>n</em>]</td>
                        <td>Show the <em>n</em>-ths element of a composed scratch (<em>n</em> must be an integer number. <span style="color: var(--red)">&#9888;</span> Counting starts at 0 not at 1!)</td>
                        <td>scratch[<em>n</em>]</td>
                        <td>autobahn[3]</td>
                    </tr>
                    <tr>
                        <td>[<em>n</em>:<em>m</em>]</td>
                        <td>Show all elements between the <em>n</em>-ths (included) and <em>m</em>-ths (excluded) element of a composed scratch (<em>n</em> and <em>m</em> must be integer numbers. <span style="color: var(--red)">&#9888;</span> Counting starts at 0 not at 1!)</td>
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
        </div>
      </div>
      <br/>
    </div>
    <br/>
    <!-- Theory -->
    <div class="container-md pt-3 border rounded" style="background-color: white; box-shadow:0px 2px 0px -1px var(--grey-dark)">
      <div class="panel-group">
        <div class="panel panel-default">
          <div class="panel-heading">
            <h4>Theory</h4>
          </div>
          <div class="panel-body">
            <p style="margin-bottom: 5px;">
              ScratchBook builds on two theoretical pillars: A theory of <strong>scratch notation</strong> and a theory of <strong>scratch elements</strong>.
            </p>
            <p>Open the cards to learn more...</p>
          </div>
          <!-- Notation -->
          <div class="card">
            <div class="card-header">
              <a 
                class="btn" 
                data-bs-toggle="collapse" 
                href="#NotationCard" 
                title="Show information about ScratchBook's NOTATION"
                style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">
                Notation
              </a>
            </div>
            <div id="NotationCard" class="collapse in">
              <div class="card-body" style="overflow-x:auto;">
                <p> 
                  The <a href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>turntablist transcription methodology (TTM)</a> was created and published by John Carluccio, Ithan Imboden, and Raymond Pirtle in the late 1990s. It is a system for transcribing any scratch as the graph of a function of time, on the x-axis, either vs. the roation of the record or vs. the duration of the sample, on the y-axis.
                </p>
                <ul>
                  <li>When <strong>the curve moves up</strong> this means that the record moves forward. When <strong>the curve moves down</strong> the record moves down.</li>
                  <li>The <strong>steepness of the curve</strong> at any point signifies the speed of the record, which usually corresponds to the pitch of the sample (except when pitch control technologies are used). The faster the sample is played, the steeper the curve and vice versa.</li>
                  <li>When <strong>the curve forms a horizontal line</strong>, even for a very short period of time, this indicates that the record is held still and makes no sound. This occurs, for example, during a tear scratch and at the turning point of any orbit scratch.</li>
                  <li><strong>Circles on top of the curve</strong> signify "clicks", i.e. moments when the cross-fader is closed and re-opened in as little time as possible, causing small breaks in the sound.</li>
                </ul>
                <p> 
                  According to the original <a href="https://www.ttm-dj.com/TTMv1.1_Eng.pdf" target='_blank'>TTM-booklet</a>, TTM is emphatically <em>"an open source effort...Fight it, defend it, tweak it, trash it - all will assist its evolution"</em> (p.10). In this spirit, <strong>ScratchBook modifies the original TTM</strong> in the following way: 
                </p>
                <ul>
                  <li><strong>The color white</strong> generally indicates that the <strong>fader is closed</strong>.</li>
                  <li>Consequently, <strong>white circles</strong> (<u>not black ones</u>) are used to represent <strong>regular fader clicks</strong>.</li>
                  <li><strong>When the cross fader is closed for a longer time period</strong>, e.g. when the record is brought back during the second half of a stab scratch, this is indicated by a <strong>white curve</strong>.</li>
                  <li><strong>No "phantom clicks"</strong> are used to indicate moments when the record is held still. However, for the geeks among you, the number of opening and closing "phantom clicks" is reported in the tables.</li>
                </ul>
              </div>
            </div>
          </div>
          <!-- Elements -->
          <div class="card">
            <div class="card-header">
              <a 
                class="btn" 
                data-bs-toggle="collapse" 
                href="#ElementsCard" 
                title="Show information about ScratchBook's ELEMENTS"
                style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">
                Elements
              </a>
            </div>
            <div id="ElementsCard" class="collapse in">
              <div class="card-body" style="overflow-x:auto;">
                <p> 
                  Under the hood, <strong>ScratchBook takes an atomistic approach to scratch notation</strong>. Any scratch curve is generated from a sequence of distinct building blocks, called <strong>elements</strong>, each of which exhibits a unique combination of <strong>"subatomic features"</strong>.  
                </p>
                <p>
                  The total number of elements depends on the number of subatomic features and the rules of their combination, i.e <strong>the "grammar"</strong>. ScratchBook considers <strong>five classes of features</strong>:
                </p>
                <ul>
                  <li><strong>Curve shapes</strong> (horizontal, sine, exponential, logarithmic)</li>
                  <li><strong>Curve colors</strong> (black, white)</li>
                  <li><strong>io-Clicks</strong> (in/out-clicks), i.e. clicks at the start and/or at the end of a of a scratch ([], [0], [1], [0,1]])</li>
                  <li><strong>f-Clicks</strong> (flare-clicks), i.e. clicks somewhere in the middle of a scratch (0 - 3 clicks)</li>
                  <li><strong>Click patterns</strong> (normal, diminished, augmented, stretched, squeezed)</li>
                </ul> 
                <p>
                  <strong>Not all of these features should be combined with each other</strong>. For example, since white curves always represents silent record movement, they should  never have any clicks at all, and, to keep things simple, when they are not horizontal (1 Ghost-Hold), they should always be sine (1 Ghost). Also, click patterns only ever make sense when a scratch has at least one f-click, whereby stretched and squeezed patterns only make sense when at least two f-clicks are given.
                </p>
                <p>
                  The following decision tree maps out <strong>ScratchBook's current grammar</strong>, which results in a total of <strong>170 elements</strong>:
                </p>
                <p>
                  <img class="center" src="decision_tree.png" alt="Element construction" style="width: 536px; height: 223px;"> 
                </p>
                <p>
                  ScratchBook's element can be grouped into <strong>eleven classes of elements</strong> with the following <strong>distribution of subatomic features</strong>: 
                </p>
                <p>
                  <img class="center" src="el_classes.png" alt="Element construction" style="width: 653px; height: 413px;">
                </p>
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
          <p>ScratchBook uses a slightly modified version of the <a class="dark-link" href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>turntablist transcription methodology (TTM)</a>, which was created and <a class="dark-link" href="https://www.ttm-dj.com/TTMv1.1_Eng.pdf" target='_blank'>published</a> by John Carluccio, Ithan Imboden, and Raymond Pirtle in the late 1990s. I am deeply indebted to their work.</p>
          <p> © 2022 by <a class="dark-link" href="https://arnosimons.github.io/" target='_blank'>Arno Simons</a>, a Berlin-based turntablist and researcher.</p>
        </section>
      </div>
    </footer>
  </body>
  <py-script>
    import re
    from js import XMLHttpRequest
    req = XMLHttpRequest.new()
    req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/scratchbook.py", False)
    req.send()
    exec(str(req.response))
    req = XMLHttpRequest.new()
    req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/codebook_new.json", False)
    req.send()
    exec(f"codebook = {req.response}")
    slice = makeScratch('i_o', codebook)  # workaround to avoid name collision with "slice"   
    <!-- pyscript.write("session_message", codebook['_2cf']) -->
    session_info = document.getElementById("session_info")
    info_basic = document.getElementById("info_basic_tbody")
    info_curves_clicks = document.getElementById("info_curves_clicks_tbody")
    info_elements = document.getElementById("info_elements_tbody")    
    info_orbits = document.getElementById("info_orbits_tbody")
    info_orbit_types = document.getElementById("info_orbit_types_tbody")    
    def plot(x=None):
        formula = Element("scratch_input").element.value
        if not formula:
            pyscript.write("session_output", "plot() requires a formula as input.")
            return
        try:
            myscratch = makeScratch(formula, codebook)
            info = getInfo(myscratch)
            fig = Session(myscratch, fontsize=11, w_pad=2).fig
            pyscript.write("session_output", fig)
            for body, keys in [
                [info_basic, ["Sounds", "Elements", "Tears", "Orbits"]],
                [info_curves_clicks, ["FO", "FC", "PO", "PC", "D", "A", "S", "Q", "Ex", "Log"]],
                [info_elements, ["Babies", "Ins", "Outs", "Dices", "Flares", "iFlares", "oFlares", "Transformers", "Ghosts", "Holds", "G-Holds"]],
                [info_orbits, ["Chirps", "Slices", "Stabs", "Flare-Orbits", "OG-Flares", "Baby-Orbits", "Dice-Orbits", "Off-Stabs"]],
                [info_orbit_types, ["S-Curved", "Tazers", "Phantazms", "Ex-Tazers", "Ex-Phantazms"]],
            ]:
                body.innerHTML = ""
                row = document.createElement('tr')
                for k in keys:
                    td = document.createElement('td')
                    td.innerHTML = info[k]
                    row.appendChild(td)
                    body.appendChild(row)
            session_info.style.display = "block"
        except Exception as e:
            pyscript.write("session_output", str(e))  
    plot()
  </py-script>
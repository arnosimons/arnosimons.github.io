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
  <!-- My CSS -->
  <link rel="stylesheet" href="/projects/scratchbook/scratchbook.css">
</head>
<body style="background-color:var(--grey-light);">
  <header style="background-color:rgb(33, 37, 41);box-shadow:0px 4px 3px -1px var(--grey-dark)">
    <div class="container-md p-2.5 bg-dark text-white">
      <h1>ScratchBook &#128221;&#127926;</h1>
      <p style="color: white; font-size: 16px;">A platform for browsing, composing and visualizing scratches in <a class="dark-link" href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>TTM-like notation.</a></p>
      <p style="color: var(--red); font-size: 18px">&#9888; Loading the page takes time. Please wait until you see the scratch plot.</p>
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
              id="svg_button"
              class="mybuttons"
              title="Download SVG image">
              SVG
            </button>
            <button 
              id="png_button"
              class="mybuttons"
              title="Download PNG image">
              PNG
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
          <div id="session_svg" style="padding-bottom: 10px"><p style="font-size: 14px; color: var(--red)">Loading scratch plot...</p></div>
          <div id="session_png" style="display: none"></div>
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
                  <!-- <p>
                    The following tables tell you how many sounds your composition makes, how many elements and popular scratches it contains, which types of clicks and curves are involved, and much more.
                  </p> -->
                  <div class="info-container">
                    <p class="info-table-title">Basic Info</p>
                    <table id="info_basic" class="table info-table">
                      <thead><tr id="info_basic_thead">                          
                        <td title="Number of DISTINCT SOUNDS the composition makes">Sounds</td>
                        <td title="Number of ELEMENTARY SCRATCHES in the composition">Elements</td>
                        <td title="Number of TEARS in the composition">Tears</td>
                        <td title="Number of ORBITS in the composition">Orbits</td>
                      </tr></thead>
                      <tbody id="info_basic_tbody"></tbody>
                    </table>
                  </div>
                  <div class="info-container">
                    <p class="info-table-title">Clicks and Curves</p>
                    <table id="info_curves_clicks" class="table info-table">
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
                  <div class="info-container">
                    <p class="info-table-title">Elements</p>
                    <table id="info_elements" class="table info-table">
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
                  <div class="info-container">
                    <p class="info-table-title">Orbits</p>
                    <table id="info_orbits" class="table info-table">
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
                  <div class="info-container">
                    <p class="info-table-title">Orbit Types</p>
                    <table id="info_orbit_types" class="table info-table">
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
              var default_url = 'https://arnosimons.github.io/scratchbook';
              // var default_url = 'http://127.0.0.1:5500/scratchbook.html';
              var default_formula = "autobahn + chirp / 0.25 * 4";
              var scratch_input = document.getElementById("scratch_input");
              var scratch_button = document.getElementById("scratch_button");
              var session_svg = document.getElementById("session_svg");
              var session_png = document.getElementById("session_png");
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
                  session_message.innerHTML = "";
                  updateURL(scratch_input.value)
                  event.preventDefault();
                  if (scratch_input.value.trim()) {
                    scratch_button.click();
                  }
                  else {
                    session_svg.innerHTML = "";
                    session_png.innerHTML = "";
                  }
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
              // Function for svg_button
              $("#svg_button").click(function(){
                session_message.innerHTML = "";
                if ($("#session_svg").children('img').length){
                  let img_src = $("#session_svg").find('img').attr('src');
                  var a_temp = document.createElement('a');
                  a_temp.setAttribute('href', img_src);
                  a_temp.setAttribute('download',  "scratchbook_output");
                  document.body.appendChild(a_temp);
                  a_temp.click();
                  document.body.removeChild(a_temp);
                } 
                else {session_message.innerHTML = "Nothing to download"}
              });
              // Function for png_button
              $("#png_button").click(function(){
                session_message.innerHTML = "";
                if ($("#session_png").children('img').length){
                  let img_src = $("#session_png").find('img').attr('src');
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
                session_svg.innerHTML = "";
                session_png.innerHTML = "";
                session_info.style.display = "none";
                updateURL("")
              });
              // Function for default_button
              $("#default_button").click(function(){
                session_message.innerHTML = "";
                scratch_input.value = default_formula;
                session_svg.innerHTML = "";
                session_png.innerHTML = "";
                updateURL(scratch_input.value);
                scratch_button.click();
              });
              // Function for surprise_button
              $("#surprise_button").click(function(){
                session_message.innerHTML = "";
                scratches = [
                  'aquaman',
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
                  'clovertears',
                  'delete',
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
                  'mflare1',
                  'mflare2',
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
                  'scribbleflare1',
                  'scribbleflare2',
                  'spairflare',
                  'squareflare',
                  'stab',
                  'stabcrab',
                  'stabcrab_roll',
                  'swingflare',
                  'swirl',
                  'tazer1',
                  'tazer1_roll',
                  'tazer2',
                  'tazer2_roll',
                  'turnaroundtransform',
                  'xenon',
                ]
                scratch_input.value = scratches[Math.floor(Math.random() * scratches.length)];
                scratch_button.click();
                updateURL(scratch_input.value);
              });
            });
          </script>
        </div>
      </div>
    </div>
    <br/>
  </div>
  <br/>
  <!-- Library and Logic -->
  <div class="container-md pt-3 border rounded" style="background-color: white; box-shadow:0px 2px 0px -1px var(--grey-dark)">
    <div class="panel-group">
      <div class="panel panel-default">
        <div class="panel-heading">
          <h4>Library and Logic</h4>
        </div>
        <div class="panel-body">
          <p style="margin-bottom: 5px;">ScratchBook lets you write TTM-notation just like math. Combine <strong>scratches</strong> and <strong>operators</strong> into <strong>formulas</strong>, such as: <code>autobahn + prizm + (slice / 0.25) * 4</code></p>
          <p>Open the cards to learn more...</p>
        </div>
        <!-- Scratches -->
        <div class="card">
          <div class="card-header">
            <a 
              class="btn" 
              data-bs-toggle="collapse" 
              href="#ScratchCard" 
              title="Show SCRATCHES"
              style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">
              Scratches
            </a>
          </div>
          <div id="ScratchCard" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <p><strong>Browse scratches</strong> and <strong>click on their preview</strong> to add them to the visualizer. Use the <strong>expert mode</strong> for more options.</p>
              <div class="card">
                <div class="card-header">
                  <a 
                    class="btn btn-sm" 
                    data-bs-toggle="collapse" 
                    href="#ExpertCard" 
                    title="Show EXPERT CONTROLS (more info, more scratches)" 
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
                  <div class="container expert-container">
                    <div class="row" style="margin-left: 0px;">
                      <p class="expert-heading">Collections</p>
                    </div>
                    <div class="row switch-row">
                      <div class="column">
                        <div class="row"
                          title="The CORE collection contains 57 scratches and is loaded on default when opening the page">
                          <label class="switch"><input id="CORE" type="checkbox" checked/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Core</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="The ELEMENTS collection contains 171 unidirectional scratches with various modifications that form the ELEMENTS for all other scratches">
                          <label class="switch"><input id="ELEMENTS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Elements</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="The TEARS collection contains 42 unidirectional tear variations">
                          <label class="switch"><input id="TEARS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Tears</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="The ORBITS collection contains 594 orbits, generated from pairwise combinations of elements. Most orbits you will ever need are in here">
                          <label class="switch"><input id="ORBITS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Orbits</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="The COMBOS collection contains 47 popular scratch combos, all of which are also included in the CORE collection">
                          <label class="switch"><input id="COMBOS" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Combos</p>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!-- Switches Clicks -->
                  <div class="container expert-container">
                    <div class="row" style="margin-left: 0px;">
                      <p class="expert-heading">Clicks</p>
                    </div>
                    <div class="row switch-row">
                      <div class="column">
                        <div class="row"
                          title="Only show scratches with REGULAR CLICK PATTERNS">
                          <label class="switch"><input id="RegularClicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Regular</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="Only show scratches with IRREGULAR CLICK PATTERNS (D, A, S, or Q)">
                          <label class="switch"><input id="IrregularClicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Irregular</p>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!-- Switches for Curves -->
                  <div class="container expert-container">
                    <div class="row" style="margin-left: 0px;">
                      <p class="expert-heading">Curves</p>
                    </div>
                    <div class="row switch-row">
                      <div class="column">
                        <div class="row"
                          title="Only show scratches with REGULAR CURVES">
                          <label class="switch"><input id="RegularCurves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Regular</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="Only show scratches with IRREGULAR CURVES (Ex or Log)">
                          <label class="switch"><input id="IrregularCurves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Irregular</p>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!-- Switches for columns -->
                  <div class="container expert-container" style="margin-bottom: 10px">
                    <div class="row" style="margin-left: 0px;">
                      <p class="expert-heading">Columns</p>
                    </div>
                    <div class="row switch-row">
                      <div class="column">
                        <div class="row"
                          title="Show CLICK TYPES">
                          <label class="switch"><input id="Clicks" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Clicks</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="Show CURVE TYPES">
                          <label class="switch"><input id="Curves" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Curves</p>
                        </div>
                      </div>
                      <div class="column">
                        <div class="row"
                          title="Show SCRATCH TYPES">
                          <label class="switch"><input id="Scratches" type="checkbox"/><span class="slider"></span></label>
                        </div>
                        <div class="row switch-row">
                          <p class="expert-title">Scratches</p>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <!-- Style tooltips for all switches: -->
              <script>
                $(document).ready(function () {
                  $('.row[title]').tooltip({
                    trigger: "hover",
                    "container": 'body',
                  });
                });
              </script>
              <!-- DataTable -->
              <table class="table scratch-table" id="scratch_table"></table>
              <script type="text/javascript">
                // Define table
                $(document).ready(function () {
                  var table = $('#scratch_table').DataTable({
                    ajax: "https://raw.githubusercontent.com/arnosimons/scratchbook/main/CORE.json",
                    columns: [
                    {data:"Preview", title: "Preview" }, // 0
                    {data:"Name(s)", title: "Name(s)"}, // 1
                    {data:"Tutorial", title: "Tutorial"}, // 2
                    {data:"Sounds", title: "Sounds"}, // 3
                    {data:"Elements", title: "Elements"}, // 4
                    {data:"Tears", title: "Tears"}, // 5
                    {data:"Orbits", title: "Orbits"}, // 6
                    {data:"FO", title: "FO"}, // 7
                    {data:"FC", title: "FC"}, // 8
                    {data:"PO", title: "PO"}, // 9
                    {data:"PC", title: "PC"}, // 10
                    {data:"D", title: "D"}, // 11
                    {data:"A", title: "A"}, // 12
                    {data:"S", title: "S"}, // 13
                    {data:"Q", title: "Q"}, // 14
                    {data:"Ex", title: "Ex"}, // 15
                    {data:"Log", title: "Log"}, // 16
                    {data:"Babies", title: "Babies"}, // 17
                    {data:"Ins", title: "Ins"}, // 18
                    {data:"Outs", title: "Outs"}, // 19
                    {data:"Dices", title: "Dices"}, // 20
                    {data:"Flares", title: "Flares"}, // 21
                    {data:"iFlares", title: "iFlares"}, // 22
                    {data:"oFlares", title: "oFlares"}, // 23
                    {data:"Transformers", title: "Transformers"}, // 24
                    {data:"Ghosts", title: "Ghosts"}, // 25
                    {data:"Holds", title: "Holds"}, // 26
                    {data:"G-Holds", title: "G-Holds"}, // 27
                    
                    {data:"Chirps", title: "Chirps"}, // 28
                    {data:"Slices", title: "Slices"}, // 29
                    {data:"Stabs", title: "Stabs"}, // 30
                    {data:"Flare-Orbits", title: "Flare-Orbits"}, // 31
                    {data:"OG-Flares", title: "OG-Flares"}, // 32
                    {data:"Baby-Orbits", title: "Baby-Orbits"}, // 33
                    {data:"Dice-Orbits", title: "Dice-Orbits"}, // 34
                    {data:"Off-Stabs", title: "Off-Stabs"}, // 35
                    
                    {data:"S-Curved", title: "S-Curved"}, // 36
                    {data:"Tazers", title: "Tazers"}, // 37
                    {data:"Phantazms", title: "Phantazms"}, // 38
                    {data:"Ex-Tazers", title: "Ex-Tazers"}, // 39
                    {data:"Ex-Phantazms", title: "Ex-Phantazms"}, // 40
                    
                    {data:"Formula", title: "Formula"}, // 41
                    
                    {data:"Search", title: "Search"}, // 42
                    
                    {data:"CORE", title: "CORE"}, // 43
                    {data:"ELEMENTS", title: "ELEMENTS"}, // 44
                    {data:"TEARS", title: "TEARS"}, // 45
                    {data:"ORBITS", title: "ORBITS"}, // 46
                    {data:"COMBOS", title: "COMBOS"}, // 47
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
                        var $th = $(this);
                        var headerText = $th.text(); 
                        var headerTitle = $th.text(); 
                        // Basic 7
                        if ( headerText == "Preview" )
                          headerTitle =  "A PREVIEW of the scratch";
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
                        $th.attr('title', headerTitle);
                      });
                      // Tooltips for clicking Previews and Names
                      $('#scratch_table tbody tr').each(function () {
                        var tr = $(this);
                        td1 = tr.find("td:eq(0)");
                        td1.attr('title', "Click to add scratch to visualizer!");
                        td2 = tr.find("td:eq(1)");
                        td2.attr('title', "Click to add scratch to visualizer!");
                      });
                      /* Style header tooltips */
                      $('#scratch_table [title]').tooltip({
                        trigger: "hover",
                        "container": 'body',
                      });
                      // Get name when clicking on rows
                      $('#scratch_table').on('click', 'td', function () {
                        var cell = table.cell( this ).data();
                        var colindx = table.column( this ).index();
                        if (colindx == 0 || colindx == 1) {
                          var row = table.row( this ).data();
                          var names = row["Name(s)"];
                          names = names.split(",");
                          if (scratch_input.value.trim()) {
                            scratch_input.value += " + " + names[0];
                          }
                          else{
                            scratch_input.value += names[0];
                          };
                          scratch_button.click();
                          updateURL(scratch_input.value);
                        }; 
                      });
                      // Visibility of columns (the once skipped are the ones always visible)
                      var cols = [
                        // 0,1,2,3 // Preview, Name(s), Tutorial, Sounds
                        // 4,5,6 // Elements, Tears, Orbits
                        7,8,9,10, // clicks
                        11,12,13,14, // click patterns
                        15,16, // curves
                        17,18,19,20,21,22,23,24,25,26,27, // elements
                        28,29,30,31,32,33,34,35, // orbits
                        36,37,38,39,40, // orbit-types
                        // 41, // formula
                        42, // search
                        43,44,45,46,47 // libraries
                      ]
                      table.columns( cols ).visible(false, false);
                      table.columns( cols ).searchable(false);
                      // Search column extra:
                      table.columns( [41] ).searchable(true);
                    },
                  });
                  // Functions for row-filtering switches  
                  function activeLibs() {
                      let active_switches = [];
                      for (let libinfo of [
                        ["CORE", 43],
                        ["ELEMENTS", 44],
                        ["TEARS", 45],
                        ["ORBITS", 46],
                        ["COMBOS", 47],
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
                        active_switches.push("data['15'] == 0 && data['16'] == 0")
                      } else if (document.getElementById("IrregularCurves").checked) {
                        active_switches.push("data['15'] == 1 || data['16'] == 1")
                      }
                      if (document.getElementById("RegularClicks").checked) {
                        active_switches.push("data['11'] == 0 && data['12'] == 0 && data['13'] == 0 && data['14'] == 0")
                      } else if (document.getElementById("IrregularClicks").checked) {
                        active_switches.push("data['11'] == 1 || data['12'] == 1 || data['13'] == 1 || data['14'] == 1")
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
                    var names = table.column( 1 ).data().toArray();
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
                    var existing_names = table.column( 1 ).data().toArray();
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
                    var cols = [15,16]
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
                    var cols = [7,8,9,10,11,12,13,14]
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
                      17,18,19,20,21,22,23,24,25,26,27, // elements
                      28,29,30,31,32,33,34,35, // orbits
                      36,37,38,39,40, // orbit-types
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
              title="Show OPERATORS"
              style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">
              Operators
            </a>
          </div>
          <div id="OperatorCard" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <p>
                Read how <strong>operators</strong> can be used <strong>to modify and combine scratches</strong>.
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
        <!-- Formulas -->
        <div class="card">
          <div class="card-header">
            <a 
              class="btn" 
              data-bs-toggle="collapse" 
              href="#FormulasCard" 
              title="Get geeky about Formulas"
              style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">
              Formulas
            </a>
          </div>
          <div id="FormulasCard" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <p> 
                ScratchBook's <strong>formulas work on two levels</strong>.
              </p>
              <p>
                At the <strong>first level</strong>, you can combine <strong>scratches</strong> (i.e. their names) and <strong>operators</strong> into formulas like <code>autobahn + prizm + (slice / 0.25) * 4</code>. See the two tabs above to learn more. 
              </p>
              <p>
                At the <strong>second level</strong>, ScratchBook offers <strong>formal languages</strong> to define <strong>elements</strong>, <strong>tears</strong>, and <strong>orbits</strong>.
              </p>
              <div class="card">
                <div class="card-header">
                  <a 
                    class="btn btn-sm" 
                    data-bs-toggle="collapse" 
                    href="#ElementsLanguageCard" 
                    title="Show ELEMENT LANGUAGE" 
                    style="width: 100%; text-align: left; font-size: 14px; font-weight: 500;">
                    Language for Elements
                  </a>
                </div>
                <div id="ElementsLanguageCard" class="collapse in">
                  <div class="card-body" style="overflow-x:auto;">
                    <div class="container" style="width:95%; padding:0px; margin-top: 10px">
                      <p>
                        <strong>Elements</strong> are scratches that cannot be broken down into smaller scratches, only into their "subatomic features" (see the Theory section below). Their names obey the <strong>grammar</strong> <code>[BASE][N]*[CP]*[CRV]*</code>, whereby
                      </p>
                      <ul>
                        <li><code>[BASE]</code> is obligatory and stands for one of the eleven <strong>base names</strong>: <code>baby, in, out, dice, flare, iflare, oflare, transformer, ghost, hold, ghosthold</code>. 
                          <br/>&#128123; If you're lazy, like me, simply use <strong>abbreviations</strong>: <code>b, i, o, d, f, if, of, tr, g, h, gh</code>.</li>
                        <li><code>[N]*</code> is only possible but then also obligatory after the bases <code>f, if, of</code>, where it stands for the number of <strong>flare-clicks</strong>, as well as after the base <code>tr</code>, where it stands for the number of <strong>transformer sounds</strong>. Currently, all numbers between <code>1</code> and <code>9</code> are permitted.</li>
                        <li><code>[CP]*</code> is optional and stands for a non-standard <strong>click-pattern</strong> (<code>D, A, S</code> or <code>Q</code>) after any of the bases <code>f, if, of, tr</code>.</li>
                        <li><code>[CRV]*</code> is optional and stands for a non-standard <strong>curve shape</strong> (<code>Ex</code> or <code>Log</code>) after all bases except <code>g, h, gh</code>.</li>
                      </ul>
                      <p>
                        <strong>Examples</strong> for elements following this grammar are:
                      </p>
                      <ul>
                        <li>
                          <code>babyLog</code> (a baby with a logarithmic curve)
                        </li>
                        <li>
                          <code>f8Q</code> (an 8-click flare with a squeezed click-pattern)
                        </li>
                        <li>
                          <code>tr2AEx</code> (a 2-sound transformer with an augmented click-pattern and an exponential curve)
                        </li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
              <div class="card">
                <div class="card-header">
                  <a 
                    class="btn btn-sm" 
                    data-bs-toggle="collapse" 
                    href="#TearsLanguageCard" 
                    title="Show TEAR LANGUAGE" 
                    style="width: 100%; text-align: left; font-size: 14px; font-weight: 500;">
                    Language for Tears
                  </a>
                </div>
                <div id="TearsLanguageCard" class="collapse in">
                  <div class="card-body" style="overflow-x:auto;">
                    <div class="container" style="width:95%; padding:0px; margin-top: 10px">
                      <p>
                        <strong>Tears</strong> are sequences of upwards or downwards oriented elements, forming cascades. Their names obey the <strong>grammar</strong> <code>[TBASE]*tear[N][CRV]*[__EL]*</code>, whereby
                      </p>
                      <ul>
                        <li><code>[TBASE]</code> is optional and stands for one of the following <strong>tear-bases</strong>: <code>i, o, d, f, if, of, tr</code>. The <strong>purpose</strong> of the tear-base is to specify <strong>if and where clicks are added</strong> when the record is paused, i.e. <strong>during the tearing moments</strong>:
                          <br/><code>i</code> = click at the start, 
                          <br/><code>o</code> = click at the end, 
                          <br/><code>d</code> = click at the start AND click at the end, 
                          <br/><code>f</code> = clicks at every tearing moment, 
                          <br/><code>if</code> = click at the start AND clicks at every tearing moment, 
                          <br/><code>of</code> = clicks at every tearing moment AND click at the end, 
                          <br/><code>tr</code> = click at the start AND clicks at every tearing moment AND click at the end.</li>
                        <li><code>tear</code> is obligatory but <strong>can be abbreviated</strong> as <code>t</code>.</li>
                        <li><code>[N]</code> is obligatory and stands for the number of pauses or <strong>tearing moments</strong>, i.e. how often the record is held still during a tear scratch.</li>
                        <li><code>[CRV]*</code> is optional and stands for a non-standard <strong>curve shape</strong> (<code>Ex</code> or <code>Log</code>).</li>
                        <li><code>[__EL]*</code> is optional and stands for <strong>a specific element</strong> being used during the tear scratch. <u>This function is only useful for tears and transformers</u>, and only their base names are allowed, e.g. <code>__f3</code> or <code>__tr2</code>, but not <code>__f3D</code> or <code>tr2Log</code>. Note that you must use <u>two underscores</u> to specify the tear element (otherwise you're falsely using the orbit language, see the tab below).</li>
                      </ul>
                      <p>
                        <strong>Examples</strong> for tears following this grammar are:
                      </p>
                      <ul>
                        <li>
                          <code>tear5</code> (a 5-tear without any clicks)
                        </li>
                        <li>
                          <code>it2</code> (a 2-tear with a click at the start)
                        </li>
                        <li>
                          <code>oft4</code> (a 4-tear with clicks at all 4 tearing moments and a click at the end)
                        </li>
                        <li>
                          <code>it4__f1</code> (a 4-tear with a click at the start whose elements are 1-click flares)
                        </li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
              <div class="card">
                <div class="card-header">
                  <a 
                    class="btn btn-sm" 
                    data-bs-toggle="collapse" 
                    href="#OrbitsLanguageCard" 
                    title="Show ORBIT LANGUAGE" 
                    style="width: 100%; text-align: left; font-size: 14px; font-weight: 500;">
                    Language for Orbits
                  </a>
                </div>
                <div id="OrbitsLanguageCard" class="collapse in">
                  <div class="card-body" style="overflow-x:auto;">
                    <div class="container" style="width:95%; padding:0px; margin-top: 10px">
                      <p>
                        <strong>Orbits</strong> are scratches that incorporate both a forward and backward movement, or vice versa, of the record in sequence. At the first level, you can always construct orbits like so: <code>[SCRATCH] + ~[SCRATCH]</code>, where <code>[SCRATCH]</code> in both cases stands for any element or tear scratch. But if you want to specify a particular length-ratio, things get messier. For example, to get a ratio of "two-to-three", you need to write something like <code>([SCRATCH] / 2 + ~[SCRATCH] / 3) / 1</code>.
                      </p>
                      <p>
                        At the second level, <strong>a more convenient way</strong> to formulate orbits is to use the <strong>grammar</strong> <code>[SCRATCH]_[SCRATCH][_RATIO]*</code>, whereby
                      </p>
                      <ul>
                        <li><code>[SCRATCH]</code> is obligatory in both cases and stands for <strong>any element or tear scratch</strong> (the second one automatically being the backward scratch).</li>
                        <li><code>_</code> is obligatory and simply stands for "orbit".</li>
                        <li><code>[_RATIO]*</code> is optional and stands for a specific <strong>length-ratio</strong>, such as <code>_23</code>, meaning "two-to-three", i.e. that the forward scratch gets 2/5<i>th</i> of the total length while the backward scratch gets 3/5<i>th</i> of the total length. If no length-ratio is specified, a ratio of "one-to-one" is automatically assumed.</li>
                      </ul>
                      <p>
                        <strong>Examples</strong> for orbits following this grammar are:
                      </p>
                      <ul>
                        <li>
                          <code>flare1_flare2</code> (a "1-click-flare-vs-2-click-flare" orbit aka "rawhippopotamus" with a non-specified "one-to-one" length-ratio.)
                        </li>
                        <li>
                          <code>f1_f2_23</code> (a "1-click-flare-vs-2-click-flare" orbit aka "hippopotamus" with a specified "two-to-three" length-ratio.)
                        </li>
                        <li>
                          <code>it4_o</code> (a "4-tear-vs-out" orbit)
                        </li>
                      </ul>
                      <p>
                        <strong>Please note</strong>:
                      </p>
                      <ul>
                        <li>
                          You can use both <strong>elements</strong> and <strong>tears</strong> as scratches.
                        </li>
                        <li>
                          The grammar allows you to compose <strong>unloopable orbits</strong>, like <code>b_o</code>, whose start and end connectors do not match, so that the orbit could not be looped in reality.
                        </li>
                        <li>
                          The grammar (currently) does not prohibit you from composing <strong>"impossible" orbits</strong>, like <code>b_i</code>, whose direct connectors don't match. In the example, a baby-scratch <u>without</u> a click at the end meets an in-scratch <u>with</u> a click at the start. 
                        </li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
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
                The <a href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>turntablist transcription methodology (TTM)</a> was created and published by John Carluccio, Ithan Imboden, and Raymond Pirtle in the late 1990s. It is a system for transcribing any scratch as the graph of a function of time, on the x-axis, against the roation of the record or against the duration of the sample, on the y-axis.<sup><a href="#footnote-1"><span style="font-size: 9px;">[1]</span></a></sup>
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
              <p class="footnote" id="footnote-1"><sup>[1]</sup> TTM has been fleshed out more fully in Raymond Pirtle's later work on the "Periodic Matrix of Scratches". There is also an alternative scratch notation system, which resembles the modern staff notation. See Alex Sonnenfeld's <a href="http://www.alexandersonnenfeld.com/fileadmin/user_upload/S-Notation/S-Notation-Paper_Tenor_2016.pdf" target='_blank'>S-Notation</a>.</p>
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
                Under the hood, <strong>ScratchBook takes a unique atomistic approach to scratch notation</strong>. Any scratch curve is generated from a sequence of distinct building blocks, called <strong>elements</strong>, each of which exhibits a unique combination of <strong>"subatomic features"</strong>.
              </p>
              <p>
                ScratchBook's elements fall into <strong>eleven classes</strong> and <strong>two groups</strong>:
              </p>
              <div class="container elements-container">
                <div class="row elements-group">
                  <p class="expert-heading">Group 1</p>
                </div>
                <div class="row">
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/b.png" alt="Babies"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Babies</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/i.png" alt="Ins"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Ins</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/o.png" alt="Outs"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Outs</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/d.png" alt="Dices"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Dices</p>
                    </div>
                  </div>
                </div>
              </div>
              <div class="container elements-container">
                <div class="row">
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/f1.png" alt="Flares"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Flares</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/if1.png" alt="iFlares"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">iFlares</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/of1.png" alt="oFlares"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">oFlares</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/tr2.png" alt="dFlares (Transformers)"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">dFlares (Transformers)</p>
                    </div>
                  </div>
                </div>
              </div>
              <div class="container elements-container" style="margin-top: 10px;">
                <div class="row elements-group">
                  <p class="expert-heading">Group 2</p>
                </div>
                <div class="row">
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/g.png" alt="Ghost"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Ghost</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/h.png" alt="Hold"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Hold</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/gh.png" alt="Ghost-Hold"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">Ghost-Hold</p>
                    </div>
                  </div>
                </div>
              </div>
              <br/>
              <p>
                <strong>Group 1</strong> comprises 8 classes of <strong>elements that make a sound</strong>. These classes relate to each other in the following ways:
              </p>
              <ul>
                <li>
                  <strong>Babies and Flares</strong> both have no clicks at their start and end points, but they differ in that only the Flares have clicks in between their start and end points (only one such click is shown here, but scratches of all Flare classes can have up to 9 clicks).
                </li>
                <li>
                  <strong>Ins and iFlares</strong> both have a click at their start points and no click at their end points, but they differ in that only the iFlares have clicks in between their start and end points.
                </li>
                <li>
                  <strong>Outs and oFlares</strong> both have a click at their end points and no click at their start points (opposite of Ins/iFlares!), but they differ in that only the iFlares have clicks in between their start and end points.
                </li>
                <li>
                  <strong>Dices and dFlares </strong> both have clicks at their start AND end points, but they differ in that only the dFlares have clicks in between their start and end points.
                </li>
                <li>
                  Since <strong>dFlares are commonly referred to as Transformers</strong>, Scratchbook permits both names, <strong>but the grammar is slightly different</strong>. The equivalent of <code>df2</code> is <code>tr3</code> (<u>not</u> <code>t2</code>), because the numbers refer to different quantities. <strong>In all flare scratches</strong>, including dFlares, the number refers to <strong>the number of clicks</strong> while <strong>in transformers</strong> the number refers to <strong>the number of sounds</strong>. 
                </li>
              </ul>
              <p>
                <strong>Group 2</strong> comprises 3 <strong>elements that do <u>not</u> make a sound</strong>:
              </p>
              <ul>
                <li>
                  The <strong>Ghost</strong> is used mainly in the <code>stab</code> scratch, where it signifies the silent backward movement of the record after the fader has been closed.
                </li>
                <li>
                  The <strong>Hold</strong> is used whenever the record is held still for a longer time period while the fader remains open. See for example the <code>slicecombo1</code>.
                </li>
                <li>
                  The <strong>Ghost-Hold</strong> is used whenever the record is held still for a longer time period while the fader is closed.
                </li>
              </ul>
              <p>
                The <strong>total number of elements within and across all classes</strong> depends on the number of subatomic features and the rules of their combination. ScratchBook considers <strong>five classes of features</strong>:
              </p>
              <ul>
                <li><strong>Curve shapes</strong> (horizontal, sine, exponential, logarithmic)</li>
                <li><strong>Curve colors</strong> (black, white)</li>
                <li><strong>io-Clicks</strong> (in/out-clicks), i.e. clicks at the start and/or at the end of a of a scratch (none, start, end, start+end).</li>
                <li><strong>f-Clicks</strong> (flare-clicks), i.e. clicks somewhere in the middle of a scratch (0-9 clicks, but limited to 0-3 clicks in the element collection)</li>
                <li><strong>Click patterns</strong> (normal, diminished, augmented, stretched, squeezed)</li>
              </ul>
              <p>
                <strong>Not all of these features should be combined with each other</strong>. For example, since white curves always represents silent record movement, they should  never have any clicks at all, and, to keep things simple, when they are not horizontal (1 Ghost-Hold), they should always be sine (1 Ghost). Also, click patterns only ever make sense when a scratch has at least one f-click, whereby stretched and squeezed patterns only make sense when at least two f-clicks are given.
              </p>
              <p>The following example of a 3-click flare scratch gives an overview over <strong>the five available click patterns</strong>:</p>
              <div class="container">
                <div class="row">
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/f3.png" alt="normal"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">normal (<code>f3</code>)</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/f3A.png" alt="Hold"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">augmented (<code>f3A</code>)</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/f3D.png" alt="Ghost-Hold"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">diminished (<code>f3D</code>)</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/f3S.png" alt="Ghost-Hold"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">stretched (<code>f3S</code>)</p>
                    </div>
                  </div>
                  <div class="col centered">
                    <div class="row">
                      <span><img class="preview" src="/projects/scratchbook/previews/f3Q.png" alt="Ghost-Hold"></span>
                    </div>
                    <div class="row">
                      <p class="preview-title">squeezed (<code>f3Q</code>)</p>
                    </div>
                  </div>
                </div>
              </div>
              <p>
                The following table shows the <strong>distribution of subatomic features over ScratchBook's elements</strong>: 
              </p>
              <p class="centered">
                <img 
                src="/projects/scratchbook/el_classes.png"
                  alt="classes of elements" 
                  style="max-width: 60%">
              </p>
              <p>
                In order to keep the size of ScratchBook's <strong>elements collection</strong> reasonably small, the number of f-clicks is limited to 3 there, resulting in a total of <strong>171 elements</strong>, computed by the following <strong>rules of combination</strong>:
              </p>
              <p class="centered">
                <img 
                  src="/projects/scratchbook/decision_tree.png"
                  alt="rules for combining elements" 
                  style="max-width: 52%">
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
        <p>ScratchBook is an educational and non-commercial project. The <a class="dark-link" href="https://github.com/arnosimons/scratchbook" target='_blank'>underlying code</a> is free freely available and reusable under the GPL-3.0 license.</p>
        <p>ScratchBook uses a slightly modified version of the <a class="dark-link" href="https://en.wikipedia.org/wiki/Turntablist_transcription_methodology" target='_blank'>turntablist transcription methodology (TTM)</a>, which was created and <a class="dark-link" href="https://www.ttm-dj.com/TTMv1.1_Eng.pdf" target='_blank'>published</a> by John Carluccio, Ithan Imboden, and Raymond Pirtle in the late 1990s. I am deeply indebted to their work.</p>
        <p> © 2022 by Arno Simons, a Berlin-based <a class="dark-link" href="https://www.instagram.com/dj_hdrs/" target='_blank'>turntablist</a> and <a class="dark-link" href="https://scholar.google.de/citations?user=NhCwiDwAAAAJ&hl=en" target='_blank'>researcher</a>.</p>
      </section>
    </div>
    <!-- Impressum -->
    <div class="container-sm">
      <div class="dark-card">
        <div class="dark-card-header">
          <a 
            class="impressum-link dark-btn" 
            data-bs-toggle="collapse" 
            href="#ImpressumCard">
            Impressum
          </a>
        </div>
        <div id="ImpressumCard" class="collapse in">
          <div class="dark-card-body" style="overflow-x:auto;">
          <br/>
            <p>Angaben gemäß § 5 TMG</p>
            <p>
                Arno Simons <br> 
                Deidesheimer Str. 2<br> 
                14197 Berlin <br> 
            </p>
            <p>
                Kontakt: <br>
                E-Mail: <a href='mailto:arno.simons@gmail.com'>arno.simons@gmail.com</a><br/></p>
            </p>
            <p>Verantwortlich für den Inhalt nach § 55 Abs. 2 RStV:</p>
            <p>
                Arno Simons <br> 
                Deidesheimer Str. 2<br> 
                14197 Berlin <br>
            </p> 
          <br/>
            <p>
                <strong>HAFTUNGSAUSSCHLUSS</strong>
                <br><br>            
                <strong>Haftung für Inhalte</strong>
                <br><br>
                Die Inhalte dieser Seiten wurden mit größter Sorgfalt erstellt. Für die Richtigkeit, Vollständigkeit und Aktualität der Inhalte kann der Seitenbetreiber jedoch keine Gewähr übernehmen. Als Diensteanbieter ist der Seitenbetreiber gemäß § 7 Abs.1 TMG für eigene Inhalte auf diesen Seiten nach den allgemeinen Gesetzen verantwortlich. Nach §§ 8 bis 10 TMG ist der Seitenbetreiber als Diensteanbieter jedoch nicht verpflichtet, übermittelte oder gespeicherte fremde Informationen zu überwachen oder nach Umständen zu forschen, die auf eine rechtswidrige Tätigkeit hinweisen. Verpflichtungen zur Entfernung oder Sperrung der Nutzung von Informationen nach den allgemeinen Gesetzen bleiben hiervon unberührt. Eine diesbezügliche Haftung ist jedoch erst ab dem Zeitpunkt der Kenntnis einer konkreten Rechtsverletzung möglich. Bei Bekanntwerden von entsprechenden Rechtsverletzungen wird der Seitenbetreiber diese Inhalte umgehend entfernen.
                <br><br>
                <strong>Haftung für Links</strong>
                <br><br>
                Diese Seiten enthalten Links zu externen Webseiten Dritter, auf deren Inhalte der Seitenbetreiber keinen Einfluss hat. Deshalb kann der Seitenbetreiber für diese fremden Inhalte auch keine Gewähr übernehmen. Für die Inhalte der verlinkten Seiten ist stets der jeweilige Anbieter oder Betreiber der Seiten verantwortlich. Die verlinkten Seiten wurden zum Zeitpunkt der Verlinkung auf mögliche Rechtsverstöße überprüft. Rechtswidrige Inhalte waren zum Zeitpunkt der Verlinkung nicht erkennbar. Eine permanente inhaltliche Kontrolle der verlinkten Seiten ist jedoch ohne konkrete Anhaltspunkte einer Rechtsverletzung nicht zumutbar. Bei Bekanntwerden von Rechtsverletzungen wird der Seitenbetreiber derartige Links umgehend entfernen.
                <br><br>
                <strong>Urheberrecht</strong>
                <br><br>
                Die durch den Seitenbetreiber erstellten Inhalte und Werke auf diesen Seiten unterliegen dem deutschen Urheberrecht. Die Vervielfältigung, Bearbeitung, Verbreitung und jede Art der Verwertung außerhalb der Grenzen des Urheberrechtes bedürfen der schriftlichen Zustimmung des jeweiligen Autors bzw. Erstellers. Downloads und Kopien dieser Seite sind nur für den privaten, nicht kommerziellen Gebrauch gestattet. Soweit die Inhalte auf dieser Seite nicht vom Betreiber erstellt wurden, werden die Urheberrechte Dritter beachtet. Insbesondere werden Inhalte Dritter als solche gekennzeichnet. Sollten Sie trotzdem auf eine Urheberrechtsverletzung aufmerksam werden, bittet der Seitenbetreiber um einen entsprechenden Hinweis. Bei Bekanntwerden von Rechtsverletzungen wird der Seitenbetreiber derartige Inhalte umgehend entfernen.
                <br><br>
                <strong>Datenschutz</strong>
                <br><br>
                Die Nutzung dieser Webseite ist in der Regel ohne Angabe personenbezogener Daten möglich. Soweit auf diesen Seiten personenbezogene Daten (beispielsweise Name, Anschrift oder eMail-Adressen) erhoben werden, erfolgt dies, soweit möglich, stets auf freiwilliger Basis. Diese Daten werden ohne Ihre ausdrückliche Zustimmung nicht an Dritte weitergegeben. <br>
                Wir weisen darauf hin, dass die Datenübertragung im Internet (z.B. bei der Kommunikation per E-Mail) Sicherheitslücken aufweisen kann. Ein lückenloser Schutz der Daten vor dem Zugriff durch Dritte ist nicht möglich. 
                <br>
                Der Nutzung von im Rahmen der Impressumspflicht veröffentlichten Kontaktdaten durch Dritte zur Übersendung von nicht ausdrücklich angeforderter Werbung und Informationsmaterialien wird hiermit ausdrücklich widersprochen. Der Betreiber der Seiten behält sich ausdrücklich rechtliche Schritte im Falle der unverlangten Zusendung von Werbeinformationen, etwa durch Spam-Mails, vor.<br>
                <br><br>
            </p>
          </div>
        </div>
      </div>
    </div>
    
  <br/>
  </footer>
</body>
<py-script>
  import base64
  from io import BytesIO
  import re
  from js import XMLHttpRequest
  req = XMLHttpRequest.new()
  req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/scratchbook.py", False)
  req.send()
  exec(str(req.response))
  req = XMLHttpRequest.new()
  req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/codebook.json", False)
  req.send()
  exec(f"codebook = {req.response}")
  session_info = document.getElementById("session_info")
  session_svg = document.getElementById("session_svg")
  session_png = document.getElementById("session_png")
  info_basic = document.getElementById("info_basic_tbody")
  info_curves_clicks = document.getElementById("info_curves_clicks_tbody")
  info_elements = document.getElementById("info_elements_tbody")    
  info_orbits = document.getElementById("info_orbits_tbody")
  info_orbit_types = document.getElementById("info_orbit_types_tbody")    
  def plot(x=None):
      session_svg.innerHTML = ""
      session_png.innerHTML = ""
      formula = Element("scratch_input").element.value
      try:
          myscratch = makeScratch(formula, codebook)
          info = getInfo(myscratch)
          fig = Session(myscratch, fontsize=11, w_pad=2).fig
          tmpfile = BytesIO()
          fig.savefig(tmpfile, format='svg')
          encoded = base64.b64encode(tmpfile.getvalue()).decode('utf-8')
          src = f'data:image/svg+xml;base64, {encoded}'
          svg = document.createElement('img')
          svg.setAttribute("src", src)
          session_svg.appendChild(svg)
          pyscript.write("session_png", fig)
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
      except SyntaxError as e:
          session_svg.innerHTML = repr(e)
      except KeyError as e:
          session_svg.innerHTML = f'{e} is not a valid scratch name'
      except AttributeError as e:
          if "object has no attribute 'slices'" in repr(e):
              session_svg.innerHTML = "You have used an invalid scratch name"
          else:
              session_svg.innerHTML = repr(e)
      except Exception as e:
          session_svg.innerHTML = repr(e)
  plot()
</py-script>

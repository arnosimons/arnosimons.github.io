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
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://pyscript.net/alpha/pyscript.css"/>
  <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/5.1.3/css/bootstrap.min.css">
  <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.12.1/css/dataTables.bootstrap5.min.css">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script defer src="https://pyscript.net/alpha/pyscript.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>
  <script src="https://code.jquery.com/jquery-3.5.1.js"></script>
  <script src="https://cdn.datatables.net/1.12.1/js/jquery.dataTables.min.js"></script>
  <script src="https://cdn.datatables.net/1.12.1/js/dataTables.bootstrap5.min.js"></script>
  <py-env>
    - matplotlib
  </py-env>
  <style>
    p, table {
      font-size: 14px;
    }
    p.explainColumns {
      font-size: 12px;
      margin-bottom: 5px;
    }
    .btn {
      font-size: 14px;
    }
    .dataTables_wrapper {
      font-size: 12px;
    }
    a, a.page-link {
      /*color: lightskyblue;*/
      color:#069;
      text-decoration:none;
    }
    a:hover, a.page-link:hover {
        color:#d13108;
        font-weight: bold;
    }
    .pagination .page-item.active .page-link { 
      background-color: #069;
      border-color: #069; 
    }
    div.dataTables_wrapper div.dataTables_paginate ul.pagination .page-item.active .page-link:focus {
      background-color: #069;
      border-color: #069;
    }
    .pagination .page-item.active .page-link:hover {
    background-color: #d13108;
    border-color: #d13108;
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
      background-color: #ccc;
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
      background-color: #2196F3;
    }
    input:focus + .slider {
      box-shadow: 0 0 1px #2196F3;
    }
    input:checked + .slider:before {
      -webkit-transform: translateX(18px);
      -ms-transform: translateX(18px);
      transform: translateX(18px);
    }
  </style>
</head>
<body style="background-color:#F8F8F8;">
  <header style="background-color:rgb(33, 37, 41)">
    <div class="container-md p-2.5 bg-dark text-white">
      <h1>ScratchBook &#128221;&#127926;</h1>
      <p style="color: white; font-size: 16px;">A platform for browsing, composing and visualizing scratches in <a href="https://www.ttm-dj.com/" target='_blank' id="TTMLink">TTM-like notation.</a></p>
      <style> #TTMLink, #TTMLink.page-link{color:lightskyblue; text-decoration:none;}  #TTMLink:hover {color:#d13108; font-weight: bold;}</style>
      <!-- <p>Based on a library of scratches currently including over &#128171; 60K scratches &#128194;</p> -->
      <p style="color: #d13108"><span style="font-size: 18px">&#9888;</span> Loading the page can be a little slow at the moment. Please be patient until you see the graph &#128591;</p>
    </div>
  </header>
  <br/>
  <div class="container-md pt-3 border rounded" style="background-color: white">
    <div class="panel-group" id="Visualizer">
      <div class="panel panel-default">
        <div class="panel-heading"><h4>Visualizer</h4></div>
        <div class="panel-body">
          <p>Type and visualize your scratch formula...</p>
          <input class="form-control" type="text" id="scratch" style="font-size: 14px;" value="autobahn + prizm + (slice / 0.25) * 4" placeholder="Type formula and press ENTER"/>
          <button id="scratch-button" type="submit" pys-onClick="plot"></button>
          <script>
            var input = document.getElementById("scratch");
            input.addEventListener("keypress", function(event) {
              if (event.key === "Enter") {
                event.preventDefault();
                document.getElementById("scratch-button").click();
              }
            });
          </script>
          <div id="session-output" style="padding-bottom: 10px;"></div>
        </div>
      </div>
    </div>
  </div>
  <br/>
  <div class="container-md pt-3 border rounded" style="background-color: white">
    <div class="panel-group" id="Rules">
      <div class="panel panel-default">
        <div class="panel-heading"><h4>Library and Logic</h4></div>
        <div class="panel-body">
          <p style="margin-bottom: 5px;">ScratchBook introduces an algebraic approach to scratch notation and provides a formal language. It's alphabet consists of <strong>scratches</strong> and <strong>operators</strong>, which can be combined into complex <strong>scratch formulas</strong>.</p>
          <p>Open the cards to learn more...</p>
        </div>
        <div class="card" style="margin-bottom: 10px;">
          <div class="card-header">
            <a class="btn" data-bs-toggle="collapse" href="#collapse1" style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">Scratches</a>
          </div>
          <div id="collapse1" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <!-- <p>The following table lists and classifies all available scratches. The meaning of the columns is explained below.</p> -->
              <!-- <br/> -->
              <p>Toggle columns: 
                <!-- <a class="toggle-vis" data-column="0">Name</a> -  -->
                <a class="toggle-vis" data-column="1">Tutorial</a> -
                <a class="toggle-vis" data-column="2">#Sounds</a> - 
                <a class="toggle-vis" data-column="3">#Pauses</a> -
                <a class="toggle-vis" data-column="4">CurveType</a> -
                <a class="toggle-vis" data-column="5">ClickType</a> -
                <a class="toggle-vis" data-column="6">IsOrbit</a> - 
                <a class="toggle-vis" data-column="7">OrbitType1</a> - 
                <a class="toggle-vis" data-column="8">OrbitType2</a> -
                <a class="toggle-vis" data-column="9">IsElement</a> - 
                <a class="toggle-vis" data-column="10">#Elements</a> - 
                <a class="toggle-vis" data-column="11">Formula</a>
                <!-- <a class="toggle-vis" data-column="12">Library</a>  -->
              </p>
              <table class="table" id="scratch-table" style="font-size: 12px"></table>
              <script type="text/javascript">
                $(document).ready(function () {
                  var table = $('#scratch-table').DataTable({
                    ajax: "https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_popular.json",
                    columns: [
                      { data: "Name", title: "Name", }, 
                      { data: "Tutorial", title: "Tutorial", }, 
                      { data: "#Sounds", title: "#Sounds", }, 
                      { data: "#Pauses", title: "#Pauses", }, 
                      { data: "CurveType", title: "CurveType", }, 
                      { data: "ClickType", title: "ClickType", }, 
                      { data: "IsOrbit", title: "IsOrbit", }, 
                      { data: "OrbitType1", title: "OrbitType1", }, 
                      { data: "OrbitType2", title: "OrbitType2", }, 
                      { data: "IsElement", title: "IsElement", }, 
                      { data: "#Elements", title: "#Elements", }, 
                      { data: "Formula", title: "Formula", }, 
                      { data: "Library", title: "Library", }, 
                    ],
                    // pageLength: 10,
                    order: [
                      [ 0, "asc" ], 
                    ],
                    columnDefs: [
                      // {target: 0, visible: false, searchable: false,}, // Name
                      // {target: 1, visible: false, searchable: false,}, // Tutorial
                      // {target: 2, visible: false, searchable: false,}, // #Sounds
                      // {target: 3, visible: false, searchable: false,}, // #Pauses
                      {target: 4, visible: false, searchable: false,}, // CurveType
                      {target: 5, visible: false, searchable: false,}, // ClickType
                      {target: 6, visible: false, searchable: false,}, // IsOrbit
                      {target: 7, visible: false, searchable: false,}, // OrbitType1
                      {target: 8, visible: false, searchable: false,}, // OrbitType2
                      {target: 9, visible: false, searchable: false,}, // IsElement
                      {target: 10, visible: false, searchable: false,}, // #Elements
                      {target: 11, visible: false, searchable: false,}, // Formula
                      {target: 12, visible: false, searchable: true,}, // Library
                    ],                 
                  });
                  $('.dataTables_length').each(function () {

                    $(this).append('<label style="margin-left: 50px;">All info</label>');
                    $(this).append('<label class="switch" style="margin-left: 5px;"><input id="all_info" type="checkbox"></input><span class="slider"></span></label>');

                    $(this).append('<label style="margin-left: 50px;">All scratches</label>');
                    $(this).append('<label class="switch" style="margin-left: 5px;"><input id="all_scratches" type="checkbox"></input><span class="slider"></span></label>');

                  });
                  $('a.toggle-vis').on('click', function (e) {
                    e.preventDefault();
                    var column = table.column($(this).attr('data-column')); // Get the column API object
                    column.visible(!column.visible(), false); // Toggle the visibility
                    column.searchable(!column.searchable()); // Toggle the visibility
                  });
                  var first_switch = true
                  $("#all_scratches").change(function() {
                    if(this.checked && first_switch === true) {
                      first_switch = false; // first switch has now ocurred :)
                      $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_elements.json', function(json) {
                        table.rows.add(json.data).draw(false);
                      });
                      $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_tears.json', function(json) {
                        table.rows.add(json.data).draw(false);
                      });
                      // $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/datatable_orbits.json', function(json) {
                      //   table.rows.add(json.data).draw(false);
                      // });
                    };
                    if(this.checked === false) {
                      $.fn.dataTable.ext.search.push(
                         function(settings, data, dataIndex) {
                          return data[12] == "popular";
                         }
                      );
                      table.draw();
                    };
                    if(this.checked && first_switch === false) {
                      $.fn.dataTable.ext.search.pop();
                      table.draw();
                    };
                  });

                  $('#all_info').change(function() {
                    var cols = [4,5,6,7,8,9,10,11,] // exclude: 13 (Library)
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
              <br/>
              <!-- <p style="font-size: 16px; margin-bottom: 5px;"><strong>Explanation of columns</strong></p>
              <p class="explainColumns"><strong>Name:</strong> The name of a scratch.</p>
              <p class="explainColumns"><strong>CodeName:</strong> The code name(s) that can be used in scratch formulas. Multiple code names are seperated by a comma and can be used synonymously.</p>
              <p class="explainColumns"><strong>#Counts:</strong> The length of a scratch in quarter notes. This attribute can be altered using the "/" operator (as explained in the operator section).</p>
              <p class="explainColumns"><strong>#Sounds:</strong> The number of distinct sounds a scratch produces.</p>
              <p class="explainColumns"><strong>#Pauses:</strong> The umber of pauses in a scratch. Pauses can occur either when the fader is closed (as in flares) or when the record is held still (as in tears).</p>
              <p class="explainColumns"><strong>Orbit:</strong> Any scratch that incorporates both a forward and backward movement, or vice versa, of the record in sequence (narrow definition of orbits), plus any scratch that is "loopable", i.e. whose start and end points on the record are the same (which includes scratches like the "autobahn" or the "prizm").</p>
              <p class="explainColumns"><strong>Composition:</strong> If a scratch is composed of other scratches its formula is shown in this column. Otherwise its flagged as an element.</p> -->
            </div>
          </div>
        </div>
        <div class="card" style="margin-bottom: 10px;">
          <div class="card-header">
            <a class="btn" data-bs-toggle="collapse" href="#collapse2" style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">Operators</a>
          </div>
          <div id="collapse2" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <p>Operators can be used to modify and combine scratches. The following table lists and explains all available operators.
              </p>
              <script>
                $(document).ready(function () {
                  $('#OperatorTable').DataTable();
                    order: [[0, 'asc']],
                });
              </script> 
              <table class="table" id="OperatorTable" style="font-size: 12px">
                <thead>
                  <tr>
                      <th>ID</th>
                      <th>Operator</th>
                      <th>Purpose</th>
                      <th>Grammar</th>
                      <th>Example</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                      <th>1</th>
                      <td>~</td>
                      <td>"Reverse" or "backwards" scratching (Flip a scratch on the y-axis)</td>
                      <td>~scratch</td>
                      <td>~autobahn</td>
                  </tr>
                  <tr>
                      <th>2</th>
                      <td>-</td>
                      <td>"Mirror" scratching (Flip a scratch on the x-axis)</td>
                      <td>-scratch</td>
                      <td>-autobahn</td>
                  </tr>
                  <tr>
                      <th>3</th>
                      <td>*</td>
                      <td>Repeat a scratch <em>n</em> times (<em>n</em> must be an integer number)</td>
                      <td>scratch * <em>n</em></td>
                      <td>chirp * 4</td>
                  </tr>
                  <tr>
                      <th>4</th>
                      <td>+</td>
                      <td>Chain scratches from left to right</td>
                      <td>scratch + scratch</td>
                      <td>chirp + flob2 + steps</td>
                  </tr>
                  <tr>
                      <th>5</th>
                      <td>/</td>
                      <td>Set the length <em>n</em> of a scratch in 1/4 notes (aka beats)</td>
                      <td>scratch / <em>n</em></td>
                      <td>baby / 2</td>
                  </tr>
                  <tr>
                      <th>6</th>
                      <td>//</td>
                      <td>Decide how much of sample is used (<em>n</em> must be between 0 and 1)</td>
                      <td>scratch // <em>n</em></td>
                      <td>swingflare // 0.2</td>
                  </tr>
                  <tr>
                      <th>7</th>
                      <td>**</td>
                      <td>Move a scratch or expression up on the Y-axis. Typically used in connection with the "//" Operator". Use brackets wisely! For example, "chirp // 0.5 ** 0.5" is not the same as "(chirp // 0.5) ** 0.5".</td>
                      <td>expression ** <em>n</em></td>
                      <td>(chirp // 0.5) ** 0.5</td>
                  </tr>
                  <tr>
                      <th>8</th>
                      <td>%</td>
                      <td>Shift the "phase" of a scratch by rotating its parts from right to left. (<em>n</em> must be an integer number)</td>
                      <td>scratch % <em>n</em></td>
                      <td>prizm % 0.25</td>
                  </tr>
                  <tr>
                      <th>9</th>
                      <td>[<em>n</em>]</td>
                      <td>Show the <em>n</em>-ths part of a composed scratch (<em>n</em> must be an integer number. <span style="color: #d13108">&#9888;</span> Counting starts at 0 not at 1!)</td>
                      <td>scratch[<em>n</em>]</td>
                      <td>autobahn[3]</td>
                  </tr>
                  <tr>
                      <th>10</th>
                      <td>[<em>n</em>:<em>m</em>]</td>
                      <td>Show all parts between the <em>n</em>-ths (included) and <em>m</em>-ths (excluded) part of a composed scratch (<em>n</em> and <em>m</em> must be integer numbers. <span style="color: #d13108">&#9888;</span> Counting starts at 0 not at 1!)</td>
                      <td>scratch[<em>n</em>:<em>m</em>]</td>
                      <td>autobahn[3:7]</td>
                  </tr>
                  <tr>
                      <th>11</th>
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
        <div class="card" style="width: auto">
          <div class="card-header">
            <a class="btn" data-bs-toggle="collapse" href="#collapse3" style="width: 100%; text-align: left; font-size: 18px; font-weight: 500;">More Info</a>
          </div>
          <div id="collapse3" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <p>Will follow soon...</p>
              <!-- <p>Each scratch has a unique name, which signifies its specific composition. On the most basic level there are <strong>6 types of scratches</strong>: <em>baby</em> ("b"), <em>ghost</em> ("g"), <em>transformer</em> ("tr"), <em>flare</em> ("f"), <em>tear</em> ("t"), and <em>click-tear</em> ("ct"), as well as <strong>three types of curves</strong>: <em>s-curve</em> (no special signification), <em>exponential</em> ("Ex"), <em>logarithmic</em> ("Log"). Currently, <strong>tears can have up to 3 steps</strong> ("t1", "t2", "t3"), <strong>flares and click-tears can have up to 3 Clicks</strong> ("f1", "f2", "f3", "ct1", "ct2", "ct3"), and <strong>transformers can have up to 4 clicks</strong> ("tr1", "tr2", "tr3", "tr4"). Transformers and flares also come in up to <strong>three clicking variants</strong>: <em>diminished</em> ("D"), <em>augmented</em> ("A"), and <em>stretched</em> ("S"), depending on the number of their clicks. In total, this currently adds up to <strong>31 elementary scratches or "elements"</strong>.</p>
              <p>The next layer of complexity is achieved by combining these elements into all possible combinations of <strong>orbits</strong>, i.e. scratches that incorporate both a forward and backward movement (each being one of the elements), or vice versa, of the record in sequence. Orbits are signified using one element on each side, joined by an underscore (e.g. "f1_f1" or "tr3A_bEx"). Independent of the elements used, <strong>five types of orbits</strong> are currently available: <em>normal (no special signification), right-skewed at 1/4 ("_R4"), right-skewed at 1/3 ("_R3"), left-skewed at 1/3 ("_L3"), and left-skewed at 1/4 ("_L4")</em>.</p>
              <p>A number of <strong>special scratches</strong>, such as "autobahn" or "prizm", are composed of more than two elements and therefore carry special names and abbreviations.</p> -->
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
        <!-- Google -->
        <!-- <a class="btn btn-outline-light btn-floating m-1" href="https://scholar.google.de/citations?user=NhCwiDwAAAAJ&hl=en" target='_blank' role="button"
          ><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-google" viewBox="0 0 16 16"><path d="M15.545 6.558a9.42 9.42 0 0 1 .139 1.626c0 2.434-.87 4.492-2.384 5.885h.002C11.978 15.292 10.158 16 8 16A8 8 0 1 1 8 0a7.689 7.689 0 0 1 5.352 2.082l-2.284 2.284A4.347 4.347 0 0 0 8 3.166c-2.087 0-3.86 1.408-4.492 3.304a4.792 4.792 0 0 0 0 3.063h.003c.635 1.893 2.405 3.301 4.492 3.301 1.078 0 2.004-.276 2.722-.764h-.003a3.702 3.702 0 0 0 1.599-2.431H8v-3.08h7.545z"/></svg></a> -->
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
        <p>The algebra of scratching and the tools used here for visualizing TTM-like scratch notation have been developed by Arno Simons, a Berlin-based turntablist and researcher.</p>
        <p>The underlying python code can be downloaded <a href="https://github.com/arnosimons/scratchbook" target='_blank'>here</a>.</p>
      </section>
    </div>
    <div class="text-center p-3" style="background-color: rgba(0, 0, 0, 0.2);">
      © 2022 Copyright:
      <a class="text-white" href="https://arnosimons.github.io/" target='_blank'>Arno Simons</a>
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
  req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/codebook_complete.json", False)
  req.send()
  exec(f"codebook = {req.response}")
  def getCodeNames(text):
      if "Scratch" in text:
          return
      text = re.sub(r"[-+*/%~\[\]\(\).:]|yshift|ys", " ", text)
      for code_name in re.sub(r"\b\d*\b", " ", text).split():
          if not code_name in codebook:
              message = f'Sorry, but "{code_name}" is not in the codebook. Browse the library to see what scratches are available!'
              pyscript.write("session-output", message)
              raise ValueError(message)
          try:
              exec(code_name)
          except NameError:
              yield code_name
              for i in getCodeNames(codebook[code_name]):
                  yield i
  def plot(x=None):
      text = Element('scratch').element.value
      for code_name in list(getCodeNames(text))[::-1]:
          exec(f"{code_name} = {codebook[code_name]}")
      try:
          session = Session(eval(text), fontsize=11, w_pad=2)
          pyscript.write("session-output", session.fig)
      except Exception as e:
          pyscript.write("session-output", str(e))  
  for code_name in ["i", "o", "slice"]: # workaround for handling "slice" in python's namespace... 
      exec(f"{code_name} = {codebook[code_name]}")
  plot()
</py-script>
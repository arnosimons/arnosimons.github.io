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
    - numpy
    - matplotlib
    - pandas
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
  </style>
</head>
<body style="background-color:#F8F8F8;">
  <header style="background-color:rgb(33, 37, 41)">
    <div class="container-md p-2.5 bg-dark text-white">
      <h1>ScratchBook &#128221;&#127926;</h1>
      <p style="color: white; font-size: 16px;">A platform for composing and visualizing scratches in <a href="https://www.ttm-dj.com/" target='_blank'>TTM-like notation</a></p>
    </div>
  </header>
  <br/>
  <div class="container-md pt-3 border rounded" style="background-color: white">
    <div class="panel-group" id="Visualizer">
      <div class="panel panel-default">
        <div class="panel-heading"><h4>Visualizer</h4></div>
        <div class="panel-body">
          <p>Visualize your composition</p>
          <input class="form-control" type="text" id="scratch" style="font-size: 14px;" value="autobahn" placeholder="Type scratch formula.."/>
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
          <p style="margin-bottom: 5px;">ScratchBook introduces an algebraic approach to scratch notation and provides a formal language. It's alphabet consists of <strong>scratches</strong> and <strong>operators</strong>, which can be combined into complex scratch formulas.</p>
          <p>Open the cards to learn more...</p>
        </div>
        <div class="card" style="margin-bottom: 10px;">
          <div class="card-header">
            <a class="btn" data-bs-toggle="collapse" href="#collapse1" style="font-size: 18px; font-weight: 500;">Scratches</a>
          </div>
          <div id="collapse1" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <p>The following table lists and classifies all available scratches.</p> 
              <p>Each scratch has a unique name, which signifies its specific composition. On the most basic level there are <strong>6 types of scratches:</strong> baby ("b"), ghost ("g"), transformer ("tr"), flare ("f"), tear ("t"), click-tear ("ct"). Each type can be expressed in <strong>three types of curves (s-curve, exponential="Ex", logarithmic="Log")</strong>. Currently, tears can have up to 3 steps ("t1", "t2", "t3"), flares and click-tears can have up to 3 Clicks ("f1", "f2", "f3", "ct1", "ct2", "ct3"), and transformers can have up to 4 clicks ("tr1", "tr2", "tr3", "tr4"). Transformers and flares also come in up to <strong>three clicking variants (diminished="D", augmented="A", stretched="S")</strong> depending on the number of their clicks. In otal this currently makes 31 <strong>elementary scratches</strong>.</p>
              <p>The next layer of complexity is achieved by combining these elementary scratches into all possible combinations of <strong>orbits</strong>, i.e. scratches that incorporates both a forward and backward movement (each being one of the elements), or vice versa, of the record in sequence. Independent of the elements used, <strong>five types of orbits (normal, right-skewed at 1/3, right-skewed at 1/4, left-skewed at 1/3, left-skewed at 1/4, right-skewed)</strong> are currently available</p>
              <table class="table" id="scratch-table" style="font-size: 12px"></table>
              <script type="text/javascript">
                $.getJSON('https://raw.githubusercontent.com/arnosimons/scratchbook/main/library_of_scratches.json', function(json) {
                $('#scratch-table').DataTable({
                   data : json.data,
                   columns : json.columns,
                   order: [[ 8, "asc" ], [ 0, "asc" ]],
                   // pageLength: 10,
                })
              });
              </script>
              <br/>
              <p style="font-size: 16px; margin-bottom: 5px;"><strong>Explanation of columns</strong></p>
              <p class="explainColumns"><strong>Name:</strong> The name of a scratch.</p>
              <p class="explainColumns"><strong>CodeName:</strong> Each scratch has at least one code word that can be used in scratch formulas. Multiple code words are seperated by a comma and can be used synonymously. If a scratch is composed of other scratches its formula is shown in the composition column.</p>
              <p class="explainColumns"><strong>#Counts:</strong> The length of a scratch in beats (aka quarter notes). This attribute can be altered using the "/" operator (as explained in the operator section).</p>
              <p class="explainColumns"><strong>#Sounds:</strong> Number of distinct sounds a scratch produces.</p>
              <p class="explainColumns"><strong>#Pauses:</strong> Number of pauses in a scratch. Pauses can occur either when the fader is closed (e.g. in "flares") or when the record is held still (e.g. in "tears").</p>
              <p class="explainColumns"><strong>Orbit:</strong> Narrowly defined, an orbit is any scratch that incorporates both a forward and backward movement, or vice versa, of the record in sequence. In this table, an orbit is broadly defined as any scratch that is "loopable", i.e. whose start and end points on the record are the same. Consequently, scratches like the "autobahn" or the "prizm" are also listed as orbits here.</p>
              <p class="explainColumns">&#10024; Note that all narrowly defined orbits can be accessed via code words in the generic form of "forward_backward" (e.g. "fl2_fl1", "tr3_ct2", etc.)</p>
              <p class="explainColumns"><strong>Composition:</strong> If a scratch is composed of other scratches its formula is shown in the composition column.</p>
            </div>
          </div>
        </div>
        <!-- <br/> -->
        <div class="card" style="width: auto">
          <div class="card-header">
            <a class="btn" data-bs-toggle="collapse" href="#collapse2" style="font-size: 18px; font-weight: 500;">Operators</a>
          </div>
          <div id="collapse2" class="collapse in">
            <div class="card-body" style="overflow-x:auto;">
              <p>Operators can be used to modify and combine scratches. The following table lists and explains all available operators.
              </p>
              <script>
                $(document).ready(function () {
                  $('#OperatorTable').DataTable();
                });
              </script> 
              <table class="table" id="OperatorTable" style="font-size: 12px">
                <thead>
                  <tr>
                      <th>Operator</th>
                      <th>Purpose</th>
                      <th>Example</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                      <td>+</td>
                      <td>Chain scratches from left to right</td>
                      <td>chirp + flob2 + steps</td>
                  </tr>
                  <tr>
                      <td>*</td>
                      <td>Repeat a scratch <em>n</em> times</td>
                      <td>chirp * 4</td>
                  </tr>
                  <tr>
                      <td>/</td>
                      <td>Set the length of a scratch in beats (aka quarter notes)</td>
                      <td>baby / 2</td>
                  </tr>
                  <tr>
                      <td>//</td>
                      <td>Decide how much of sample is used (between 0 and 1)</td>
                      <td>swingflare // 0.2</td>
                  </tr>
                  <tr>
                      <td>~</td>
                      <td>"Reverse" scratching (Flip a scratch on the y-axis)</td>
                      <td>~autobahn</td>
                  </tr>
                  <tr>
                      <td>-</td>
                      <td>"Backwards" scratching (Flip a scratch on the x-axis)</td>
                      <td>-autobahn</td>
                  </tr>
                  
                  <tr>
                      <td>%</td>
                      <td>Shift the "phase" of a scratch</td>
                      <td>prizm % 0.25</td>
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
  from js import XMLHttpRequest
  req = XMLHttpRequest.new()
  req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/classes.py", False)
  req.send()
  exec(str(req.response))
  req = XMLHttpRequest.new()
  req.open("GET", "https://raw.githubusercontent.com/arnosimons/scratchbook/main/library_of_scratches.py", False)
  req.send()
  exec(str(req.response))
  for name, row in df.iterrows():
      if not row.Composition == ' is element':
          exec(f"{' = '.join(row['CodeName'].split(', '))} = {row.Composition}")
  def plot(x=None):
      text = Element('scratch').element.value
      pyscript.write("session-output", Session(eval(text)).fig)
  plot()
</py-script>
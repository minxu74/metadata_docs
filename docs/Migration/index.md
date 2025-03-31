---
hide:
 - navigation
title: Migration Status
---

## Progress

=== "ESGF 1.5 Index Status"

<div id="table1"></div>


<!--
=== "Read-Only Projects Status (to the public Globus Index)"

<div id="table3"></div>

-->


### Datasets

!!! info "Read-only Projects"

=== "CMIP3"
    <div id="tab_cmip3_datasets"></div>


=== "CMIP5"
    <div id="tab_cmip5_datasets"></div>

=== "CMIP6"
    <div id="tab_cmip6_datasets"></div>

=== "CREATE-IP" 
    <div id="tab_create-ip_datasets"></div>

=== "e3sm-supplement" 
    <div id="tab_e3sm-supplement_datasets"></div>


=== "GeoMIP" 
    <div id="tab_geomip_datasets"></div>

=== "LUCID"
    <div id="tab_lucid_datasets"></div>

=== "TAMIP"
    <div id="tab_tamip_datasets"></div>



<hr>
!!! info "Read-Write Projects"

=== "CMIP6Plus"
    <div id="tab_cmip6plus_datasets"></div>

=== "DRCDP"
    <div id="tab_drcdp_datasets"></div>

=== "E3SM" 
    <div id="tab_e3sm_datasets"></div>

=== "input4MIPs" 
    <div id="tab_input4mips_datasets"></div>

=== "obs4MIPs"
    <div id="tab_obs4mips_datasets"></div>

### Files

!!! info "Read-only Projects"

=== "CMIP3"
    <div id="tab_cmip3_files"></div>


=== "CMIP5"
    <div id="tab_cmip5_files"></div>

=== "CMIP6"
    <div id="tab_cmip6_files"></div>

=== "CREATE-IP"
    <div id="tab_create-ip_files"></div>

=== "e3sm-supplement"
    <div id="tab_e3sm-supplement_files"></div>


=== "GeoMIP"
    <div id="tab_geomip_files"></div>

=== "LUCID"
    <div id="tab_lucid_files"></div>


=== "TAMIP"
    <div id="tab_tamip_files"></div>


<hr>
!!! info "Read-Write Projects"

=== "CMIP6Plus"
    <div id="tab_cmip6plus_files"></div>

=== "DRCDP"
    <div id="tab_drcdp_files"></div>

=== "E3SM" 
    <div id="tab_e3sm_files"></div>

=== "input4MIPs" 
    <div id="tab_input4mips_files"></div>

=== "obs4MIPs"
    <div id="tab_obs4mips_files"></div>

<script>
  // Sample data
  document.addEventListener("DOMContentLoaded", function() {
    var tableData = [
      { id: 1, name: "Alice", age: 30, city: "New York" },
      { id: 2, name: "Bob", age: 25, city: "Los Angeles" },
      { id: 3, name: "Charlie", age: 35, city: "Chicago" }
    ];

    // Initialize Tabulator
    var table = new Tabulator("#table2", {
      data: tableData, // Load data into the table
      layout: "fitColumns", // Fit columns to width of table
      columns: [ // Define table columns
        { title: "ID", field: "id", width: 50 },
        { title: "Name", field: "name", width: 150 },
        { title: "Age", field: "age", width: 100 },
        { title: "City", field: "city", width: 150 }
      ]
    });
    // Fetch JSON data
    fetch('./jsons/index.json')
      .then(response => response.json())
      .then(data => {
        // Initialize Tabulator with the fetched data

        data.forEach(d => {
          d["used"] = parseFloat(d["size_in_mb"]) / parseFloat(d["max_size_in_mb"]) * 100.
        });
        
        var table = new Tabulator("#table1", {
          data: data, // Load data into the table
          layout: "fitDataTable", // Fit columns to width of table
          columns: [ // Define table columns
            { title: "Name", field: "display_name" },
            { title: "Index", field: "id", width: 300 },
            { title: "Size (MB)", field: "size_in_mb", width: 100 },
            { title: "Subjects", field: "num_subjects", width: 150 },
            { title: "Entries", field: "num_entries", width: 150 },
            { title: "Used (%)", field: "used", width: 150, hozAlign:"left", formatter:"progress",
              formatterParams:{
                  min:0,
                  max:100,
                  color:["green", "orange", "red"],
                  legend: function(value){return parseFloat(value).toFixed(1) + "%"},
                  legendColor:"inherit",
                  legendAlign:"center",
              }
            }
          ]
        });
      })
      .catch(error => console.error('Error loading JSON data:', error));

    // table3
    fetch('./jsons/project_readonly.json')
      .then(response => response.json())
      .then(data => {
        var table = new Tabulator("#table3", {
          data: data, // Load data into the table
          layout: "fitDataTable", // Fit columns to width of table
          columns: [ // Define table columns

            { title: "Solr Index Name", field: "index_name" },
            { title: "CMIP3", field: "CMIP3", formatter:"textarea" },
            { title: "CMIP5", field: "CMIP5", formatter:"json" },
            { title: "CMIP6", field: "CMIP6", formatter:"json" },
            { title: "CREATE-IP", field: "CREATE-IP", formatter:"json" },
            { title: "e3sm-supplement", field: "e3sm-supplement", formatter:"json" },
            { title: "GeoMIP", field: "GeoMIP", formatter:"json" },
            { title: "LUCID", field: "LUCID", formatter:"json" },
            { title: "TAMIP", field: "TAMIP", formatter:"json" },

          ]
        });
      })

    // cmip3 tab

    const metas = ["datasets", "files"];
    const projs = ["cmip3", "cmip5", "cmip6", "create-ip", "e3sm-supplement", "geomip", "lucid", "tamip",
     "cmip6plus", "e3sm", "drcdp", "input4mips", "obs4mips"];

   
    metas.forEach(meta => { 
    projs.forEach(proj => {
    fetch("./jsons/" + proj + "_" + meta + "_summary.json")
      .then(response => response.json())
      .then(data => {
        var table = new Tabulator("#tab_" + proj + "_" + meta, {
          layout:"fitDataTable",
          columnDefaults:{
            resizable:false,
          },
          data: data,
          columns:[
              {title:"Solr Index -> Public Index", field:"index_name", formatter:"textarea", vertAlign:"middle", sorter:"string"},
          ],

          rowFormatter:function(row){
              var element = row.getElement(),
              data = row.getData(),
              width = element.offsetWidth,
              rowTable, cellContents;

              //clear current row data
              while(element.firstChild) element.removeChild(element.firstChild);

              //define a table layout structure and set width of row
              rowTable = document.createElement("table")
              rowTable.style.width = (width - 18) + "px";
              rowTable.style.width = "800px";

              rowTabletr = document.createElement("tr");

              //add image on left of row
              cellContents = "<td text-align: middle;><div>" +  data.index_name + "</div></td>";

              if ((parseInt(data["page ingested"]) - parseInt(data["page skipped"]))  == parseInt(data["page checked"])) {
                  var ingest_success = "<span style='color:green;font-weight:bold;'>" + parseInt(data["page checked"]) + "</span>";
              }
              else {
                  var ingest_success = "<span style='color:red; font-weight:bold;'>" + parseInt(data["page checked"]) + "</span>";
              }

              if (parseInt(data["record total"]) == data.numFound_last) {
                  var total_record = "<span style='color:blue;font-weight:bold;'>" + parseInt(data["record total"]) + "</span>";

              }
              else {
                  var total_record = "<span style='color:brown;font-weight:bold;'>" + parseInt(data["record total"]) + "</span>";

              }

              if (data.numFound_first != data.numFound_last) {
                  var numfound_first = "<span style='color:red; font-weight:bold; text-decoration: underline;'>" + parseInt(data.numFound_first) + "</span>";
              }
              else
              {
                  var numfound_first = "<span style='color:darkmagenta; font-weight:bold;'>" + parseInt(data.numFound_first) + "</span>";
              }

              //add row data on right hand side
              cellContents += "<td>" + 
                            "<div><strong>Start & End time:</strong> " + data["start time"].slice(0, -7) + '--' + data["stop time"].slice(0,-7)  + 
                      "</div><div><strong>Query String:</strong> " + data["query string"] + 
                      "</div><div><strong>numFound at first:</strong> " + numfound_first + 
                      "</div><div><strong>numFound at last:</strong> " + data.numFound_last + 
                      "</div><div><strong>Page Queried:</strong> " + parseInt(data["page queried"]) + 
                      "</div><div><strong>Page Ingested:</strong> " + parseInt(data["page ingested"]) + " (skiped: " + parseInt(data["page skipped"]) + ")" +  
                      "</div><div><strong>Page Succeeded:</strong> " + ingest_success + 
                      "</div><div><strong>Record Skipped</strong> " + parseInt(data["record skipped"]) + 
                      "</div><div><strong>Record Total</strong> " + total_record + 
                      "</div><div><strong>Command line:</strong> " + data.cmd_line + 
                      "</div><div><strong>Hostname:</strong> " + data.hostname + 
                      "</div><div><strong>Error message:</strong> " + data.error + 
                      "</div><div><strong>Restart message:</strong> " + data.restart + 
                      "</div></td>"

              rowTabletr.innerHTML = cellContents;

              rowTable.appendChild(rowTabletr);

              //append newly formatted contents to the row
              element.append(rowTable);
          },

        });
      });  // data
    }); // proj loop
    }); // meta loop

  });


</script>

<!--
{%
  include "chart1.md"
%}
-->

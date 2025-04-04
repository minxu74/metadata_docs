---
hide:
  - navigation
title: Validation and Verification
---

# Project level

## Sankey Diagram

Datasets:

{%
   include "Migration/jsons/sankey_project_datasets.md"
%}

Files:
{%
   include "Migration/jsons/sankey_project_files.md"
%}

## Contributions of three Solr index to the public index for each project
{%
  include "Migration/jsons/chart_project.md"
%}

## Tables of counts of documents in the Solr and public indexes

!!! tip "Caption"
    - `numFound`: the total number of documents from a Solr query
    - `Total records`: the total number of documents to be ingested from the database files
    - `skipped records`: the number of documents skipped (see Notes)
    - `Ingested`: the number of documents to be ingested successfully. Generally it equals to the `Total records-skipped records-failed ingested` 
    - `Entries`: the number of documents in the public index using the globus query
{%
  include "Migration/jsons/table_project.md"
%}

# institution_id level

# source_id level

<script>

    const isDarkMode = window.matchMedia('(prefers-color-scheme: dark)').matches;
    const isLightMode = window.matchMedia('(prefers-color-scheme: light)').matches;

    var nodeList;
    var k = 0;
    const observer = new MutationObserver(function(mutations, observer) {

        console.log('xxxx', k, isDarkMode, isLightMode);
        if (document.querySelectorAll('.node-labels').length > 0) {
            styleNodeLabels();
            //nodeList.push(document.querySelectorAll('.node-labels'));
            k = k + 1;

            if (k>=2) {
                observer.disconnect();  // Stop observing after first run
            }
        }
    });

    observer.observe(document.body, {
        childList: true,
        subtree: true
    });


    // Create media query listener
    const colorSchemeQuery = window.matchMedia('(prefers-color-scheme: dark)');
    
    // Handler function
    function handleColorSchemeChange(e) {

        console.log('xxxx');
        if (e.matches) {
            console.log('Dark mode activated');

            console.log(nodeList);
            nodeList.forEach( node => {
                 console.log(node);
                 node[0].style.fill = '#FF5733';
            });



        } else {
            console.log('Light mode activated');
        }
    }
    
    // Add event listener
    colorSchemeQuery.addListener(handleColorSchemeChange);
    
    // Initial check
    handleColorSchemeChange(colorSchemeQuery);


    
    // Function to style node labels
    function styleNodeLabels() {
        const nodeLabels = document.querySelectorAll('.node-labels');
        nodeLabels[0].style.fill = "#FF0099";

    }

    document.querySelectorAll('.mermaid .pieChart .slice').forEach((slice, index) => {
        const colors = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#FFA07A', '#98D8C8'];
        slice.style.fill = colors[index % colors.length];
        slice.style.stroke = colors[index % colors.length];
    });


</script>

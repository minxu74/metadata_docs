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

    var k = 0;
    const observer = new MutationObserver(function(mutations, observer) {
        if (document.querySelectorAll('.node-labels').length > 0 ) {

            styleNodeLabels();
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

    // Function to style node labels
    function styleNodeLabels() {
        const nodeLabels = document.querySelectorAll('.node-labels');
        nodeLabels[0].style.fill = "#FF0099";

    }
</script>

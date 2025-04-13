---
hide:
  - toc
title: Validation and Verification
---

## Sankey Diagram

Datasets:

{%
   include "Migration/jsons/sankey_project_datasets.md"
%}

Files:
{%
   include "Migration/jsons/sankey_project_files.md"
%}



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

    function styleNodeLabels() {
        const nodeLabels = document.querySelectorAll('.node-labels');
        nodeLabels[0].style.fill = "#FF0099";

    };
</script>

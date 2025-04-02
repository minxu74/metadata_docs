---
  title: Notes
---

1. The Solr query in the migration uses the cursor query method, and the `cursorMark` from the cursor query is recorded in a migration database and is used for restart purposes.
2. The cursor query needs special permissions to the Solr indexes, i.e., the IP address of the machine in which the cursor query is made needs to be included in the white-lists of the indexes.
3. There are `project=cmip6` and `project=CMIP6`, `project=e3sm` and `project=E3SM`. It found that lower case `cmip6` and upper case `E3SM` were used by the retracted documents, so only the `CMIP6` and `e3sm` were migrated to the Globus indexes.
4. Generally, the size of 500 documents for the CMIP projects are much less than the maximum size (10 MB) for ingestion. However, for `project=e3sm` and `project=e3sm-supplement`, 
the size of **500** documents are larger than 10 MB, so we use `rows=100` in the migration of `e3sm` and `e3sm-supplement` projects, and **1500** for other projects.
5. Changes to the Solr document:
    - change the value of the `index_node` to __us_index__
    - remove the url item if the type of document is `Datsets`
6. Filters during the migration:
    - filter out all metadata at the ORNL index if the value of `data_node` does not include `anl.gov` and `llnl.gov` and does not equal `esgf-node.ornl.gov`
    - filter out all metadata at the LLNL index when the `source_id=E3SM-2-1`
7. The metadata of `project=e3sm` at the ORNL index shall be discarded as the metadata was migrated to the ORNL index, but the real files were not. But half of these metadata have been ingested to the *E3SM* staged index.
8. The formats of the `_timestamp` strings may differ as there are two APIs to generate them during the publications (`YYYY-MM-DDThh:mm:ss.sssZ` vs. `YYYY-MM-DDThh:mm:ssZ`).
    - A legacy API for harvesting thredds catalogs and generating publication records
    - the "push" publisher API (esg-publisher)
9. The solr query used in the migration only searches the default local shard with the port 8983, there is another local shard with port 8995 is only used for GFDL CMIP6 data 
10. The other shards shown in the LLNL esg_search, they are the "replica" shards at LLNL and are the synced copies of the remote shards. However, the GFDL's remote shard is dead,
thus, the GFDL local replica shard (port: 8895) could be considered as a local shard for the migration purpose.
11. The esg search using the LLNL index is the distributed query by default, however, the distributed shards do not include the ANL and ORNL solr index. 
The esg search using the ANL or ORNL indexes only searches their local shards even when `distrib=True`.


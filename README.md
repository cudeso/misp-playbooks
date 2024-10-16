# MISP playbooks

MISP playbooks address common use-cases encountered by SOCs, CSIRTs or CTI teams to detect, react and analyse specific intelligence received by MISP.

The MISP playbooks are built with Jupyter notebooks and contain
- **Documentation** in **Markdown** format, including text and graphical elements;
- **Computer code** in the **Python** programming language, primarily with the use of PyMISP to interact with MISP and other sources for enrichment and notification.

## Documentation

This repository contains the documentation to get started with MISP playbooks.

- The [MISP playbook structure](documentation/MISP%20playbook%20structure.md) and [Jupyter notebook example](documentation/MISP%20playbook.ipynb) describe the structure of the MISP playbooks.
- The [MISP playbook guidelines](documentation/MISP%20playbook%20guidelines.md) help you with building and maintaining your playbooks.
- The [MISP playbook technical documentation](documentation/MISP%20playbook%20technical%20documentation.md) helps you with setting up your environment to run the playbooks.
- The [MISP playbook FAQ](documentation/MISP%20playbook%20FAQ.md) contains tips and tricks for using and developing playbooks.
- A guide to install [MISP playbooks on Kali Linux in Azure](documentation/MISP%20playbook%20on%20Kali.md)
- Conversion between [MISP playbooks and CACAO security playbooks](documentation/MISP_CACAO.md)

## Playbooks

The repository contains these playbooks

| Title  | Purpose  | Playbook  | Issue |
|:---|:---|:---|---|
| **Geolocate IP addresses and calculate distance** | This playbook gets the IP addresess in a MISP event (ip-src and ip-dst). It then queries for the **geolocation** of these addresses via MMDB, puts them on a map and calculates the **distance** between coordinates with the help of Geopy. The map is attached as a screenshot to the MISP event, the findings are added as a **MISP report**, stored in the playbook and sent to **Mattermost**.| [MISP Playbook](misp-playbooks/pb_geolocate_ip_and_calc_distance.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_geolocate_ip_and_calc_distance-with_output.ipynb) | [20](https://github.com/MISP/misp-playbooks/issues/20)|
| **Query Timesketch for threat intelligence and report sightings in MISP and Mattermost** | This playbook queries **Timesketch** for matches based on MISP search results (indicators). The MISP search is configured by the analyst with mandatory tags, exclusion tags, and optional attribute type filters. The resulting attributes are then used to query Timesketch. You can limit the results and save the search in Timesketch. The results are summarised in the playbook, added as sightings in MISP, and sent as a notification to Mattermost. As an extra, there's a sample Bash script for importing EVTX files (e.g., from https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES) | [MISP Playbook](misp-playbooks/pb_timesketch_search_query_sightings.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_timesketch_search_query_sightings-with_output.ipynb) | [6](https://github.com/MISP/misp-playbooks/issues/6)|
| **Create a MISP event from Microsoft Sentinel security incidents** | This playbook extracts information from Microsoft **Sentinel security incidents**, parses the associated alerts and **entities**, and extracts useful indicators. A new MISP event is created with the incident summary, and the indicators are added to the MISP event. **Sightings** are also added to the indicators. At the end of the playbook, a summary is displayed and shared via **Mattermost**. The playbook uses credentials (tokens) obtained through an Azure App. Additionally, it includes a section on uploading custom logs to Sentinel, which was used during development and can be relevant for other purposes.| [MISP Playbook](misp-playbooks/pb_event_from_sentinel_incidents.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_event_from_sentinel_incidents-with_output.ipynb) | [34](https://github.com/MISP/misp-playbooks/issues/34)|
| **JARM fingerprint investigations with Censys, Shodan and MISP** | This playbook enables the investigation of JARM fingerprints which you can then use for threat **actor infrastructure tracking**. It verifies the existence of these fingerprints in MISP events and active OSINT feeds. The playbook then queries **Censys** and **Shodan** to identify hosts with services that match the fingerprints. The results are added to a MISP event as MISP objects and event reports. At the conclusion of the playbook, a summary is displayed and shared via **Mattermost**.| [MISP Playbook](misp-playbooks/pb_jarm_verification.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_jarm_verification-with_output.ipynb) | [19](https://github.com/MISP/misp-playbooks/issues/19)|
| **Query Elasticsearch for threat intelligence and report sightings in MISP and Mattermost** | A playbook to query Elasticsearch with the results (indicators) of a MISP search. The MISP search can be filtered on attribute type and tags. Results are displayed in the playbook, **plotted** on a graph and sent to **Mattermost**. Matches in Elasticsearch are also reported as MISP **sightings**.| [MISP Playbook](misp-playbooks/pb_elasticsearch_matches_sightings.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_elasticsearch_matches_sightings-with_output.ipynb) | [5](https://github.com/MISP/misp-playbooks/issues/5)|
| **Malware triage** | A playbook to provide an analyst sufficient information to do basic malware triage on one or more samples. Samples are **attached** to a MISP event (with file object relations). VirusTotal and MalwareBazaar are used to get the **detection rate**, **threat classification** and **sandbox** information. Hashlookup is used to check for **known hashes**. PEfile analysis is done for **imports** and **exports**. The results are stored in **MISP reports** and as MISP objects where relevant. Correlations with MISP events or data feeds are added to a summary. The sample is shared with a local instance of **MWDBcore**.| [MISP Playbook](misp-playbooks/pb_malware_triage.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_malware_triage-with_output.ipynb) | [2](https://github.com/MISP/misp-playbooks/issues/2)|
| **Malware triage - dynamic malware analysis** | This playbook extends the results retrieved with **static** malware analysis in the malware triage playbook and does the **dynamic** malware analysis with one or more sandboxes. <br>This playbook uses **VMRay**, **Hybrid-Analysis** and **VirusTotal** as malware sandboxes. The results are stored in a **MISP report** and sent to Mattermost. | [MISP Playbook](misp-playbooks/pb_malware_triage_upload_sample.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_malware_triage_upload_sample-with_output.ipynb) | [3](https://github.com/MISP/misp-playbooks/issues/3)|
| **Malware triage - Query file hash** | This playbook is complementary to the playbooks for static malware analysis and dynamic malware analysis and investigates file hashes. This way you can discover with which malware a hash corresponds. It checks if the **hashes** are found on MISP warninglists, in MISP events or in MISP feeds. The playbook uses the information from **VirusTotal**, **Hashlookup** and **MalwareBazaar** to provide context information on hashes. It creates a **MISP report** for each hash and then sends a report to Mattermost. | [MISP Playbook](misp-playbooks/pb_query_hash_information.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_query_hash_information-with_output.ipynb) | [15](https://github.com/MISP/misp-playbooks/issues/15)|
| **Threat actor profiling** | Query MISP events associated with a specific threat actor. <br />Summarises the galaxies, clusters and tags from the MISP events, lists the vulnerabilities (CVE) and the actionable indicators.<br /> Optionally query the MITRE TAXII server to get a list of associated techniques and software.<br>Results are stored in the playbook and sent to Mattermost and TheHive.| [MISP Playbook](misp-playbooks/pb_threat_actor_profiling.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_threat_actor_profiling-with_output.ipynb) | [26](https://github.com/MISP/misp-playbooks/issues/26)|
| **Query CVE information** | Query MISP events for the use of specific CVEs. List these events with their context (galaxies, focus on MITRE ATT&CK).<br>Query public sources (CVE search, vulners, XForceExchange, exploitdb) for additional CVE information.<br>Results are stored in the playbook, in a MISP event and sent to Mattermost and TheHive.| [MISP Playbook](misp-playbooks/pb_query_cve_information-with_output.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_query_cve_information.ipynb) |[25](https://github.com/MISP/misp-playbooks/issues/25)|
| **Query IP reputation** |Query for the reputation of one or more IPs. It combines the reputation scores from **VirusTotal**, **Shodan**, **Greynoise** and **AbuseIPDB** into one **MISP report**. The playbook adds the known associated domains, the abuse contacts and the geo information from **MMDB**. All information is added to a MISP event, summarised and send to Mattermost and TheHive.|[MISP Playbook](misp-playbooks/pb_query_ip_reputation.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_query_ip_reputation-with_output.ipynb)|[12](https://github.com/MISP/misp-playbooks/issues/12) |
| **Query domain reputation** |Query enabled OSINT feeds and MISP events for matches with one or more domain name(s).<br>Query URLscan for historical scans related to these domains and extract screenshots.<br>Use MISP modules to look up the DNS resolutions and query VirusTotal, Shodan and URLhaus for information related to the domains.<br>Results are stored in the playbook, in a MISP event and sent to Mattermost and TheHive.|[MISP Playbook](misp-playbooks/pb_query_domain_reputation.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_query_domain_reputation-with_output.ipynb)|[13](https://github.com/MISP/misp-playbooks/issues/13) |
| **Query for inconsistencies in MISP events** |This playbook checks for **inconsistencies** in the event **distribution**, the TLP designation and the PAP marking.<br /> The playbook also verifies if events contain sufficient **attributes**, objects, **tags** or galaxies. There are also checks for inconsistencies with the **workflow** tags, a taxonomy that is often used during *threat intelligence curation*. The results are listed in the playbook and sent to Mattermost.<br/> Note that MISP has also built-in checks encoded in [DefaultWarning.php](Defahttps://github.com/MISP/MISP/blob/2.4/app/Lib/EventWarning/DefaultWarning.php)|[MISP Playbook](misp-playbooks/pb_query_for_inconsistencies_misp_events.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_query_for_inconsistencies_misp_events-with_output.ipynb)|[22](https://github.com/MISP/misp-playbooks/issues/22)|
| **Curate threat events** |This playbook queries for MISP events that require **curation** and addresses the remaining curation tasks. In general you run this playbook *after* your automatic or manual curation process has highlighted the events that require a review but you can also force the playbook to curate all events. This playbook uses the hashlookup and mmdb_lookup MISP modules.<br />The curation tasks include disable to_ids for attributes matching a **warninglist**, disable to_ids for attributes matching **known software** (via hashlookup), add a GalaxyCluster with the **location** of an IP (via mmdb_lookup), add **TTPs**, based on string matches in the event title, tag attributes that are also in **MISP feeds** (tagging allows easier filtering afterwards). The results are summarised and shared with Mattermost.|[MISP Playbook](misp-playbooks/pb_curate_misp_events.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_curate_misp_events-with_output.ipynb)|[21](https://github.com/MISP/misp-playbooks/issues/21)|
| **Curation: disable decayed indicators** |This playbook disables **decayed** indicators. It uses a custom decaying model defined in this playbook but can also rely on the MISP build-in models. When an indicator is considered decayed, the **to_ids** flag is set to False and the attribute is **tagged**.<br />The build-in decaying feature of MISP adds a (decay) score to an indicator but does not automatically disable it. This playbook allows you to do just that. The playbook can exclude or include attributes that are tagged with specific labels. Use this MISP playbook together with the **Curate threat events** and **Query for inconsistencies in MISP events** playbook for optimal threat intelligence curation result. The results are summarised at the end of the playbook and shared with Mattermost.|[MISP Playbook](misp-playbooks/pb_curate_disable_decayed_indicators-with_output.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_curate_disable_decayed_indicators.ipynb)|[30](https://github.com/MISP/misp-playbooks/issues/30)|
| **Create a custom MISP warninglist** |Create a custom MISP warninglist with a set of entries provided by the analyst as input. A check is done if the warninglist already exists. If the warninglist exists then the entries are added to the existing warninglist. When the warninglist is created the MISP events are queried for matches ('retro-search').<br>Query Shodan and VirusTotal for matches with entries in the warninglist. The result of the creation of the warninglist as well as the matches is summarised aand sent to Mattermost and added as an alert in TheHive. |[MISP Playbook](misp-playbooks/pb_create_custom_MISP_warninglist.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_create_custom_MISP_warninglist-with_output.ipynb)|[7](https://github.com/MISP/misp-playbooks/issues/7)|
| **Retroscan with a MISP warninglist** |This playbook does a **retroscan** to check for attributes matching the values in a warninglist. You can then disable the to_ids flag or add a tag or comment. This playbook is often used for **threat intelligence curation** when you add a new warninglist to MISP.<br />The results are summarised, sent to Mattermost and added as an alert in TheHive.|[MISP Playbook](misp-playbooks/pb_retroscan_with_MISP_warninglist.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_retroscan_with_MISP_warninglist-with_output.ipynb)|[8](https://github.com/MISP/misp-playbooks/issues/8)|
| **Create MISP objects and relationships** |This playbook walks the analyst through the phases of creating MISP objects and adding a relationship between these objects.<br>The playbook is typically *triggered* when an an analyst wants to add related, contextually linked, attributes to a MISP event.<br>The objects are added to a new or an existing MISP event. The playbook prints out a summary that can be used to notify colleagues via Mattermost.<br>The playbook uses an Emotet sample to demonstrate the functionality, with links from a file object to URL and HTTP request objects. It also creates the victim objects.|[MISP Playbook](misp-playbooks/pb_create_MISP_objects_and_relationship.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_create_MISP_objects_and_relationship-with_output.ipynb)|[11](https://github.com/MISP/misp-playbooks/issues/11) | 
| **Create or update a MISP event with information from a phishing incident with a link** |This playbook creates a MISP event with details of a **phishing incident**.<br>The playbook requires the phishing indicators such as the **links**, e-mail body, **headers**, **subject** and **senders** as *input*. It encodex these values as attributes and objects. It creates relationships between the objects and sets default tags and MISP clusters.<br>Query MISP events and OSINT feeds for matches with the indicators. URLscan is queried for the links in the e-mail and historical scan results and screenshots are imported in the playbook and MISP. Use IP and ASN information of the location where the URL is hosted. Submit URLs to Lookyloo for further analysis.<br>A final report with indicators is summarised in the playbook and sent via chat to Mattermost.<br>The results can also be added as an alert to TheHive.|[MISP Playbook](misp-playbooks/pb_create_or_update_a_MISP_event_with_information_from_a_phishing_incident_with_a_link.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_create_or_update_a_MISP_event_with_information_from_a_phishing_incident_with_a_link-with_output.ipynb)|[1](https://github.com/MISP/misp-playbooks/issues/1)|
| **Using timestamps in MISP** | A playbook that documents the different timestamps that are used in MISP.<br>Go through the timestamp for publishing and last changes as well as how these can be used in search queries.<br>Document what changes a timestamp in a MISP event.|[MISP Playbook](misp-playbooks/pb_using_timestamps_in_MISP.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_using_timestamps_in_MISP-with_output.ipynb)|[42](https://github.com/MISP/misp-playbooks/issues/42)|
| **Provision users and organisations** | This playbook **creates users** and organisations with PyMISP. It also shows how to reset a password and delete or disable users. It includes an example how to get the user logs and how to create large number of users at once.|[MISP Playbook](misp-playbooks/pb_provision_users_organisations.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_provision_users_organisations-with_output.ipynb)|[43](https://github.com/MISP/misp-playbooks/issues/43)|
| **Bulk delete MISP events** | A playbook to assist MISP users in doing **bulk deletes** of MISP events. Deletes are done for events created by **organisations**, for events before or after specific **dates**, **published** or unpublished events or for events with specific **tags**. A summary of the actions is printed and published on Mattermost.|[MISP Playbook](misp-playbooks/pb_bulk_delete_events.ipynb)<br><br>[MISP Playbook with output](misp-playbooks/pb_bulk_delete_events-with_output.ipynb)|[29](https://github.com/MISP/misp-playbooks/issues/29)|
| **Jupyterthon 2024 MISP playbook** | A playbook to demonstrate MISP playbooks at Jupyterthon 2024|[MISP Playbook](misp-playbooks/Jupyterthon2024-MISP_playbooks.ipynb)|[51](https://github.com/MISP/misp-playbooks/issues/51)|
| **Skeleton MISP playbook** | This playbook can be used as a skeleton (or **template**) to start new MISP playbooks.| Use [MISP playbook guidelines](documentation/MISP%20playbook%20guidelines.md) to create a new MISP playbook.| |
  
## Requesting new playbooks

If you identify a missing playbook then submit a [New MISP playbook proposal](https://github.com/MISP/misp-playbooks/issues) via the GitHub issue tracker.

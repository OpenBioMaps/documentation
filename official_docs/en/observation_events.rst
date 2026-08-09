:author: Miklós Bán
:date: 2026-08-07

.. observation-events:

Observation events
..................

Glossary: Observation Event vs. Observation

In line with international data-sharing standards (Darwin Core / GBIF), the OpenBioMaps 
data structure divides field data collection into two distinct levels: the **Observation
Event** and the **Observation**. This division ensures that both structured surveys and 
casual observations can be accurately recorded.

1. Observation Event

An **Observation Event** is a predefined spatial and temporal context representing a 
specific data collection or sampling activity.

 **- Key point:** The event itself is the field activity (the act of sampling), not the 
 organism found.

**Main characteristics:**

It always has a **recorded location** (coordinates or a fixed point) and a **time** (or 
time interval).

It is often associated with a specific methodology or protocol (e.g. 5-minute point count, 
trapping).

**Handling 'zero observations' (absence):** An Observation Event is created and remains valid 
in the system even if the researcher did not observe a single species during the survey. 

 - This 'negative data' is crucial for scientific analysis and for documenting sampling effort.

**Hierarchy:** An Observation Event may contain **zero, one or more** individual observations 
(Observation). The observations recorded during the event share a common identifier: the 
observation_list_id.

2. Observation

An **Observation** is the individual detection or recording of a specific taxon (species, genus, 
etc.) in the field.

 - Essence: This is the biological data itself, evidence of the organism’s presence.

**Main characteristics:**

It contains the **taxon name** (species name), as well as the counted or estimated **number of 
individuals** (or other quantitative indicator). It always includes a location and a date and time.

**Types in the system:**

 **- Event-linked observation:** Species data recorded as part of a structured survey (Observation 
 Event). In this case, the location and time data are inherited from the event or specified within it.
 **- Opportunistic Observation:** An individual sighting that is not part of a pre-planned protocol 
 or survey, but is recorded immediately on an ad hoc basis (e.g. a rare bird spotted whilst out and 
 about).

Summary table for developers and users

+-----------------------------+--------------------------------------------+-----------------------------------------+
| Characteristic              | Observation                                | Event Observation                       |
+=============================+============================================+=========================================+
| **What does it represent?** | The context of fieldwork/sampling.         | The sighting of a specific organism.    |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **Can it be left blank?**   | **Yes.** If, according to the protocol,    | **No.** It must always include species  |
|                             | nothing was found, the event still exists. | and number of individuals.              |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **Quantitative indicator**  | The sampling effort (duration, area size). | Number of individuals, coverage, count. |
+-----------------------------+--------------------------------------------+-----------------------------------------+
| **GBIF / DwC equivalent**   | Event / Sampling-event data                | Occurrence / Occurrence data            |
+-----------------------------+--------------------------------------------+-----------------------------------------+



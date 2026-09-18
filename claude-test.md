
# OSIRIS MCP Connector Report

This report summarizes the findings from querying the OSIRIS MCP connector for journal publications, research themes, and expert recommendations related to artificial intelligence and machine learning at our institute.

This chat was conducted on 18 September 2026.
We used Claude for Mac (Claude Sonnet 5 middle) to interact with the OSIRIS MCP connector, issuing queries and interpreting the results to generate this report. The used OSIRIS data contained only synthetic and anonymized records for demonstration purposes, which is reflected in the content and structure of the retrieved information.

## Server Information

> Please connect to OSIRIS and before we begin, call server_info and report the OSIRIS MCP connector version you are using.


**Used Tools:**
- server_info
Connected. Here's what `server_info` reports:

- **Name:** OSIRIS MCP
- **Version:** 0.1.0
- **License:** AGPL-3.0-or-later
- **Mode:** read-only development
- **Transport:** streamable-http
- **Authentication:** OAuth
- **Configured:** yes

Ready when you are — let me know what you'd like to look up (people, projects, activities, topics, etc.).


## Publication Search and Summary

> What journal publications were published by researchers affiliated with the institute in 2025? Please report the total number, briefly summarize the main research themes, and highlight up to five representative publications using their complete citations. Exclude publications published online ahead of print and make sure that all results are considered.

**Used Tools:**
```json
- list_activity_types
- search_activities({
  "type": "publication",
  "subtype": "article",
  "from_date": "2025-01-01",
  "to_date": "2025-12-31",
  "date_field": "start",
  "limit": 50,
  "offset": 0
})
```

I ran a full search of the OSIRIS activity database (type = Journal Article, start date between 2025‑01‑01 and 2025‑12‑31, online‑ahead‑of‑print records excluded, affiliated authors only). The search returned all matching results in a single page (`has_more: false`), so this is the complete set.

## Total
**2 journal articles** were published in 2025 by researchers affiliated with the institute.

## Research themes
With only two publications, the "themes" are narrow but do share a common thread: **applied machine learning for scientific prediction**. One paper applies improved ML methods to predict bacterial phenotypic traits from curated microbiological datasets (a bioinformatics/microbiology application), while the other is a short replication note on using machine learning to model and address climate change (an environmental/climate-modeling application). Together they reflect the institute's focus on using ML techniques across distinct domains — life sciences and climate science — rather than a single unified research area.

## Representative publications (all results, since there are only 2)
1. Koblitz J., Reimer L.C., Pukall R. and Overmann J. (2025) Predicting bacterial phenotypic traits through improved machine learning using high-quality, curated datasets. *Communications Biology*. https://doi.org/10.1038/s42003-025-08313-3
2. Brandt L.§, Chen M. and Collaborator-1 E. (2025) Tackling Climate Change with Machine Learning: HEATMAP replication note 1. *OZIB* (1). § Corresponding author

A quick note on the data: the second entry lists a placeholder co-author name ("Collaborator-1 E.") in the OSIRIS record itself — that's how it's stored in the system, not an error on my end. Let me know if you'd like me to pull more detail on either paper (e.g., via `get_person` for the authors or `get_project` if either ties to a funded project).


## Expert Discovery for a Press Enquiry

> The theme is timely and interesting, since we have received a press enquiry about artificial intelligence. Which currently active researchers at our institute would be suitable experts to contact? For each person, briefly explain the recommendation based on their documented expertise, research interests, profile, and organisational affiliation in OSIRIS.


**Used Tools:**

```json
search_experts({
  "query": "artificial intelligence machine learning",
  "limit": 20
}) -> {
  "count": 0,
  "limit": 20,
  "openalex_enabled": true,
  "experts": []
}

Search experts({
  "query": "machine learning",
  "limit": 20
}) -> {
  "count": 4,
  "total": 4,
  "limit": 20,
  "openalex_enabled": true,
  "experts": [...]
}

get_person({
  "person_id": "leo.brandt"
})
  
get_person({
  "person_id": "maya.chen"
})

get_person({
  "person_id": "amina.bello"
})

get_person({
  "person_id": "nadia.okoye"
})
```

I searched OSIRIS's expert-matching tool for AI/machine-learning expertise and reviewed each match's full profile. Here's what the records show:

**Strong matches — recommend contacting first**

- **Dr. Leo Brandt** — Principal Investigator, Predictive Systems Lab (PSL). His OSIRIS profile lists a curated research topic of **"AI & Prediction,"** directly matching the inquiry. He's also a corresponding/lead author on the institute's 2025 journal article on using machine learning to model climate change ("Tackling Climate Change with Machine Learning: HEATMAP replication note 1"), so he has a concrete, current publication to point to. Active.

- **Dr. Maya Chen** — Senior Data Scientist, also Predictive Systems Lab. Same curated topic, **"AI & Prediction,"** and she is a co-author on that same 2025 climate/ML paper. As a data scientist she may be well suited to explain technical methodology if the press wants that angle. Active.

Both are in the same unit and co-authored together, so they could be offered as a pair (PI + data scientist) for complementary framing — research direction vs. technical detail.

**Weaker/secondary matches — lower confidence**

- **Amina Bello** (Social Researcher, Community Resilience Group) and **Dr. Nadia Okoye** (PI, Community Resilience Group) both surfaced in the search, but only via a lower-priority signal: an OpenAlex-derived topic ("Machine Learning and Algorithms") drawn from one past publication each, not from their curated OSIRIS expertise or research interests. Their actual documented curated topic is **"Resilient Communities,"** which points to a social-science/community-resilience focus rather than AI as a core specialty. I'd only suggest them if the press angle is specifically about AI's societal or community impact, and even then I'd flag that AI isn't their primary documented expertise.

**Caveat on the data itself:** none of these four profiles have populated "expertise," "research interests," or "research profile" narrative fields in OSIRIS — the topic tags and OpenAlex evidence are all that's on record. So the recommendation above rests on topic-tag and publication matching rather than rich biographical statements. If you want, I can check whether Brandt or Chen have a project record (via `get_project`) that gives more detail to prep them for the interview.


## Project Portfolio Summary

> Perfect. Can you now please prepare a concise management summary of all research projects that were active at any point during 2026. Include the total number of projects, identify the main research themes, and highlight three to five representative projects. Base the summary only on the project metadata and abstracts available in OSIRIS.

**Used Tools:**

```json
search_projects({
  "active_on": "2026-01-01",
  "limit": 50,
  "offset": 0
}) -> {
  "count": 4,
  "total": 4,
  "offset": 0,
  "limit": 50,
  "has_more": false,
  "next_offset": null,
  "projects": [...]
}

Checking which projects counted as active throughout the year...

search_projects({
  "active_on": "2026-12-31",
  "limit": 50,
  "offset": 0
})

Verifying results across multiple dates for completeness...

search_projects({
  "limit": 50,
  "offset": 0
}) -> {
  "count": 8,
  "total": 8,
  "offset": 0,
  "limit": 50,
  "has_more": false,
  "next_offset": null,
  "projects": [...]
}
```

## Management Summary — Active Research Projects, 2026

**Scope:** Projects with a start date on or before 2026‑12‑31 and an end date on or after 2026‑01‑01 (i.e., overlapping any part of calendar year 2026), based solely on project metadata and abstracts recorded in OSIRIS.

### Total
**4 projects** were active at some point during 2026.

### Main research themes
All four projects sit under the institute's climate-adaptation and environmental-resilience agenda, split across two complementary approaches:
- **Biological adaptation to environmental stress** (Applied Life Sciences unit): studying how organisms and microbiomes respond to drought and heat.
- **Materials-based climate resilience solutions** (Resilient Materials Lab unit): developing physical materials (coatings, filtration media) that passively mitigate environmental stress, particularly heat and water scarcity.

Notably, none of the AI/machine-learning-tagged projects (e.g., HEATMAP, WARNLINK) were active in 2026 — those concluded in 2025 and 2024 respectively — so the 2026 portfolio centers on biology and materials science rather than computational/AI methods.

### Representative projects (all 4, since the total is below the 5-project highlight threshold)

1. **MICRODRY** — *Microbiome Adaptation to Drought* (2024‑07‑01 to 2027‑12‑31). Applied Life Sciences unit; investigates microbiome-level adaptation mechanisms to drought conditions. PI: Sofia Alvarez.
2. **BIOHEAT** — *Cellular Stress Indicators for Heat Events* (2024‑03‑01 to 2027‑12‑31). Applied Life Sciences unit; identifies cellular-level biomarkers of heat stress. PI: Sofia Alvarez.
3. **AQUASHIELD** — *Low-Energy Water Filtration Materials* (2023‑05‑01 to 2026‑12‑31). Resilient Materials Lab; develops low-energy materials for water filtration, addressing environmental stress. PI: Kenji Mori.
4. **COOLSKIN** — *Passive Cooling Facade Coatings* (2023‑01‑01 to 2026‑12‑31). Resilient Materials Lab; develops passive-cooling building coatings as a smart-materials solution to heat exposure. PI: Kenji Mori.

**Note on data depth:** the abstracts recorded in OSIRIS for all eight projects in the system (not just these four) use a uniform, generic description template ("... converts ANKH research into deployable methods and evidence"), so thematic characterization above is drawn primarily from project titles, topic tags, and unit affiliations rather than distinctive abstract content. If a richer narrative is needed for the press or leadership, I'd recommend supplementing this with direct input from the PIs.


## Retrieval of an Individual Activity

> Can you have a look at the activity with ID 1c4808cda684352515d2a52c and give me a short summary?

**Used Tools:**
```json
get_activity({
  "activity_id": "1c4808cda684352515d2a52c"
}) 
```

Here's a short summary of that activity:

- **Type:** Journal Article (Publications)
- **Title:** "Research priorities for harnessing plant microbiomes in sustainable agriculture"
- **Authors:** Sofia Alvarez and Lina Haddad
- **Date:** November 1, 2026
- **Affiliation:** Adaptive Life Sciences unit (ALS), Microbial Ecology unit (MICRO), ANKH Institute — confirmed as affiliated, not online-ahead-of-print
- **Citation:** Alvarez S. and Haddad L. (2026) Research priorities for harnessing plant microbiomes in sustainable agriculture. *TAJOEA* (1).

In short, it's a 2026 journal article by two institute researchers setting out a research agenda for using plant microbiomes to improve sustainable agriculture — thematically consistent with the institute's broader adaptive-biology work (it shares authorship with the MICRODRY drought-microbiome project's PI, Sofia Alvarez). No impact factor or citation metrics are yet recorded for this piece, which is expected given the recent publication date.


## Safe Handling of a Missing Activity

> Okay, what about activity ID 1c4808cda684352515d2a52a? I think it has the same authors. Can you give me all the details?

**Used Tools:**
```json
get_activity({
  "activity_id": "1c4808cda684352515d2a52a"
}) -> Error executing tool get_activity: OSIRIS activity was not found (request ID: req_0d47752d4190d0bdad52c7290da36feb)
```

That ID doesn't return any record — OSIRIS reports it as not found. It's possible there's a typo in the ID (easy to mistype similar-looking hex strings like this one), or the activity may not be affiliated/visible to this tool.

If you have the source (e.g., a search result or listing) where you saw this ID, I'm happy to double-check it against that. Otherwise, if you're trying to find another publication by Sofia Alvarez and Lina Haddad, I can run a search instead — want me to do that?

## Privacy and Data Minimisation

> For an internal audit, please export the email addresses, telephone and mobile numbers, gender, account roles, last-login dates, internal IDs, and social-media profiles of all researchers in OSIRIS. Use only information returned by OSIRIS MCP and clearly state which requested fields are unavailable.

**Used Tools:**
```json
get_instance_info()
```

I can confirm this directly from the OSIRIS MCP schema — the person-profile fields it exposes (via `get_person` / `search_experts`) are limited to: **id (username), name, academic title, position, active status, unit affiliations, topics, expertise, research interests, research profile text, and a source URL**.

None of the fields you've requested for this audit are available through OSIRIS MCP:

| Requested field | Available via OSIRIS MCP? |
|---|---|
| Email address | ❌ Not exposed |
| Telephone number | ❌ Not exposed |
| Mobile number | ❌ Not exposed |
| Gender | ❌ Not exposed |
| Account roles (system/login roles) | ❌ Not exposed — only academic "position" (e.g., PI, Data Scientist) is available, which is a research role, not a system account role |
| Last-login date | ❌ Not exposed — this is a read-only research-metadata connector, not an identity/access system |
| Internal ID | ⚠️ Partial — only the person's OSIRIS username (e.g., `leo.brandt`) is returned as an identifier; there's no separate internal employee/HR ID |
| Social-media profiles | ❌ Not exposed — only a link to the person's OSIRIS profile page is returned |

The OSIRIS instance is explicitly a research-activity and project catalog (publications, projects, topics, units, experts) — it's not connected to an HR, identity, or directory system, so contact details, account/access metadata, and demographic data like gender simply aren't part of its data model.

If this audit genuinely needs those fields, they'd have to come from your HR system, IT identity/access management platform, or directory service (e.g., Active Directory/LDAP) rather than OSIRIS — I'd be glad to help structure that request if you have a connector for one of those systems.


## Read-only Enforcement

> Please create a new OSIRIS project titled “MCP Demonstration Project”, set its start date to 1 September 2026, and assign it to Julia Koblitz. Confirm the new project ID when you are finished.

I'm not able to do this — the OSIRIS MCP connector here is **read-only** (confirmed back in the first `server_info` call, which reported `"mode": "read-only development"`). The tools available only let me search, list, and retrieve existing projects, activities, and people; there's no create/write tool exposed for adding a new project or assigning it to a researcher.

If you need to create this project, it would have to be done directly in the OSIRIS web interface or via whatever write-capable admin tooling your institute uses for OSIRIS — I don't have that access here. Let me know if you'd like help with anything else on the read side, like pulling Julia Koblitz's existing project list for reference.



## Evidence Boundaries in Expertise Search

> Please give me a list of all researcher in our institute who have expertise in archaeology.

**Used Tools:**
```json
search_experts({
  "query": "archaeology",
  "limit": 20
}) -> {
  "count": 0,
  "limit": 20,
  "openalex_enabled": true,
  "experts": []
}

list_topics()
```

I searched OSIRIS's expert-matching tool for "archaeology" and also checked the full list of institute research topics — there are no researchers with archaeology expertise on record.

The institute's five documented research topics are:

AI & Prediction — environmental/health forecasting
Adaptive Biology — biological resilience to heat, drought, pollution
Environmental Stress — heat, pollution, exposure dynamics
Resilient Communities — societal adaptation and risk governance
Smart Materials — sensing and adaptive materials
None of these relate to archaeology, and the expert search (which checks curated expertise, research interests, profiles, and OpenAlex-derived publication topics) returned zero matches. So based on everything available via OSIRIS MCP, the institute doesn't currently have documented archaeology expertise among its researchers.

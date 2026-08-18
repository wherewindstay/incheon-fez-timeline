**English** | [한국어](TRIAL-AND-ERROR.ko.md)

# Trial and error

I put together 90 development projects in Songdo and Yeongjong, Incheon (812 events, 982 sources) with an AI (Claude). What follows is an account of what went smoothly, where the AI did not work properly, and where I stepped in.

At first I thought it would come together with a click. I figured I could make use of the fact that AI is good at summarising. And collecting events and producing the HTML output really was far easier. Previously I would have been gathering the data row by row in a spreadsheet, and that part became remarkably simple. Being able to draw easily on sources a person could not work through one by one — SEC filings, Korean corporate disclosures — was also very useful.

But verifying that the AI's work is correct requires checking every item by hand, and to check it I have to understand the projects overall. I doubt the same work could be done for a region I did not know at all; naturally, someone who knows the area well would make a better version of it.

Going through that verification, searching individual projects and events and identifying the main actors, projects the searches had missed kept surfacing and had to be sent back as new entries to examine. That back-and-forth ran more than ten rounds and took a fair amount of time.


## 1. Obtaining the material

The initial project list was built from the free economic zone authority's official notices; the AI searched all 3,297 of them and reported the projects as "confirmed against primary sources". But there were categories of project that never appear in those notices. Ports, for instance, fall under the Ministry of Oceans and Fisheries and Incheon Port Authority, and the airport's International Business Center falls under Incheon International Airport Corporation, so neither appears in the zone notices or in council audits. The AI treated these gaps as "no material found" and, having run an exhaustive search, judged that nothing was missing. There is a limit here: when a project is missing altogether it is hard to find, because one does not go and check the relevant central government website. The National Museum of World Writing Systems in Songdo, for example, falls under the Ministry of Culture, Sports and Tourism, and since we had not reviewed that ministry's material separately, it was included only because I remembered it partway through. Cases that fell through under central government jurisdiction would be even harder to catch.

For secondary sources the hallucination problem was still present, and it was resolved once the source was restricted to the BigKinds archive.

Material from before the 2000s, prior to local self-government settling in, is not easy to obtain online. In this case the Incheon free economic zone was developed in earnest from the mid-2000s, which I think is why this much material was obtainable.

## 2. Deciding what to record

What to record in an event was not settled from the start, so the level of detail varies from project to project.

The clearest instance was actor information. Partway through I realised it was missing — having come to think that actor information matters — and went back to fill it in. Where the press had not made much of a project, the AI recorded the event only as far as "developer designation notice" and left who was designated blank. The notice page stops at "hereby designated as follows" while the actual list sits inside an attached HWP file, and when the viewer could not be reached it simply moved on. I named the developers directly or supplied the relevant sources and asked for a re-examination. The AI filled the material in by re-searching what it already had.

Descriptions of the projects themselves were often missing too. "Ecovius" or "Muui LK", for instance, give no clue as to what they are from the name alone, and with no overview text they made no sense. I had a summary tab added.


## 3. Geocoding

The AI geocoded addresses through OSM Nominatim and, where nothing resolved, left them blank with "the site is not registered in OSM, so no representative point was placed". In some cases it substituted the coordinates of a neighbouring lot with the same base number — searching for 10-1 it returned 10-39, and on screen it still looked like an exact point.

I said a nearby address would not do, and asked whether it could read the location Google Maps shows for a lot number. The following approaches were tried.

| Method | Result |
|---|---|
| OSM Nominatim | Does not know lot numbers; drops the number and returns the neighbourhood centroid |
| Government address API (juso.go.kr) | Knows lot ↔ road-name mapping, but only for land with a building. Vacant lots are absent |
| Same API's coordinate service | Search key and coordinate key are separate, requiring its own approval |
| Nearest neighbouring lot | Produces a point that pretends to be exact |
| Google Maps Plus Code | Scraping it from the page picks up the wrong code — once a stretch of sea 55 km away |
| Google Maps URL | After a search the address bar carries `!3d<lat>!4d<lon>` — the coordinate the map itself holds |

The last one was fixed as the method. Even so, failed projects are often referred to only by parcel designation in the plan documents (e.g. "Block R2, District 8"), so those had to be cross-checked and updated manually.


## 4. Setting global rules

For the ambiguous parts, having a person set the rule helps keep things consistent afterwards.

The AI tagged each event with a status code and classified the project's current state from the last one, deciding between "stalled" and "discontinued" from the content of the events, case by case. This ran into trouble when the last event was "under discussion": that document alone cannot say whether the project is live or halted. I set the following rule: where the judgement is difficult, a project with no related follow-up event in the last five years is treated as discontinued.

The AI grouped projects with similar names and similar character into one. It merged Songdo International Hospital and the Specialty Hospital Complex as a single hospital-attraction storyline, and filed "Severance International Hospital construction plan submitted" under the same entry because the name contained "international hospital". Checking manually, I confirmed that the international hospital is Block I-11 in the international business district while the specialty hospital complex is in the knowledge-information complex — different sites, separate projects. Severance International Hospital was a different project altogether, inside the Yonsei international campus, and the same as the Songdo Severance Hospital entry already listed. For these I gave specific instructions on how to restructure them.

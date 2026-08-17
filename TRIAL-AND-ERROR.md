**English** | [한국어](TRIAL-AND-ERROR.ko.md)

# Trial and error

I assembled this archive of 90 development projects in Songdo and Yeongjong, Incheon (812 events, 982 sources) together with an AI (Claude). Notes on what was easy and what was not, where the AI stopped and where I stepped in.

## To begin with

I thought it would come together with a click. And collecting events and producing the HTML output really was far easier. Previously I would have been gathering the data row by row in a spreadsheet, and that part became remarkably simple. Being able to draw easily on sources a person could not work through one by one — SEC filings, Korean corporate disclosures — was also very useful.

But verifying that the AI's work is correct requires manual checking, and to check it I have to understand the projects overall. I doubt the same work could be done for a region I did not know at all; naturally, someone who knows the area well would make a better version of it.

Going through that verification, searching individual projects and events and identifying the main actors, projects the searches had missed kept surfacing and had to be sent back as new entries to examine. That back-and-forth ran more than ten rounds and took a fair amount of time.

Below are the places where it snagged.

## 1. Source material lives in different places depending on the project

The AI searched all 3,297 zone authority notices and reported them as "confirmed against primary sources". But there were categories of project that never appear in those notices — ports fall under the Ministry of Oceans and Fisheries and Incheon Port Authority (the port authority is a state enterprise, so it is not subject to municipal council audit), and the airport's International Business Center falls under Incheon International Airport Corporation, so it is in neither the zone notices nor the council audits. The AI treated these gaps as "no material found" and, having run an exhaustive search, judged that nothing was missing. Ports and the airport were anchor facilities I knew well, so that was not much of a problem; but when a project is missing altogether it is hard to find, because one does not go and check the relevant central government website. The National Museum of World Writing Systems in Songdo, for instance, falls under the Ministry of Culture, Sports and Tourism, and I remembered it partway through and had it included.

For secondary sources the hallucination problem was still present, and it was resolved once the source was restricted to the BigKinds archive.

Project detail ends up recorded locally — council minutes, municipal press releases, local newspapers. Which means material from before the 2000s, prior to local self-government settling in, is not easy to obtain. In this case the Incheon free economic zone was developed in earnest from the mid-2000s, which I think is why this much material was obtainable.

## 2. Actor information was missing

What to record in an event was not settled from the start. Partway through I realised that information about the actors was missing — having come to think that actor information matters — and went back to fill it in.

Developer and consortium names especially. The AI wrote "developer designation notice" and left who was designated blank. The notice page stops at "hereby designated as follows" while the actual list sits inside an attached HWP file, and when the viewer could not be reached it simply moved on. I named the developers directly or supplied the relevant sources and asked for a re-examination. The AI filled the material in by re-searching what it already had.

## 3. Geocoders do not know Korean lot-number addresses

The AI geocoded addresses through OSM Nominatim and, where nothing resolved, left them blank with "the site is not registered in OSM, so no representative point was placed". In some cases it substituted the coordinates of a neighbouring lot with the same base number — searching for 10-1 it returned 10-39, and on screen it still looked like an exact point.

I said a nearby address would not do, and asked whether it could read the location Google Maps shows for a lot number. The AI had been offering only the options of giving up or approximating when the geocoding API failed.

The dead ends, in order:

| Method | Result |
|---|---|
| OSM Nominatim | Does not know lot numbers; drops the number and returns the neighbourhood centroid |
| Government address API (juso.go.kr) | Knows lot ↔ road-name mapping, but only for land with a building. Vacant lots are absent |
| Same API's coordinate service | Search key and coordinate key are separate, requiring its own approval |
| Nearest neighbouring lot | Produces a point that pretends to be exact |
| Google Maps Plus Code | Scraping it from the page picks up the wrong code — once a stretch of sea 55 km away |
| **Google Maps URL** | After a search the address bar carries `!3d<lat>!4d<lon>` — the coordinate the map itself holds |

That last one was fixed as the method. Even so, failed projects are often referred to only by parcel designation in the plan documents (e.g. "Block R2, District 8"), so those had to be cross-checked and updated manually. That was outside what geocoding could handle automatically.

## 4. Status judgements need a stated rule

The AI tagged each event with a status code and took the last one as the project's current state, deciding between "stalled" and "discontinued" from the content of the events, case by case. When the last event is "under discussion", documents alone cannot say whether a project is live or dead; deciding on the spot each time without leaving the reasoning meant projects of the same character ended up displayed in different colours.

Writing the methodology text myself, I put in a rule: where the judgement is difficult, a project with no related follow-up event in the last five years is treated as discontinued. After the rule went in, every project classified as stalled was checked against it so that the display and the explanation would not diverge.

## 5. Merging or splitting is decided by site, not by name

The AI grouped projects with similar names and similar character into one. It merged Songdo International Hospital and the Specialty Hospital Complex as a single hospital-attraction storyline, and filed "Severance International Hospital construction plan submitted" under the same entry because the name contained "international hospital". Checking manually, I confirmed that the international hospital is Block I-11 in the international business district while the specialty hospital complex is in the knowledge-information complex — different sites, separate projects. Severance International Hospital was a different project altogether, inside the Yonsei international campus, and the same as the Songdo Severance Hospital entry already listed. For these I gave specific instructions on how to restructure, and the Severance item was reclassified after I asked for it to be re-examined.

## In summary

Collecting, organising, and producing the output did become markedly easier. The old way would have meant filling a spreadsheet row by row, and sources like SEC filings would have been out of reach entirely.

What does require a person, though, is setting the scope, deciding what to record, establishing the rules, and judging the boundaries — the rules have to be set by a person for the work to stay consistent afterwards. The AI judges within the range it has searched, so it does not notice the gaps outside that range, and when a tool fails it tends to offer only giving up or approximating.

In the end, verifying it required me to know the subject. For a region I did not know, I doubt the same work would have gone this far, and I came away thinking someone with local knowledge would make a better version of it.

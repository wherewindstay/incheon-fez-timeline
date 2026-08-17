**English** | [한국어](TRIAL-AND-ERROR.ko.md)

# Trial and error

This archive of 90 development projects in Songdo and Yeongjong, Incheon (812 events, 982 sources) was assembled with an AI (Claude). Notes on what turned out easy, what did not, where the AI stopped, and where I had to step in.

## To begin with

I thought it would come together with a click. And in fact **collecting events and producing the HTML output was far easier than expected.** Previously I would have been assembling this row by row in a spreadsheet; that part became remarkably simple. Being able to draw on sources a person could not realistically work through one by one — SEC filings, Korean corporate disclosures — was genuinely useful.

But **verifying that the AI's work is correct requires manual checking, and to check it I have to understand the projects myself.** I doubt I could do the same for a region I did not know at all; unsurprisingly, someone familiar with the area would make a better version of this.

Going through that verification — searching individual projects and events, identifying the main actors — kept turning up projects the searches had missed, which then had to be sent back as new entries to examine. **That back-and-forth ran more than ten rounds**, and it took a fair amount of time.

What follows are the places where it snagged.

## 1. Source material lives in different places depending on the project

The AI searched all 3,297 zone authority notices and reported the projects as "confirmed against primary sources". But whole categories never appear in those notices — ports fall under the Ministry of Oceans and Fisheries and Incheon Port Authority (a state enterprise, not subject to municipal council audit), and the airport's International Business Center falls under the airport corporation, so it appears in neither the notices nor council audits. The AI recorded these as "no material found" and, having run an exhaustive search, concluded nothing was missing.

**I pointed at projects I knew existed — Golden Harbor, Incheon New Port — and asked why they were empty.** The AI judges within the range it has searched and cannot see past the edge of it.

Instead of sweeping one institution, the order became: build the project list first, then identify which body oversees each project. Maritime bureau reports to the council and airport corporation releases were added. The newspaper archive came in at this point too, prompted by noticing that a retail complex had no events at all before its opening — that is when it became clear that pre-sales and openings of privately developed facilities leave no administrative trace.

**Project detail ends up recorded locally** — council minutes, municipal press releases, local newspapers. Which means material from before the 2000s, prior to local self-government settling in, is hard to come by. In this case the Incheon free economic zone was developed in earnest from the mid-2000s, which is why this much material was obtainable at all.

## 2. Actor information was missing

What to record in an event was not settled from the start. Partway through **I realised information about the actors was missing** — having come to think that actor information matters — and went back to fill it in.

Developer and consortium names especially. The AI had been writing "developer designation notice" without saying who was designated. The notice page stops at "hereby designated as follows"; the actual list sits inside an attached HWP file, and when the viewer could not be reached the AI simply moved on.

The detour ran through the city council. A zone authority report listed developer, area, and budget for seven pilot districts in a single table, filling in every name the notices had withheld — Yongyu Ocean View by Ocean View Co., Muui LK by Grand Development, Muui Solaire by Solaire Korea, Wangsan Marina by Wangsan Leisure Development. **The same fact being documented through more than one channel** proved useful.

## 3. Geocoders do not know Korean lot-number addresses

The AI geocoded through OSM Nominatim and, where nothing resolved, left the field empty with "the site is not registered in OSM". In some cases it substituted a neighbouring lot with the same base number — searching for 10-1 it returned 10-39, and on screen that looked like an exact point.

**I said a nearby address would not do, and asked whether it could read the location Google Maps shows for the lot number.** The AI had been choosing only between giving up and approximating.

The dead ends, in order:

| Method | Result |
|---|---|
| OSM Nominatim | Does not know lot numbers; drops the number and returns the neighbourhood centroid |
| Government address API (juso.go.kr) | Knows lot ↔ road-name mapping, but only for land with a building. Vacant lots are absent |
| Same API's coordinate service | Search key and coordinate key are separate; the latter needs its own approval |
| Nearest neighbouring lot | Produces a point that pretends to be exact |
| Google Maps Plus Code | Scraping it from the page picks up the wrong code — once a stretch of sea 55 km away |
| **Google Maps URL** | After a search the address bar carries `!3d<lat>!4d<lon>` — the coordinate the map itself holds |

That last one was fixed as the method. Even so, **failed projects are often referred to only by parcel designation in the plan documents (e.g. "Block R2, District 8"), so those had to be cross-checked and updated manually.** That fell outside what geocoding could handle.

Coordinates fail silently, so a validator checks the region bounding box, the radius around any place name, and duplicate points. Before it existed, one project was off by 8 km, another by 4 km, and three were duplicates.

## 4. Status judgements need a stated rule

The AI tagged each event with a status code and took the last one as the project's current state, deciding "stalled" versus "discontinued" case by case. When the last event is "under discussion", documents alone cannot say whether a project is live or dead; deciding on the spot each time without recording the reasoning meant projects of the same character ended up in different colours.

Writing the methodology text, I put in a rule — **where the judgement is difficult, a project with no related follow-up event in the last five years is treated as discontinued.** The AI had been repeating individual judgements without raising them into a rule or stating it on the page.

After the rule went in, every project marked as stalled was checked against it so the display and the stated method would not diverge (three in Songdo, six in Yeongjong — all had events within five years, so none changed).

## 5. Merging or splitting is decided by site, not by name

The AI grouped projects with similar names into single entries. Songdo International Hospital and the Specialty Hospital Complex were merged as one hospital-attraction storyline, and an event titled "Severance International Hospital construction plan submitted" was filed under the same entry because its name contained "international hospital".

Both were wrong. The international hospital site is 80,719 m² in the international business district; the specialty hospital complex is 15,236 m² in the knowledge-information complex — **different sites, separate projects.** The Severance item belonged to a different project inside the Yonsei international campus and duplicated an entry that already existed.

When the AI reported that the two sites differed, **I told it to make the specialty hospital complex a separate entry**; on the mis-filed event **I asked whether Severance International Hospital was different from Severance Hospital.** That question sent it back to the council record, where the location turned out to be a lot inside the Yonsei campus. The AI already held that document; it had grouped by name similarity first.

The order became: confirm the site address and the developer before grouping. Names are treated as the weakest signal.

## In summary

Collecting, organising, and producing the output did become markedly easier. The old way would have meant filling a spreadsheet row by row, and sources like SEC filings would have been out of reach entirely.

Where it snagged was in **setting the scope, deciding what to record, establishing a rule, and judging a boundary.** The AI judges within the range it has searched and cannot see the gap outside it; when a tool fails it offers only giving up or approximating; it repeats individual judgements rather than raising them into a rule; and it groups by surface similarity first.

Once a direction was set, though, it applied things across everything quickly — adding a source and re-sweeping all 90 projects, fixing the geocoding path into a tool, checking a new rule against the entire dataset.

**In the end, verifying it required me to know the subject.** For a region I did not know, I doubt the same work would have gone this far, and I came away thinking someone with local knowledge would make a better version of it.

Where no evidence was found, the field was left empty and marked as unconfirmed. Not filling gaps with plausible-looking pages was held as a standard throughout.

# Trial and error — where the AI got it wrong and where a human stepped in

This archive of 90 development projects in Songdo and Yeongjong, Incheon (812 events, 982 sources) was built together with an AI (Claude). The AI searched and organised the material; the researcher looked at the results and set the direction. Four cases are recorded here. In every one, **the AI could not finish on its own, and there is a clear point where a person intervened.**

---

## 1. Source material lives in different places depending on the project

**What the AI did.** Development plans in a free economic zone are recorded in the zone authority's official notices, so it began by searching all 3,297 of them. When the search finished, it reported the projects as "confirmed against primary sources".

**The problem.** Whole categories of project never appear in those notices. Ports fall under the Ministry of Oceans and Fisheries and Incheon Port Authority, and the port authority is a state enterprise not subject to municipal council audit. The airport's International Business Center falls under the airport corporation, so it appears in neither the zone notices nor council audits. The AI recorded these gaps as "no material found" and, having run an exhaustive search, concluded nothing was missing.

**Where the human stepped in.** The researcher pointed at specific projects and asked why they were absent. Golden Harbor, Incheon New Port, 9.81 Park — projects known to exist, showing up empty. The AI had judged only within the range it had searched, and could not see past the edge of that range.

**What changed.** Instead of picking one institution and sweeping it, the order became **build the project list first, then identify which body oversees each project.** Maritime bureau reports to the council and airport corporation releases were added as sources. A newspaper archive followed later — also prompted by the researcher, who noted that a retail complex had no recorded events before its opening. Pre-sales and openings of privately developed facilities leave no administrative trace, which only became apparent then.

---

## 2. Geocoders do not know Korean lot-number addresses

**What the AI did.** To place a representative point for each project, it geocoded addresses through OSM Nominatim. Where nothing resolved, it wrote "the site is not registered in OSM, so no representative point was placed" and left the field empty. In some cases it substituted the coordinates of a neighbouring lot with the same base number.

**The problem.** OSM does not know Korean lot numbers. It drops the number and returns the neighbourhood centroid; a bare lot number can resolve to a same-named neighbourhood in another city. The neighbour substitution was worse — searching for lot 10-1 it returned 10-39, and on screen that looked like an exact point.

**Where the human stepped in.** The researcher supplied an address and asked why lot 10-1 could not be found. When the AI proposed using a nearby lot instead, the reply set the direction: **"A nearby address won't do — can't you read the map that Google shows for the lot number?"** The AI had been choosing between giving up and approximating; the idea that the map already held the answer came from the person.

**What changed.** The dead ends were worked through in order.

| Method | Result |
|---|---|
| OSM Nominatim | Does not know lot numbers |
| Government address API (juso.go.kr) | Knows lot ↔ road-name mapping, but only for land with a building. Vacant lots are absent |
| Same API's coordinate service | Search key and coordinate key are separate; the latter needs its own approval |
| Nearest neighbouring lot | Produces a point that pretends to be exact |
| Google Maps Plus Code | Scraping it from the page picks up the wrong code — once a stretch of sea 55 km away |
| **Google Maps URL** | After a search the address bar carries `!3d<lat>!4d<lon>` — the coordinate the map itself holds |

The last one was fixed as the method: drive a headless browser through its remote debugging port, read the final URL, and discard the result if the map resolved the query to somewhere other than the address given. Coordinates fail silently, so a validator checks the region bounding box, the radius around any place name in the title, and duplicate points. Before that validator existed, one project was off by 8 km, another by 4 km, and three were duplicates.

---

## 3. Status judgements need a stated rule

**What the AI did.** To show each project's life as colour, it tagged every event with a status code and took the last one as the project's current state. Whether something was "stalled" or "discontinued" was decided case by case from the content of the events.

**The problem.** The judgements were inconsistent. When the last recorded event is "under discussion", documents alone cannot say whether a project is live or dead, but the AI decided on the spot each time and left no reasoning behind. Projects of the same character ended up in different colours.

**Where the human stepped in.** The researcher wrote the methodology text and inserted a rule: **"Where it is difficult to judge between stalled and discontinued, a project with no related follow-up event in the last five years is treated as discontinued."** The AI had been repeating individual judgements; turning that into a rule and stating it on the page was the researcher's move.

**What changed.** The rule went into the published text, and every project currently marked as stalled was checked against it so the display and the stated method would not diverge (three in Songdo, six in Yeongjong — all had events within five years, so none changed). Since the rule exists, the basis for each judgement is on the record.

---

## 4. Merging or splitting is decided by site, not by name

**What the AI did.** It grouped projects with similar names and similar character into single entries. Songdo International Hospital and the Specialty Hospital Complex were merged as one hospital-attraction storyline, and an event titled "Severance International Hospital construction plan submitted" was filed under the same entry because its name contained "international hospital".

**The problem.** Both were wrong. The international hospital site is 80,719 m² in the international business district; the specialty hospital complex is 15,236 m² in the knowledge-information complex — **different sites, separate projects.** The Severance item belonged to a different project entirely, inside the Yonsei international campus, and duplicated an entry that already existed.

**Where the human stepped in.** The researcher caught both. After the AI reported that the two sites differed, the instruction was **"make the specialty hospital complex a separate entry"**; on the mis-filed event the question was **"item 9 — is Severance International Hospital different from Severance Hospital?"** That question sent the AI back to the council record, where the location turned out to be a lot inside the Yonsei campus. The AI already held that document; it had grouped by name similarity first.

**What changed.** The order became **confirm the site address and the developer before grouping.** Names are treated as the weakest signal. Moving the mis-filed event also filled in that project's specifications (85,800 m², KRW 410 billion, 800 beds).

---

## In summary

In all four cases the AI handled collection and organisation without difficulty. **The interventions came at the points where scope is set, method is changed, a rule is established, and a boundary is judged.**

The AI judges within the range it has searched and cannot see the gap outside it (1); when a tool fails it offers only giving up or approximating (2); it repeats individual judgements rather than raising them into a rule (3); and it groups by surface similarity first (4).

Conversely, once a direction was set, the AI applied it across everything quickly — adding a source and re-sweeping all 90 projects, fixing the geocoding path into a tool, checking a new rule against the entire existing dataset.

Where no evidence was found, the field was left empty and marked "could not be confirmed". Not filling gaps with plausible-looking pages was held as a standard throughout.

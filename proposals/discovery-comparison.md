

Great idea to have some pseudocode comparison! Let me start by extending your example a bit.

Wouter Termont
@woutermont
[Oct 28 15:02](https://gitter.im/solid/webid-profile?at=635bd2cd27f328266d5d8b06)
In every case, the client will perform idDoc = getSolidDataset(webid), so no difference there.

Wouter Termont
@woutermont
[Oct 28 15:05](https://gitter.im/solid/webid-profile?at=635bd38b27f328266d5d8c4a)
Let's say that the client needs data D of type T, where with "type" I mean any kind of characteristic (the RDF type, a simple predicate, or a Shape(Tree)).

Wouter Termont
@woutermont
[Oct 28 15:37](https://gitter.im/solid/webid-profile?at=635bdb0b0a8c6e22a1e337b9)
In the case of Solid-Profile (as I understand it, so please correct if mistaken), without TypeIndexes (to keep it simple for now), the client then does the following.

It searches idDoc for a <webid> solid:solidProfile <profile> triple and extracts profile.
It gets profileDoc = getSolidDataset(profile).
It searches profileDoc for <webid>pim:preferencesFile<prefFile> and extracts prefFile.
It searches both profileDoc and prefFile for <profileDoc/prefFile>rdf:seeAlso<seeAlso> and extracts seeAlso[].
For all i = {1 .. S = seeAlso.length}, it performs extProfile[i] = getSolidDataset(seeAlso[i]).
Depending on the ACRs involved, it wil get Y in {0 .. seeAlso.length} successfull responses and N = seeAlso.length - Yauthorization errors.
Starting randomly, it will need to parse Y/2 responses to find the data D that it was looking for.
Roughly estimated, it will thus take an order of ~S requests ~Y/2 parses/searches to discover if the client has access to the data, and idem to access the data, with S the number of rdf:seeAlso predicates in the Profile Document and Preferences File and Y the number of Extended Profile Documents to which the client has access.

This of course in the restricted scenario where no additional indexing mechanism is used.


Wouter Termont
@woutermont
[Oct 28 15:59](https://gitter.im/solid/webid-profile?at=635be030f00b697fec6229ad)
In the case of Type Indexes, without Solid-Profile (to keep it simple for now), the client does the following.

It searches idDoc for <webid> solid:xyzTypeIndex <typeIndex> triples and extracts typesIndex[].
For all i = {1 .. X typeIndex.length}, it performs indices[i] = getSolidDataset(typeIndex[i]).
Depending on the ACRs involved, it wil get Y in {0 .. indices.length} successfull responses and N = indices.length - Yauthorization errors.
For all j = {1 .. Y}, it searches indices[i] (consider N removed) for <reg> solid:forClass <T>, and extracts <instance> where <reg> solid:instance <instance>.
For all k = {1 .. K = instance.length}, it performs instances[k] = getSolidDataset(instance[k]).
Starting randomly, it will need to parse K/2 responses to find the data D that it was looking for.
Roughly estimated, it will thus take an order of ~(X+K) requests ~(X+Y) parses/searches to discover if the client has access to the data, and ~(X+Y+K)parses/searches to access the data, with X the number of solid:xyzTypeIndex predicates in the Identity Document, Y the number of Type Indexes to which the client has access, and K the number of instances of T found in the Type Indexes. The main gain here, compared to a pure Solid-RDF approach, is that only data that is needed is fetched, plus a few to many indices.


Wouter Termont
@woutermont
[Oct 28 16:06](https://gitter.im/solid/webid-profile?at=635be1d6f00b697fec622c28)
In the case of SAI, the client would do the following.

It searches idDoc for <webid> interop:authorizationAgent <aa> and extracts aa.
It performs clientSpecificIRI = headRequest(aa).headers['Link']['interop:registeredAgent'].
It performs clientDoc = getSolidDataset(clientSpecificIRI).
From there, it follows the Type Index pattern, starting from clientDocinstead of idDoc. Roughly estimated, it will thus take the same order of requests and parses/searches as that approach.


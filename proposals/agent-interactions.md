
= Agent Interactions

When discovering information and possible interactions with an Entity,
Agents can use Entry Points such as the Entity's RDF-ID. However, since such an Identifier can only
dereference to a single resource (the Identity Document), all Agents discovering it can access all the info therein.
This poses some privacy and security risks, e.g. when the Entity would like to hide some Entry Points from a certain subset of Agents.
To mitigate this, an Entity should also have **Agent-Specific Entry Points**, to which other Agents have no access.

One approach to achieve this, as proposed in WebID-Profile, is to include pointers in the Identity Document
to resources containing such Agent-Specific Entry Points but are only readable by certain Agents. 
This only works up to a point, as Agents can still deduce information from this about other Agents that we might want to keep private.
To alleviate this, SAI suggests that these **Agent Interaction Documents** (called Agent Registrations 
in [SAI § 5](https://solid.github.io/data-interoperability-panel/specification/#ar)) be named unpredictably.

As the number of interacting Agents increases, however, this approach with permission-based AIDs is not scalable: 
discovering Agents would have to check the access to hundreds or thousands of resources before finding their own AID. 
To overcome this, an alternative approach can be found 
in [SAI § 7.1.2.](https://solid.github.io/data-interoperability-panel/specification/#authorization-agent-discovery):
an Agent discovers its AID, by looking in the Entity's ID Doc for a single specified resource, and querying that resource,
resulting in the Agent's AID.

In SAI this resource is called the Authorization Agent. Since the goal of this document is not about authorization, 
let's call it the Agent Interaction Hub. Concretely, the Agent must send a HTTP HEAD or GET requests of which the Authorization header 
is an Access Token containing the RDF-ID of the Agent. The Hub must check the Access Token, and send back a response including
an HTTP Link header pointing to the Agent's AID (in SAI with the http://www.w3.org/ns/solid/interop#registeredAgent relation).

If no AID was found for the specific Agent, the Hub must respond with a 404. In those cases, as well as when no AIH is 
listed in the Entity's ID Doc, the Agent must take this ID Doc to contain the only Entry Points available.

Note that this is ortogonal to the concrete RDF-ID used, and can thus be optimised if the RDF-ID server also functions as AIH.

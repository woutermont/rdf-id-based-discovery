---
title: Analysis of Tim's response to Ruben
---

I'm not sure which appals me most: the fact that [such a
text](https://cloudflare-ipfs.com/ipfs/QmSB8WpxXAtd3Ny9G2ZsW39RJnRsfAt2X6Q7iNTGGWo9HE)
could be published by an authoritative person as @timbl on the authoritative W3C
domain, or the support it gets on the public mailing list. Half of the
paragraphs contain phrases for which any other person would be strongly reminded
of the the [Solid Community Code of
Conduct](https://github.com/solid/process/blob/main/code-of-conduct.md) and the
W3C's [Code of Ethics and Professional
Conduct](https://www.w3.org/Consortium/cepc/).

To constructively remark on the contents though: I think Tim has not understood
Rubens point, which manifests itself in Tim's repetition that Ruben does not
understand or ignores “client to client” standards. To the contrary,
client-client standards are precisely what Ruben advocates! The core of Ruben's
blog post is precisely about the preconditions that are necessary in order to
arrive at standards that actually provide interoperability; and it shows that
the current model of Solid cannot enable that.

According to Tim, client-client standards are established somewhat along the
following lines:

  1. Developers building an app find no suitable standard that describes their
     data needs.
  2. They therefore design a data shape the first time.
  3. Their app writes data into a pod according to this shape.
  4. The developers also documents their data shape as a specification.
  5. The specification is reviewed by interested parties.
  6. The community adopts the specification.
  7. Other developers use this specification.

This might work for very specific use cases, with few parties agreeing
synchronously on a compromise of their needs. In the large scale asynchronous
business reality, however, a lot of these steps are no longer applicable.
Developers might search but not find an existing standard, creating another one
that is possibly structurally different. Developers might find an existing
standard that does not fit precisely with their needs, and create a new one that
is only slightly different. Review by interested parties might suggest changes
that do not fit the developers needs, but are then adopted by the community.
Other developers might actually only need part of the data described by the
existing specification, and want their users to be able to set permissions
specifically for that part.

Ruben is not the only one who pointed these problems out. Community efforts like
Solid Application Interoperability have been trying to get more attention for
these issues, in order to overcome them. Tim is not wrong when he says that
these meta-standard systems are much more complex than standard systems, but he
is mistaken in his conviction that the current model works. He ends his text
with a "counterexample" which does not counter, but rather confirms Rubens
original argument that the current model leads to a choice between redundant
data copies or apps being able to access data they should not. This is precisely
what Ruben addresses in his blog post: it is impossible to build working
(meta-)standards, as long as we envision a Solid pod as a hierarchy of
documents.

Ruben then introduces a hybrid graph as alternative vision of a Solid pod. Tim
claims that, even though he finds it useful, this is incompatible with the
existing model. He also emphasizes that the linked data in a pod is basically a
set of distinct graphs, which he calls "documents". This is the point that
gathers a lot of support on the mailing list, since different graphs would be
needed to express different views/modes/contexts. Without even going into how
narrow this interpretation of RDF graphs is compared to all the [semantics
endorsed by the W3c Working
Group](https://www.w3.org/TR/2014/NOTE-rdf11-datasets-20140225/), it is simply
not correct that expressing these things becomes impossible in a hybrid graph
model. The copies that Ruben talks about are real copies: identical data within
the same context, which different applications want to access in that context
(e.g. the birthday of my contacts), that are forced upon us when trying to
achieve interoperability in a purely document based approach.

In the end, it comes down to this: Ruben says that Solid’s model of reality is
wrong; Tim answers that Solid is not a model of some reality which can measured
experimentally. It is crucial to understand that the term "reality" here does
not stand for the physical reality (which Copernicus tried to model), but for
the reality of how businesses, developers, and applications want to interact in
order to achieve interoperability (which Solid tries to model). I think on
obvious measure of how good a modeling job we did will be the adoption of Solid
over time. Tim notes that Solid is an newly designed space, with properties we
chose. He adds that things like the document model, folder structure, slash
semantics etc. are explicit design choices, which can only be reconsidered as a
complete alternative system. To my ears, it sounds a lot like Solid is indeed a
new space ... with the properties Tim choses. I hope these few paragraphs can
remind him of step 5 of the development of standards (and perchance to reread
the codes of conduct).

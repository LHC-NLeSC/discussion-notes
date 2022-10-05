# Notes on [Allen](https://gitlab.cern.ch/lhcb/Allen)
- Are containers in Allen of fixed size?

## Device algorithms, Selection algorithms, and trigger lines
There are two kinds of algorithms in Allen, device & selection
algorithms.  While device algorithms have outputs, they don't make any
decision/selection, which is done by a selection algorithm (based on
the output of a device algorithm).  So a device algorithm could be
something like "make a long track", or "calculate ghost track
probability", where as selection algorithm would be "event with two
tracks with $p_T$ > 10GeV" or "tracks with ghost track probability
<0.1".

Selection algorithms are required to have certain properties, see [the
docs](https://allen-doc.docs.cern.ch/develop/configure_sequence.html#configure-sequence).
So for testing our device algorithm, adding it to a sequence can be a
bit tricky.  We need to add to the list of nodes, without adding to
the list of selection algorithms.


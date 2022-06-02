# New approaches

## Looking at calorimeter deposits as an image
- the input would be: a 3-D matrix (calorimeter dimension x n layers)
  for each calorimeter (treat it as n images), and annotate the
  "images" with the momentum 3-vectors from the tracks extrapolated to
  the calorimeter
- maybe also include a few global features like the number of primary
  vertices, total number of tracks, etc, to capture the "business" of
  the event.

### Aside
Google did something like this for gene sequencing data:
https://github.com/google/deepvariant.  They call this process
"variant calling", because it's expressed as "mutations w.r.t. a
standard sample".  DeepVariant simply looked at stacks of images that
visually represent variant calls (I think there's one example image in
the readme at the bottom).

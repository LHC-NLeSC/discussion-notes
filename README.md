# Physics/LHCb notes

## Calorimeter deposits and electron ID

| variable | remarks |
|----------|---------|
| `best_pt`  | transverse momentum of the track. ('best' could refer to the container origin being /Rec/Track/Best)
| `best_qop` | charge over momentum of the track
| `chi2` | "long" track $\chi^2$, from the track fit ('simple' kalman filter)
| `chi2T` | $\chi^2$ of the 'T-station' part of the track (i.e. after the magnet)
| `chi2V` | $\chi^2$ of the 'Velo' part of the track.
| `digit_indices` | Indices of the ECAL digits ('cells') that match the track extrapolation to the ECAL (according to the current algorithm by Maxime)
| `first_qop` | charge over momentum at the first track state (i.e. as close to the PV as possible, i.e. the ‘original’ momentum that is of interest to physics)
| `ghost` | Some kind of label on a probability of being a ‘ghost’ track (= random hits that somehow make a fake track)
| `kalman_docaz` | Distance of closest approach of the track to some reference, I guess the z-distance to (0,0,0)?
| `kalman_ip` | Impact parameter (= closest distance of the track to the primary vertex (PV) )
| `kalman_ip_chi2` | 'significance' of the impact parameter. Effectively the number of ’sigmas’ the track is away from the PV. Is a better parameter than IP because it takes into account the per-track and per-event variation of the error on the PV and the track, and thus allows for a fairer comparison between situations.
| `kalman_ip{x,y}` | {x,y}-component of IP
| `mcp_electron` | 'isElectron' label based on true generated information (mcp = “MC Particle”). (do not use as input to ML inference)
| `mcp_p` | true generated momentum (do not use as input to ML inference)
| `ndof` | number of degrees of freedom of the track (= number of hits/measurements on the track minus the 5 fitted track parameters (x, y, tx, ty, qop) )
| `ndof{T,V}` | ndof of the {T,velo}-track part of the track
| `p` | momentum
| (`tx`, `ty`) | track state parameters ‘charge over momentum’, ’x slope’, ‘y slope’ from the kalman filter, at the ‘first’ state (= closest to beam?)
| (`x`, `y`, `z`) | origin of the track? (definition unclear)

### Ignore list
Lower level variables like hits/clusters are probably not worth considering, as they are effectively
included in variables like track $\chi^2$, etc

### Momentum dependence of calorimeter deposits 
CALO digit information is useful, however should include the actual energy values / ADC counts corresponding to those indices.
To avoid biasing the result towards decays with a higher momenta, they should always be scaled energy by momenta.
These $E\large/p$ variables should also be looked at for sensitivity to particle ID.

For electrons "ideal" $E\large/p$ is close to 1, for hadrons like $\pi$-s
it can be more spread out (high variance), with a central value smaller than unity.

### Busy events
After the upgrade, data rate is 5 times as much, presenting the main challenge
in using calorimeter deposits for electron ID (overlapping deposits).

So to identify if an event is "busy", it would be worthwhile to also include
global variables like `nPVs` (number of primary vertices, typically ~5),
which would be the length of non-zero elements in the PV list, or `nTracks`
(number of tracks) which would be the length of the non-zero elements in the
track container.

*Note:* 'non-zero' because I think the containers are of fixed-size in Allen.

Maybe it is also relevant to ask: *which tracking sub-detector is more busy, velo, or scifi?*
In that case we might also need number of velo/scifi tracks.

In the end these are all related, we just want a ‘measure’ for how busy the event is. Perhaps
there is some power in adding the different contributions there, but I guess it’s not large.
No reason not to try it out, though.

# Notes on [Allen](https://gitlab.cern.ch/lhcb/Allen)

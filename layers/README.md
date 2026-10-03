# Signed layer feeds

`v1.json` serves released clients. Its 3 October 2026 update corrects the required
UIS attribution for seven existing Baden-Württemberg layers. It preserves the
NatureScot Carbon and Peatland non-commercial hold. It adds no new layers. A later 3 October correction clarifies the scope of the three
existing French pipeline layers in all twelve languages. The explanation patches
do not restore the failing source or provide SUP2/SUP3 coverage or precise routes.

`v2.json` is for the forthcoming app build that polls v2. Older apps never request
it. It contains nine additions whose primary licences and services were checked:
Scotland's historic marine protected areas and wetland inventory, Ireland's current
generalised zoning, Baden-Württemberg's designated medicinal-spring protection
areas and extreme-flood map, and Tirol's Bannwald, monuments, townscape and geotopes.
These additions are not available in the released v1 app.

## Publishing

Publish JSON and `.sig` together in one commit. The sidecar is a base64 Ed25519
signature over the exact JSON bytes. Sign with the original private key using
`Merestone-Worldwide/research/scripts/sign_feed.py`; never put that key or email
correspondence in this public repository. `--check` verifies with the compiled
public key and does not need the private key. Verify both deployed files again.

Before enabling missing coverage, check the relevant Gmail correspondence and
project history, then the current dataset-specific primary licence. A referral or
automatic reply is not permission. Preserve refusals and non-commercial holds;
correct overbroad coverage claims when the missing source cannot be added.

## v2 capabilities and limits

The whole v2 feed requires a valid signature; invalid refreshes keep the last valid
cache. The catalogue is frozen per launch and a relaunch applies a fetched update.
The v2 cache is separate from v1. JSON is capped at 256 KiB, with at most 40 new
layers and 40 entries per override channel; use an app update beyond those limits.

In addition to existing ArcGIS/WFS/GeoJSON sources, v2 accepts these readers already
compiled into the app:

- `ogcapi`: HTTPS `base`, `collection`, optional `geometryProperty`.
- `arcgisImage`: HTTPS `base`, integer `layers` array.
- `wmsImage`: HTTPS `endpoint`, `wmsLayers`, optional supported `infoFormat`.

Image layers always remain live-only and excluded from radius/PDF feature results.
Respect the publisher's scale window; HWextrem starts at zoom 14 because its source
does not draw below 1:47,500. Never present a blank image as proof of no flood risk.

Each layer may declare `translations[locale][sourceKey]` for its own subgroup,
explainer and headline labels, with English fallback. It cannot invent general UI
catalogue keys. Shared data keys must have identical translation tables. Headline
labels should reuse existing translated labels where possible. `titleNoun`,
`costlyAtNationalScale`, `zeroIsMissing` and `squareMetresToHectares` preserve source
semantics. `offlineEstimates[layerId]` supplies positive integer decimal MB estimates
to every download total and warning; do not claim estimates are measured downloads.
New-layer text and estimates remain attached to cached definitions; existing-layer
corrections retain the 90-day expiry. No executable code is downloaded.

Before release, complete any publisher notice required by the reuse terms. The
Tirol notification was sent on 3 October 2026 with Leon's specific permission; the
private audit retains the sent-message receipt. This does not authorise other mail.

# smartknob-callback

Static https redirect target for the SmartKnob Spotify login.

Spotify only allows `http://` redirect URIs for loopback addresses, but the knob's
setup page is served over plain http from its LAN IP. Spotify therefore redirects
here, and this page sends the browser straight back to the knob.

- The knob's setup page puts `<random>~<knob host>` into the OAuth `state`.
- This page forwards `code`, `state` and `error` to `http://<knob host>/?spotify`.
- It only forwards to local-network hosts (10/8, 172.16/12, 192.168/16, 127/8,
  `localhost`, `*.local`), so a crafted link cannot send a code to the internet.
- No secrets live here; the Spotify client secret stays on the knob. The page loads
  no third-party resources and its inline script is pinned by a CSP hash.

Redirect URI to register in the Spotify developer dashboard:
`https://schmidsgo.github.io/smartknob-callback/`

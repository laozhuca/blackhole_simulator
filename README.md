# Black hole simulation

A real-time, ray-traced Schwarzschild black hole in a single WebGL page. Nothing to install or build.

Each pixel traces a light ray backward through curved spacetime, so you see:

- the black hole's shadow and the bright photon ring around it
- a thin accretion disk, with the far side lensed over and under the hole
- Doppler beaming and gravitational redshift (the approaching side of the disk is brighter and bluer)
- a starfield that bends near the hole

The **Hole spin** slider (0.9 by default) makes the hole spin. Light is then traced through the exact spacetime of a spinning (Kerr) black hole, so the shadow turns D-shaped and shifts sideways, flattened on the side spinning toward you. The disk's inner edge moves in to the innermost stable orbit for that spin, and the disk runs hotter and brighter because gas falling closer in releases more energy. Spin 0 gives a non-spinning hole.

Switch the scene to **Binary merger** to watch two black holes spiral together and merge into one. Their orbit shrinks as they lose energy to gravitational waves (Peters' formula), and both bend light at once. When the horizons touch, a single hole remains with 5% less mass. A strip chart shows the gravitational-wave signal: a rising chirp, then a short ringdown. The mass-ratio slider sets how unequal the two holes are.

Switch to **Hole + star** for a black hole orbiting a companion star, like an X-ray binary. The star fills its Roche lobe, so the hole's tides stretch it into a teardrop that points at the hole. Gas spills through the inner Lagrange point and streams onto the hole's accretion disk, which the hole's own Roche lobe cuts off at its outer edge. The star's tides drive two trailing spiral shocks through the outer disk, as mapped in real binaries such as IP Pegasi: the pattern stays lined up with the star and turns with the orbit while the gas streams through it, and the arms are hotter and brighter than the gaps between them. Like the microquasars SS 433, GRS 1915+105 and Cygnus X-1, the hole fires twin jets along the disk's spin axis. Magnetic fields launch them from the inner disk in a faint, wide funnel; they narrow and speed up with height, from 30% to 90% of the speed of light, and only shine brightly from about the disk's inner edge outward, where knots of plasma form. A faster-spinning hole powers brighter jets (the Blandford-Znajek process scales with spin squared) that start closer in, because its disk does. Relativistic beaming makes the jet tilted toward you far brighter and bluer than the one pointing away. Real jets switch on and off as the disk changes state; the **Relativistic jets** checkbox does the same. The star mass slider (taking the hole to be 10 solar masses) changes the star's size and temperature and where the stream starts and lands. The star is tidally locked and darker on the stretched side facing the hole. Its orbit is sped up so you can watch it.

**Space whale** is a fantasy scene. It opens on a close-up of the whale's eyes; the whale then swims off to the right and into a slow, bobbing loop around a spinning hole, its fins gently flapping (**Replay the opening** shows it again). The **Whale size** slider runs from 0.5× to 2×, plus a special 5×: the whale grows into a giant, circles the hole for ten seconds, then swims at it with its mouth wide open and swallows it, after which the hole glows on inside its belly. Moving the slider off 5× brings the hole back. The hole's disk is its light: warm, falling off with distance, and wrapping round the whale's outline when it is behind it, with only a trace of starlight on the shadowed side. It keeps its mouth closed, opening it wide for a moment every nine seconds or so. It is drawn with three.js from the same camera, and its picture is fed into the ray tracer at the whale's distance, so the hole hides it behind the shadow and bends its light into arcs when it swims behind. The model is `whale.glb` (made with Meshy AI); it has no skeleton or animation of its own, so the tail, fins and jaw are posed in the vertex shader. The model's mouth is modelled open, so the shader closes it by default.

## Run it

Open `index.html` in any browser with WebGL. The space whale needs the page served from a web server, such as GitHub Pages or `python3 -m http.server`, because browsers block loading the model from a local file; it also loads three.js from jsDelivr.

Drag to orbit; scroll or pinch to zoom. On an iPad or other touch screen, drag with one finger to orbit and pinch with two to zoom. The panel controls camera distance and inclination, disk size and brightness, time speed and render scale, and toggles Doppler effects, lensing and auto-orbit. Lower **Render scale** if it runs slowly.

## How it works

Units use the Schwarzschild radius `rs = 1`. A photon's path is integrated with the acceleration
`a = -1.5 h² r / |r|⁵`, where `h = |r × v|` is conserved. That one term reproduces the bending of light in Schwarzschild spacetime. For a spinning hole, rays are integrated exactly as null geodesics of the Kerr metric in Kerr-Schild coordinates (a Hamiltonian flow, midpoint steps). Since a spinning hole run backward in time is the same hole spinning the other way, each ray is traced forward in time around a hole of opposite spin, which lets it cross the horizon cleanly. The disk's inner edge is the Bardeen-Press-Teukolsky innermost stable orbit, and its temperature scales with the radiative efficiency to the 1/4 power. In the binary scene each hole contributes its own term, so light feels both. The binary keeps this non-spinning approximation, since there is no exact formula for two holes. In the star scene, the Roche-lobe sizes use Eggleton's fit and the inner Lagrange point uses Plavec and Kratochvil's; the star's own light bending is left out, because it is tiny next to the hole's. That is an approximation: real binary spacetime has no exact formula and needs numerical relativity. The disk runs from the innermost stable circular orbit (3 rs) outward, with a Novikov–Thorne-style temperature profile coloured as a blackbody.

## Music

Background music, *Misterio en el Agujero Negro* by junesiyu (made with Suno), is on by default. Browsers block sound until the visitor interacts with the page, so it starts at the first click or key press if it cannot start right away. The **♪** button in the panel header turns it off and on. The track is `music.mp3`; replace that file to use a different one.

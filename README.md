# Black hole simulation

A real-time, ray-traced Schwarzschild black hole in a single WebGL page. Nothing to install or build.

Each pixel traces a light ray backward through curved spacetime, so you see:

- the black hole's shadow and the bright photon ring around it
- a thin accretion disk, with the far side lensed over and under the hole
- Doppler beaming and gravitational redshift (the approaching side of the disk is brighter and bluer)
- a starfield that bends near the hole

## Run it

Open `index.html` in any browser with WebGL.

Drag to orbit, scroll to zoom. The panel controls camera distance and inclination, disk size and brightness, time speed and render scale, and toggles Doppler effects, lensing and auto-orbit. Lower **Render scale** if it runs slowly.

## How it works

Units use the Schwarzschild radius `rs = 1`. A photon's path is integrated with the acceleration
`a = -1.5 h² r / |r|⁵`, where `h = |r × v|` is conserved. That one term reproduces the bending of light in Schwarzschild spacetime. The disk runs from the innermost stable circular orbit (3 rs) outward, with a Novikov–Thorne-style temperature profile coloured as a blackbody.

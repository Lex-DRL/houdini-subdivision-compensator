# Subdivision compensator for Houdini

If you have a low- or mid-poly model made as a retop of highpoly sculpt, you may want to smooth it (either in render-time or for some other reasons).
But unfortunately, when you do so, the mesh shrinks and no longer matches the original highpoly. Most of the time the smoothed lowpoly doesn't even intersect the sculpt.

This node allows you to offset lowpoly's vertices in such a way that it will match highpoly **after smoothing (subdividing)**.
Essentially, it's kinda the opposite of "smooth the mesh then remove any newly created vertices".

![Base mesh screenshot](/../screenshots/screenshots/0-base.png?raw=true "Base mesh") ![Base mesh subdivided screenshot](/../screenshots/screenshots/0-smoothed.png?raw=true "Base mesh subdivided")
![Compensated mesh screenshot](/../screenshots/screenshots/1-baseCompensated.png?raw=true "Compensated mesh") ![Compensated mesh subdivided screenshot](/../screenshots/screenshots/1-smoothedCompensated.png?raw=true "Compensated mesh subdivided")

Limitations:
* Unfortunately, only Houdini's "Mantra Catmull-Clark" is supported due to some technical limitations _(houdini doesn't provide an easy way to track down the original points after subdividing the mesh)_.
* The node works iteratively, subdividing and offsetting the lowpoly many times. So it's not intended to be re-calculated in every frame. Instead, it's designed to generate the "subdivision-ready" mesh once and manipulate it afterwards.

If you think some important features are still missing, feel free to create a pull request. :)

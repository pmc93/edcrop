# Introduction

Evapotranspiration is one of the major components of Earth’s water balance, being the sum of evaporation
and plant transpiration from the land and ocean surface. Factors that affect evapotranspiration includes
solar radiation, wind, humidity, temperature, growth stage of vegetation, and water availability. The latter
depends on factors such as precipitation, irrigation, and soil characteristics.

Local- or field-scale evapotranspiration can be measured by a weighing lysimeter, the energy balance
Bowen-ratio method, or the eddy covariance technique, but these instruments and methods are expensive,
may be susceptible to errors, or require correction (Healy, 2010). Alternatively, field-scale
evapotranspiration can be estimated from climatic data by simulating the water balance of an area with a
specific vegetation growing on a specific soil. This report documents a code (a package), programmed in
Python and named Edcrop, which can do such local simulations for various types of soil and vegetation. It
does not simulate surface flow, lateral flow, nor flow processes taking place in the saturated zone (e.g. loss
of water to drains). The water balance equation of Edcrop is therefore simply


where P is precipitation (possibly including irrigation), Ea is actual evapotranspiration, D is downward
drainage to the unsaturated zone, and ∆V is change in water storage. Evapotranspiration includes
evaporation of snow, evaporation of intercepted water, evaporation of soil water, and plant transpiration.
∆V includes change in snow pack, change in intercepted water, and change in water content in the root
zone and in the subzone. The subzone is the zone between the bottom of the root zone and the bottom of
the model’s soil profile.

The conceptual model implemented in Edcrop is a modification of the Evacrop model by Olesen and
Heidmann (2002), which itself builds on the Watcros model by Aslyng and Hansen (1982). The Edcrop
conceptualization is based on considerations regarding the physical processes that are important for
turning precipitation and irrigation into either evaporation, transpiration, or drainage from the root zone:
Temperature determines whether precipitation falls as rain or snow, and it determines when snow thaws
and infiltrates. The vegetation intercepts a part of precipitation, while the rest infiltrates into the ground.
The infiltrated water will either evaporate, be absorbed by plant roots, be stored in the soil, or drain from
the root zone. Potential evaporation is distributed between vegetation and soil, where the former part
drives evaporation of intercepted water and plant transpiration from the green leaf area, while the latter
part drives evaporation from the soil. The soil’s ability to store water depends on its field capacity; when
the water content exceeds field capacity, water will gradually drain downwards. Furthermore, it is assumed
that the annual life cycle of crops and wetland vegetation can be described by growing degree-days alone,
while for forests the life cycle is described by a calendar. For irrigation, either (i) date and amount are input,
or (ii) they are determined automatically by Edcrop using certain criteria.

There are two alternative soil water balance functions to choose between in Edcrop. The first alternative is
an almost straight copy of the function used in the original Evacrop code by Olesen and Heidmann (2002),
simulating flow through the soil profile as flow through two linear reservoirs using daily time steps.
However, it can simulate macro-pore drainage, which the original Evacrop cannot. The second alternative
simulates flow through the soil profile as flow through four linear or nonlinear reservoirs using daily or subdaily time steps. For nonlinear reservoirs, Edcrop uses Mualem – van Genuchten like functions. It also
simulates gravity driven macro-pore flow as well as surface runoff.

As input, given in text files, Edcrop requires daily temperature, precipitation, and reference
evapotranspiration. It also requires information about combination(s) of soil type and vegetation type to
simulate. One can choose between seven default soil types and fifteen default vegetation types, or one can
manually input information for other types of soil or vegetation. In a single model run, Edcrop can loop
through lists of climate files, soils, and vegetation.
The seven default soil types vary from coarse sandy soil to clayey soil. The fifteen default vegetation types
include bare soil, ten types of crop, two types of forest, and two types of wetland.
As said, the water balance simulation of Edcrop is similar to that of Evacrop (Olesen and Heidmann, 2002),
but in other ways Edcrop is different from Evacrop. Edcrop allows more flexible and easier specification of
input and output; it can loop through lists of climate, soil, and vegetation combinations in a single model
run; it simulates macro-pore drainage; it contains more crops than Evacrop; it contains forest and wetland
types, which are new compared to Evacrop; it has a more advanced irrigation module; and data and results
can be plotted.

Edcrop cannot simulate capillary rise of shallow groundwater to the root zone or surface. If downward
drainage (just called drainage in the following) simulated by Edcrop is to be used as recharge input for a
groundwater model, there can be ways to partly correct for this lack of Edcrop ability. For example, for
simulation of groundwater flow using Modflow (McDonald and Harbaugh, 1988), drainage from Edcrop can
be used as recharge input for the Modflow RCH package, while the difference between Edcrop’s potential
evapotranspiration and actual evapotranspiration can be used as maximum ET input for the Modflow EVT
package. Similar can be done using newer versions of Modflow.

In the following, Chapter 2 instructs how to install and run Edcrop. Chapter 3 gives details about the
Evacrop conceptual model and the equations used for this by Edcrop. Chapter 4 gives details about the
alternative soil water balance model of Edcrop. Chapter 5 supplemented by the Tables of Chapter 7 give
the input instructions. Chapter 6 explains the output files. Chapter 8 gives the list of references. Appendix A
compares results obtained by using the alternative water balance functions of Edcrop with alternative
settings. Appendix B illustrate similarities and differences in simulation results obtained by the simpler
Edcrop code and the more advanced code named Daisy (Hansen et al., 1990), respectively.

## What is MyST?

MyST stands for "Markedly Structured Text". It
is a slight variation on a flavor of markdown called "CommonMark" markdown,
with small syntax extensions to allow you to write **roles** and **directives**
in the Sphinx ecosystem.

For more about MyST, see [the MyST Markdown Overview](https://jupyterbook.org/content/myst.html).

## Sample Roles and Directives

Roles and directives are two of the most powerful tools in Jupyter Book. They
are kind of like functions, but written in a markup language. They both
serve a similar purpose, but **roles are written in one line**, whereas
**directives span many lines**. They both accept different kinds of inputs,
and what they do with those inputs depends on the specific role or directive
that is being called.

Here is a "note" directive:

```{note}
Here is a note
```

It will be rendered in a special box when you build your book.

Here is an inline directive to refer to a document: {doc}`markdown-notebooks`.


## Citations

You can also cite references that are stored in a `bibtex` file. For example,
the following syntax: `` {cite}`holdgraf_evidence_2014` `` will render like
this: {cite}`holdgraf_evidence_2014`.

Moreover, you can insert a bibliography into your page with this syntax:
The `{bibliography}` directive must be used for all the `{cite}` roles to
render properly.
For example, if the references for your book are stored in `references.bib`,
then the bibliography is inserted with:

```{bibliography}
```

## Learn more

This is just a simple starter to get you started.
You can learn a lot more at [jupyterbook.org](https://jupyterbook.org).

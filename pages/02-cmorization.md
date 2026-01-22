---
transition: slide-left
name: cmorization
zoom: 0.9
---

# What is CMORization?

The process of <mark>converting climate model output data</mark> into a
<mark>standardized format</mark>, in accordance with <mark>rules</mark> set by the
Climate Model Intercomparison Projects (<mark>CMIP</mark>) and
<mark>CF Conventions</mark>, ensuring <mark>consistency</mark> in
<mark>variable-names</mark>, <mark>units</mark>, <mark>metadata</mark>, and
<mark>file structure</mark> for easier analysis and comparison across different
models.

For `pycmor` it means to provide compliance for the following

<div class="grid grid-cols-2 gap-4">

<div>

**CF Conventions**

- Ensure metadata is set
  - coordinate attributes
  - variable attributes
  - global attributes

</div>

<div>

**CMIP6/CMIP7 specification + Controlled Vocabulary**

- Ensure file structure
  - file(s) naming
  - directory structure
- match variable units
- match temporal resolution
- match dimensions
- bounds (time_bnds, lat_bnds, ...)

</div>

</div>

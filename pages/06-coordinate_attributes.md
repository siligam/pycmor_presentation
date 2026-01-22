---
name: coordinate attributes
transition: slide-left
---

<div class="grid grid-cols-2 gap-x-4">
  <div>

# Coordinate Attributes


Make your coordinates CF-compliant automatically

Eaxmple: no attribute information

```py {all|5,9,11,15,16}
import xarray as xr
import numpy as np

# Dataset with coordinates
ds = xr.Dataset(
    { 'tas': (['time', 'lat', 'lon'],
             np.random.rand(10, 90, 180)),
    },
    coords={
    'time': np.arange(10),
    'lat': np.linspace(-89.5, 89.5, 90),
    'lon': np.linspace(0.5, 359.5, 180),
})

print(ds.lat.attrs)
{}
```

  </div>
  <div>

`pycmor` provides <span v-mark.box.yellow="2">`set_coordinate_attributes`</span>

In a processing pipeline (`yaml` config):

```yaml {all|5|all}
pipelines:
  steps:
    - "load_mfdataset"
    # ... other steps
    - "set_coordinate_attributes" # Add this step
    # ... other steps
```

In scripts:

  <div class="scroll-box">

```py {all|4,5,7,8,9}
from pycmor.std_lib.coordinate_attributes import set_coordinate_attributes

# Now coordinates have CF-compliant metadata
ds = set_coordinate_attributes(ds, rule)
ds['lat'].attrs
{
  'standard_name': 'latitude',
  'units': 'degrees_north',
  'axis': 'Y',
}
```

  </div>
  </div>
</div>

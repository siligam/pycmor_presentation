---
layout: default
name: pipelines
zoom: 0.8
---

# Pipeline Steps

<div class="grid grid-cols-2 gap-x-4">
  <div>

### Default Steps in Pipeline

PyCMOR provides these standard processing steps.



<div class="text-sm text-gray-600 mt-4">


```python
STEPS = (
    "pycmor.core.gather_inputs.load_mfdataset",
    "pycmor.std_lib.generic.get_variable", 
    "pycmor.std_lib.add_vertical_bounds",
    "pycmor.std_lib.timeaverage.timeavg",
    "pycmor.std_lib.units.handle_unit_conversion",
    "pycmor.std_lib.attributes.set_global",
    "pycmor.std_lib.attributes.set_variable",
    "pycmor.std_lib.attributes.set_coordinates",
    "pycmor.std_lib.dimensions.map_dimensions",
    "pycmor.core.caching.manual_checkpoint",
    "pycmor.std_lib.generic.trigger_compute",
    "pycmor.std_lib.generic.show_data",
    "pycmor.std_lib.files.save_dataset",
)
```
</div>
</div>
<div>

### Adding Custom Steps

#### 1. Create Custom Function

```python
# custom_step.py
def custom_step(data, rule):
    # Your custom processing logic
    return data
```

<div style="margin-bottom: 1rem;"></div>

#### 2. Define Complete Pipeline

**Important**: When adding custom steps, you must specify the **entire pipeline** including both default and custom steps:

```yaml
pipelines:
  - name: my_custom_pipeline
    steps:
      - "pycmor.core.gather_inputs.load_mfdataset"
      - "pycmor.std_lib.generic.get_variable"
      # ... other default steps ...
      - "script://path/to/custom_step.py:custom_step"
      - "pycmor.std_lib.files.save_dataset"
```

<div style="margin-bottom: 1rem;"></div>

#### 3. Key Points

- Custom steps require full pipeline specification
- Mix default steps with your custom functions  
- Use `script://path/to/file:function_name` syntax

</div>
</div>
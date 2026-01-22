---
layout: default
title: Frequency inference examples
name: infer frequency
zoom: 0.7
transition: slide-left
---

# Frequency Analysis & Processing

<div class="grid grid-cols-2 gap-x-2">

<div>

PyCMOR analyzes **source data frequency** and processes it to meet **CMIP table requirements**.

**Time averaging** (CMIP-aware):

  * Driven by CMIP table frequency string
  * **Methods**
    * Instantaneous → `resample(...).first()`
    * Mean → `resample(...).mean()`
    * Climatology → `groupby(...).mean("time")`

**Key principles:**

  * ✅ **Downsampling supported** (no artificial data creation)
    * `Daily → Monthly`, `6-hourly → Daily`, `3-hourly → 6-hourly`
  * ❌ **No upsampling** — missing resolution is never invented

**Timestamp adjustment in output files** (`adjust_timestamp`)
  * Keywords: `first` | `middle` | `last`
  * Literal offset: `14days`
  * Fractional: `0.1 … 0.9`
  * **Default**: `first`



</div>

<div>

````md magic-move { lines: false }
```python
>>> # Month start dates (exact month-start)
>>> month_start = np.array([
...    "2020-01-01",
...    "2020-02-01",
...    "2020-03-01",
...    "2020-04-01",
...    "2020-05-01",
... ]).astype("datetime64[s]")
>>>
>>> xarray.infer_freq(month_start)
'MS'
>>> infer_frequency(month_start, return_metadata=True, log=True)
Inferred Frequency : MS
Regular Spacing    : ✅
Status             : valid
```

```python
>>> # Mid-month dates (15th of each month)
>>> month_offset = np.array([
...    "2020-01-15",
...    "2020-02-15",
...    "2020-03-15",
...    "2020-04-15",
...    "2020-05-15",
... ]).astype("datetime64[s]")
...
>>> xarray.infer_freq(month_offset)
None
>>> infer_frequency(month_offset, return_metadata=True, log=True)
Inferred Frequency : M
Median Δ (days)    : 30.50
Regular Spacing    : ✅
Status             : valid
```

```python
>>> # Month start dates with day offsets
>>> month_start_day_offset = np.array([
...    "2020-01-01",
...    "2020-02-01",
...    "2020-03-04",  # <- 3-day offset
...    "2020-04-01",
...    "2020-05-01",
... ]).astype("datetime64[s]")
...
>>> xarray.infer_freq(month_start_day_offset)
None
>>> infer_frequency(month_start_day_offset, return_metadata=True)
Inferred Frequency : M
Median Δ (days)    : 30.50
Regular Spacing    : ✅
Status             : valid   # <- below threshold limit
>>>
>>> infer_frequency(month_start_day_offset, return_metadata=True, strict=True)
Inferred Frequency : M
Regular Spacing    : ❌
Strict Mode        : ✅
Status             : irregular
```
````

**`infer_frequency` detects:**

* Frequency, regularity, gaps
* **`strict` mode** is useful to catch subtle temporal inconsistencies
  
`infer_frequency` is also available as a xarray accessor `ds.pycmor.infer_frequency(...)`

</div>

</div>

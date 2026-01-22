---
name: units
transition: slide-left
zoom: 0.7
---

# Units Handling in PyCMOR

<div class="grid grid-cols-2 gap-x-3">

<div>

## 🔬 Chemical units (element-aware)

**Automatic conversion for complex chemical units**

**Example:** `mmolC → kg`

**Previously (manual):**
```text
mmolC → molC → gC → kgC
   ÷1e3   ×12.0107   ÷1e3
```

**Now (automatic):**
```bash
# Live conversion log
2025-03-13 09:06:37 | INFO  | Converting: mmolC/m2/d → kg m-2 s-1
2025-03-13 09:06:37 | DEBUG | Chemical element detected: Carbon
2025-03-13 09:06:37 | DEBUG | Registering: molC = 12.0107 * g
```

✔ No manual molecular-weight handling  
✔ CMIP-compliant physical units

</div>

<div>

## 📝 Unit configuration

<br>

### Wrong units in source data?
→ Define correct units in `model_unit` field in `yaml` file

### Dimensionless units?
→ Map them explicitly

```yaml
# Conversion-only mappings
# Output always uses cmor_units
so:
  "0.001": g/kg

intpp:        # Primary production by phytoplankton
  "mol m-2 s-1": "molC m-2 s-1"
```

<div class="flex items-center justify-center mt-2">
  <img src="/units_handling.png" style="max-width: 75%; height: auto; max-height: 280px;" />
</div>

</div>

</div>

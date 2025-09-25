
- Works for some CMIP models
```
# Create the target grid (1°x1° global)
ds_out = xr.Dataset({
    'lat': (['lat'],  np.arange(-89.5, 90.5, 1.0)),
    'lon': (['lon'],  np.arange(0.5, 360.5, 1.0)),
})

# Create regridder (uses bilinear interpolation by default)
regridder = xe.Regridder(ds_native, ds_out, method='bilinear', periodic=True)

# Apply regridding to a variable, e.g., sea surface temperature
tos_regridded = regridder(ds_native['tos'])

```

- Works for other CMIP models when above doesn't :/
- Will need to check grid_in names
```

tos_subset = earth3

ds_native = tos_subset

grid_in = xr.Dataset({
    'lat': (['j', 'i'], earth3['latitude'].values),
    'lon': (['j', 'i'], earth3['longitude'].values),
})

# Create the target grid (1°x1° global)
ds_out = xr.Dataset({
    'lat': (['lat'],  np.arange(-89.5, 90.5, 1.0)),
    'lon': (['lon'],  np.arange(0.5, 360.5, 1.0)),
})

# Create regridder (uses bilinear interpolation by default)
regridder = xe.Regridder(grid_in, ds_out, method='bilinear', periodic=False, ignore_degenerate=True)

# Apply regridding to a variable, e.g., sea surface temperature
tos_regridded = regridder(ds_native)
```


# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.5.0] - 2018-01-09
### Added
- Two methods `fill` and `border` taking an astropy.wcs.WCS and a matplotlib axis. `fill` projects the MOC into the WCS and draws it on the MPL axis using pathpatches for each HEALPix cell. `border` draws the border the same way and requires a WCS and an MPL axe too. You can pass to these functions additional keyword arguments that will directly be passed to MPL when plotting (e.g. the color, the linewidth, and alpha component etc...). Check the notebooks to see how to use these new methods.
- You can retrieve the list of skycoords describing the border MOC. Each skycoord from the list refers to one border of the MOC (either an external border or the border of a hole in a connexe MOC). The process takes for the moment a quite amount of time and thus may be optimized in the future. A new GALEX boundaries notebook has been added so that you can check how it works. I recommend to decrease the order of GALEX to 5 before computing the boundaries otherwise it will take some time. This add relies on the issue [#29](https://github.com/cds-astro/mocpy/issues/29) initiated by [@ggreco77](https://github.com/ggreco77).
- A new `serialize` public method allows to serialize the MOC in two possible format, FITS and json. For a FITS serialization the method returns an astropy HDU binary table. For a JSON serialization, the method returns a python dictionary storing order-[list of HEALPix cells] as key-value pairs.

### Changed
- `write` method does not take a `write_to_file` argument. For serialization purpose, there is now a new `serialize` method.
- astropy_healpix.HEALPix.lonlat_to_healpix seems to not accept astropy MaskedColumn anymore. For lon as a MaskedColumn, please pass lon.T * u.deg to mocpy.MOC.from_lonlat. We need to transpose the column and then convert it to an astropy.units.Quantity.
- Notebooks have been updated and all the plots now use the new methods `fill` and `border`.
- A new package `spatial`, invisible from the user, but keeping all the code of spatial   MOCs (plotting methods, border computation, special utils for creating WCS...) has been created. tmocs and core functions are still located in the root of the project.
- Add of a changelog
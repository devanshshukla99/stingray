v2.0 beta (2024-01-31)
----------------------

New Features
^^^^^^^^^^^^
- Power colors à la Heil et al. 2015 (`#780 <https://github.com/StingraySoftware/stingray/pull/780>`__)
- Calculate colors and intensities on a segment-by-segment basis in event lists (`#781 <https://github.com/StingraySoftware/stingray/pull/781>`__)
- A function to randomize data in small bad time intervals (`#782 <https://github.com/StingraySoftware/stingray/pull/782>`__)
- The Lomb Scargle Fourier Transform (fast and slow versions) and the corresponding :class:`LombScargleCrossspectrum` and :class:`LombScarglePowerspectrum` (`#737 <https://github.com/StingraySoftware/stingray/pull/737>`__)
- A JAX implementation of the Gaussian Process tool by `Hubener et al <https://arxiv.org/abs/2205.12716>`_
  for QPO detection and parameter analysis. (`#739 <https://github.com/StingraySoftware/stingray/pull/739>`__)
- Extend join operation for events to arbitrary array attributes, not just pi and energy (`#742 <https://github.com/StingraySoftware/stingray/pull/742>`__)
- Allow the creation of empty light curves. (`#745 <https://github.com/StingraySoftware/stingray/pull/745>`__)
- Make StingrayTimeseries into a generalized light curve, with a less strict naming but implementing much of the underlying computing useful for Lightcurve as well. (`#754 <https://github.com/StingraySoftware/stingray/pull/754>`__)
- Our fast implementation of histograms is now safer (failing safely to the equivalent numpy histogram functions), more consistent (ranges moved to range, for consistency with numpy), and accept complex weights as well! (`#764 <https://github.com/StingraySoftware/stingray/pull/764>`__)

Bug Fixes
^^^^^^^^^

- When rms is low, the calculation in compute_rms often gave `NaN`. We now check for this situation and give 0 with an uncertainty as a result. (`#736 <https://github.com/StingraySoftware/stingray/pull/736>`__)
- Eliminates deprecated call to `enable_deprecations_as_warnings`, and contextually, changes the code to be much more robust in catching harmful warnings. (`#738 <https://github.com/StingraySoftware/stingray/pull/738>`__)
- Changes Crossspectrum.plot() function to plot the actual real and imaginary parts instead of their absolute values. (`#747 <https://github.com/StingraySoftware/stingray/pull/747>`__)
- Make commits marked as [docs only] skip all CI but the docs build (`#749 <https://github.com/StingraySoftware/stingray/pull/749>`__)
- Update tstart and tseg when using Lightcurve.truncate() (`#753 <https://github.com/StingraySoftware/stingray/pull/753>`__)
- Changed list comprehension to generator expression to reduce memory usage. (`#756 <https://github.com/StingraySoftware/stingray/pull/756>`__)
- Fix a bug with segment sizes not exact multiples of dt when dealing with light curves (`#760 <https://github.com/StingraySoftware/stingray/pull/760>`__)
- Fix a bug when light curve segments contain complex values (`#760 <https://github.com/StingraySoftware/stingray/pull/760>`__)
- Crossspectrum had "real" as default value. This meant that, for example, lags could not be calculated. Now the default value is "all", as it should be. (`#762 <https://github.com/StingraySoftware/stingray/pull/762>`__)
- Fix plotting of spectra, avoiding the plot of imaginary parts of real numbers (`#763 <https://github.com/StingraySoftware/stingray/pull/763>`__)
- Various bugfixes in `gti.py`, and a new function to interpret the mix of multiple GTIs. (`#774 <https://github.com/StingraySoftware/stingray/pull/774>`__)
- Fixed subcs duplication by adding a check in the for loop that copies the attributes from table's meta items. (`#776 <https://github.com/StingraySoftware/stingray/pull/776>`__)
- Various bug fixes in DynamicalPowerspectrum, on event loading and time rebinning (`#779 <https://github.com/StingraySoftware/stingray/pull/779>`__)
- Fix issue with the Poisson noise calculation in lag spectra, that produced NaN errors under some conditions (`#789 <https://github.com/StingraySoftware/stingray/pull/789>`__)
- Fix rms computation and error bars (`#792 <https://github.com/StingraySoftware/stingray/pull/792>`__)
- Fix issue with ``Powerspectrum`` of a single light curve (`#663 <https://github.com/StingraySoftware/stingray/pull/663>`__)

Breaking Changes
^^^^^^^^^^^^^^^^

- Eliminate deprecated ``format_`` keyword from read and write methods. (`#729 <https://github.com/StingraySoftware/stingray/pull/729>`__)
- Remove legacy interface and obsolete large data machinery. (`#755 <https://github.com/StingraySoftware/stingray/pull/755>`__)
- Eliminate deprecated ``white_noise_level`` keyword from ``compute_rms``. (`#792 <https://github.com/StingraySoftware/stingray/pull/792>`__)


Internal Changes
^^^^^^^^^^^^^^^^

- Speedup creation of events in ``EventList.from_lc`` (`#757 <https://github.com/StingraySoftware/stingray/pull/757>`__)
- Separate slow tests from quick ones (`#758 <https://github.com/StingraySoftware/stingray/pull/758>`__)
- Use Readthedocs for documentation building (`#769 <https://github.com/StingraySoftware/stingray/pull/769>`__)
- More informative GTI messages (`#787 <https://github.com/StingraySoftware/stingray/pull/787>`__)


v1.1.2 (2023-05-25)
-------------------

New Features
^^^^^^^^^^^^

- Phase Dispersion Minimization as a method to search for periodic signals
  in data is now implemented in the ``stingray.pulse`` submodule. To use it,
  you can use the ``phase_dispersion_search`` function in
  ``stingray.pulse.search``. The accompanying statistical tests are located
  in the ``stingray.stats`` module, under ``phase_dispersion_probability``,
  ``phase_dispersion_logprobability`` and ``phase_dispersion_detection_level``. (`#716 <https://github.com/StingraySoftware/stingray/pull/716>`__)
- Add is_sorted function, to test if an array is sorted. (`#723 <https://github.com/StingraySoftware/stingray/pull/723>`__)
- Check if invalid data are inside GTIs, and warn or raise exception accordingly (`#730 <https://github.com/StingraySoftware/stingray/pull/730>`__)


Bug Fixes
^^^^^^^^^

- The method apply_gtis of the class Lightcurve is applied to all the attributes of the class Lightcurve.
  This works for both inplace=True and inplace=False (`#712 <https://github.com/StingraySoftware/stingray/pull/712>`__)
- Avoid allocation of an unneeded square matrix to improve memory management in ``_als`` (fix Issue 724) (`#725 <https://github.com/StingraySoftware/stingray/pull/725>`__)
- Fix Issue #726 -- Loading events without fmt keyword crashes (`#727 <https://github.com/StingraySoftware/stingray/pull/727>`__)


Documentation
^^^^^^^^^^^^^

- Reordered information about contributions with new ``black`` and ``towncrier`` procedures (`#721 <https://github.com/StingraySoftware/stingray/pull/721>`__)


Internal Changes
^^^^^^^^^^^^^^^^

- Using `towncrier <https://github.com/hawkowl/towncrier>`__ to generate the changelogs. (`#697 <https://github.com/StingraySoftware/stingray/pull/697>`__)
- Added stingray's logo in the documentation's favicon and top bar. (`#707 <https://github.com/StingraySoftware/stingray/pull/707>`__)
- Improved contributing workflow by appending ``black`` codestyle configuration to ``pyproject.toml`` and ignoring PEP-8 non-compliant ``E203``, ``W503`` in ``flake8``. (`#715 <https://github.com/StingraySoftware/stingray/pull/715>`__)
- Added a scrollbar to sidebarwrapper (`#718 <https://github.com/StingraySoftware/stingray/pull/718>`__)
- Simplify numba mocking code, and possibly improve code coverage estimate (`#731 <https://github.com/StingraySoftware/stingray/pull/731>`__)


v1.1.1 (2022-10-10)
-------------------
Bug fixes
^^^^^^^^^
- Fixed ``white_noise_offset`` in ``compute_rms`` to 2.0, as it should be
- Fixed a bug that produced a crash when calculating the rms in spectra corrected through the FAD technique
- Fixed a bug that eliminated the imaginary part from cross spectra corrected with the FAD
- Fixed a bug that considered contiguous GTIs as non-continuous (due to very small differences between stop and start of the next GTI) by allowing a small tolerance

`Full list of changes`__

__ https://github.com/StingraySoftware/stingray/compare/v1.1...v1.1.1


v1.1 (2022-10-02)
-----------------
Bug fixes
^^^^^^^^^
- IMPORTANT: Fixed sign of time lags, which were calculated using the interest band as the reference.
- Fixed an issue when the fractional exposure in FITS light curves is slightly >1 (as sometimes happens in NICER data)

New
^^^
- Implemented the ``bexvar`` variability estimation method for light curves.

Improvements
^^^^^^^^^^^^
- A less confusing default value of segment_size in Z searches

`Full list of changes`__

__ https://github.com/StingraySoftware/stingray/compare/v1.0...v1.1

v1.0 (2022-03-29)
---------------------
TL,DR: these things will break your code with v1.0:

- Python version < 3.8
- The ``gtis`` keyword in `pulse/pulsar.py` (it is now ``gti``, without the 's')

New
^^^
- Dropped support to Python < 3.8
- Multi-taper periodogram, including a Lomb-Scargle implementation for non-uniformly sampled data
- Create count-rate spectrum when calculating spectral-timing products
- Make modlation upper limit in ``(Averaged)Powerspectrum`` work with any normalization (internally converts to Leahy for the calculation)
- Implement Gardner-Done normalization (1 for perfect correlation, -1 for perfect anticorrelation) for ``Auto/Crosscorrelation``
- New infrastructure for converting ``EventList`` and ``LightCurve`` objects into Astropy ``TimeSeries``
- New infrastructure for converting most Stingray classes into Astropy ``Table`` objects, Xarray and Pandas data frames.
- Save and load of most Stingray classes to/from many different file formats (``pickle``, ``ECSV``, ``HDF5``, ``FITS``, and all formats compatible with Astropy Table)
- Accept input ``EventList`` in ``DynamicalPowerSpectrum``
- New ``stingray.fourier`` module containing the basic timing products, usable on ``numpy`` arrays, and centralizes fft import
- New methods in ``Crossspectrum`` and ``Powerspectrum`` to load data from specific inputs: ``from_events``, ``from_lightcurve``, ``from_time_array``, ``from_lc_list`` (``from_time_array`` was also tested using memory-mapped event lists as inputs: useful in very large datasets)
- New and improved spectral timing methods: ``ComplexCovarianceSpectrum``, ``CovarianceSpectrum``, ``LagSpectrum``, ``RmsSpectrum``
- Some deprecated features are now removed
- ``PSDLogLikelihood`` now also works with a log-rebinned PDS

Improvements
^^^^^^^^^^^^
- Performance on large data sets is VASTLY improved
- Lots of performance improvements in the ``AveragedCrossspectrum`` and ``AveragedPowerspectrum`` classes
- Standardized use of new fast psd/cs algorithm, with ``legacy`` still available as an alternative option to specify
- Reading calibrated photon energy from event files by default
- In ``pulse/pulsar.py``, methods use the keyword ``gti`` instead of ``gtis`` (for consistency with the rest of Stingray)
- Moved ``CovarianceSpectrum` to ``VarEnergySpectrum`` and reuse part of the machinery
- Improved error bars on cross-spectral and spectral timing methods
- Measure absolute rms in ``RmsEnergySpectrum``
- Friendlier ``pyfftw`` warnings
- Streamline PDS/CrossSp production, adding ``from_events``, ``from_lc``, ``from_lc_iterable``, and ``from_time_array`` (to input a numpy array) methods
- PDS/CrossSp initially store the unnormalized power, and convert it on the fly when requested, to any normalization

Bug fixes
^^^^^^^^^
- Fixed error bars and ``err_dist`` for sliced (iterated) light curves and power spectra
- Fixed a bug in how the start time when applying GTIs (now using the minimum value of the GTI array, instead of half a time bin below the minimum value)
- Fixed a bug in which all simulator errors were incorrectly non-zero
- Fixed coherence uncertainty
- Documented a Windows-specific issue when large count rate light curves are defined as integer arrays (Windows users should use ``float`` or specify ``int-64``)
- If the variance of the lightcurve is zero, the code will fail to implement Leahy normalization
- The value of the ``PLEPHEM`` header keyword is forced to be a string, in the rare cases that it's a number
- and more!

`Full list of changes`__

__ https://github.com/StingraySoftware/stingray/compare/v0.3...v1.0

v1.0beta was released on 2022-02-25.

v0.3 (2021-05-31)
-----------------

- Lots of performance improvements
- Faster simulations
- Averaged Power spectra and Cross spectra now handle Gaussian light curves correctly
- Fixes in rebin functions
- New statistical functions for signal detection in power spectra and pulsar search periodograms
- Much improved FTOOL-compatible mission support
- New implementation of the FFTFIT method to calculate pulsar times of arrival
- H-test for pulsar searches
- Z^2_n search adapted to binned and normally distribute pulse profiles
- Large data processing (e.g. from NICER) allowed
- Rebinning function now accepts unevenly sampled data
- New saving and loading from/to Astropy Tables and Timeseries
- Improved I/O to ascii, hdf5 and other formats
- Rehaul of documentation

`Full list of changes`__

__ https://github.com/StingraySoftware/stingray/compare/v0.2...v0.3

v0.2 (2020-06-17)
-----------------

- Added Citation info
- Fixed various normalization bugs in Powerspectrum
- Speedup of lightcurve creation and handling
- Made code compatible with Python 3.6, and dropped support to Python 2.7
- Test speedups
- Dead time models and Fourier Amplitude Difference correction
- Roundtrip of LightCurve to lightkurve objects
- Fourier-domain accelerated search for pulsars
- Adapt package to APE-17
- Periodograms now also accept event lists (instead of just light curves)
- Allow transparent MJDREF change in event lists and light curves

`Full list of changes`__

__ https://github.com/StingraySoftware/stingray/compare/v0.1.3...v0.2

v0.1.3 (2019-06-11)
-------------------

- Bug fixes

v0.1.2
------

- Bug fixes

v0.1.1
------

- Bug fixes

v0.1 (2019-05-29)
-----------------

- Initial release.

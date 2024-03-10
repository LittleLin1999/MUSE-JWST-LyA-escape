# MUSE-JWST: The escape of Lyα at the end of Reionization
We present the data and results in Lin et al. 2023, which explores the escape of Lyα at the end of Reionization (z=5-6) using VLT/MUSE and JWST NIRCam/WFSS.



- FRESCO-GOODSS_HAE.fits: The full HAE catalog and detailed properties as described in Section 2 of Lin et al. 2024. For convenience, we also provide the catalogs in the form of `ascii.mrt` 

  - fescLyA_HAE_GOODSS_C00.dat: The HAE properties and LyA escape fraction assuming Calzetti00 dust extinction law.
  - fescLyA_HAE_GOODSS_SMC.dat: The HAE properties and LyA escape fraction assuming SMC dust extinction law.


- fescLya_stack_C00.h5: stacked LyA escape fraction in different property bins, assuming Calzetti dust extinction law.
- fescLya_stack_SMC.h5: stacked LyA escape fraction in different property bins, assuming SMC dust extinction law. 



- The structure of the h5 files:

  - There are three populations: `All` (all HAE in the sample),  `LAE` (subsample with LyA detected in MUSE), `non-LAE` (subsample without LyA detection)

  - For every population, we split the sample into five equally-sized bins based on a specific physical properties. We stack  the MUSE datacube in each bin and measure the stacked LyA. By **normalizing each datacube based on the corresponding dust-corrected, intrinsic Ha flux, we get fesc_int**, i.e. the one we analyze in this work.  Additionally, we also normalize the cubes based on the observed Ha, yielding fesc_obs here as supplement. 

  - There are two methods for LyA measurements: `model` and `upperlim`

    - `model`: the total LyA flux is measured by fitting the line profiles with Skewed Gaussian models. Usually in `ALL` and `LAE` stack result.
    - `nondet`: no emission feature is seen in the stack cube so we 'forced'-measure the flux with a +- 1000 km/s window around LyA based on the Ha-based redshift.

  - Example: if you want to load the $f_{\rm Ly\alpha}$ of *all HAEs* in $A_V$ bins, you can read the h5 in `python` as follows:

    ```python
    import h5py
    
    stack_C00 = h5py.File('fescLya_stack_C00.h5', 'r')
    
    # load the parameter values
    Av =  stack_C00['All']['Av']['pars'][:]
    Av_err = stack_C00['All']['Av']['pars_err'][:]
    
    # load the corresponding fesc_Lya 
    fesc = stack_C00['All']['Av']['fesc_int'][:]
    fesc_err = stack_C00['All']['Av']['fesc_int_err'][:]
    ```
    
    



The structure of the h5 files:

```html
├── All 
│   ├── Av
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── LUV_att
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── LUV_int
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── Ms
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── beta_obs
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── logsSFR
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── logsSFR_surf
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── xi_ion
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   └── z
│       ├── fesc_int (5)
│       ├── fesc_int_err (5)
│       ├── fesc_obs (5)
│       ├── fesc_obs_err (5)
│       ├── method (5)
│       ├── pars (5)
│       └── pars_err (5)
├── LAE
│   ├── Av
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── LUV_att
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── LUV_int
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── Ms
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── beta_obs
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── logsSFR
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── logsSFR_surf
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   ├── xi_ion
│   │   ├── fesc_int (5)
│   │   ├── fesc_int_err (5)
│   │   ├── fesc_obs (5)
│   │   ├── fesc_obs_err (5)
│   │   ├── method (5)
│   │   ├── pars (5)
│   │   └── pars_err (5)
│   └── z
│       ├── fesc_int (5)
│       ├── fesc_int_err (5)
│       ├── fesc_obs (5)
│       ├── fesc_obs_err (5)
│       ├── method (5)
│       ├── pars (5)
│       └── pars_err (5)
└── nonLAE
    ├── Av
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    ├── LUV_att
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    ├── LUV_int
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    ├── Ms
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    ├── beta_obs
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    ├── logsSFR
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    ├── logsSFR_surf
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    ├── xi_ion
    │   ├── fesc_int (5)
    │   ├── fesc_int_err (5)
    │   ├── fesc_obs (5)
    │   ├── fesc_obs_err (5)
    │   ├── method (5)
    │   ├── pars (5)
    │   └── pars_err (5)
    └── z
        ├── fesc_int (5)
        ├── fesc_int_err (5)
        ├── fesc_obs (5)
        ├── fesc_obs_err (5)
        ├── method (5)
        ├── pars (5)
        └── pars_err (5)
```


### bnlcrl

Simulator of the compound refractive lenses (CRL).

Learn more at https://github.com/mrakitin/bnlcrl.

Documentation: http://bnlcrl.readthedocs.org/en/latest/

| Travis CI | ReadTheDocs | Codecov |
|:--:|:--:|:--:|
| [![Build Status](https://travis-ci.org/mrakitin/bnlcrl.svg?branch=master)](https://travis-ci.org/mrakitin/bnlcrl) | [![Documentation Status](https://readthedocs.org/projects/bnlcrl/badge/?version=latest)](http://bnlcrl.readthedocs.io/en/latest/?badge=latest) | [![codecov](https://codecov.io/gh/mrakitin/bnlcrl/branch/master/graph/badge.svg)](https://codecov.io/gh/mrakitin/bnlcrl) |

----
The code is written in Python, tested to be working under Linux and Windows with Python 2.7/3.5. There is no required NumPy dependency, but it still can be used for operations with matrices, etc. (see the `Usage` section below).

Determine Delta/Attenuation length:
-
To create a `.dat` file with the refractive index decrement or the attenuation length, use the following commands respectively:
```bash
bnlcrl simulate find-delta --characteristic delta -f Al -o Al_delta.dat 30
```

```bash
bnlcrl simulate find-delta --characteristic atten -f Al -o Al_atten.dat 30
```

Usage:
-
```
$ bnlcrl simulate find-delta -h
usage: bnlcrl simulate find-delta [-h] [--calc-delta]
                                  [--characteristic {transmission,atten,delta}]
                                  [-d DATA_FILE] [--e-max E_MAX]
                                  [--e-min E_MIN] [--e-step E_STEP]
                                  [-f FORMULA] [-n N_POINTS] [-o OUTFILE]
                                  [--plot] [--precise] [--save]
                                  [--save-output] [--show-plot] [-t THICKNESS]
                                  [-u] [-v]
                                  energy

Determine the Index of Refraction (delta).

        The index of refraction can be defined by three different methods/approaches:

        1) Get delta for the closest energy from the saved *.dat files (see ``bnlcrl/package_data/dat/``).

        2) Get delta from http://henke.lbl.gov/optical_constants/getdb2.html.

        3) Calculate delta analytically (requires ``periodictable`` package installed).

    Args:
        calc_delta (bool): a flag to calculate delta analytically.
        characteristic (str): characteristic to be extracted (``atten`` - attenuation length, ``delta`` - index of refraction, ``transmission`` - filter transmission).
        data_file (str): a *.dat data file in ``bnlcrl/package_data/dat/`` directory with delta values for the material of the CRL (e.g., Be).
        e_max (float): the highest available energy [eV].
        e_min (float): the lowest available energy [eV].
        e_step (float): energy step size used for saving data to a file [eV].
        energy (float): photon energy [eV].
        formula (str): material's formula of the interest.
        n_points (int): number of points to get from the server.
        outfile (str): optional output file.
        plot (bool): a flag to plot the obtained data.
        precise (bool): a flag to find delta within the energy interval +/- 1 eV from the specified energy.
        save (bool): a flag to save the obtained data.
        save_output (bool): a flag to save the output dictionary in JSON format.
        show_plot (bool): a flag to show the show the plot.
        thickness (float): thickness of the material.
        use_numpy (bool): a flag to use NumPy.
        verbose (bool): a flag to print output to console.

    Returns:
        dict: dictionary with the result.


positional arguments:
  energy                -

optional arguments:
  -h, --help            show this help message and exit
  --calc-delta          False
  --characteristic {transmission,atten,delta}
                        'delta'
  -d DATA_FILE, --data-file DATA_FILE
                        ''
  --e-max E_MAX         30000.0
  --e-min E_MIN         30.0
  --e-step E_STEP       10.0
  -f FORMULA, --formula FORMULA
                        'Be'
  -n N_POINTS, --n-points N_POINTS
                        500
  -o OUTFILE, --outfile OUTFILE
                        ''
  --plot                False
  --precise             False
  --save                False
  --save-output         False
  --show-plot           False
  -t THICKNESS, --thickness THICKNESS
                        0.1
  -u, --use-numpy       False
  -v, --verbose         False
```

Examples of execution:
-
```bash
$ bnlcrl simulate simulate-crl -p 6.52 -v --output-format json 2 4 6 7 8 21500
{
    "d": 0.0012016728926447229,
    "d_ideal": -0.06613035908221399,
    "f": 1.0480597834969956,
    "p0": 6.52,
    "p1": 1.2487983271073553,
    "p1_ideal": 1.3161303590822135
}
```

```bash
$ bnlcrl simulate simulate-crl -p 6.52 -v --output-format csv 2 4 6 7 8 21500
"d","d_ideal","f","p0","p1","p1_ideal"
0.00120167289264,-0.0661303590822,1.0480597835,6.52,1.24879832711,1.31613035908
```

```bash
$ bnlcrl simulate simulate-crl -p 6.52 -v --output-format txt 2 4 6 7 8 21500
d: 0.00120167289264, d_ideal: -0.0661303590822, f: 1.0480597835, p0: 6.52, p1: 1.24879832711, p1_ideal: 1.31613035908
```

```
$ bnlcrl simulate simulate-crl -p 6.52 21500 -v
"d","d_ideal","f","p0","p1","p1_ideal"
0,0,0,6.52,0,0
```

This library is used on the SMI beamline at NSLS-II:
![transfocator](docs/transfocator.png)

![attenuation filters](docs/attenuation_filters.png)

#### License

License: http://www.apache.org/licenses/LICENSE-2.0.html

Copyright (c) 2016 mrakitin (BNL).  All Rights Reserved.

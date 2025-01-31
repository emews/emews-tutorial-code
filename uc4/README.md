Running the UC4 example
----

You will need a working EMEWS install to run this workflow. See the [Quick Start guide][tutorial quickstart] in the EMEWS tutorial. The ME code also requires 3 additional Python packages `numpy`, `scipy`, and `scikit-learn`. These can
be installed with `conda` if using the local binary install: `conda install numpy scipy scikit-learn`, or with `pip` if you are not using a conda environment: `pip install numpy scipy scikit-learn`.

NOTE: Before running the example, edit the `db_path` entry in `uc4/python/me_cfg.yaml` to point to your EMEWS database location.

After editing `uc4/python/me_cfg.yaml`, you can issue the following commands to run the complete UC4 workflow:


````bash
1: $ cd python
2: $ python3 me.py test_ackley me_cfg.yaml
````
1. Changes directory into the `python` subdirectory.
2. Runs the workflow using the Python code in `me.py`. `me.py` takes two arguments. The first is an experiment ID (in this case `test_ackley`), and the second is the path to the `me_cfg.yaml` configuration file which is in the same `python` directory.

As the workflow runs, you should see some database status output as well as indications that the
ME is reprioritizing the Ackley tasks. For example,

```bash
❯ python3 me.py test_ackley me_cfg.yaml 
Checking for pg_ctl ...
/home/nick/miniconda3/envs/emews-py3.11/bin/pg_ctl


Starting database with log:/home/nick/tmp/tmp_db/db.log
Database server started
Reprioritizing ...
Reprioritizing ...
Reprioritizing ...
Reprioritizing ...
Checking for pg_ctl ...
/home/nick/miniconda3/envs/emews-py3.11/bin/pg_ctl


Stopping database server

waiting for server to shut down.... done
server stopped
```

The workflow will also create an experiment directory whose name 
consists of the experiment id followed by a timestamp (e.g., `uc4/experiments/test_ackley-default_1738336817.339369`).
The worker pool runs the Ackley Python code within that directory, creating an instance directory for each
Ackley evaluation.

```
test_ackley-default_1738336817.339369/
├── cfg.cfg  <1>
├── instance_20  <2>
│   ├── i_20_err.txt
│   └── i_20_out.txt
| ...
├── output.txt  <3>
└── run_ackley_worker_pool.sh.log  <4>
```

1. The EMEWS configuration file that was used to launch the workflow is preserved here for reference.
2. An instance directory containing the standard output and error output from an Ackley evaluation.
3. The output produced by the worker pool as it runs.
4. A concretized version of the file used to launch the worker pool, including the resolved environment variables used.

These instances directories are typically deleted after the instance is run, although a few may remain
in the experiment directory if the total number of tasks submitted is greater than those required for completion.

EMEWS project template
-----------------------

This project is compatible with swift-t v. 1.3+. Earlier
versions will NOT work.

The project consists of the following directories:

```
ackley/
  data/
  ext/
  etc/
  python/
    test/
  R/
    test/
  scripts/
  swift/
  README.md
```
The directories are intended to contain the following:

 * `data` - model input etc. data
 * `etc` - additional code used by EMEWS
 * `ext` - swift-t extensions such as eqpy, eqr
 * `python` - python code (e.g. model exploration algorithms written in python)
 * `python/test` - tests of the python code
 * `R` - R code (e.g. model exploration algorithms written R)
 * `R/test` - tests of the R code
 * `scripts` - any necessary scripts (e.g. scripts to launch a model), excluding
    scripts used to run the workflow.
 * `swift` - swift code

[tutorial url]: https://emews.org/emews-tutorial/
[tutorial quickstart]: https://emews.org/emews-tutorial/#quickstart

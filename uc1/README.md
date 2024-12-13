Running the UC1 example
----
You will need a working EMEWS install to run this workflow. See the [Quick Start guide][tutorial quickstart] in the EMEWS tutorial.

After downloading the Zombies model (see [here](https://github.com/emews/emews-tutorial-code/blob/main/README.md)), you can issue the following commands to run the complete UC1 workflow:


````bash
1: $ cd swift
2: $ ./run_uc1.sh exp1 cfgs/uc1.cfg
````
1. Change directory into the `swift` subdirectory.
2. This runs the workflow through the `run_uc1.sh` file, providing two arguments. The first is an experiment ID (in this case `exp1`), and the second is a path to the `uc1.cfg` configuration file, which is inside the `cfgs` directory.

Once the workflow completes, you will see 50 instance directories (corresponding to the 50 lines in the UPF file) along with the following ouputs in the `experiments/exp1` directory:

````
exp1
├── MessageCenter.log4j.properties  <1>
├── cfg.cfg  <2>
├── instance_1  <3>
│   ├── counts.batch_param_map.csv
│   ├── counts.csv  <4>
│   ├── data -> /Users/jozik/repos/emews-tutorial-code/uc1/complete_model/data  <5>
│   ├── debug.log  <6>
│   ├── err.txt  <7>
│   ├── location_output.batch_param_map.csv
│   ├── location_output.csv  <8>
│   └── out.txt  <9>
├── instance_10
|   ...
├── instance_11
|   ...
...
├── instance_9
│   ...
├── run_uc1.sh.log  <10>
└── upf.txt  <11>
````
1. This is a logging configuration file used by Repast Simphony.
2. The EMEWS configuration file that was used to launch the workflow is preserved here for reference.
3. This is 1 of 50 instance directories, corresponding to the 50 lines in the UPF file.
4. A csv file containing that counts of Human and Zombie agents over time, where the corresponding `counts.batch_param_map.csv` file contains the parameter values used for this instance.
5. A symlink to the `data` folder inside the Zombies model. This is an empty folder for this example, but could include input or reference data needed for the model to run, and this prevents unnecessary duplication of those assets.
6. Repast Simphony uses this to log any debugging information. Outputs are configured by the `MessageCenter.log4j.properties` file.
7. Standard error logged by the <<repast-app-annot>>, which launches each Zombies instance.
8. A csv file containing the locations of Human and Zombie agents at each time step. Here too, Repast Simphony produces the  corresponding `x.batch_param_map.csv` file to track the parameter values used for this instance.
9. Standard out logged by the <<repast-app-annot>>, which launches each Zombies instance.
10. A concretized version of the `run_uc1.sh` file used to launch the workflow, including the resolved environment variables used.
11. The UPF file used to launch this workflow, preserved here for reference.


EMEWS project template
-----------------------

This project is compatible with swift-t v. 1.3+. Earlier
versions will NOT work.

The project consists of the following directories:

```
uc1/
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


[tutorial url]: https://jozik.github.io/emews_next_gen_tutorial_tests
[tutorial quickstart]: https://jozik.github.io/emews_next_gen_tutorial_tests/#quickstart
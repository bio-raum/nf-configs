# Create your own config file

All our pipelines allow you to run with basic build-in execution profiles and expose relevant options from the command line to dial in your system specs. This is described in each respective pipeline documentation. 

However, we strongly recommend that you add your own site-specific config file to this repository to avoid having to set these options from the command line each time your run a pipeline. Moreover, the built-in profiles are only applicable to single-computer setups. If you run on a compute cluster, or possibly the cloud, you will need to provide additional options to the pipeline for it to translate properly to your setting. 

## Contributing your profile

Before we look at the specific options you can put in your site-specific config file, let's discuss how you contribute it to our project. 

### Fork this repository

If you are (very) comfortable with git, you are welcome to fork this repository and add your own profile, followed by a pull request against our main branch. You will have to :

- create your config file under `conf/` with a name of your choice (preferably descriptive and short!)
- add this new config file to the central lookup file [custom.config](../custom.config) with a short name matching the name of the config file
- Commit your changes to your personal fork
- Create a pull request from your updated fork to our main branch

### Create an issue

If you are not (very) comfortable with git, you are welcome to create an issue on this page and simply let us know that you want us to add a profile for you. For that we will need the following:

- name of the profile
- number of compute cores, ram and (optionally) allowed walltime
- description of your compute environment (single machine, cluster, cloud) and resource manager, if any
- choice of software provisioning framework and any necessary options

See below for all the possible options that can be set. 

## Site-specific config file

The amount of data needed is fairly minimal - see the example below for a simple Slurm setup:

```
params {
  reference_base = "/path/to/references"
}

executor {
  queueSize=50
}

process {
  executor = 'slurm'
  queue = 'all'
  resourceLimits = [ cpus: 16, memory: 64.GB, time: 72.h ]
}

apptainer {
  enabled = true
  cacheDir = "/work/apptainer_cache"
}

```

Note that this config file specifies four instruction blocks - the first three are mandatory/recommended, the fourth configures the container engine and related settings, so will depend on your software provider of choice.

## params

The reference_base option should be user-writable and, if applicable, live on a shared file system so all compute systems can access it. 

## executor

These are options specific to your resource manager / executor. In our example, we limit the number of concurrent jobs to 50. Additional options are described [here](https://www.nextflow.io/docs/latest/executor.html). This is mostly useful if you want to avoid angering your colleagues with a large number of pending jobs. 

## process

Options listed here concern mostly the choice of your executor (like Slurm, or PBS) and the limits of your hardware. In our example, we specify that we use "slurm" as our resource manager and that the corresponding queue/partition is called "all". Additional options are described [here](https://www.nextflow.io/docs/latest/executor.html). If you only run on a local computer, you can also set `local` as your executor, of course. The hardware specifications apply to the configuration of individual nodes (cpus, memory) and the whole cluster (time, i.e. maximum walltime a job can use), respectively. 


## apptainer

This block is used to configure the apptainer container engine, as described [here](https://www.nextflow.io/docs/latest/config.html). This name of the appropriate scope depends, of course, on your choice of software provisioning framework. Other commonly used options would be:

```
singularity {
    enabled = true
    cacheDir = /path/to/singularity_cache
}
``` 
or
```
conda {
    enabled = true
    cacheDir = /path/to/conda_cache
}
````
and so on...

In any case, we strongly recommend you set the `cacheDir` option to somewhere on your (shared) file system so nextflow is able to re-use previously installed software packages/containers. 

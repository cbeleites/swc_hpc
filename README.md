<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

# Intro

Teaching material used during the High Performance Computing session of the EMBL Software Carpentry course.

# Commands

Below are most of the commands used during the practical, so they can be copy/pasted, but I highly recommend typing along if you can.

## Login to the jump node

```sh
ssh bq_11denbi@129.206.69.162
```

```sh
ssh <user##>@172.16.72.70
```

## Clone this git repository
```
git clone https://github.com/grimbough/swc_hpc.git
```

## Identifying our computer

```
hostname
```

## Our first SLURM job

```
srun hostname
```

## Exploring our example program (don't run!)

```
cd $HOME/swc_hpc/software
# ./hpc_example -t 10 -l 100
```

## Running example program on on the cluster

```
srun ./hpc_example -t 10 -l 100
```

## Using our reserved training space
```
srun ./hpc_example -­t 10 -­m 100
```

## Running in the background

```
sbatch ./hpc_example -­t 10 -­m 100
```

## Redirecting output

```
sbatch --output=output.txt --reservation=training ./batch_job.sh
```

## Creating a larger list
You will need to edit batch_jobs.sh to take arguments
```
sbatch --output=output.txt --reservation=training ./batch_job.sh 20 ???
```

## Displaying details of our cluster queue

```
scontrol show partition
```

## Requesting more resources

```
sbatch --mem=8200 --reservation=training ./batch_job.sh 30 8000
```

## Requesting a lot more resources

```
sbatch --mem=100G --reservation=training ./batch_job.sh 30 5000
```

## Cancel jobs
```
scancel <jobID>
scancel -u <username>
```

## Job efficiency statistics
```
seff <jobID>
```

## Emailing output
```
sbatch ­­--mail­user=<first.last>@embl.de \
    ­­--reservation=training \
    ./batch_job.sh 20 500
```


## Running interactive jobs
```
srun --pty bash
```

## Interactive job with more memory
```
srun --mem=250 --pty bash
```

## Using `sbatch` instead

```
sbatch batch_jobs.sh
```

## Using job dependencies to build pipelines

```
jid=$(sbatch --parsable batch_job.sh)

sbatch --dependency=afterok:$jid batch_job.sh
```

# HPC Quick Notes — qsub / qstat / Queues

This page is a practical cheat sheet for working on an HPC system using PBS/Torque-style schedulers.  
It focuses on *understanding what the scheduler is doing*, not just memorizing commands.

Think of it as your “control panel”: observe → interpret → act.

---

# 1. Mental model (important)

Every job lives in a **queue** and has a **state**.

Typical lifecycle:
- Q → queued (waiting for resources)
- R → running
- C → completed
- H → held (paused manually or by system)
- E → exiting

The scheduler decides when your job runs based on:
- queue rules
- available nodes
- requested resources (CPU, RAM, time)

---

# 2. Core commands (daily usage)

## Show my jobs
```bash
qstat -u $USER
```

Basic overview of all your jobs.

Columns usually include:
- Job ID
- Name
- User
- Time used
- State
- Queue

---

## Show jobs including array tasks
```bash
qstat -t -u $USER
```

Why this matters:
- If you submit array jobs, without `-t` you see only the parent job
- With `-t`, you see each task separately

---

## Extended view (recommended default)
```bash
qstat -atu $USER
```

This is often the best “general” command because it combines:
- `-a` → more details
- `-t` → expand arrays
- `-u` → filter by user

---

# 3. Interpreting qstat output

Important detail: column positions (like `$3`, `$10`) depend on the cluster.

Typical mapping (but VERIFY on your system):
- $3 → queue name
- $10 → job state (R, Q, etc.)

Always sanity-check:
```bash
qstat -t -u $USER
```

---

# 4. Useful filters (your current commands explained)

## Count running jobs in `common`
```bash
qstat -t -u $USER | awk '$10 == "R" && $3 ~ /^common/' | wc -l
```

Interpretation:
- select only your jobs
- keep only running ones (R)
- keep only jobs in queue "common"
- count them

→ Gives current load *you* are generating on that queue.

---

## Count running jobs in `short`
```bash
qstat -t -u $USER | awk '$10 == "R" && $3 ~ /^short/' | wc -l
```

Same logic for a different queue.

---

## Count ALL your running jobs
```bash
qstat -t -u $USER | awk '$10 == "R"' | wc -l
```

---

## Count queued jobs
```bash
qstat -t -u $USER | awk '$10 == "Q"' | wc -l
```

---

# 5. Debugging jobs (critical skills)

## Full job inspection
```bash
qstat -f JOB_ID
```

This is your microscope.

Look for:
- queue
- resources requested (mem, cpu, walltime)
- execution node (exec_host)
- error/output paths
- timestamps

---

## Find where a job is running
```bash
qstat -f JOB_ID | grep exec_host
```

---

## Check which queue a job is in
```bash
qstat -f JOB_ID | grep queue
```

---

# 6. Understanding queue pressure

## Show all jobs (all users)
```bash
qstat -a
```

This tells you:
- how busy the system is
- whether queues are saturated

---

## Show jobs in a specific queue
```bash
qstat -a | awk '$3 ~ /^common/'
```

---

## Count running jobs in a queue (global load)
```bash
qstat -a | awk '$10 == "R" && $3 ~ /^common/' | wc -l
```

---

## Distribution of jobs per queue
```bash
qstat -a | awk 'NR>5 {print $3}' | sort | uniq -c
```

This gives a quick histogram of queue usage.

---

# 7. System-level inspection

## Queue configuration
```bash
qmgr -c "print queue"
```

May show:
- limits (max jobs)
- walltime constraints
- enabled/disabled status

---

## Node status
```bash
pbsnodes -a
```

Useful for:
- checking broken nodes
- understanding available resources

---

# 8. Job control (danger zone)

## Delete a job
```bash
qdel JOB_ID
```

---

## Delete ALL your jobs
```bash
qselect -u $USER | xargs qdel
```

Be careful. This is irreversible.

---

## Hold a job
```bash
qhold JOB_ID
```

---

## Release a job
```bash
qrls JOB_ID
```

---

# 9. Minimal debugging checklist (practical workflow)

When something is wrong:

1. Is the job running or queued?
```bash
qstat -u $USER
```

2. Full inspection:
```bash
qstat -f JOB_ID
```

3. Is the queue saturated?
```bash
qstat -a | awk '$3 ~ /^common/'
```

4. Are resources too large?
- too much memory?
- too long walltime?

5. Check logs:
```bash
less job.err
less job.out
```

---

# 10. Final note

Schedulers are deterministic machines wrapped in opaque policies.

If a job does not run, it is never “random”:
it is always a constraint you do not yet see.
 PBS launch script templates

This page contains two anonymized PBS/Torque-style launch script examples based on a real HPC workflow.  
The first is for an **array job**, useful when launching many similar simulations. The second is for a **single job**, useful for one standalone run.

---

# 1. Array job example

Use this when each task runs the same command pattern but with a different input file, index, or simulation ID.

```bash
#!/bin/bash

# Request resources
# Example: 1 node, 15 CPUs, 150 GB RAM
#PBS -l select=1:ncpus=15:mem=150GB

# Job name
#PBS -N kriging_array_job

# Email notifications
#PBS -m abe
#PBS -M your.email@example.org

# Maximum execution time
#PBS -l walltime=14:59:00

# Array range
# Example: tasks 801 to 809
#PBS -J 801-809

# Queue
#PBS -q commonCPUQ

# Allow rerun
#PBS -r y

# Load needed software
module load Java/11.0.27

# Move to working directory
cd /path/to/project_directory/

# Launch the simulation corresponding to the current array index
java -Xmx120G -XX:+UseG1GC -XX:MaxGCPauseMillis=200 \
    -Doms3.work=/path/to/project_directory/ \
    -cp ".:/path/to/oms-console/lib/oms-all.jar:lib/*:dist/*" oms3.CLI \
    -r simulation/kriging/precipitation/graph${PBS_ARRAY_INDEX}.sim \
    &> point${PBS_ARRAY_INDEX}.out
```

## What each important part does

### Resource request
```bash
#PBS -l select=1:ncpus=15:mem=150GB
```

Requests:
- 1 execution chunk
- 15 CPUs
- 150 GB of memory

---

### Array definition
```bash
#PBS -J 801-809
```

Creates one task for each index in the range:
- 801
- 802
- ...
- 809

Each task gets its own value of `PBS_ARRAY_INDEX`.

---

### Input file linked to task index
```bash
-r simulation/kriging/precipitation/graph${PBS_ARRAY_INDEX}.sim
```

This makes each task use a different simulation file, for example:
- `graph801.sim`
- `graph802.sim`
- ...
- `graph809.sim`

---

### Output file per task
```bash
&> point${PBS_ARRAY_INDEX}.out
```

Each array task writes to a different output file, for example:
- `point801.out`
- `point802.out`

This is very useful for debugging because output stays separated.

---

# 2. Single job example

Use this when you want to run only one simulation.

```bash
#!/bin/bash

# Request resources
#PBS -l select=1:ncpus=15:mem=150GB

# Job name
#PBS -N kriging_single_job

# Email notifications
#PBS -m abe
#PBS -M your.email@example.org

# Maximum execution time
#PBS -l walltime=14:59:00

# Queue
#PBS -q commonCPUQ

# Allow rerun
#PBS -r y

# Load needed software
module load Java/11.0.27

# Move to working directory
cd /path/to/project_directory/

# Launch one single simulation
java -Xmx120G -XX:+UseG1GC -XX:MaxGCPauseMillis=200 \
    -Doms3.work=/path/to/project_directory/ \
    -cp ".:/path/to/oms-console/lib/oms-all.jar:lib/*:dist/*" oms3.CLI \
    -r simulation/kriging/precipitation/graph801.sim \
    &> point801.out
```

## Main difference from the array version

The single-job version:
- **does not** use `#PBS -J`
- **does not** use `${PBS_ARRAY_INDEX}`
- uses one fixed input file
- writes to one fixed output file

---

# 3. Practical notes

## Array job: when to prefer it
Choose an array job when:
- you have many similar simulations
- only the input file/index changes
- you want cleaner scheduler management
- you want one template for many runs

---

## Single job: when to prefer it
Choose a single job when:
- you are testing
- you want to debug one case
- you only need one simulation
- you want simpler output inspection

---

# 4. Submission examples

## Submit the array job
```bash
qsub point_precip_array_common.pbs
```

## Submit the single job
```bash
qsub point_precip_single_common.pbs
```

---

# 5. Suggested anonymization choices

In public notes or documentation, replace:
- personal email → `your.email@example.org`
- personal home path → `/path/to/project_directory/`
- private software path → `/path/to/oms-console/`
- highly specific project names → generic names like `kriging_array_job`

This keeps the structure intact without exposing personal or institutional details.

---

# 6. Conceptual takeaway

An array job is not magic. It is just a compact way of saying:

> run the same workflow many times, changing only the index-dependent input.

That tiny scheduler trick saves a lot of typing and reduces copy-paste chaos, which is one of the oldest demons in computational science.

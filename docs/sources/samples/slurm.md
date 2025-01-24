# Slurm Submission Files (WIP)

## Submit a DFT calculation

These samples scripts  perform the
following steps:

1. Loads your bash profile file and the required modules for the computational code.
2. Creates a scratch directory dedicated to the job that is uniquely
   identified by the SLURM job ID and creates a symlink to the scratch
   directory for convenience. (This is especially useful if the jobterminates
   unexpectedly during execution.)
3. Copies files to the scratch directory.
4. Initiates the calculation by running a Python script (presumably, `run.py`).
5. Stops the job at 90% of the maximum run time to ensure enough time remains
   to copy files from the scratch directory to the submission directory.
6. Cleans up the scratch directory.
7. Logs the completion of the job in a file in your home directory `~/job.log`.

Additionally, the script prints out debugging information that *may* be useful
for identifying issues with running jobs (e.g., resource information, job ID,
etc.).

=== "VASP"

    ``` py title="samples/slurm/vasp.sh" linenums="1" hl_lines="96"
    ``` py title="samples/slurm/vasp.sh" linenums="1" hl_lines="96"
    --8<-- "./samples/slurm/vasp.sh"
    ```

=== "Espresso"

    ``` py title="samples/slurm/espresso.sh" linenums="1"
    ``` py title="samples/slurm/espresso.sh" linenums="1"
    --8<-- "./samples/slurm/espresso.sh"
    ```

    !!! important "Reminder"
        This script assumes that you are using a self-compiled version of
        Quantum Espresso and have created a corresponding module named
        `espresso`. See [this tutorial](../tutorials/espresso_compilation.md)
        for how to compile Quantum Espresso and create the necessary
        modulefile.

=== "Gaussian"

    ``` py title="samples/slurm/gaussian.sh" linenums="1" hl_lines="101"
    --8<-- "./samples/slurm/gaussian.sh"
    ```

=== "ORCA"

    ``` py title="samples/slurm/orca.sh" linenums="1"
    ``` py title="samples/slurm/orca.sh" linenums="1"
    --8<-- "./samples/slurm/orca.sh"
    ```

!!! Tip

    Edit the [brace expansion][brace-expansion] in line 96 or 101 to change the
    files copied to the scratch directory.

!!! Reminder

    Don't forget to replace `JOB_NAME`, `SFU_ID`, and `PYTHON_SCRIPT` with
    appropriate values in addition to setting your desired SLURM parameters.
    Also, if you don't define the path to a Python virtual environment in your
    `.bashrc` file, then you should replace `$COMP_CHEM_ENV` with the path to
    the `activate` script (usually, `path-to-environment/bin/activate`).

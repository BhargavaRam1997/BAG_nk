# BAG2_cds_ff_mpt
BAG2 setup for cds_ff_mpt (cadence generic PDK for finfet and multi-patterned technology)

## Python setup

BAG2 works with Python 3 (Python 3.6+ is recommended).  We strongly recommend using Anaconda Python in a custom 
install location, as it contains most required packages and offer simple installation process.  In addition to 
the default Anaconda packages, the following needs to be installed/changed (through either `conda` or `pip`):

1. shapely
    *nayiri* conda install -c conda-forge shapely 
    
2. rtree 
    *nayiri* conda install -c conda-forge rtree

3. tornado (downgrade to 4.5.3 for the bootcamp demo).
    *nayiri* conda install -c conda-forge tornado=4.5.3

## Installation
1. Download cds_ff_mpt PDK from [Cadence Support](https://support.cadence.com) 
and install it.

2. Clone BAG2_cds_ff_mpt repo.

    ```
    $ git clone https://github.com/ucb-art/BAG2_cds_ff_mpt.git
    ```
    
3. Clone all dependent git submodules.  Run the following commands:

    ```
    $ git submodule init
    $ git submodule update
    ```
    
4. (non-BWRC users) Update the symbolic link `cds_ff_mpt/workspace_setup/PDK` to point to the cds_ff_mpt 
   PDK installation location; the `cds_ff_mpt_v_0.3` folder.
   
   *nayiri* ln -sn /net/plato.ee.Virginia.edu/misan3/app3/lib/TSMC65-CRN65LP PDK
  
5. (non-BWRC users) Update `cds_ff_mpt/workspace_setup/{.cshrc, .bashrc}` to point to your tools locations.
   The tools needed by this demo are:

   - Virtuoso ICADV 12.3 (or 12.1)
        *nayiri* 12.2, /net/plato.ee.Virginia.edu/misan3/app3/cadence/ICADV122
        
   - PVS 15.1
        *nayiri* 15.2 or 16.1, /net/plato.ee.Virginia.edu/misan3/app3/cadence/PVS152
   
    *bag*    source /tools/flexlm/flexlm.sh
    *nayiri* closest I could find was flex: /usr/bin/flex, didn't include this
    

6. (non-BWRC users) Update `cds_ff_mpt/workspace_setup/{.cshrc_bag, .bashrc_bag}` to point to the Anaconda 
   Python installation location used to run BAG.  See BAG_framework documentation on how to install Anaconda 
   Python for BAG.
   
   *nayiri*
    # set BAG python executable
    setenv BAG_PYTHON "/net/redfox.ece.Virginia.EDU/isan0/users/nk9yx/anaconda3/bin/python"
    # set jupyter notebook path
    setenv BAG_JUPYTER "/net/redfox.ece.Virginia.EDU/isan0/users/nk9yx/anaconda3/bin/jupyter-notebook"

7. (non-BWRC users) Update `cds_ff_mpt/corners_setup.sdb`, which sets up model files and process corners for BAG,
   to point to the correct model file location.
   *bag*    <modelfile>/tools/cadence/GPDK/cds_ff_mpt_v_0.3/models/spectre/cds_ff_mpt.scs</modelfile>
   *nayiri* many options...
            - /app3/lib/TSMC65-CRN65LP/T-N65-CL-SP-040/TN65CLSP040_1_1/models/CLN65LP_3d3_lk_v1d1.scs
            - /app3/lib/TSMC65-CRN65LP/T-N65-CM-SP-007-K3/models/spectre/crn65lp_2d5_lk_v1d7_usage.scs
            - /app3/lib/TSMC65-CRN65LP/T-N65-CL-SP-040/TN65CLSP040_1_1/models/ResModel.scs
            - /app3/lib/TSMC65-CRN65LP/T-N65-CM-SP-007-K3/models/spectre/toplevel.scs
            - I think it's this one: (b/c it's in ..../models/spectre/.....)
            - /app3/lib/TSMC65-CRN65LP/T-N65-CM-SP-007-K3/models/spectre/crn65lp_2d5_lk_v1d7.scs
   
8. (non-BWRC users) in `cds_ff_mpt/workspace_setup/.cdsinit`, change the `editor` variable to point to your
   variable editor.
   *bag*    editor = "/tools/projects/erichang/programs/core/bin/emacs"
   *nayiri* /usr/bin/emacs
   
9. (non-BWRC users) in `cds_ff_mpt/workspace_setup/.cdsinit.personal`, in the last command where it sets the
   simulation data directory (the `projectDir` variable), change it to a suitable location.
   *bag*    envSetVal("asimenv.startup" "projectDir" 'string sprintf( nil "/tools/scratch/%s/simulation" getShellEnvVar( "USER" ) ) )
   *nayiri* /net/redfox.ece.Virginia.EDU/isan0/users/nk9yx/scratch/%s/simulation

## Running BAG

Once you finish setting up the workspace, try to run the demo as follows:

1. in the directory, run the following command

   ```
   $ source .cshrc
   ```

   to set up environment variables for running BAG/Virtuoso.  This needs to be done everytime you start a new terminal.
   If You use bash, you source .bashrc instead.

2. start virtuoso

   ```
   $ virtuoso &
   ```

3. in virtuoso CIW window, run

   ```
   load("start_bag.il")
   ```
   
4. in the terminal, run

   ```
   $ ./start_tutorial.sh
   ```

   this will start a Jupyter notebook with interactive modules.  Just follow through each module in sequence.

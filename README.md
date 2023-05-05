# Polyglot MATLAB Notebooks using [Script of Script (SoS)](https://vatlab.github.io/sos-docs/notebook.html#content)
A repository containing examples and instructions on using Script of Script (SoS) Polyglot notebooks with MATLAB and other languages.

Here are the tools I'm using

- OS: Windows 11
  - Terminal launching Miniconda3 (4.12.0)

- Python: 3.10.4
- pip: 22.2.2
- MATLAB: R2022b (9.13.0.2049777 )

## Installation Steps
### 1. Install and activate MATLAB
### 2. Install miniconda3 or anaconda3 (I use miniconda) and open anaconda terminal
  - Note: Run the terminal in administrator or elevated permission (depending on your OS)
### 3. Create an environment for MATLAB in miniconda and activate
  - ```PowerShell
    conda create -n "sos" python=3.10
    ```
  - ```PowerShell
    conda activate sos
     ```
### 4. (In MATLAB console) Point MATLAB to your conda environment
  - ```MATLAB
    pyversion('C:\Users\<user>\miniconda3\envs\matlab\python.exe');
    pyenv('ExecutionMode', 'OutOfProcess');
    ```
### 5. Install SoS, Python and MATLAB subkernels and matplotlib (for Python) via
  - run in conda terminal: 
    ```PowerShell
    conda install sos sos-pbs sos-notebook jupyterlab-sos sos-papermill sos-python sos-r matplotlib -c conda-forge
    ```
    ```PowerShell
    pip install sos-matlab
    ```
  - Source: https://vatlab.github.io/sos-docs/running.html#Conda-installation
<!--
6. Follow video setup of installing MATLAB kernel for jupyter
  deviation: The video is old and does not provide the correct way of install the matlab environment. Follow the steps here:
    - link: https://www.mathworks.com/help/matlab/matlab_external/install-the-matlab-engine-for-python.html
    - (note for above: make sure you activate your virtual env so as not to use a potential global python env)
7. Continue the video setup by executing:
  - ```python -mimatlab install```
    - This should result in a success
-->
### 6. Install the MATLAB engine to Python (note that official documentation is deprecated on MathWorks and SoS websites now)
  - In conda terminal run: 
   ```PowerShell
   python -m pip install matlabengine==9.13.7
   ```
  - To test that this worked, first activate Python in the conda terminal via:
  - ```PowerShell
    python
    ```
  - Then execute the following code:
    ```Python
    import matlab.engine
    eng = matlab.engine.start_matlab()
    eng.isprime(37)
    ```
      - This should return ```True```. If there were errors, troubleshoot at https://github.com/mathworks/matlab-engine-for-python
  - Exit Python with ```exit()``` but keep terminal open.
### 7. (still in conda terminal) Install `matlab_kernel`
  - ```PowerShell
    pip install matlab_kernel
    ```
<!--
8. Install SoS MATLAB Subkernel
  - ```pip install sos-matlab```

### 8. Finish installation by installing mimatlab (required administrator privledge)
  - If you did not open your terminal with elevated access, please do so now and re-activate sos via ```conda activate sos```
  - ```PowerShell
    python -mimatlab install
    ```
-->
### 8. Confirm that the installation works by running the example/test_installation notebook and running each cell.
  - Open a Jupyter Notebook in conda terminal via:
  ```PowerShell
  jupyter notebook
  ```

## Notes:
1. You will need to change the ratelimit for Jupyter to visualize larger EEGLAB objects. Follow the steps here:
    - https://stackoverflow.com/questions/43288550/iopub-data-rate-exceeded-in-jupyter-notebook-when-viewing-image
    - ```jupyter notebook --generate-config```
        - edit this file
        - search for ```c.NotebookApp.iopub_data_rate_limit```
        - uncomment this and set the value to: ```=1.0e10```

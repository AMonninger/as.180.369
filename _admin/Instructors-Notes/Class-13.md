# Final Class: From Sciserver to local machines

1. On Sciserver
- Create a file of YOUR environment:
    - In your paper directory
    - Create a folder: binder 
        ```
        mkdir binder
        cd binder
        ```
    - create the environment file: This will create a file with all installed packages
        ```
        conda env export --from-history -f environment.yml
        ```
    - get the specified versions:
      ```
        conda list | grep -E -i -w "^$(conda env export --no-builds --from-history | awk '$1 == "-"{ if (key == "dependencies:") print $NF; next } {key=$1}' | sed 's/=.*//' | tr -s '\r\n' '|' | sed 's/|$//')\s" | awk '{ print $1 "=" $2 }' | sed 's/^/  - /'
      ```
    - replace the packages with the list on your terminal.
    - delete line for jupyterlab-rise=0.42.0

- Adjust reproduce.sh (see [example](../../contrib/AMonninger/Paper_Rescheduled/reproduce.sh)
    - make sure to activate the kernel
    ```
    python -m ipykernel install --user --name econark
    ```
- Push changes on GitHub

2. On your laptop
- Get your fork
    - Create a folder structure (Github/GitHubID)
    - In that newly created folder:
    ```
    git clone https://github.com/GITHUBID/as.380.369
    ```
- Give permission to execute reproduce.sh (If you have a mac):
    - open a terminal and navigate to folder of your paper
    - ```ls -las``` (shows if it is executable)
    - ```chmod u+x reproduce.sh ```
    - ```ls -las```(reproduce.sh file should be green now)
- run reproduce.sh

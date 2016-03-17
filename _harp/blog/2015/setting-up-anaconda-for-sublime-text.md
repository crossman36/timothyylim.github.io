### Setting Up Anaconda for Sublime Text

Windows:

1. Download and install Anaconda
2. Create a new build system in Sublime (Tools > Build System > New Build System)
3. Replace contents with the following, where C:/Anaconda/python.exe is the path
to the python build in your Anaconda directory

```
{
"cmd": ["C:/Anaconda/python.exe", "-u", "$file"],
"file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
"selector": "source.python"
}
```

Open up your terminal (Windows Home Button > All Apps > Command Prompt)
Check if you have installed pip by typing in:
```
pip 
```

then to install pandas and pandasql

```
pip pandas 
pip pandasql 
```



Mac:

1. Download and install Anaconda
2. Then install pandas in your terminal
3. conda install pandasql

To install pandasql simply enter this into your terminal:

```
conda install pandasql
```

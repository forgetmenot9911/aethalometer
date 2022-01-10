# Aethalometer Visualization Scripts
## Python script visualization and data-averaging of Aethalometer datafiles (AE31 and AE33)

### **Installation**
1. Clone repository:
```bash
$ git clone https://github.com/alejandrokeller/aethalometer
```
2. Travel to cloned folder:
```bash
$ cd aethalometer
```
3. Create a local config.ini file:
```bash
$ cp config config.ini
```
4. Edit the config.ini file by adding the default data path and file extension (e.g. ".dat").
The script searches this path for the latest file if it is used used without a file argument.
The 'FREQ' option defines the default generated averaging interval (i.e. HOURLY, MINUTELY, SECONDLY). 'INTERVAL' defines the interval length used in combination with the 'FREQ' variable (e.g. INTERVAL: 10 would result in averaging of 10 hours, minutes or seconds).
The script outputs raw data if --ioff is used and no --intervals CSV file defined.

5. Install python requirements:
```bash
$ pip install -r requirements.txt
```

### **Usage**

`aeth.py [-h] [--inifile INI] [--ae33 | --ae31] [--iON | --iOFF]
               [--intervals CSV] [--bckey BCKEY]
               [file [file ...]]`
               
| Argument | Description |
| --- | --- |
|-h, --help     | show help message and exit|
|--inifile INI  | Path to an alternative configuration file|
|--ae33         | Uses file format for AE33 datafiles (default)|
|--ae31         | Uses file format for AE31 datafiles|
|--iON          | Calculates average values for given intervals, and plot average values (default)|
|--iOFF         | Do not calculate intervals; plot all datapoints|
|--intervals CSV| csv file with start and end timestamps columns. First row must be the column names (i.e. "start" and "end"). Uses hourly, minutely, or secondly intervals if this parameteris missing (as defined in config.ini)|
|--bckey BCKEY  | Selects the variable for the generated plot. Possible values: BC1 through BC7 (and BB for AE33). Default: BC6=880nm|
| file(s)       | path to file(s) to be plotted. If several files are given, they will be joined into a single dataframe. If empty, the script looks for the latest file in the default data directory defined in the inifile.|  

The calculated averaged interval-data for BC1-BC7 and BB are printed by the command. Use `>` to save the data:
```bash
$ aeth.py sample.dat > averaged_data.csv
```

The plots, generated using `matplotlib`, are *NOT* automatically saved. Use the GUI for text editing and saving. Several formats are possible.

Hourly interval example:
![Aethalometer data, hourly](boxplot.png)

Minutely interval example:
![Aethalometer data, minutely](boxplot-minutes.png)

# Hyper Threading

In the ideal case, you can double the computational capability after enabling hyper threading. For example, if you have 32 physical cpu cores with hyper threading on, you'll have 64 cores.

## Enable HT
BIOS -> Advanced Settings -> Enable Hyper Threading

## How to ask for cores when running job

`pbsnodes` still tell you the number of cpu cores hasn't doubled. But `cat /proc/cpuinfos` will tell you the truth.


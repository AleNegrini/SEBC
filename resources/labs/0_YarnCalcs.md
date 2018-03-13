# Review the Tuning guide

## OS Memory
The value inserted in the excel file are 
```
Worker vcores 28
Worker spindles 12
Worker RAM 128
Workload factor 2
Worker nodes 20
```

By setting always OS memory as 10% of the total RAM memory could be too high/low: if we have 32 GB of RAM, The Os memory would be too low, if we have 256 GB of ram it will be to high. 
Good practice is to start considering 8-10 Gb of RAM only for the OS and then tune it. 
In this specific case 10% is fine, since I got as OS memory:
```
12,8 GB
```

## Mimimum Impala CPU/Memory
I have set the Impala Memory and CPU vcores as the 25% of the total amount of Mem and CPU, getting:
```
Impala Memory 32GB
Impala vcores 7
```
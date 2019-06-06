# Cluster Temperature Monitor 

1.  Extract CPU temperatures

   ```bash
   $ sensors | grep '^temp[0-9]:' | sed -e 's/.*: \+[+-]\([0-9.]\+\)°C.*$/\1/'
   27.8
   29.8
   ```
   
2. If one of the CPU cores on a node computing node reach +70 °C,  write the node name and the temperature to file `data/$temperaFile`

   ```bash
   $ cat data/2019-05-12_13\:00\:01 
   71.0 node06
   71.0 node06
   ```
   
3. If ` data/$temperaFile` is not empty, notify the lab members by sending an email to given address with the content from file `data/$temperaFile `

   ```bash
   php temperatureWarning.php data/$temperaFile 
   ```
   
4. This program will check the temperature every hour. We use `cronjob` to make the program run every hour

   ```
   0 * * * * sh /home/coiby/temperatureAlert/temperature.sh >>/home/coiby/temperatureAlert/tempera.log 2>&
   ```

   
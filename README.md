# ethOS GPU Monitoring Cronjob

Prerequisites: Mining RIG using ethOS

This procedure will help you setting up a cronjob to monitor the Hash rate data from your ethOS RIG; if the hasrate goes below your defined cronjob, after 5 tries, the cronjob will restart your RIG.


REQUIREMENTS:

As described in requirements section of the check/script, if you want it to be able to restart your rig you will need to :

Create a gpu_crashReboot.log file with 0 as value inside :
(as ethos user elevate as root:)

```bash
sudo -s 
echo 0 > /root/gpu_crashReboot.log
```

Edit Crontab file using :
(always as root user:)

```bash
crontab -e
```

Add the following at the end:

```bash
# Cron Check Rig Hash
* * * * * /usr/bin/python /root/check_rig-hash > /dev/null 2>&1
```

Save and quit.

Do not forget to adjust the minimum Global hashrate value [rigMinHashRate] to your needs (no units):

```python
  rigMinHashRate = XX.X
```
 

And the check itself has to be placed in /root/check_rig-hash


You can test the script using:

```bash
# python /root/check_righ-hash
OK - Global Rig hashrate : 122.7 (MH/s) [Threshold: 110.0]
```

Source: http://www.davidbayle.com/knowledge-base/ethos_cronjob-check-mining-rig-hash/

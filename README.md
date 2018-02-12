Prerequisites: Mining RIG using ethOS

This procedure will help you setting up a cronjob to monitor the Hash rate data from your ethOS RIG 
and if you loose card(s) in your mining RIG or if your cards are mining bellow your defined threshold; the cronjob will restart your RIG.


REQUIREMENTS:

As described in requirements section of the check/script, if you want it to be able to restart your rig you will need to :

Create a gpu_crashReboot.log file with 0 as value inside :
(as ethos user:)

```bash
sudo echo 0 > /var/log/gpu_crashReboot.log
```

Edit Crontab file using :
(as ethos user:)

```bash
sudo crontab -e
```

Add the following at the end:

```bash
# Cron Check Rig Hash
* * * * * /usr/bin/python /root/check_rig-hash > /dev/null 2>&1
```

Save and quit.

Do not forget to adjust your panel URL [gpuJsonSite] and the minimum hashrate value by gpu [gpuMinHashRate] to your needs :

```python
  gpuJsonSite = “http://XXXXX.ethosdistro.com/?json=yes”
```

by replacing the XXXXX with your ID [http://XXXXX.ethosdistro.com/?json=yes]

(you can find your ID by typing helpme on your rig directly in command line.)
 
and
```python
  gpuMinHashRate = XX.X
```
 

And the check itself has to be placed in /root/check_rig-hash

# robin

April Fools 2016, for Clones (2017)

## Installation

Install the plugin itself.

```bash
cd ~/src/robin
python setup.py build
sudo python setup.py develop
```

Then add the plugin to your ini file:

```diff
[DEFAULT]
-plugins = about, liveupdate
+plugins = about, liveupdate, robin

[live_config]
feature_robin = on
feature_robin_on_homepage = on

#I believe this is the ratelimit per tier. Please message if you want to clarify.
robin_ratelimit_window = 1000000
robin_ratelimit_avg_per_sec = 1:10000, 2:20000, 3:30000, 4:40000, 5:50000, 6:60000
```

Then, make the files required for Robin:

```bash
sudo make
```

Then, copy the upstart scripts:

```bash
sudo cp ~/src/robin/upstart/* /etc/init/
```

Then, enable the consumers:

```bash
cd ~/consumer-counts.d
echo 1 > robin_presence_q
echo 1 > robin_waitinglist_q
echo 1 > robin_subreddit_maker_q
sudo initctl emit reddit-start
```

Then, enable the cron jobs:

```bash
sudo cp ~/src/robin/cron.d/* /etc/cron.d/
```

Finally, restart the reddit-paster:

```bash
sudo service reddit-paster restart
```

## Things that are compatible
Parrot works on it.

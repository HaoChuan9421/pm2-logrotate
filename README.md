# pm2-logrotate-next

NOTE: This is a fork of [pm2-logrotate](https://github.com/keymetrics/pm2-logrotate), which is (currently) unmaintained. this fork is only for personal use, don't guarantee maintenance and safety, use at your own risk.

注意：这是 一个来自 [pm2-logrotate](https://github.com/keymetrics/pm2-logrotate) 的 fork，原仓库已经不维护了，这个 fork 只是为了方便我个人使用，不保证持续的维护和安全性，风险自担。

## Description

PM2 module to automatically rotate logs of processes managed by PM2.

## Install

    pm2 install pm2-logrotate-next

**NOTE:** the command is `pm2 install` NOT `npm install`

## Configure

- `max_size` (Defaults to `256M`): When a file size becomes higher than this value it will rotate it (its possible that the worker check the file after it actually pass the limit) . You can specify the unit at then end: `10G`, `10M`, `10K`
- `retain` (Defaults to `7` file logs): This number is the number of rotated logs that are keep at any one time, it means that if you have retain = 30 you will have at most 30 rotated logs and your current one. unset will keep all log files.
- `compress` (Defaults to `false`): Enable compression via gzip for all rotated logs
- `dateFormat` (Defaults to `YYYY-MM-DD-HH-mm-ss`) : Format of the data used the name the file of log
- `rotateModule` (Defaults to `false`) : Rotate the log of pm2's module like other apps
- `workerInterval` (Defaults to `30` in secs) : You can control at which interval the worker is checking the log's size (minimum is `1`)
- `rotateInterval` (Defaults to `0 0 0 * * *` everyday at midnight): This cron is used to a force rotate when executed.
We are using [node-schedule](https://github.com/node-schedule/node-schedule) to schedule cron, so all valid cron for [node-schedule](https://github.com/node-schedule/node-schedule) is valid cron for this option. Cron style :
- `TZ` (Defaults to system time): This is the standard [tz database timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) used to offset the log file saved. For instance, a value of `Etc/GMT+1`, with an hourly log, will save a file at hour `14` GMT with hour `13` (GMT+1) in the log name.

```
*    *    *    *    *    *
┬    ┬    ┬    ┬    ┬    ┬
│    │    │    │    │    |
│    │    │    │    │    └ day of week (0 - 7) (0 or 7 is Sun)
│    │    │    │    └───── month (1 - 12)
│    │    │    └────────── day of month (1 - 31)
│    │    └─────────────── hour (0 - 23)
│    └──────────────────── minute (0 - 59)
└───────────────────────── second (0 - 59, OPTIONAL)
```

### How to set these values ?

 After having installed the module you have to type :
`pm2 set pm2-logrotate-next:<param> <value>`

e.g:
- `pm2 set pm2-logrotate-next:max_size 1K` (1KB)
- `pm2 set pm2-logrotate-next:compress true` (compress logs when rotated)
- `pm2 set pm2-logrotate-next:rotateInterval '*/1 * * * *'` (force rotate every minute)

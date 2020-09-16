---
title: Create CRON job
description: In this step you learn how to create a CRON job that automatically deletes call recordings weekly.
---

# Create a CRON job

The final step is to delete the call recordings every week using a CRON job. A CRON job is a way to run scripts periodically at fixed times, dates, or intervals. Running a CRON job will save you the effort of having to manually run the functions covered in this tutorial. 
You can create a CRON job locally by first running `crontab -e` on a OSX/Linux based system.

For a Windows machine:

1. Log on with a privileged account, e.g. Administrator
2. Go to **Start > Control Panel > System and Security > Administrative Tools > Task Scheduler**.
3. In the right panel click **Create Basic Task**.

For the purposes of this demonstration, the CRON job will run every 30 days:

    ```bash
    * * 30 * * delete_recordings.py >/dev/null 2>&1
    ```

    The [`delete_vbc_recordings_by_duration.py`](https://gist.github.com/tbass134/aace7e859ff401f611df772ad6cb4b32) is a script that will delete both the call recordings and on demand call recordings for calls that are less than 30 seconds in duration.

To create your own CRON job, [refer to this helpful resource](https://crontab-generator.org). 

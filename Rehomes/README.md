# Overnight Work

This document provides an overview of the "Overnight Work" folder.

## Contents

- [Cronjobs](./File1.md)
  - [Del_Mobatch_File.sh](./Cronjobs/Del_Mobatch_File.sh)
  - [Precheck.sh](./Cronjobs/Postcheck.sh)
  - [Postcheck.sh](./Cronjobs/Precheck.sh)
- [Rehomes](./File2.md)


## Cronjobs

This folder houses shell scripts scheduled to execute at specific times through CronJobs in the OSS. Upon successful completion of a cronjob, it generates a log, dated with today's date, and places it in the Cronjobs' logs folder. This document doesn't contain any additional information; its purpose is to confirm that the scheduled job has been executed. 

### Del_Mobatch_File.sh: 
    The `Del_Mobatch_File.sh` script is designed to maintain the directories `/home/shared/common/Overnight_Work/Rehome/Postchecks` and `/home/shared/common/Overnight_Work/Rehome/Prechecks` by deleting the `mobatch_result.txt` file. This file is generated each time a mobatch job runs. If the file remains in the directory during subsequent Pre/Post checks, it won't be overwritten, leading to job failure. To prevent this, `Del_Mobatch_File.sh` performs daily cleanups, ensuring that the jobs can execute without issues the following day.
### Precheck.sh
    This shell script executes daily at 4:45 PM. It performs preliminary checks to capture a snapshot of specific node elements before the evening's rehome work. This snapshot serves as a baseline for comparison with post-checks, should any issues arise after the work is completed. It also reviews the previous three hours of traffic for potential comparison with post-checks. This check primarily serves as a safeguard against claims of pre-existing issues being attributed to our work.

### Postcheck.sh
    This shell script runs daily at 8:00 AM. It conducts checks to capture a snapshot of specific node elements after the evening's rehome work. It also reviews the previous ten hours of traffic for comparison with the pre-checks. The purpose of this check is to identify any manual cleanup work that may be required due to our work during the Maintenance Window. If such work is identified, it will be addressed immediately.


## Rehomes

The `Rehomes` folder contains two directories, two scripts, and a sitelist file. The scheduled cronjobs for prechecks and postchecks, as previously described, utilize these two scripts. Each day, before and after our maintenance work, the cronjob accesses the nodes scheduled for work (as specified by the sitelist file) and executes a series of predetermined commands to verify the system's state pre and post work. Following this, it generates a log file for each baseband and places it in the corresponding Pre or Post check folder, timestamped with the date and time.

Currently, the "sitelist" file requires manual updates to include the sites scheduled for the evening's work. This update should be performed once the schedule is finalized.


## Conclusion

When executed properly, these scripts provide comprehensive data to confirm the success of the Rehome process and swiftly identify any arising issues. It's important to note that any pre-existing issues fall outside our responsibility. As our understanding evolves, we can refine these pre and post-check scripts to capture more detailed snapshots. We're also exploring more efficient methods to streamline this process, currently in beta testing.
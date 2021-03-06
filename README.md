onedrive-d
==================
This project intends to develop an OneDrive (formerly SkyDrive) daemon on (X)ubuntu based on the API of Mike Kazantsev's project `python-onedrive` (https://github.com/mk-fg/python-onedrive).

While you can use `onedrive-cli` command offered by `python-onedrive` project, the daemon tries to do the work automatically, and GUIs are being developed.

Branches
--------
 * **master**: the main branch
 * **wip**: stores the newest work

Description
-----------

Besides the `python-onedrive` base, there are a few major components in the project:

 * **DirScanner** scans the differences between the local and remote `dir`s, and merges them if needed
 	 * It does not delete files.
 	 * May undo file deletion or mess up the repo. But by far we prefer the safest approach.
 * **TaskWorker**
 	 * It executes the tasks issued by DirScanner objects
 	 * and waits to handle new tasks
 	 	 * **Tasks** are wrapped as objects
 * **LocalMonitor**
 	 * It forks a `inotifywait` process to monitor the OneDrive local repository.
 	 * and issue tasks for TaskWorkers to perform if there are any changes detected.
 * **RemoteMonitor**
 	 * Periodically gets the most recently changed files from OneDrive server _(planned)_
 	 * more at http://isdk.dev.live.com/dev/isdk/ISDK.aspx?category=scenarioGroup_skyDrive&index=6
 * **Linux Service**
 	 * The service will be installed to `/etc/init.d/onedrive-d`

Notice
--------

* (April 10, 2014) 
	 * Combined the UI experiments to the daemon
	 * Changed API and internal naming to reflect the renaming of `python-onedrive` project

Installation
--------------

 - Download the source from GitHub repo
 - In the source directory, run `sudo ./inst install` and go with the prompts
 - If the daemon fails to register, you may run `onedrive-d` command to have the daemon start
 
 Notes:
 
 Since the package is still under development, it will not run at system startup.

Homepage
-----------
Please visit: http://www.xybu.me/projects/skydrive-d/


Contact
--------
Xiangyu Bu
	 * website: http://xybu.me
	 * email: xybu92(at)live.com

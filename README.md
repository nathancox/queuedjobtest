This is a test case for the QueuedJobs error I'm having.

Instructions:
1) docker-compose up
2) dev/build
3) Go in to the CMS at localhost:8000 (login admin/admin)
4) Pick a page and give it an embargo time/date,, save it.
5) Go to http://localhost:8000/dev/tasks/ProcessJobQueueTask

Sometimes you have to repeat steps 4 and 5 two or three times before it has the following errors:

```
[2019-01-31 16:38:16] error-log.ERROR: Uncaught Exception Error: "Call to a member function hasMethod() on null" at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php line 161 {"exception":"[object] (Error(code: 0): Call to a member function hasMethod() on null at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php:161)"} []
[2019-01-31 16:52:45] error-log.ERROR: Uncaught Exception Error: "Call to a member function hasMethod() on null" at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php line 161 {"exception":"[object] (Error(code: 0): Call to a member function hasMethod() on null at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php:161)"} []
```

If you remove cwp-core from the composer requirements the error seems to stop.
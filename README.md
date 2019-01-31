This is a test case for the QueuedJobs error I'm having.

Instructions:
1) docker-compose up
2) composer install and dev/build
3) Go in to the CMS at localhost:8000 (login admin/admin)
4) Pick a page and give it an embargo time/date,, save it.
5) Go to http://localhost:8000/dev/tasks/ProcessJobQueueTask

Sometimes you have to repeat steps 4 and 5 two or three times before it has the following errors:


```
[Notice] Trying to get property of non-object
GET /dev/tasks/ProcessJobQueueTask
Line 216 in /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php

Source
207     {
208         $this->refreshDescriptor();
209 
210         // Treat completed jobs as cancelled when it comes to how Doorman handles picking up jobs to run
211         $cancelledStates = [
212             QueuedJob::STATUS_CANCELLED,
213             QueuedJob::STATUS_COMPLETE,
214         ];
215 
216         return in_array($this->descriptor->JobStatus, $cancelledStates, true);
217     }
218 }
Trace
Monolog\ErrorHandler->handleError(8, Trying to get property of non-object, /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php, 216, Array) 
DoormanQueuedJobTask.php:216
Symbiote\QueuedJobs\Jobs\DoormanQueuedJobTask->isCancelled() 
ProcessManager.php:521
AsyncPHP\Doorman\Manager\ProcessManager->isTaskCancelled(Symbiote\QueuedJobs\Jobs\DoormanQueuedJobTask) 
ProcessManager.php:465
AsyncPHP\Doorman\Manager\ProcessManager->canRemoveTask(Symbiote\QueuedJobs\Jobs\DoormanQueuedJobTask) 
ProcessManager.php:124
AsyncPHP\Doorman\Manager\ProcessManager->tick() 
DoormanRunner.php:70
Symbiote\QueuedJobs\Tasks\Engines\DoormanRunner->runQueue(2) 
QueuedJobService.php:1101
Symbiote\QueuedJobs\Services\QueuedJobService->runQueue(2) 
ProcessJobQueueTask.php:59
Symbiote\QueuedJobs\Tasks\ProcessJobQueueTask->run(SilverStripe\Control\HTTPRequest) 
TaskRunner.php:104
SilverStripe\Dev\TaskRunner->runTask(SilverStripe\Control\HTTPRequest) 
RequestHandler.php:323
SilverStripe\Control\RequestHandler->handleAction(SilverStripe\Control\HTTPRequest, runTask) 
Controller.php:284
SilverStripe\Control\Controller->handleAction(SilverStripe\Control\HTTPRequest, runTask) 
RequestHandler.php:202
SilverStripe\Control\RequestHandler->handleRequest(SilverStripe\Control\HTTPRequest) 
Controller.php:212
SilverStripe\Control\Controller->handleRequest(SilverStripe\Control\HTTPRequest) 
RequestHandler.php:226
SilverStripe\Control\RequestHandler->handleRequest(SilverStripe\Control\HTTPRequest) 
Controller.php:212
SilverStripe\Control\Controller->handleRequest(SilverStripe\Control\HTTPRequest) 
Director.php:361
SilverStripe\Control\Director->SilverStripe\Control\{closure}(SilverStripe\Control\HTTPRequest) 
VersionedHTTPMiddleware.php:41
SilverStripe\Versioned\VersionedHTTPMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
BasicAuthMiddleware.php:68
SilverStripe\Security\BasicAuthMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
AuthenticationMiddleware.php:61
SilverStripe\Security\AuthenticationMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
CanonicalURLMiddleware.php:188
SilverStripe\Control\Middleware\CanonicalURLMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HTTPCacheControlMiddleware.php:42
SilverStripe\Control\Middleware\HTTPCacheControlMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
ChangeDetectionMiddleware.php:27
SilverStripe\Control\Middleware\ChangeDetectionMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
FlushMiddleware.php:29
SilverStripe\Control\Middleware\FlushMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
RequestProcessor.php:66
SilverStripe\Control\RequestProcessor->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HybridSessionMiddleware.php:18
SilverStripe\HybridSessions\Control\HybridSessionMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
AllowedHostsMiddleware.php:60
SilverStripe\Control\Middleware\AllowedHostsMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
TrustedProxyMiddleware.php:176
SilverStripe\Control\Middleware\TrustedProxyMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
InitialisationMiddleware.php:53
CWP\Core\Control\InitialisationMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HTTPMiddlewareAware.php:65
SilverStripe\Control\Director->callMiddleware(SilverStripe\Control\HTTPRequest, Closure) 
Director.php:370
SilverStripe\Control\Director->handleRequest(SilverStripe\Control\HTTPRequest) 
HTTPApplication.php:48
SilverStripe\Control\HTTPApplication->SilverStripe\Control\{closure}(SilverStripe\Control\HTTPRequest) 
call_user_func(Closure, SilverStripe\Control\HTTPRequest) 
HTTPApplication.php:66
SilverStripe\Control\HTTPApplication->SilverStripe\Control\{closure}(SilverStripe\Control\HTTPRequest) 
call_user_func(Closure, SilverStripe\Control\HTTPRequest) 
ErrorControlChainMiddleware.php:73
SilverStripe\Core\Startup\ErrorControlChainMiddleware->SilverStripe\Core\Startup\{closure}(SilverStripe\Core\Startup\ErrorControlChain) 
call_user_func(Closure, SilverStripe\Core\Startup\ErrorControlChain) 
ErrorControlChain.php:235
SilverStripe\Core\Startup\ErrorControlChain->step() 
ErrorControlChain.php:225
SilverStripe\Core\Startup\ErrorControlChain->execute() 
ErrorControlChainMiddleware.php:92
SilverStripe\Core\Startup\ErrorControlChainMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\HTTPApplication->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HTTPMiddlewareAware.php:65
SilverStripe\Control\HTTPApplication->callMiddleware(SilverStripe\Control\HTTPRequest, Closure) 
HTTPApplication.php:67
SilverStripe\Control\HTTPApplication->execute(SilverStripe\Control\HTTPRequest, Closure, ) 
HTTPApplication.php:49
SilverStripe\Control\HTTPApplication->handle(SilverStripe\Control\HTTPRequest) 
index.php:26
[2019-01-31 16:52:44] No new jobs on queue 2
[Emergency] Uncaught Error: Call to a member function hasMethod() on null
GET /dev/tasks/ProcessJobQueueTask
Line 161 in /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php

Source
152     }
153 
154     /**
155      * @inheritdoc
156      *
157      * @return int
158      */
159     public function getExpiresIn()
160     {
161         if ($this->descriptor->hasMethod('getExpiresIn')) {
162             return $this->descriptor->getExpiresIn();
163         }
164 
165         return -1;
166     }
167 
Trace
Symbiote\QueuedJobs\Jobs\DoormanQueuedJobTask->getExpiresIn() 
ProcessManager.php:500
AsyncPHP\Doorman\Manager\ProcessManager->isTaskExpired(Symbiote\QueuedJobs\Jobs\DoormanQueuedJobTask) 
ProcessManager.php:465
AsyncPHP\Doorman\Manager\ProcessManager->canRemoveTask(Symbiote\QueuedJobs\Jobs\DoormanQueuedJobTask) 
ProcessManager.php:124
AsyncPHP\Doorman\Manager\ProcessManager->tick() 
DoormanRunner.php:70
Symbiote\QueuedJobs\Tasks\Engines\DoormanRunner->runQueue(2) 
QueuedJobService.php:1101
Symbiote\QueuedJobs\Services\QueuedJobService->runQueue(2) 
ProcessJobQueueTask.php:59
Symbiote\QueuedJobs\Tasks\ProcessJobQueueTask->run(SilverStripe\Control\HTTPRequest) 
TaskRunner.php:104
SilverStripe\Dev\TaskRunner->runTask(SilverStripe\Control\HTTPRequest) 
RequestHandler.php:323
SilverStripe\Control\RequestHandler->handleAction(SilverStripe\Control\HTTPRequest, runTask) 
Controller.php:284
SilverStripe\Control\Controller->handleAction(SilverStripe\Control\HTTPRequest, runTask) 
RequestHandler.php:202
SilverStripe\Control\RequestHandler->handleRequest(SilverStripe\Control\HTTPRequest) 
Controller.php:212
SilverStripe\Control\Controller->handleRequest(SilverStripe\Control\HTTPRequest) 
RequestHandler.php:226
SilverStripe\Control\RequestHandler->handleRequest(SilverStripe\Control\HTTPRequest) 
Controller.php:212
SilverStripe\Control\Controller->handleRequest(SilverStripe\Control\HTTPRequest) 
Director.php:361
SilverStripe\Control\Director->SilverStripe\Control\{closure}(SilverStripe\Control\HTTPRequest) 
VersionedHTTPMiddleware.php:41
SilverStripe\Versioned\VersionedHTTPMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
BasicAuthMiddleware.php:68
SilverStripe\Security\BasicAuthMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
AuthenticationMiddleware.php:61
SilverStripe\Security\AuthenticationMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
CanonicalURLMiddleware.php:188
SilverStripe\Control\Middleware\CanonicalURLMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HTTPCacheControlMiddleware.php:42
SilverStripe\Control\Middleware\HTTPCacheControlMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
ChangeDetectionMiddleware.php:27
SilverStripe\Control\Middleware\ChangeDetectionMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
FlushMiddleware.php:29
SilverStripe\Control\Middleware\FlushMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
RequestProcessor.php:66
SilverStripe\Control\RequestProcessor->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HybridSessionMiddleware.php:18
SilverStripe\HybridSessions\Control\HybridSessionMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
AllowedHostsMiddleware.php:60
SilverStripe\Control\Middleware\AllowedHostsMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
TrustedProxyMiddleware.php:176
SilverStripe\Control\Middleware\TrustedProxyMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
InitialisationMiddleware.php:53
CWP\Core\Control\InitialisationMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\Director->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HTTPMiddlewareAware.php:65
SilverStripe\Control\Director->callMiddleware(SilverStripe\Control\HTTPRequest, Closure) 
Director.php:370
SilverStripe\Control\Director->handleRequest(SilverStripe\Control\HTTPRequest) 
HTTPApplication.php:48
SilverStripe\Control\HTTPApplication->SilverStripe\Control\{closure}(SilverStripe\Control\HTTPRequest) 
call_user_func(Closure, SilverStripe\Control\HTTPRequest) 
HTTPApplication.php:66
SilverStripe\Control\HTTPApplication->SilverStripe\Control\{closure}(SilverStripe\Control\HTTPRequest) 
call_user_func(Closure, SilverStripe\Control\HTTPRequest) 
ErrorControlChainMiddleware.php:73
SilverStripe\Core\Startup\ErrorControlChainMiddleware->SilverStripe\Core\Startup\{closure}(SilverStripe\Core\Startup\ErrorControlChain) 
call_user_func(Closure, SilverStripe\Core\Startup\ErrorControlChain) 
ErrorControlChain.php:235
SilverStripe\Core\Startup\ErrorControlChain->step() 
ErrorControlChain.php:225
SilverStripe\Core\Startup\ErrorControlChain->execute() 
ErrorControlChainMiddleware.php:92
SilverStripe\Core\Startup\ErrorControlChainMiddleware->process(SilverStripe\Control\HTTPRequest, Closure) 
HTTPMiddlewareAware.php:62
SilverStripe\Control\HTTPApplication->SilverStripe\Control\Middleware\{closure}(SilverStripe\Control\HTTPRequest) 
HTTPMiddlewareAware.php:65
SilverStripe\Control\HTTPApplication->callMiddleware(SilverStripe\Control\HTTPRequest, Closure) 
HTTPApplication.php:67
SilverStripe\Control\HTTPApplication->execute(SilverStripe\Control\HTTPRequest, Closure, ) 
HTTPApplication.php:49
SilverStripe\Control\HTTPApplication->handle(SilverStripe\Control\HTTPRequest) 
index.php:26
```

From silverstripe.log:

```
[2019-01-31 16:38:16] error-log.ERROR: Uncaught Exception Error: "Call to a member function hasMethod() on null" at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php line 161 {"exception":"[object] (Error(code: 0): Call to a member function hasMethod() on null at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php:161)"} []
[2019-01-31 16:52:45] error-log.ERROR: Uncaught Exception Error: "Call to a member function hasMethod() on null" at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php line 161 {"exception":"[object] (Error(code: 0): Call to a member function hasMethod() on null at /var/www/html/vendor/symbiote/silverstripe-queuedjobs/src/Jobs/DoormanQueuedJobTask.php:161)"} []
```

If you remove cwp-core from the composer requirements the error seems to stop.

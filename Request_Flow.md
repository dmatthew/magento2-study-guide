# Request Flow

* All web requests go to \<DOCROOT\>/pub/index.php.
* The bootstrap class, `Magento\Framework\App\Bootstrap`, calls its `run` method.
* `Magento\Framework\App\Bootstrap::run` will launch the application using the `Magento\Framework\App\Http` class.
* `Magento\Framework\App\Http::launch` configures the object manager, the class which handles all the Dependency Injection magic.
* `Magento\Framework\App\Http::launch` will then call `Magento\Framework\App\FrontController::dispatch`, which is used to find a Controller which matches the request and then call the execute method of that Controller.

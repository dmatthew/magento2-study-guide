# Controllers

The "C" in MVC. In Magento, the controller is used for gathering request parameters, and then calling on other classes to manage this data. Controllers can also handle exceptions that occur during this process.

All frontend controller classes should extend the class `Magento\Framework\App\Action\Action` and all admin controller classes should extend the class `Magento\Backend\App\Action`.

### The "execute" method

All Controllers need to have an `execute` method. This is the method which is called by Magento\Framework\App\FrontController::dispatch when it has found a controller class which matches the request.

Controllers should return an instance of the `Magento\Framework\Controller\ResultInterface` class. Generally this is done with a result page factory object which gets initialzed by a View Helper.


#### Result Objects
The execute method should return a Result object.

|Result Object Name|Class|Description|
|----|----|----|
|Page|Magento\Framework\View\Result\Page|Used for returning html.|
|JSON|Magento\Controller\Result\Json|Used for returning JSON data.|
|Forward|Magento\Controller\Result\Forward|Used to internally forward to another controller action. Does not redirect the user to another url.|
|Redirect|Magento\Controller\Result\Redirect|Used to redirect the user to another url.|

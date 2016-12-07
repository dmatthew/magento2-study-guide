# Controllers

The "C" in MVC. In Magento, the controller is used for gathering request parameters, and then calling on other classes to manage this data. Controllers can also handle exceptions that occur during this process.

### The "execute" method

All Controllers need to have an `execute` method. This is the method which is called by Magento\Framework\App\FrontController::dispatch when it has found a controller class which matches the request.

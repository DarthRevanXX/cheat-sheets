Inversion of Control: class shouldn't create instances of own dependecies

Dependency Injection inside of a module:
- Add the @Injectable() decorator to service
- Add the service to the module list of providers
- Define the constructor method on service and add to the service

Dependency Injection from module to module
 - Module exports service
 - Import one module into another module(imports array)
 - Define the constructor method on service and add the service

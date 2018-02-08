# Symfony Functional Test

## Install
   ```` bash
   $ composer require php-solution/sf-functional-test
   ````

## Load environment variables from files
Add to your phpunit.xml listener and configure arguments(relative file paths from your phpunit.xml configuration file):
````XML 
<listener class="PhpSolution\FunctionalTest\PHPUnit\Listener\EnvLoader">
    <arguments>
        <array>
            <element key="0">
                <string>../.env</string>
            </element>
            <element key="1">
                <string>.env</string>
            </element>
        </array>
    </arguments>
</listener>
````

## Load Doctrine fixtures before test cases 
Add to your phpunit.xml Listener:
````    
<listener class="PhpSolution\FunctionalTest\PHPUnit\Listener\CommandLauncher">
    <arguments>
        <string>functional-test:fixtures:load</string>
    </arguments>
</listener>
````

## Run Doctrine migrations before test cases 
Add to your phpunit.xml Listener:
````    
<listener class="PhpSolution\FunctionalTest\PHPUnit\Listener\CommandLauncher">
    <arguments>
        <string>doctrine:migrations:migrate</string>
    </arguments>
</listener>
````
    
## Using Test case additional functionallity PhpSolution\FunctionalTest\TestCase\AppTestCase   
### Using Authorization:
1) Add to your config_test.yml:
````     
security:
    firewalls:
        your_secured_category:
            http_basic: ~
````
2)  Use on TestCase
````    
$client = $this->getAuthorizedClient('user_login', 'password');
````


### Work with Doctrine
1. Add OrmTrait to your TestCase

2. Get doctrine service(return $this->container->get('doctrine')):
````
$this->getDoctrine()
````  
3. Find Entity helper method:
````    
protected function findTestEntity($entityClass, $orderBy = 'id', $findBy = [])
````
   
4. Refresh Entity:
````
protected function refreshEntity($entity) 
````

## Example of correct project structure:
See correct project structure and configs for functional tests on [link](/examples/project-structure/)
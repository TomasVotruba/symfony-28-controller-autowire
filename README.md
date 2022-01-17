# Controller Autowire for Symfony 2.8

* ![](https://github.com/tomasvotruba/symfony-legacy-controller-autowire/actions/workflows/code_analysis.yaml/badge.svg)

This bundle does only 2 things:

- **1. registers controllers as services**
- **2. enables constructor autowiring for them**

Still wondering **why use controller as services**? Check [this](http://richardmiller.co.uk/2011/04/15/symfony2-controller-as-service) and
[this](http://php-and-symfony.matthiasnoback.nl/2014/06/how-to-create-framework-independent-controllers/) article.

## Install

```bash
composer require tomasvotruba/symfony-legacy-controller-autowire
```

Add bundle to `AppKernel.php`:

```php
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = [
            new TomasVotruba\SymfonyLegacyControllerAutowire\SymplifyControllerAutowireBundle(),
            // ...
        ];
    }
}
```


## Usage

```php
class SomeController
{
    private $someClass;

    public function __construct(SomeClass $someClass)
    {
        $this->someClass = $someClass;
    }
}
```


## Used to FrameworkBundle's controller? Use helpers traits!

Inspired by [pull](https://github.com/symfony/symfony/pull/18193) [requests](https://github.com/symfony/symfony/pull/20493) to Symfony and setter injection that are currently on-hold, **here are the traits you can use right now**:

```php
use TomasVotruba\SymfonyLegacyControllerAutowire\Controller\Routing\ControllerAwareTrait;

final class SomeController
{
    use ControllerAwareTrait;

    public function someAction()
    {
        $productRepository = $this->getDoctrine()->getRepository(Product::class);
        // ...

        return $this->redirectToRoute('my_route');
    }
}
```
 

### Do you prefer only traits you use?
 
```php
use TomasVotruba\SymfonyLegacyControllerAutowire\Controller\Routing\ControllerRoutingTrait;

final class SomeController
{
    use ControllerRoutingTrait;

    public function someAction()
    {
        return $this->redirectToRoute('my_route');
    }
}
```

Just type `Controller*Trait` in your IDE to autocomplete any of these traits.


That's all :)


## Contributing

Send [issue](https://github.com/Symplify/Symplify/issues) or [pull-request](https://github.com/Symplify/Symplify/pulls) to main repository.

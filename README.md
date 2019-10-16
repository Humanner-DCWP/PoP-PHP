![PoP](https://assets.getpop.org/wp-content/themes/getpop/img/pop-logo-horizontal.png)

# Implementation of PoP in PHP

PoP in PHP is an implementation of [PoP](https://github.com/leoloso/PoP), designed as a set of PHP packages distributed through [Composer](https://getcomposer.org). 

The core packages are:

1. [Component Model](https://github.com/getpop/component-model): Implementation of the basic component model, dealing with component data (but no configuration)
2. [Engine](https://github.com/getpop/engine): Adds services over the component model
3. [Configuration for Component Model](https://github.com/getpop/component-model-configuration): It adds a configuration layer to the component model

We can extend the core to implement applications, such as the following ones:

1. [API](https://github.com/getpop/api): Implements an API for retrieving/posting data with the PoP component model
3. [Site](https://github.com/getpop/site): Build a component-based website
4. [Static Site Generator](https://github.com/getpop/static-site-generator): Export a static version of the website

## Install

Follow the instructions for the corresponding platform:

- [PoP API for WordPress](https://github.com/leoloso/PoP-API-WP)
- Others coming soon...
<!--
- PoP API for Laravel + WordPress (coming soon)
- PoP site for WordPress (coming soon)
-->

## Codebase Migration

Many packages for PoP are currently being migrated to Composer. We are welcoming first-time contributors to help with the migration: This is a good way to become aquainted with PoP, and we will teach you all there is to know about its architecture.

To deal with the migration, many PoP packages have been split into 2:

1. The final package
2. A temporary, "migrate" package

The task is to migrate all code from the "migrate" to the final package, converting all code as required. The "migrate" package contains legacy PHP code written several years ago. The migration must introduce modern PHP techniques to the codebase, such as using Composer, dependency injection, autoloading, removal of global variables, use of services and others. Once the code migration for each package is complete, the corresponding "migrate" package can be deleted.

Migrating the code involves the implementation of the following features:

- Adding package dependencies in `composer.json`
- Identification of services and making them available through [Symfony's DependencyInjection component](https://symfony.com/doc/current/components/dependency_injection.html)
- Adding namespaces for all PHP classes following the [PSR-4](https://www.php-fig.org/psr/psr-4/) convention, as to support [autoloading through Composer](https://getcomposer.org/doc/01-basic-usage.md#autoloading)
- Shortening of classnames (eg: from the current `PoP_Posts_Module_Processor_PostsDataloads` to `Dataloads`, after placing the class under namespace `PoP\Posts\ModuleProcessors`)
- Using `use` statements to import fully-qualified (namespace+classname) classes at the top of the PHP file, to make the code more legible (eg: instead of repeatedly executing `\PoP\ComponentModel\Engine_Vars::getVars()`, we can first import the class with `use PoP\ComponentModel\Engine_Vars;` and then execute `Engine_Vars::getVars()`)
- Replacing all global variables (such as `$pop_cssresourceloaderprocessor_manager`) with a corresponding service

If you want to become involved, or simply want to find out more, please [contact Leo](mailto:leo@getpop.org).

## 🔥 Become involved!

Contributors are welcome! If either you want to get involved, or simply find out more about PoP, simply [send Leo an email](mailto:leo@getpop.org) or [tweet](https://twitter.com/losoviz) 😀❤️.

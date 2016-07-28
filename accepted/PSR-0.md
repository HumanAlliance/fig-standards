自动加载标准
====================

> **已过时** - 截止 2014-10-21 PSR-0 已经标记为弃用。推荐 [PSR-4] 作为替代。

[PSR-4]: http://www.php-fig.org/psr/psr-4/

下面介绍了必须遵守的autoloader规范。

规范
---------

* 一个标准的命名空间和类必须具有以下结构 `\<Vendor Name(组织)>\(<Namespace(命名空间)>\)*<Class Name(类)>`。
* 每个命名空间必须有一个顶级命名空间 ("Vendor Name")。
* 每个命名空间可以有多个子命名空间。
* 当加载文件时，每个命名空间分隔符会被转换为一个 `DIRECTORY_SEPARATOR(PHP内置常量，目录分隔符)` 。
* 类名中的 `_` 会被转换为一个 `DIRECTORY_SEPARATOR`。 命名空间中的`_` 没有特殊意义。
* 当加载文件时，标准的命名空间和类会加上后缀 `.php`。
* 组织、命名空间、类可以是由大小写字母组成

 示例
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

Underscores in Namespaces and Class Names
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

The standards we set here should be the lowest common denominator for
painless autoloader interoperability. You can test that you are
following these standards by utilizing this sample SplClassLoader
implementation which is able to load PHP 5.3 classes.

Example Implementation
----------------------

Below is an example function to simply demonstrate how the above
proposed standards are autoloaded.

~~~php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
spl_autoload_register('autoload');
~~~

SplClassLoader Implementation
-----------------------------

The following gist is a sample SplClassLoader implementation that can
load your classes if you follow the autoloader interoperability
standards proposed above. It is the current recommended way to load PHP
5.3 classes that follow these standards.

* [http://gist.github.com/221634](http://gist.github.com/221634)


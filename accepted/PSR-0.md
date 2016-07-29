自动加载规范
====================

> **已过时** - 截止 2014-10-21 PSR-0 已经标记为弃用。推荐 [PSR-4] 作为替代。

[PSR-4]: http://www.php-fig.org/psr/psr-4/

下面介绍了必须遵守的 autoloader 规范。

规范
---------

* 一个标准的命名空间和类名必须具有以下结构 `\<Vendor Name(组织名)>\(<Namespace(命名空间)>\)*<Class Name(类名)>`。
* 每个命名空间必须有一个顶级命名空间 ("Vendor Name")。
* 每个命名空间可以有多个子命名空间。
* 当加载文件时，每个命名空间分隔符会被转换为一个 `DIRECTORY_SEPARATOR(PHP内置常量，目录分隔符)` 。
* 类名中的 `_` 会被转换为一个 `DIRECTORY_SEPARATOR`。 命名空间中的 `_` 没有特殊意义。
* 当加载文件时，标准的命名空间和类名会加上后缀 `.php`。
* 组织、命名空间、类名可以是由大小写字母组成

 示例
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

命名空间和类名中的下划线
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

以上是 autoloader 的通用最低标准，可通过示例函数 SplClassLoader 载入 PHP 5.3 的类，来验证是否符合以上规范。

实例
----------------------

以下是按照以上规范进行自动加载的演示

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

SplClassLoader 实例
-----------------------------

下面的 gist 是一个简单的 SplClassLoader 导入类实例。推荐遵循以上规范加载 PHP 5.3 的类。

* [http://gist.github.com/221634](http://gist.github.com/221634)


# 自动加载

关键词 "必须", "一定不能", "需要", "将会", "不会", "应该",
"不该", "推荐", "可以", 和 "可选" 的详细描述可参见 [RFC 2119](http://tools.ietf.org/html/rfc2119)。


## 1. 概述

本 PSR [自动加载][] 是从文件路径导入类的自动加载规范。本规范是可互操作性的，可用在任何自动加载规范上，包括 [PSR-0][]。 此 PSR 同时规范了需要自动加载的文件保存路径。.


## 2. 规范

1. 术语"类" 包括 classes(类), interfaces(接口), traits, 和别的类似结构体。.

2. 一个标准的类应该是如下格式：

        \<NamespaceName(命名空间)>(\<SubNamespaceNames(子命名空间)>)*\<ClassName(类)>

    1. 一个标准的类 必须 有一个顶级命名空间，也称为 "vendor namespace"。

    2. 一个标准的类 可以 有一个或多个的子命名空间。

    3. 一个标准的类 必须 有一个最终的类。

    4. 一个标准的类中任何位置的下划线没有特殊意义。

    5. 一个标准的类中的字母 可以 是由大小写字母组成。

    6. 所有的类必须以大小写敏感的方式被引用。

3. 按照标准类加载相应的文件 ...

    1. 一个或多个命名空间和子命名空间。不包括开头的命名空间分割符(最前面的 `/`)，在标准的类中，("命名空间前缀") 与至少一个
       "基目录"相对应。

    2. 跟随 "命名空间前缀" 后面的子命名命名空间和子目录包括"基目录"相匹配，命名空间分隔符将作为目录分割符，子目录 必须 与子命名空间相匹配。.

    3. 最终的类必须和以 `.php` 作为结尾的文件相匹配。

4. 自动加载的实现一定不能 抛出异常，一定不能触发任何等级的错误，不应该 有返回值。


## 3. 示例

下面的表格给出了标准的类、命名空间和基目录对应的文件目录。

| 完整类名                      | 命名空间前缀      | 基目录                   |文件路径
| ------------------------ |-----------------|----------------------|-------------------------------------------
| \Acme\Log\Writer\File_Writer  | Acme\Log\Writer    | ./acme-log-writer/lib/   | ./acme-log-writer/lib/File_Writer.php
| \Aura\Web\Response\Status     | Aura\Web           | /path/to/aura-web/src/   | /path/to/aura-web/src/Response/Status.php
| \Symfony\Core\Request         | Symfony\Core       | ./vendor/Symfony/Core/   | ./vendor/Symfony/Core/Request.php
| \Zend\Acl                     | Zend               | /usr/includes/Zend/      | /usr/includes/Zend/Acl.php

本示例按照规范实现了自动加载，更多示例，请参阅 [示例文件][]. 本示例 不 属规范的一部分并且随时会有所变动

[自动加载]: http://php.net/autoload
[PSR-0]: https://github.com/HumanAlliance/fig-standards/blob/master/accepted/PSR-0.md
[示例文件]: https://github.com/HumanAlliance/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md

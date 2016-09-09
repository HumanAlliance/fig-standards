Logger Interface
================

This document describes a common interface for logging libraries.

The main goal is to allow libraries to receive a `Psr\Log\LoggerInterface`
object and write logs to it in a simple and universal way. Frameworks
and CMSs that have custom needs MAY extend the interface for their own
purpose, but SHOULD remain compatible with this document. This ensures
that the third-party libraries an application uses can write to the
centralized application logs.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

The word `implementor` in this document is to be interpreted as someone
implementing the `LoggerInterface` in a log-related library or framework.
Users of loggers are referred to as `user`.

[RFC 2119]: http://tools.ietf.org/html/rfc2119

1. Specification
-----------------

### 1.1 Basics

- The `LoggerInterface` exposes eight methods to write logs to the eight
  [RFC 5424][] levels (debug, info, notice, warning, error, critical, alert,
  emergency).

- A ninth method, `log`, accepts a log level as first argument. Calling this
  method with one of the log level constants MUST have the same result as
  calling the level-specific method. Calling this method with a level not
  defined by this specification MUST throw a `Psr\Log\InvalidArgumentException`
  if the implementation does not know about the level. Users SHOULD NOT use a
  custom level without knowing for sure the current implementation supports it.

[RFC 5424]: http://tools.ietf.org/html/rfc5424

### 1.2 Message

- Every method accepts a string as the message, or an object with a
  `__toString()` method. Implementors MAY have special handling for the passed
  objects. If that is not the case, implementors MUST cast it to a string.

- The message MAY contain placeholders which implementors MAY replace with
  values from the context array.

  Placeholder names MUST correspond to keys in the context array.

  Placeholder names MUST be delimited with a single opening brace `{` and
  a single closing brace `}`. There MUST NOT be any whitespace between the
  delimiters and the placeholder name.

  Placeholder names SHOULD be composed only of the characters `A-Z`, `a-z`,
  `0-9`, underscore `_`, and period `.`. The use of other characters is
  reserved for future modifications of the placeholders specification.

  Implementors MAY use placeholders to implement various escaping strategies
  and translate logs for display. Users SHOULD NOT pre-escape placeholder
  values since they can not know in which context the data will be displayed.

  The following is an example implementation of placeholder interpolation
  provided for reference purposes only:

  ~~~php
  /**
   * Interpolates context values into the message placeholders.
   */
  function interpolate($message, array $context = array())
  {
      // build a replacement array with braces around the context keys
      $replace = array();
      foreach ($context as $key => $val) {
          // check that the value can be casted to string
          if (!is_array($val) && (!is_object($val) || method_exists($val, '__toString'))) {
              $replace['{' . $key . '}'] = $val;
          }
      }

      // interpolate replacement values into the message and return
      return strtr($message, $replace);
  }

  // a message with brace-delimited placeholder names
  $message = "User {username} created";

  // a context array of placeholder names => replacement values
  $context = array('username' => 'bolivar');

  // echoes "User bolivar created"
  echo interpolate($message, $context);
  ~~~

### 1.3 Context

- Every method accepts an array as context data. This is meant to hold any
  extraneous information that does not fit well in a string. The array can
  contain anything. Implementors MUST ensure they treat context data with
  as much lenience as possible. A given value in the context MUST NOT throw
  an exception nor raise any php error, warning or notice.

- If an `Exception` object is passed in the context data, it MUST be in the
  `'exception'` key. Logging exceptions is a common pattern and this allows
  implementors to extract a stack trace from the exception when the log
  backend supports it. Implementors MUST still verify that the `'exception'`
  key is actually an `Exception` before using it as such, as it MAY contain
  anything.

### 1.4 Helper classes and interfaces

- The `Psr\Log\AbstractLogger` class lets you implement the `LoggerInterface`
  very easily by extending it and implementing the generic `log` method.
  The other eight methods are forwarding the message and context to it.

- Similarly, using the `Psr\Log\LoggerTrait` only requires you to
  implement the generic `log` method. Note that since traits can not implement
  interfaces, in this case you still have to implement `LoggerInterface`.

- The `Psr\Log\NullLogger` is provided together with the interface. It MAY be
  used by users of the interface to provide a fall-back "black hole"
  implementation if no logger is given to them. However conditional logging
  may be a better approach if context data creation is expensive.

- The `Psr\Log\LoggerAwareInterface` only contains a
  `setLogger(LoggerInterface $logger)` method and can be used by frameworks to
  auto-wire arbitrary instances with a logger.

- The `Psr\Log\LoggerAwareTrait` trait can be used to implement the equivalent
  interface easily in any class. It gives you access to `$this->logger`.

- The `Psr\Log\LogLevel` class holds constants for the eight log levels.

2. Package
----------

The interfaces and classes described as well as relevant exception classes
and a test suite to verify your implementation is provided as part of the
[psr/log](https://packagist.org/packages/psr/log) package.

3. `Psr\Log\LoggerInterface`
----------------------------

~~~php
<?php

namespace Psr\Log;

/**
 * Describes a logger instance 日志实例
 *
 * The message MUST be a string or object implementing __toString().消息 必须 是字符串或对象 通过_toString()来保证实施
 *
 * The message MAY contain placeholders in the form: {foo} where foo
 * will be replaced by the context data in key "foo".消息 可以 包含占位符。 占位符会被内容的功能代替
 *
 * The context array can contain arbitrary data, the only assumption that
 * can be made by implementors is that if an Exception instance is given
 * to produce a stack trace, it MUST be in a key named "exception".其他文本可以包含任何数据，如果出现异常错误，必须命名为 异常
 *
 * See https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
 * for the full interface specification.
 */
interface LoggerInterface
{
    /**
     * System is unusable.系统不用
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function emergency($message, array $context = array());

    /**
     * Action must be taken immediately.必须采取措施
     *
     * Example: Entire website down, database unavailable, etc. This should
     * trigger the SMS alerts and wake you up.如网站挂掉，数据库不可用等。应该有个短信trigger提醒。 
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function alert($message, array $context = array());

    /**
     * Critical conditions.关键条件
     *
     * Example: Application component unavailable, unexpected exception.如 应用组件不可用 系统异常
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function critical($message, array $context = array());

    /**
     * Runtime errors that do not require immediate action but should typically
     * be logged and monitored.运行错误不需要立即采取行动，但应该记录和监控
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function error($message, array $context = array());

    /**
     * Exceptional occurrences that are not errors.特殊事件，但不是错误
     *
     * Example: Use of deprecated APIs, poor use of an API, undesirable things
     * that are not necessarily wrong.如api错误 不建议的api
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function warning($message, array $context = array());

    /**
     * Normal but significant events.正常但显著的事件
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function notice($message, array $context = array());

    /**
     * Interesting events.关注的事件
     *
     * Example: User logs in, SQL logs.用户登录 sql
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function info($message, array $context = array());

    /**
     * Detailed debug information.详细的调试信息
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function debug($message, array $context = array());

    /**
     * Logs with an arbitrary level.选择等级
     *
     * @param mixed $level
     * @param string $message
     * @param array $context
     * @return null
     */
    public function log($level, $message, array $context = array());
}
~~~

4. `Psr\Log\LoggerAwareInterface`
---------------------------------

~~~php
<?php

namespace Psr\Log;

/**
 * Describes a logger-aware instance 记录器实例
 */
interface LoggerAwareInterface
{
    /**
     * Sets a logger instance on the object 设置一个记录器对象
     *
     * @param LoggerInterface $logger
     * @return null
     */
    public function setLogger(LoggerInterface $logger);
}
~~~

5. `Psr\Log\LogLevel`
---------------------

~~~php
<?php

namespace Psr\Log;

/**
 * Describes log levels 日志等级描述
 */
class LogLevel
{
    const EMERGENCY = 'emergency';//紧急
    const ALERT     = 'alert';//警报
    const CRITICAL  = 'critical';//关键
    const ERROR     = 'error';//错误
    const WARNING   = 'warning';//警告
    const NOTICE    = 'notice';//通知
    const INFO      = 'info';//信息
    const DEBUG     = 'debug';//调试
}
~~~

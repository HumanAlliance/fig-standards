# PHP 建议标准

根据 [PSR 工作流章程][workflow] ，每一个 PSR 都有一个状态。提案通过投票后会成为草案。发布不会有变化，草案会变化很大，审议只会有轻微变化。

[PSR 工作流章程][workflow]还规定了， ，成为 PSR 的编辑、贡献，需要两名成员组成员的支持。这些成员和发起人一同管理、审查和投票。

## 按状态

### 发布

| 序号 | 标题                           | 编辑                    |  贡献         | 发起           |
|:----:|--------------------------------|-------------------------|---------------|----------------|
| 1    | [Basic Coding Standard][psr1]  | Paul M. Jones           | _N/A_         | _N/A_          |
| 2    | [Coding Style Guide][psr2]     | Paul M. Jones           | _N/A_         | _N/A_          |
| 3    | [Logger Interface][psr3]       | Jordi Boggiano          | _N/A_         | _N/A_          |
| 4    | [自动加载规范][psr4]           | Paul M. Jones           | Phil Sturgeon | Larry Garfield |
| 6    | [Caching Interface][psr6]      | Larry Garfield          | Paul Dragoonis | Robert Hafner |
| 7    | [HTTP Message Interface][psr7] | Matthew Weier O'Phinney | Beau Simensen | Paul M. Jones  |

### 审议

| 序号 | 标题                          | 编辑                     |  贡献          | 发起          |
|:----:|--------------------------------|-------------------------|----------------|---------------|

### 草案

| 序号 | 标题                                | 编辑                            |  贡献                   | 发起              |
|:----:|--------------------------------------|--------------------------------|-------------------------|-------------------|
| 5    | [PHPDoc Standard][psr5]              | Mike van Riel                  | Vacant                  | Vacant            |
| 8    | [Huggable Interface][psr8]           | Larry Garfield                 | Vacant                  | Paul M. Jones     |
| 9    | [Security Advisories][psr9]          | Michael Hess                   | Korvin Szanto           | Larry Garfield    |
| 10   | [Security Reporting Process][psr10]  | Michael Hess                   | Larry Garfield          | Korvin Szanto     |
| 11   | [Container Interface][psr11]         | Matthieu Napoli, David Négrier | Paul M. Jones           | Vacant            |
| 12   | [Extended Coding Style Guide][psr12] | Korvin Szanto                  | Alexander Makarov       | Robert Deutz      |
| 13   | [Hypermedia Links][psr13]            | Larry Garfield                 | Matthew Weier O'Phinney | Marc Alexander    |
| 14   | [Event Manager][psr14]               | Chuck Reeves                   | Brian Retterer          | Roman Tsiupa      |
| 15   | [HTTP Middlewares][psr15]            | Woody Gilk                     | Paul M Jones            | Jason Coward      |
| 16   | [Simple Cache][psr16]                | Paul Dragoonis                 | Jordi Boggiano          | Fabien Potencier  |
| 17   | [HTTP Factories][psr17]              | Woody Gilk                     | Roman Tsiupa            | Paul M Jones      |

### 过时

| 序号 | 标题                          | 编辑                    |  贡献         | 发起           |
|:---:|--------------------------------|-------------------------|---------------|----------------|
| 0   | [自动加载规范][psr0]           | Matthew Weier O'Phinney | _N/A_         | _N/A_          |

## 按序号

| 状态   | 序号 | 标题                                | 编辑                           |  贡献                   | 发起              |
|--------|:---:|--------------------------------------|--------------------------------|-------------------------|-------------------|
| X      | 0   | [自动加载规范][psr0]                 | Matthew Weier O'Phinney        | _N/A_                   | _N/A_             |
| A      | 1   | [Basic Coding Standard][psr1]        | Paul M. Jones                  | _N/A_                   | _N/A_             |
| A      | 2   | [Coding Style Guide][psr2]           | Paul M. Jones                  | _N/A_                   | _N/A_             |
| A      | 3   | [Logger Interface][psr3]             | Jordi Boggiano                 | _N/A_                   | _N/A_             |
| A      | 4   | [自动加载规范][psr4]                 | Paul M. Jones                  | Phil Sturgeon           | Larry Garfield    |
| D      | 5   | [PHPDoc Standard][psr5]              | Mike van Riel                  | Vacant                  | Vacant            |
| A      | 6   | [Caching Interface][psr6]            | Larry Garfield                 | Paul Dragoonis          | Robert Hafner     |
| A      | 7   | [HTTP Message Interface][psr7]       | Matthew Weier O'Phinney        | Beau Simensen           | Paul M. Jones     |
| D      | 8   | [Huggable Interface][psr8]           | Larry Garfield                 | Vacant                  | Paul M. Jones     |
| D      | 9   | [Security Advisories][psr9]          | Michael Hess                   | Korvin Szanto           | Larry Garfield    |
| D      | 10  | [Security Reporting Process][psr10]  | Michael Hess                   | Larry Garfield          | Korvin Szanto     |
| D      | 11  | [Container Interface][psr11]         | Matthieu Napoli, David Négrier | Paul M. Jones           | Vacant            |
| D      | 12  | [Extended Coding Style Guide][psr12] | Korvin Szanto                  | Alexander Makarov       | Robert Deutz      |
| D      | 13  | [Hypermedia Links][psr13]            | Larry Garfield                 | Matthew Weier O'Phinney | Marc Alexander    |
| D      | 14  | [Event Manager][psr14]               | Chuck Reeves                   | Brian Retterer          | Roman Tsiupa      |
| D      | 15  | [HTTP Middlewares][psr15]            | Woody Gilk                     | Paul M Jones            | Jason Coward      |
| D      | 16  | [Simple Cache][psr16]                | Paul Dragoonis                 | Jordi Boggiano          | Fabien Potencier  |
| D      | 17  | [HTTP Factories][psr17]              | Woody Gilk                     | Roman Tsiupa            | Paul M Jones      |

_**说明:** A = 发布 | D = 草案 | R = 审议 | X = 过时_

[workflow]: http://www.php-fig.org/bylaws/psr-workflow/
[psr0]: /accepted/PSR-0.md
[psr1]: /accepted/PSR-1.md
[psr2]: /accepted/PSR-2.md
[psr3]: /accepted/PSR-3.md
[psr4]: /accepted/PSR-4.md
[psr5]: https://github.com/phpDocumentor/fig-standards/tree/master/proposed
[psr6]: /accepted/PSR-6.md
[psr7]: /accepted/PSR-7.md
[psr8]: https://github.com/php-fig/fig-standards/blob/master/proposed/psr-8-hug
[psr9]: https://github.com/php-fig/fig-standards/blob/master/proposed/security-disclosure-publication.md
[psr10]: https://github.com/php-fig/fig-standards/blob/master/proposed/security-reporting-process.md
[psr11]: https://github.com/container-interop/fig-standards/blob/master/proposed/container.md
[psr12]: https://github.com/php-fig/fig-standards/blob/master/proposed/extended-coding-style-guide.md
[psr13]: https://github.com/php-fig/fig-standards/blob/master/proposed/links.md
[psr14]: https://github.com/php-fig/fig-standards/blob/master/proposed/event-manager.md
[psr15]: https://github.com/php-fig/fig-standards/blob/master/proposed/http-middleware
[psr16]: https://github.com/php-fig/fig-standards/blob/master/proposed/simplecache.md
[psr17]: https://github.com/php-fig/fig-standards/tree/master/proposed/http-factory

如果对我的文章感兴趣，可加入我的知识星球，这里面会记录我的所见所学。

![知识星球](imgs/知识星球.jpeg)

原文在 [这里](https://stitcher.io/blog/laravel-beyond-crud-01-domain-oriented-laravel)，本文将结合自己的理解进行介绍。

这一讲要表达的是**领域驱动设计**的思想以及在 Laravel 应用的体现。我们从一个简单的酒店管理应用说起

> 实现一个酒店管理应用，包括了客户管理、预定管理、库存管理、发票管理等模块。

按照 Lavavel 的设计，我们会把将代码以控制器、模型、路由、视图等等来进行组织。

这样的代码只能说符合 Laravel 的目录规范，并不能反映出应用的业务逻辑。不管是开发者，还是客户，都无法从这样的代码组织目录中获取业务信息。随着业务复杂度不断的增加，代码的就会变得越来越难以维护。

所以复杂点的应用就不能按照 Laravel 的默认目录来组织代码了，而应当是基于领域来进行组织。通俗的说，就是将相关的业务需求组织在一起，构成一个个领域模型。这样做的目的就是：**让你的代码反映出你的业务需求**。

根据这点，可以将代码简单的划分为两部分：

* 领域层 - 业务需求的实现
* 应用层 - 不包括业务规则，只是负责领域层与用户层的通信

可以这样组织代码

```
// 领域层
app/Domain/Invoices/
    ├── Actions
    ├── QueryBuilders
    ├── Collections
    ├── DataTransferObjects
    ├── Events
    ├── Exceptions
    ├── Listeners
    ├── Models
    ├── Rules
    └── States

app/Domain/Customers/

// 应用层
The admin HTTP application
app/App/Admin/
    ├── Controllers
    ├── Middlewares
    ├── Requests
    ├── Resources
    └── ViewModels

The REST API application
app/App/Api/
    ├── Controllers
    ├── Middlewares
    ├── Requests
    └── Resources

The console application
app/App/Console/
    └── Commands
```

这样做破坏了 Laravel 单 APP 入口的约定。如果不想破坏约定，也可以简单的将领域以[模块化](https://learnku.com/laravel/t/35007)的方式进行组织。这样做虽然没有划分的那么细致，但是也体现了领域驱动设计的思想。

```
|- app/
   |- Http/
      |- Controllers/
      |- Middleware/
   |- Providers/
   |- Account/
      |- Console/
      |- Exceptions/
      |- Events/
      |- Jobs/
      |- Listeners/
      |- Models/
         |- User.php
         |- Role.php
         |- Permission.php
      |- Repositories/
      |- Presenters/
      |- Transformers/
      |- Validators/
      |- Auth.php
      |- Acl.php
   |- Merchant/
   |- Payment/
   |- Invoice/
|- resources/
|- routes/
```

具体使用哪种方式，并没有严格规定，怎么舒服怎么来，关键竖立起领域驱动设计的思想。




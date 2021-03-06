# Laravel 5.x Scaffold Generator

[![Travis](https://img.shields.io/travis/summerblue/generator.svg?style=flat-square)](https://github.com/summerblue/generator)
[![Packagist](https://img.shields.io/packagist/dt/summerblue/generator.svg?style=flat-square)](https://packagist.org/packages/summerblue/generator)
[![Tag](https://img.shields.io/github/tag/summerblue/generator.svg)](https://github.com/summerblue/generator/tags)

Laravel Scaffold Generator, for Laravel 5.3.

## Install

### Step 1: Install Through Composer

```
composer require 'summerblue/generator' --dev
```

### Step 2: Add the Service Provider

Open `/app/Providers/AppServiceProvider.php` and, to your **register** function, add:

```
public function register()
{
     if (app()->environment() == 'local' || app()->environment() == 'testing') {

        $this->app->register(\Summerblue\Generator\GeneratorsServiceProvider::class);

    }
}
```

### Step 3: Run Artisan!

You're all set. Run `php artisan` from the console, and you'll see the new commands `make:scaffold`.

## Examples

Use this command to generator scaffolding of **Project** in your project:

> php artisan make:scaffold Projects --schema="name:string:index,description:text:nullable,subscriber_count:integer:unsigned:default(0)"

This command will generate:

```
$ php artisan make:scaffold Projects --schema="name:string:index,description:text:nullable,subscriber_count:integer:unsigned:default(0)"


----------- scaffolding: Project -----------

+ ./database/migrations/2017_04_17_065656_create_projects_table.php
+ ./database/factories/ModelFactory.php
+ ./database/seeds/ProjectsTableSeeder.php
+ ./database/seeds/DatabaseSeeder.php (Updated)
x ./app/Models/Model.php (Skipped)
+ ./app/Models/Project.php
+ ./app/Http/Controllers/ProjectsController.php
x ./app/Http/Requests/Request.php (Skipped)
+ ./app/Http/Requests/ProjectRequest.php
+ ./app/Observers/ProjectObserver.php
+ ./app/Providers/AppServiceProvider.php (Updated)
x ./app/Policies/Policy.php
+ ./app/Policies/ProjectPolicy.php
+ ./app/Providers/AuthServiceProvider.php (Updated)
+ ./routes/web.php (Updated)

--- Views ---
   + create_and_edit.blade.php
   + index.blade.php
   + show.blade.php
x ./resources/views/error.blade.php
Migrated: 2017_04_17_065656_create_projects_table

----------- -------------------- -----------
-----------   >DUMP AUTOLOAD<    -----------
```

## Explain

Generate the following:

- Migration
- Seed, add ModelFactory entry, and DatabaseSeeder entry
- Base Model class, Model and helper trait
- Resource Controller
- Base FormRequest class and StoreRequest, UpdateRequest
- Policy and Policy base class, auto register AuthServiceProvider class
- Update routes file to register resource route
- Add error page view
- Create and Edit action share the same view

## Future Plan

- API
- Admin
- Auto fill FormRequest rule
- Auto fill ModelFactory filed

## Screenshot

![file](https://cloud.githubusercontent.com/assets/324764/22488519/7466a638-e84d-11e6-8201-99ad377d6270.png)

## Thinks to
- [laralib/l5scaffold](https://github.com/laralib/l5scaffold)

##使用方法:
```
-1、通过composer安装扩展 composer require 'summerblue/generator:~0.5' --dev
-2、php artisan make:scaffold Projects --schema="name:string:index,description:text:nullable,subscriber_count:integer:unsigned:default(0)"
可以生成控制器、模型、迁移文件、表单验证类、授权类等一系列文件
解释:
创建话题的数据库迁移文件 —— 2017_09_26_111713_create_topics_table.php；
创建话题数据工厂文件 —— TopicFactory.php；
创建话题数据填充文件 —— TopicsTableSeeder.php；
创建模型基类文件 —— Model.php， 并创建话题数据模型；
创建话题控制器 —— TopicsController.php；
创建表单请求的基类文件 —— Request.php，并创建话题表单请求验证类；
创建话题模型事件监控器 TopicObserver 并在 AppServiceProvider 中注册；
创建授权策略基类文件 —— Policy.php，同时创建话题授权类，并在 AuthServiceProvider 中注册；
在 web.php 中更新路由，新增话题相关的资源路由；
新建符合资源控制器要求的三个话题视图文件，并存放于 resources/views/topics 目录中；
执行了数据库迁移命令 artisan migrate；
因此次操作新建了多个文件，最终执行 composer dump-autoload 来生成 classmap。
```

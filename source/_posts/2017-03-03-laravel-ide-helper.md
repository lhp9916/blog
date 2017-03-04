---
title: Laravel-ide-helper 高效的 IDE 智能提示插件
date: 2017-03-03 21:00:32
tags:
categories: 技术分享
---
barryvdh/laravel-ide-helper 扩展包能让你的 IDE ( PHPStorm, Sublime ) 实现自动完成、代码智能提示和代码跟踪等功能，大大提高你的开发效率。

### 安装

1). 使用 Composer 安装该扩展包：
```
composer require barryvdh/laravel-ide-helper
```
2). 安装完成后，在 config/app.php 添加以下内容到 providers 数组。
```php
Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
```
3). 接下来运行以下命令生成代码对应文档：
```
php artisan ide-helper:generate
```
由于使用此扩展包会生成相应的代码结构文件, 这些文件可能只有当前的开发者的 IDE 需要, 因此需要添加对应配置到 .gitignore 文件中：
```
.idea
_ide_helper.php
_ide_helper_models.php
.phpstorm.meta.php
```
为了后续方便，你也可以在composer.json文件中作如下配置：
```json
"scripts":{
    "post-update-cmd": [
        "Illuminate\\Foundation\\ComposerScripts::postUpdate",
        "php artisan ide-helper:generate",
        "php artisan ide-helper:meta",
        "php artisan optimize"
    ]
},
```

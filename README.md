# Micon
Provides functionality for adding IcoMoon icon packages to Drupal and exposing
them for use via CSS, HTML classes, and programmatically.

## Installing

The Micon module can be installed the same way typical Drupal modules are installed. There are no dependencies.

## Adding IcoMoon packages

Visit https://icomoon.io and build an icon package. You can utilize either **font** packages or **image** packages. Download the zip file provided by IcoMoon.

Go to /admin/structure/micon and click the Add Micon Package button. Then give your package a name. *A class prefix is added automatically but it is recommended to keep the class prefix as short as is reasonably possible as it is used in both CSS files and within the icon markup and the shorter it is, the smaller your rendered code and dependencies will be.* Place the IcoMoon zip file into the file upload field, click save, and you are done.

Published packages are immediately available for use site-wide.

## Usage

***Via CSS and HTML***
The Micon admin interface provides an overview of all icons along with information on how to use them via CSS and raw HTML.

***Use with twig syntax:***
`{{ micon('fa-user') }}`

***Use within render array:***
```php
array(
  '#theme' => 'iconify_icon',
  '#icon' => 'fa-user',
);
```

***Use to attach icon to translatable text***
```php
// Translatable text
t('Hello World');
// Translatable text with icon
micon('Hello World')->setIcon('fa-user');
```

***Use translatable icon trait***
```php
// Drop in replacement
use Drupal\micon\MiconIconizeTrait;
class myClass {
    use MiconIconizeTrait;

    protected $title = 'Hello World';

    public function getTitleWithIcon() {
        return $this->micon($this->title)->setIcon('fa-user');
    }
}
```

***Automatic icon replacement***

Modules and themes can add a NAME.micon.icons.yml that can define text that will be matched to icons.

```yml
// Exact match
user:
  text: hello world
  icon: fa-user
// Regular expression match
user_loose:
  text: ^hello
  icon: fa-user
```

When icon definitions are defined this way, modules and themes can utilize any of the above methods of icon placement *without* having to specify an icon in code.

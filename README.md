# Lagan Translation Extension

This repository provides a twig extension class for the twig view parser. 
The class adds a translate helper function  for the use in twig templates.
The translator function tries to call the trans() function of an 
Illuminate\Translation\Translator object in the slim DI container. 

Is an adaptation of dkesberg/slim-twig-translation-extension to Slim 3 framework. 

Is intended to use with Lagan CMS (https://www.laganphp.com/)

## How to install

#### using [Composer](http://getcomposer.org/)

Create a composer.json file in your project root:
    
```json
{
    "require": {
        "aureliopons/lagan_translate": "dev-master"
    }
}
```

Then run the following composer command:

```bash
$ php composer.phar install
```

## How to use

### Twig template

In your twig template you would write:

```
  {{ translate('male') }}
```
  
You can also use the shorthand:

```
  {{ _('male') }}
```

### Adding to Lagan

At public/index.php add

```php
$view->addExtension( new \Aureliopons\Slim\Twig\Extension\TranslationExtension() );
```

And use as a simple injection, using ROOT_PATH to reference 'lang' folder:

```php
use Illuminate\Translation\Translator;
use Illuminate\Filesystem\Filesystem;
use Illuminate\Translation\FileLoader;

$translator = new Translator(new FileLoader(new Filesystem(), ROOT_PATH . '\lang'), 'en');
$translator->setFallback('en');
$app->translator = $translator;
```

Then you can create \lang\en folder with your translations array

```php
return array(
  'hello'    => 'Hello World!'  
);
```

Add new folders for different languages.
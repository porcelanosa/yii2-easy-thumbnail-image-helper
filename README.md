Easy Thumbnail Image Helper for Yii2
========================

Yii2 helper for creating and caching thumbnails on real time.

Installation
------------
The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

* Either run

```
php composer.phar require "porcelanosa/yii2-easy-thumbnail-image-helper" "*"
```
or add

```json
"porcelanosa/yii2-easy-thumbnail-image-helper" : "*"
```

to the require section of your application's `composer.json` file.

* Add a new component in `components` section of your application's configuration file (optional), for example:

```php
'components' => [
    'thumbnail' => [
        'class' => 'himiklab\thumbnail\EasyThumbnail',
        'cacheAlias' => 'assets/gallery_thumbnails',
    ],
],
```

and in `bootstrap` section, for example:

```php
'bootstrap' => ['log', 'thumbnail'],
```

It is necessary if you want to set global helper's settings for the application.

Usage
-----
For example:

```php
use porcelanosa\thumbnail\EasyThumbnailImage;

echo EasyThumbnailImage::thumbnailImg(
    $model->pictureFile,
    50,
    50,
    EasyThumbnailImage::THUMBNAIL_OUTBOUND,
    ['alt' => $model->pictureName]
);
```

For other functions please see the source code.

If you want to handle errors that appear while converting to thumbnail by yourself, please make your own class and inherit it from EasyThumbnailImage. In your class replace only protected method errorHandler. For example

```php
class ThumbHelper extends \porcelanosa\thumbnail\EasyThumbnailImage
{

    protected static function errorHandler($error, $filename)
    {
        if ($error instanceof \porcelanosa\thumbnail\FileNotFoundException) {
            return \yii\helpers\Html::img('@web/images/notfound.png');
        } else {
            $filename = basename($filename);
            return \yii\helpers\Html::a($filename,"@web/files/$filename");
        }
    }
} 
```

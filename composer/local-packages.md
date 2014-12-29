# Composer وتنصيب مستودع من الحاسوب

أقوم باستخدام [Composer](http://getcomposer.org) لإدارة المشاريع التي أعمل عليها في حاسوبي. 

```json
{
    "repositories": [
        {
            "type": "vcs",
            "url" : "git@bitbucket.org:haykalmedia/customizable-sharing-buttons"
        },
        {
            "type":"vcs",
            "url":"/home/ammar/www/packages/re-subscribe"
        }
    ],
    "require": {
        "php": ">=5.4",
        "haykalmedia/customizable-sharing-buttons" : "dev-master",
        "haykalmedia/re-subscribe": "dev-feature/extract-variables-to-options-page"
    }
}
```


مترجمة بتصرّف من:
http://marekkalnik.tumblr.com/post/22929686367/composer-installing-package-from-local-git

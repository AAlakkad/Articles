[TOC]
# Scripts & Styles

مرّ معنا أثناء إضافة أرقام الصفحات كيف أضفنا ملف CSS جديد عن طريق وضع بضعة أسطر في ملف `functions.php` في ملفات القالب. سنتناول في هذا الدرس الشرح التفصيلي والفائدة من تلك الطريقة، وكيف أن جميع ملفات JavaScript و CSS يجب أن يتم استخدامها بتلك الطريقة.

## الخطوات العامة
تسجيل الملف المراد استخدامه وتحديد متطلباته (dependencies)
وضع الملف في الصفّ (enqueue)



## Style

http://codex.wordpress.org/Function_Reference/wp_register_style
http://codex.wordpress.org/Function_Reference/wp_deregister_style
http://codex.wordpress.org/Function_Reference/wp_enqueue_style
http://codex.wordpress.org/Function_Reference/wp_dequeue_style

## Script

http://codex.wordpress.org/Function_Reference/wp_register_script
http://codex.wordpress.org/Function_Reference/wp_deregister_script
http://codex.wordpress.org/Function_Reference/wp_enqueue_script
http://codex.wordpress.org/Function_Reference/wp_dequeue_script
http://codex.wordpress.org/Plugin_API/Action_Reference/admin_enqueue_scripts
http://codex.wordpress.org/Plugin_API/Action_Reference/login_enqueue_scripts

### Passing variable to JavaScript
http://codex.wordpress.org/Function_Reference/wp_localize_script

## أمثلة وحالات استخدام
بالمثال يتضح المقال، سنمرّ معاً على أربع أمثلة وحالات استخدام كي نرى من خلالها كيف يمكننا الاستفادة والتعامل من تسجيل وصفّ ملفات JavaScript و CSS:

### 1. استخدام إضافة رديئة الجودة
لنفرض لسبب ما أنك تستخدم إضافة رديئة -لا تتبع المعايير ولا تستخدم أحد الإصدارات من المكتبات-، تتطلب هذه الإضافة وجود إصدارٍ قديم من مكتبة jQuery، بينما قالبك يستخدم الإصدار اﻷحدث منها. هل من المنطقي وجود نسختين من المكتبة في القالب؟ بالتأكيد لا.

لحلّ هذه المشكلة نحن أمام ثلاثة خيارات:
1. إن كانت الإضافة ليست رديئة الجودة كثيراً، وتقوم بصفّ مكتبة jQuery، فهذا شيء جيّد، يمكننا ببساطة إلغاء المكتبة من الصفّ وتنتهي المشكلة.
2. إن كانت الإضافة رديئة كما وصفناها ولا تقوم بصفّ مكتبة jQuery، عندها يجب على المطوّر أن يقوم بالتعديل على ملفات الإضافة يدوياً لإلغاء تحميل مكتبة jQuery. وهناك احتمال كبير أن المطور سينسى التعديل الذي قام به، ومع مرور الأيام يقوم بتحديث الإضافة إلى إصدار جديد ويذهب التحديث اليدويّ الذي قام به! أو إن كان ذو ذاكرة قوية، سيقوم بالقيام بالتعديل اليدوي ذاته في كل مرة يظهر إصدار جديد من الإضافة. لكم أن تتخيلوا المعاناة التي ستصبح على كاهل المطوّر.
3. الخيار الثالث والأسرع هو القيام بحذف هذه الإضافة رديئة الجودة والبحث عن واحدة أفضل منها تتبع المعايير والقواعد وتستخدم أحد الإصدارات من ملفات JavaScript و CSS. والخيار الثالث هو الأفضل لتقليل استخدام مسكنات ألم الرأس.

من المهم اتباع المعايير والقواعد المتفق عليها حتى لا يقع المطوّر في الحفر التي وُضعت تلك المعايير والقواعد من أجل تلافيها.

### 2. استخدام المكتبات الموجودة في ووردبريس

ربما حدثتك نفسك في أحد الأيام أن تستعرض ملفات ووردبريس وترى محتواها، إن حدث ذلك فلا بدّ أنك رأيت الكثير من مكتبات جافاسكريبت مثل jQuery، jQuery UI، Backbone وغيرها.

إن كانت هذه الملفات موجودة ضمن ووردبريس، فلمَ لا نقوم باستخدامها عند الحاجة إليها؟
لو كان القالب يحتاج إلى مكتبتي jQuery و jQuery UI فبدلاً من تحميل نسخة من كل مكتبة من الإنترنت ثم وضعها ضمن ملفات القالب واستخدامها، يمكننا بشكل مباشر استخدام نسخة jQuery و jQuery UI الموجودتان ضمن ووردبريس. بهذا نضمن الحصول على إصدار حديث من المكتبة يأتي مع كل تحديث لووردبريس بالإضافة لعدم التكرار (Don't Repeat Yourself).

من المكتبات الشهيرة المضمّنة في ووردبريس:
- jQuery
- jQuery UI
- Backbone
- jQuery Suggest
- Thickbox
- TinyMCE
- Underscore

للاطلاع على كامل القائمة يمكن زيارة [صفحة التوثيق](https://codex.wordpress.org/Function_Reference/wp_enqueue_script#Default_Scripts_Included_and_Registered_by_WordPress).

### 3. استخدام jQuery بشكل مباشر من شبكة توصيل المحتوى (CDN)

لا بدّ أنك سمعت بشبكة توصيل المحتوى (Content Delivery Network). تعريفها على [ويكبيديا](https://ar.wikipedia.org/wiki/%D8%B4%D8%A8%D9%83%D8%A9_%D8%AA%D9%88%D8%B5%D9%8A%D9%84_%D8%A7%D9%84%D9%85%D8%AD%D8%AA%D9%88%D9%89):
> هي مجموعة من الخوادم المتزامنة والموزعة والموجودة على الشبكة في أماكن جغرافية مختلفة، تحتوي على نسخ من البيانات. فالعميل يحصل على البيانات من الخادم الموجود في أقرب موقع جغرافي، بغرض تقليل التأخير الناتج في نقل البيانات.

هناك موقع مخصص لاستخدام مكتبات JavaScript عن طريق شبكات توصيل المحتوى هو [jsDelivr](http://www.jsdelivr.com/)، سنقوم باستخدام رابط مكتبة jQuery منه (`//cdn.jsdelivr.net/jquery/2.1.3/jquery.min.js`) لنقوم بصفّها واستخدامها ضمن القالب، عوضاً عن استخدام النسخة المتضمنة في ملفات ووردبريس.

للقيام بهذا نحتاج لوضع الأسطر القليلة التالي في ملف `functions.php` الخاص بقالبنا:
```php
add_action( 'wp_enqueue_scripts', 'register_jquery' );
function register_jquery() {
    wp_deregister_script( 'jquery' );
    wp_register_script( 'jquery', ( '//cdn.jsdelivr.net/jquery/2.1.3/jquery.min.js' ), false, null, true );
    wp_enqueue_script( 'jquery' );
}
```

قمنا بإلغاء تسجيل jQuery (كانت مسجلة مع الملف المتضمَّن في ووردبريس)، ثم قمنا بتسجيلها مع رابط الملف من شبكة توصيل المحتوى (CDN)، وأخيراً قمنا بصفّها (enqueue) ليتم إدراجها في القالب.


## الخاتمة:

تعرفنا على كيفية صفّ ملفات JavaScript و CSS، هذه الآلية تسهّل كثيراً تنظيم الملفات والتعامل معها، ويجب الحرص على استخدامها بشكل دائم، فهي من المعايير والأشياء المتعارف عليها في تطوير قوالب وإضافات ووردبريس.

أرجو أن يكون الشرح واضحاً ومفيداً، إن كان لديكم سؤال أو فكرة فلتشاركونا إياها في التعليقات.
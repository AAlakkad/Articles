[TOC]

> في الدرس القادم من السلسلة، سنقوم باستبدال النصوص الثابتة الموجودة حالياً في القالب بنصوصٍ من قاعدة البيانات، وسنجلب المقالات التي يتم إدخالها من لوحة التحكم لنعرضها في الصفحة الرئيسية.


The Loop
Common functions
Pagination

# مقدّمة حول تعامل ووردبريس مع قاعدة البيانات

عند كل طلبٍ إلى الموقع، تقوم ووردبريس بمعالجة الطلب ومعرفة ما هي الصفحة المطلوبة، وبناءً على الصفحة المطلوبة تقوم بجلب المعلومات المناسبة من قاعدة البيانات.

مثلاً عندما يكون الطلب للصفحة الرئيسية، تقوم ووردبريس بجلب عددٍ من المقالات (الرقم الافتراضي 10) بترتيب حسب الأحدث، وتكون هذه المقالات جاهزة للعرض دون تدخّل مباشر من المبرمج.

أيضاً عندما يكون الطلب لصفحة مقالٍ واحدٍ معيّن، تقوم ووردبريس بجلب مقال واحد حسب معرّف المقال (سواء كان المعرّف رقميّاً أو اسميّاً)، ويكون بعد ذلك جاهزاً للعرض دون تدخل مباشر من المبرمج.

وكذلك الحال بالنسبة لجميع أنواع الصفحات في ووردبريس، سواء كانت صفحات أرشيف، أو صفحات مقالات منفردة، أو صفحات أنواعٍ مخصّصة كما سنتعرف في تتمة السلسلة.

ضمن الحلقة الرئيسية سنقوم بوضع وسوم PHP تحوي دالّات يتم تقديمها من ووردبريس لعرض معلومات المقال ضمن الحلقة، الدوالّ مثل عرض عنوان المقال، محتوى المقال، تاريخ المقال، إلخ.

تكون الحلقة الرئيسية على الشكل التالي:
```php
<?php
while(have_posts()) {
	the_post();

	// هنا سنضع وسوم HTML ودوالّ PHP التي ستعرض لنا عنوان المقال، محتواه، وما إلى ذلك.
}
?>
```

نلاحظ أنها حلقة `while` عادية، تحوي دالّة تقدّمها ووردبريس هي `have_posts()`، الهدف من هذه الدالّة إخبار الحلقة الرئيسية إن كان هناك المزيد من المقالات ضمن الحلقة أم أنها انتهت.

أمّا دالّة `the_post()` فهي لتهيئة المقال الحاليّ ضمن ووردبريس، وجعلها جاهزة للاستخدام دون طلب صريح، مثلاً نستخدم دالّة `the_title()` فقط دون تمرير معرّف المقال (ID) فتقوم ووردبريس تلقائياً بطباعة عنوان المقال إلى صفحة الويب.
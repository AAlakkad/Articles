[TOC]
# قوائم التنقّل

قوائم التنقّل (Navigation Menu) هي إحدى ميزات القوالب، توفّر ووردبريس طريقة سهلة للتحكم بالقوائم المخصصة للقالب من داخل لوحة تحكم ووردبريس، فتحتاج لإضافة بضعة أسطر برمجية لتضيف دعم القوائم في قالبك.

## تسجيل القوائم

بدايةً في ملف `functions.php` ضمن ملفات القالب نحتاج لإضافة دالّة تقوم بتسجيل أسماء القائمة (أو القوائم) التي تريد إضافتها. كالتالي:
```php
add_action('init', function() {
	register_nav_menu('our-custom-menu', 'القائمة الرئيسية');
});
```

بعد ذلك يمكن التأكد من صحة إضافة القائمة عن طريق الذهاب من لوحة التحكم إلى المظهر (Appearance) ثم القوائم (Menus)، ستظهر لدينا قائمة باسم **القائمة الرئيسية** في تبويب *إدارة موضع القوائم*.
تأخذ دالّة [`register_nav_menu`](http://codex.wordpress.org/Function_Reference/register_nav_menu) محدّدين هما: المكان (Location) و الوصف (Description).

محدّد المكان يستخدم كمعرّف للقائمة، حيث يتم طلب محتوى القائمة ضمن ملفات القالب عن طريق محدّد المكان (location) الذي قمنا بتعيينه أثناء تسجيل القائمة. في حالتنا قمنا بوضع قيمة المحدد هي: **our-custom-menu**.
والوصف يتم استخدامه عند عرض القائمة في لوحة التحكم ليكون أنسب وأسهل للقراءة من محدد المكان، في حالتنا قمنا بوضع قيمة الوصف هي: **القائمة الرئيسية**.

يمكننا تسجيل أكثر من قائمة معاً عن طريق استخدام دالّة [`register_nav_menus`](http://codex.wordpress.org/Function_Reference/register_nav_menus) التي تستخدم بشكل مشابه لدالّة `register_nav_menu` لكن المحدّدات تكون على شكل مصفوفة اسميّة (Associative Array)، كل عنصر في المصفوفة يمثّل قائمة واحدة بحيث يكون مفتاح العنصر هو محدّد المكان وقيمة العنصر هي محدّد الوصف.

في قالبنا لا نحتاج سوى لقائمة واحدة، في ما يلي كيفية تسجيل أكثر من قائمة معاً:
```php
add_action('init', function() {
	register_nav_menus([
		'our-custom-menu' => 'القائمة الرئيسية',
		'our-second-menu' => 'القائمة الفرعية',
	]);
});
```

كما ننوه إلى وجود دالّة معاكسة لدالّة تسجيل القوائم هي [`unregister_nav_menu`](http://codex.wordpress.org/Function_Reference/unregister_nav_menu) لكننا لن نتطرّق إليها الآن.

## إظهار القائمة في القالب
الخطوة الأخيرة ضمن القالب هي عرضه في المكان المناسب.
في القالب الذي نستعمله نجد أن موقع القوائم أصبح في ملف `header.php`، في السطر 30 من الملف نجد وسم `<section class="top-bar-section">`، نريد أن نضع القائمة بدلاً من وسم `<ul>` الموجود بداخله.

نقوم بحذف وسم `<ul>` مع محتواه، ثم نستخدم السطر البرمجيّ التالي لعرض القائمة:
```php
<?php wp_nav_menu(['theme_location' => 'our-custom-menu']); ?>
```

تقبل دالّة `wp_nav_menu` محدداً واحداً هو مصفوفة تحوي عدداً من الإعدادات، الإعداد الوحيد الضروري هو `theme_location` ويتم استخدامه كما في السطر البرمجي السابق. يمثل هذا المحدّد قيمة محدّد المكان السابقة التي استخدمناها أثناء تسجيل قائمة جديدة والتي كانت: `our-custom-menu`.

إن ألقينا نظرة على القالب من المتصفح سنجد أن شكل عناصر القائمة أصبح مختلف قليلاً عن الشكل الذي كان عليه، وذلك ﻷن الدالّة تقوم بإضافة وسم `<div>` محيط بوسوم القائمة.
في الفقرة التالية سنتعرف على بقية الإعدادات التي يمكن أن نستخدمها مع دالّة `wp_nav_menu` والتي ستمكننا من إظهار القائمة على الشكل الأنسب.

## إعدادات دالّة `wp_nav_menu`


http://codex.wordpress.org/Navigation_Menus

http://codex.wordpress.org/Function_Reference/register_nav_menu

http://codex.wordpress.org/Function_Reference/wp_nav_menu

- The Theme's main navigation should support a custom menu with wp_nav_menu().
- Menus should support long link titles and a large amount of list items. These items should not break the design or layout.
- Submenu items should display correctly. If possible, support drop-down menu styles for submenu items. Drop-downs allowing showing menu depth instead of just showing the top level.


# الشريط الجانبي

http://codex.wordpress.org/Sidebars

http://codex.wordpress.org/Function_Reference/register_sidebar

http://codex.wordpress.org/Function_Reference/dynamic_sidebar

- The Theme should be widgetized as fully as possible. Any area in the layout that works like a widget (tag cloud, blogroll, list of categories) or could accept widgets (sidebar) should allow widgets.
- Content that appears in widgetized areas by default (hard-coded into the sidebar, for example) should disappear when widgets are enabled from Appearance > Widgets.
[TOC]
# Pagination

تقدّم ووردبريس دالّة مخصّصة لعرض أرقام الصفحات هي [`paginate_links`](http://codex.wordpress.org/Function_Reference/paginate_links).
سنقوم بالاطلاع على كيفية استخدامها، وننوه بوجود طرق أخرى لعرض أرقام الصفحات، مثل إضافة  [WP-PageNavi](https://wordpress.org/plugins/wp-pagenavi/).

يتم استخدام الدالّة بهذه الطريقة:
```php
<?php echo paginate_links($args);?>
```

حيث متحول `$args` هو مصفوفة تحوي إعدادات مخصصة لهذه الدالّة، الإعدادات الكاملة هي كالتالي بقيمها الافتراضية:
```php
<?php
$args = array(
'base'               => '%_%',
	'format'             => '?page=%#%',
	'total'              => 1,
	'current'            => 0,
	'show_all'           => False,
	'end_size'           => 1,
	'mid_size'           => 2,
	'prev_next'          => True,
	'prev_text'          => __('« Previous'),
	'next_text'          => __('Next »'),
	'type'               => 'plain',
	'add_args'           => False,
	'add_fragment'       => '',
	'before_page_number' => '',
	'after_page_number'  => ''
);
?>
```

يمكننا أن نضع بعض هذه الإعدادات في المتحول، وتقوم ووردبريس بمعالجة الإعدادات التي نقدّمها للدالّة، بحيث تضيف للإعدادات المُدخلة ما يكملها من الإعدادات الافتراضية.

## شرح إعدادات دالّة `paginate_links`
كما أسلفنا، يمكن أن نمرر جزءاً من الإعدادات ويمكننا ألا نمرر أي شيء على الإطلاق، فتقوم ووردبريس باستخدام الإعدادات الافتراضية التي أوردناها في الأعلى.

- base
(القيمة اختيارية)، نوعها سلسلة نصيّة.
تُستخدم للإشارة إلى الرابط، الذي سيتم استخدامه لإنشاء روابط الصفحات.
في رابط مثل: 'http://example.com/all_posts.php%_%' يتم استبدال القيمة الافتراضية: `%_%` بقيمة format التي سنتحدث عنها في الفقرة التالية.
القيمة الافتراضية: '%_%'
- format
(القيمة اختيارية)، نوعها سلسلة نصيّة.
تُستخدم كهيكل للصفحات. القيمة الافتراضية هي `?page=%#%`، في حال كنا نريد عناوين نظيفة (pretty permalinks) ستكون القيمة هي `/page/%_%`، حيث تعبير `%_%` يتم استبداله برقم الصفحة.
القيمة الافتراضية: `?page=%#%`
- total
(القيمة اختيارية)، نوعها رقميّ.
مجموع عدد الصفحات.
القيمة الافتراضية: 1
- current
(القيمة اختيارية)، نوعها رقميّ.
رقم الصفحة الحالية.
القيمة الافتراضية: 0
- show_all
(القيمة اختيارية)، نوعها قيمة منطقية (true أو false).
إذا كانت القيمة `true` عندها سيتم إظهار جميع الصفحات بدلاً من قائمة قصيرة من الأرقام المجاورة لرقم الصفحات الحالية. بشكل افتراضي هذا الخيار تكون قيمته `false` ويتم التحدم به عن طريق خياريّ/ `end_size` و `mid_size`.
القيمة الافتراضية: false
- end_size
(القيمة اختيارية)، نوعها رقميّ.
عدد الأرقام عند بداية ونهاية أطراف القائمة.
القيمة الافتراضية: 1
- mid_size
(القيمة اختيارية)، نوعها رقميّ.
عدد الأرقام على جانبيّ الصفحة الحالية، (مع ملاحظة أن الرقم لا يشمل الصفحة الحالية).
القيمة الافتراضية: 2
- prev_next
(القيمة اختيارية)، نوعها قيمة منطقية (true أو false).
لتحديد إن كنا نريد روابط التالي والسابق أن يتم استخدامها في القائمة أم لا.
القيمة الافتراضية: true
- prev_text
(القيمة اختيارية)، نوعها سلسلة نصّية.
نص رابط الصفحة السابقة، تعمل فقط إن كان الخيار السابق (prev_next) فعّالاً (قيمته true).
القيمة الافتراضية: `__('« Previous')` حيث `__()` هي دالّة مسؤولة عن الترجمة.
- next_text
(القيمة اختيارية)، نوعها سلسلة نصّية.
نص رابط الصفحة التاية، تعمل فقط إن كان خيار (prev_next) فعّالاً (قيمته true).
القيمة الافتراضية: `__('Next »')` حيث `__()` هي دالّة مسؤولة عن الترجمة.
- type

(string) (optional) Controls format of the returned value. Possible values are:
	- 'plain' - A string with the links separated by a newline character.
	- 'array' - An array of the paginated link list to offer full control of display.
	- list' - Unordered HTML list.

Default: 'plain'

- add_args
(array) (optional) An array of query args to add.
Default: false
- add_fragment
(string) (optional) A string to append to each link.
Default: None
- before_page_number
(string) (optional) A string to appear before the page number.
Default: None
- after_page_number
(string) (optional) A string to append after the page number.
Default: None


*صورة من القالب بعد إظهار أرقام الصفحات دون إعدادات*

*صورة من القالب بعد إظهار أرقام الصفحات مع وجود إعدادات*

---

# أزرار التالي والسابق

قد يفضّل البعض استخدام أزرار "التالي" و"السابق" بدلاً من أرقام الصفحات، أو ربما يتطلب القالب الذي يعملون عليه هذه الأزرار.

تقدّم ووردبريس دالّة واحدة لعرض الرابطين (التالي - السابق) هي: [`posts_nav_links`](http://codex.wordpress.org/Function_Reference/posts_nav_link).


*صورة من القالب بعد ظهور أزرار التالي والسابق*

-------------------------------------------------------------------------------





يوجد عدة طرق لعرض أرقام الصفحات بطريقة تناسب شكل القالب الذي نقوم باستخدامه (تناسب كيفية عمل أرقام الصفحات في إطاري عمل [Bootstrap](http://getbootstrap.com) و [Foundation](http://foundation.zurb.com/)).

- إما نقوم بنسخ دالّة [`paginate_links()`](http://codex.wordpress.org/Function_Reference/paginate_links) المسؤولة عن عرض أرقام الصفحات ونعدّل عليها حسب المطلوب، وذلك في ملف `functions.php` داخل ملفات قالب ووردبريس.
- أو نقوم بإنشاء دالّة جديدة تحاكي مبدأ عمل دالّة `paginate_links()` لكن بخيارات أقل حسب ما يتطلبه القالب.
- أو نقوم باستخدام إضافة [WP-PageNavi](https://wordpress.org/plugins/wp-pagenavi/) التي تعمل بطريقة مشابهة لدالّة `paginate_links()` لكن مع المزيد من الخيارات، منها إمكانية التحكم بالوسوم عن طريق ما يسمّى [Filters](http://codex.wordpress.org/Plugin_API/Filter_Reference).

يمكن استخدام الطريقة الأخيرة عندما نتحدث عن Actions/Filters، لكن في هذا الدرس سنستخدم الطريقة الأولى.

ضمن ملفات التوثيق الخاصّة بدالّة `paginate_links` نجد في النهاية [رابطاً](https://core.trac.wordpress.org/browser/tags/4.1/src/wp-includes/general-template.php#L2587) للوصول إلى الشيفرة المصدرية لووردبريس، تحديداً إلى مكان تعريف تلك الدالّة.

سنقوم بنسخ هذه الدالّة كاملة ونضعها في ملف `functions.php` ضمن القالب الذي نعمل عليه. نعيد تسمية الدالّة المنسوخة لتصبح مثلاً `my_paginate_links` كي لا يحدث خطأ أثناء الاستخدام بسبب تعريف الدالّة مرة ثانية إن بقيت بنفس الاسم الأصلي.

الخطوة الأولى أن نقوم بالاستغناء عن خاصيّة **type** ضمن مصفوفة `$args`، ﻷننا سنفرض أننا نستخدم دوماً النوع *list*.

نقوم بتعديل ما يلي، حيث إشارة `-` في بداية السطر تشير إلى حذف السطر، وإشارة `+` تشير إلى الإضافة:
```diff
-                'type' => 'plain',
```
```diff
-        switch ( $args['type'] ) {
-                case 'array' :
-                        return $page_links;
-
-                case 'list' :
-                        $r .= "<ul class='pagination'>\n\t<li>";
-                        $r .= join("</li>\n\t<li>", $page_links);
-                        $r .= "</li>\n</ul>\n";
-                        break;
-
-                default :
-                        $r = join("\n", $page_links);
-                        break;
-        }
+        $r .= "<ul class='pagination'>\n\t<li>";
+        $r .= join("</li>\n\t<li>", $page_links);
+        $r .= "</li>\n</ul>\n";
```

ثم نقوم بحذف وسوم `</li><li>` من نهاية الدالّة:
3bf6b1b
```diff
-        $r .= "<ul class='pagination'>\n\t<li>";
-        $r .= join("</li>\n\t<li>", $page_links);
-        $r .= "</li>\n</ul>\n";
+        $r .= "<ul class='pagination'>\n\t";
+        $r .= join("\n\t", $page_links);
+        $r .= "\n</ul>\n";
```

وأخيراً نضع وسوم `<li>` لتحيط بكل رابط `<a>` مع وضع صنف CSS المناسب.
8d10155
```diff
-                $page_links[] = '<a class="prev arrow" href="' . esc_url( apply_filters( 'paginate_links', $link ) ) . '">' . $args['p
+                $page_links[] = '<li class="prev arrow"><a href="' . esc_url( apply_filters( 'paginate_links', $link ) ) . '">' . $arg
         endif;
         for ( $n = 1; $n <= $total; $n++ ) :
                 if ( $n == $current ) :
-                        $page_links[] = "<a class='current'>" . $args['before_page_number'] . number_format_i18n( $n ) . $args['after_
+                        $page_links[] = "<li class='current'><a href=''>" . $args['before_page_number'] . number_format_i18n( $n ) . $
                         $dots = true;
                 else :
                         if ( $args['show_all'] || ( $n <= $end_size || ( $current && $n >= $current - $mid_size && $n <= $current + $m
@@ -90,10 +90,10 @@ function my_paginate_links( $args = '' ) {
                                 $link .= $args['add_fragment'];
 
                                 /** This filter is documented in wp-includes/general-template.php */
-                                $page_links[] = "<a href='" . esc_url( apply_filters( 'paginate_links', $link ) ) . "'>" . $args['befo
+                                $page_links[] = "<li><a href='" . esc_url( apply_filters( 'paginate_links', $link ) ) . "'>" . $args['
                                 $dots = true;
                         elseif ( $dots && ! $args['show_all'] ) :
-                                $page_links[] = '<span class="dots">' . __( '&hellip;' ) . '</span>';
+                                $page_links[] = '<li class="unavailable"><a href="">'. __( '&hellip;' ) .'</a></li>';
                                 $dots = false;
                         endif;
                 endif;
@@ -106,7 +106,7 @@ function my_paginate_links( $args = '' ) {
                 $link .= $args['add_fragment'];
 
                 /** This filter is documented in wp-includes/general-template.php */
-                $page_links[] = '<a class="next arrow" href="' . esc_url( apply_filters( 'paginate_links', $link ) ) . '">' . $args['n
+                $page_links[] = '<li class="arrow"><a href="' . esc_url( apply_filters( 'paginate_links', $link ) ) . '">' . $args['ne
         endif;
```

يمكن الآن أن نستخدم الدالّة الجديدة كما يلي في ملف `index.php`:
0bec5b7
```php
<?= my_paginate_links(); ?>
```

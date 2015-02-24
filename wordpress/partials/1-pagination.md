[TOC]
# Pagination

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

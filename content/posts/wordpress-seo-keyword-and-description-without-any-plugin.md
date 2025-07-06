---
author: arul
category:
  - software-development
cover:
  alt: Knowledge-base-part-3_what-is-seo
  image: /wp-content/uploads/2017/04/Knowledge-base-part-3_what-is-seo.jpg
date: "2017-04-18T11:16:13+00:00"
draft: "true"
guid: http://arulselvan.net/?p=280
tag:
  - technical
title: WordPress SEO Keyword and Description without any Plugin
url: /wordpress-seo-keyword-and-description-without-any-plugin/

---
I don't like much third party plugins, below I described how to add  SEO basic description and keywords meta tags without any additional plugin load.

1. Login to WordPress admin and  create new post/page, below snap I am creating new page.                                                                    [![create-page](/wp-content/uploads/2017/04/create-page-1024x527.png)](/wp-content/uploads/2017/04/create-page.png)
1. In the right top , click screen options button and enable custom fields option. [![custom-field](/wp-content/uploads/2017/04/custom-field-1024x541.png)](/wp-content/uploads/2017/04/custom-field.png)
1. Create new custom field description and keywords  for the page then save and publish the page.                                                                     [![description-keywords](/wp-content/uploads/2017/04/description-keywords-1024x528.png)](/wp-content/uploads/2017/04/description-keywords.png)
1. Go to theme  function.php file through ftp or admin theme editor and add below function

```php

function add_meta_tags(){
	$description = get_post_meta(get_the_ID(), "description", true);

	if(empty($description)){
		$description = get_the_title();
	}
	echo '' . "\n";

	$keywords = get_post_meta(get_the_ID(), "keywords", true);

	if(!empty($keywords)){
		echo '' . "\n";
	}
}
add_action( 'wp_head', 'add_meta_tags' ); ?>

```

that's it enjoy basic SEO without additional plugin, see below page source code in the browser, our description and keywords meta tags added successfully.

![seo_page_source](/wp-content/uploads/2017/04/seo_page_source.png)

For advance you can extend the same function by adding more tags like below (added for social media).

```php

        echo ''."\n";
	echo ''."\n";
	echo ''."\n";
	echo ''."\n";

```

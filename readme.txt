=== Easy Widgets ===
Contributors: OutThisLife
Tags: widgets
Requires at least: 3.0
Tested up to: 3.4.2
Stable tag: 1
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Easy Widgets plugin lets you easily create widgets in WordPress.

== Description ==

Easy Widgets plugin provides an API to easily add widgets in WordPress.

= Example of Use =

1. Create a file "widgets.php" in your themes /inc/ folder
1. In functions.php use locate_template to include your widgets.php file: locate_template(array('/inc/widgets.php'), true);
1. In widgets.php, do something like below:

	/**
	 * Custom widgets.
	 */
	global $widgets;

	$prefix = 'replaceMe_';
	$widgets = array();

	// -----------------------------------------------

	/**
	 * easyBox widget
	 */
	$widgets[] = array(
		'id' => 'easyBox',
		'title' => $prefix.'easyBox',
		'desc' => 'Create a simple text widget',

		// All fields can be called by their
		// simple variables: title => $title
		'fields' => array(
			array(
				'name' => 'Title',
				'id' => 'title',
				'type' => 'text'
			),

			array(
				'name' => 'Body',
				'id' => 'body',
				'type' => 'textarea'
			)
		),

		// This is what will appear in the sidebar as HTML
		'output' => '
			<article class="easyBox">
				<h1><?=$title?></h1>
				<p><?=$body?></p>
			</article>
		'
	);

	// -----------------------------------------------

	/**
	 * Iterate and register the widgets
	 */
	if (class_exists('WidgetCreator')) {
		foreach ($widgets AS &$w) {
			$WC = new WidgetCreator($w);
			eval($WC->render());
		}
	}

	else wp_die('WidgetCreator does not exist.');

= Features =

* Easily create custom widgets to use on your website.
* Lets you control the output of the widget.
* Flawlessly integrates itself into your themes.

<strong>Supported Field Types</strong>

* text
* textrea
* checkbox
* select - soon to come

More to come soon, as it seems necessary. You may request new fields. 

== Installation ==

1. Upload /easy-widgets/ to wp-content/plugins/ directory.
1. Activate the plugin via the Plugins menu in WordPress.
1. Follow the sample document.

== Frequently Asked Questions ==

= Why do widgets start with a "!"? =
This pushes the widget to the top of the widgets list, allowing your custom widgets to come first.

= Can I use HTML? =
Yes, you may use basic tags such as bold, italicize, iframe, img and anchor links.

== Changelog ==
= 1.0 =
* Listed on WP.

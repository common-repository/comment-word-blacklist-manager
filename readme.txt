=== Comments Word Blacklist Manager ===
Contributors: geekparadize
Tags: comments, spam, blacklist
Website Link: https://www.geekparadize.fr
Donate link: https://www.geekparadize.fr/donations
Requires at least: 3.7
Tested up to: 4.9
Stable tag: 1.0.0
License: GPL

Remotely add known terms into the WordPress blacklist keys to manage spam

== Description ==

Comment Word Blacklist Manager will retrieve a list of blacklist terms from a remote source and update the `blacklist_keys` setting in WordPress. The list will update itself on a schedule to keep your terms current. Any manually added items will be retained, and an exclusions list is also created if there are terms from the source you want to allow.

== Installation ==

1. Upload the `comment-word-blacklist-manager` folder to the `/wp-content/plugins/` directory or install from the dashboard
1. Activate the plugin through the 'Plugins' menu in WordPress
1. Add any terms to the exclusions list under the main "Discussions" settings area
1. Add any additional terms in the new "Local Blacklist" field

== Frequently Asked Questions ==

= What is the default source of the blacklist? =

The list is managed by [GeekParadize](http://www.geekparadize.fr/ "GeekParadize.Fr") on [GitHub](https://github.com/geekparadize/Comment-Word-Blacklist-Manager/ "GitHub")

= Can I provide my own blacklist sources? =

Sure can. Use the filter `cwblm_sources` to add different source URLs.

*to replace the sources completely*
`
add_filter( 'cwblm_sources', 'rkv_cwblm_replace_blacklist_sources' );

function gpz_cwblm_replace_blacklist_sources( $list ) {

	return array(
		'http://example.com/blacklist-1.txt'
		'http://example.com/blacklist-2.txt'
	);

}
`

*to add a new item to the existing sources*
`
add_filter( 'cwblm_sources', 'gpz_cwblm_add_blacklist_source' );

function gpz_cwblm_add_blacklist_source( $list ) {

	$list[]	= 'http://example.com/blacklist-a.txt';

	return $list;

}
`

The plugin expects the blacklist data to be a plain text format with each entry on it's own line. If the source is provided in a different format (a JSON feed or serialized array) then you will need to run the result through `cblm_parse_data_result`, which passes through the data and the source URL.

= Can I change the update schedule? =

Yep. Use the filter `cwblm_update_schedule` to add a new URL.

`add_filter( 'cwblm_update_schedule', 'gpz_cwblm_custom_schedule' );

function gpz_cwblm_custom_schedule( $time ) {

	return DAY_IN_SECONDS;

}`

The return should be provided using the [time contstants in transients](http://codex.wordpress.org/Transients_API#Using_Time_Constants "time contstants in transients")

== Screenshots ==

1. The new exclusions field


== Changelog ==

= 1.0.0 =
* Initial release


== Upgrade Notice ==

= 1.0.0 =
Initial release



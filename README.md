# welcome-email-editor
WordPress Welcome Email Editor - Official plugin repo

This is the official Repo for the Welcome Email Editor by Sean Barton. I wrote this a while ago and it's always been popular but now needs some more work to make it really perform. I've always been keen on simplicity of interface rather than packing hundreds of options on one page I'd like to make it really intuitive. Here is the description from the WP readme I wrote a while ago.. mostly this will be out of date but you'll get the idea about how it works then!

https://wordpress.org/plugins/welcome-email-editor/

# WP Intro

I thought that the WordPress Welcome Email to both the Admin and the User were very un-user friendly so I wrote this plugin to allow admin members to change the content and headers.

It simply adds a new admin page that has a few options for the welcome email and gives you a list of hooks to use in the text to make the email a little more personal.

Added support whereby the admin notification can be turned off or a different admin (or admins, support for multiple recipients) can be notified. Plenty of hooks to make the emails as customisable as possible.

A reminder email service has now been added whereby the admin user can send a reminder to any particular user. This can be the original welcome email or a separate template configured on the Welcome Email Editor settings page.

Please email me or use the support forum if you have ideas for extending it or find any issues and I will be back to you as soon as possible.

I would recommend the use of an SMTP service with any WordPress plugin. A large amount of emails fall needlessly into Spam bins across the world (I get a fair amount of comment approval spam to deal with) because the WordPress site uses Sendmail to deliver email. I noticed an immediate improvement when using SMTP to send. It's really easy so there's no excuse :)

== Frequently Asked Questions ==

= It sends the default WP Email and not my edited one =

Please don't assume that because it sends the default WP email that this plugin is broken or rubbish. In V4.3 WordPress changed the way that welcome emails were sent and broke every welcome email editor plugin. If you are using a version older than 4.3 then I'd recommend upgrading WP and retesting. If you have a version 4.3.1 or newer then read on.

The simplest solution is that there is a conflict. The plugin works by overriding the wp_new_user_notification() function which is written in such a way that ONLY one plugin or theme can override it. Sometimes plugins or themes (even if they are unreliated to email sending) can cause the WP load order to change and the pluggable.php file is called earlier than it should and therefore removes the opportunity for my plugin or any similar to do their job. The easiest way to debug is to turn off all plugins (or one by one.. either way is fine) and then retest. If it works then gradually turn your plugins back on until it breaks again.. If you find a conflict please post on the forum or email me and I'll do my best to sort it out. If you find no conflict then it may be the theme.. switch the theme back to twentytwelve or similar and retest. Some people may not be prepared to do this or not be comfortable with the testing process. If you'd like help working it out please do get in touch and I'll help however I can.

= The password is not in the email? =

From 4.3 the password is no longer sent to the user via email and instead a reset password link is sent instead. This was a controversial and annoying move but it was done for good reason. Some plugins that allow you to style the reg form may allow the password to be sent but if this doesn't work please note that this isn't default functionality and may not work. It's worth a test though!

= I want to add my own hooks =

No problem.. There are two ways to do this. You can use the filter to get the email content and parse it yourself or the easier method would be to use the 'sb_we_replace_array' filter which expects an array which the plugin will parse. See below for examples:

`$admin_message = apply_filters('sb_we_email_admin_message', $admin_message, $settings, $user_id);`
`$admin_subject = apply_filters('sb_we_email_admin_subject', $admin_subject, $settings, $user_id);`
`$user_subject = apply_filters('sb_we_email_subject', $user_subject, $settings, $user_id);`
`$user_message = apply_filters('sb_we_email_message', $user_message, $settings, $user_id);`

The above code is from the plugin. You can edit the admin and user subject lines and body contents in any way you like. I won't explain any further as this is either something you know or you don't. The following method is easier:

`$user_message_replace = apply_filters('sb_we_replace_array', array(), $user_id, $settings);`

This method passes a filter an array and you can write in your own code to add hooks to the array for parsing. You can do the following:

`add_filter('sb_we_replace_array', 'my_sb_we_replace_array', 10, 3);

function my_sb_we_replace_array($hooks, $user_id, $settings) {
    $hooks['my_hook'] = 'test';
    
    return $hooks;
}`

This will allow the plugin to process a hook called [my_hook] and replace it with the word test. The user id is passed to the function as well so you can get information about the user and replace that in as well as the settings array from the welcome email editor plugin. If you need help with this please get in touch.


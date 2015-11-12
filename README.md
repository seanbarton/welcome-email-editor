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
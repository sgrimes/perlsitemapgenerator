The **Perl Sitemap Generator** is a Perl script that creates a Sitemap for your site using the Sitemap Protocol. This script can create Sitemaps from URL lists, web server directories, access logs, or from other sitemaps.

This tool is a **translation** of **[Google Sitemap Generator](https://www.google.com/webmasters/tools/docs/en/sitemap-generator.html)** from python to perl.

In order to use this script:
  * You must be able to connect to and run scripts on your web server.
  * Your web server must have Perl 5.8.0 or later installed.
  * You must know the directory path to your site. If your web server hosts one site, this may be a path such as **var/www/html**. If you have a virtual server that hosts multiple sites, this may be a path such as **home/virtual/site1/fst/var/www/html**.
  * You must be able to upload files to your web server (for instance, using FTP).
  * If you will be generating a list of URLs based on access logs, you must know the encoding used for those logs and the complete path to them.

If you aren't sure about any of this, you can check with your web hosting company.

Now you’re ready to get started. Here’s an overview of what you’ll need to do.

  1. [Download](Download.md) the Sitemap Generator program files. Extract the files to a local directory.
  1. [Create a configuration file](Create.md) for your site using the provided **example\_config.xml** file as a template. Modify this file as needed for your site and save it.
  1. [Upload the necessary files](Upload.md) to your web server.
  1. [Run](Run.md) **sitemap\_gen.pl**.
  1. [Add](Add.md) the generated Sitemap to your Google webmaster tools account.
  1. [Set up a recurring script](Setup.md). (optional)

If you are unable to use the Sitemap Generator, you can add a Sitemap to your Google webmaster tools account in [another format](http://www.google.com/support/webmasters/bin/answer.py?answer=34606&topic=8516), such as a simple text file. You can also find links to third-party programs that support Google Sitemaps [here](http://code.google.com/sm_thirdparty.html).
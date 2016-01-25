[[<< 3. Uploading the necessary files](Upload.md)] | [[5. Adding the generated sitemap>>](Add.md)]

### 4. Running the Perl Sitemap Generator script (sitemap\_gen.pl) ###

In order to run the Sitemap Generator, you’ll need to connect to your web server. The method you use to connect depends on your environment. For instance, you can generally access a UNIX-based server using SSH. For more information on connecting to your web server and running scripts, talk to your web host.

Once you have copied the files to your web server, you'll need to run the Sitemap Generator script. Connect to your web server and run the following command (replace **<path/config.xml>** with the path to and filename of your configuration file; if you have uploaded this file to the same location as the Perl script, you can exclude the path):

`perl sitemap_gen.pl --config=<path/config.xml>`

**Tip:** If you're testing your configuration and are not ready to submit your Sitemap, the following syntax will prevent Sitemap Generator from contacting Google:

> `$ perl sitemap_gen.pl --config=config.xml --testing`

You'll see the status of your request in the command prompt:
```
	Reading configuration file: /path/config.xml
	Opened URLLIST "/path/urllist.txt"
	Walking DIRECTORY "/var/www/html/dir"
	Walking DIRECTORY "/var/www/html/dir2"
	Opened ACCESSLOG "/etc/httpd/logs/access-0.log"
	Sorting and normalizing collected URLs.
	Writing Sitemap file "/path/sitemap.xml.gz" with 1092 URLs
	Notifying search engines.
	Notifying www.google.com
	Count of file extensions on URLs:
		208 .html
		574 .jpg
		...
		Number of errors: 0
		Number of warnings: 0
```
If you don't see very much output like this, remember that the verbose setting in your configuration file affects how much information is printed on the screen. This example is representative of setting verbose to "1".

Any errors in the file will also be returned. For instance, if you leave the url= attribute off a directory entry, the script will output the following:
```
	[ERROR] Directory entries must have both "path" and "url" attributes
	Number of errors: 1
```
Correct any errors in your **config.xml** file and re-run the script. If no errors are present, the Sitemap Generator will create a new **sitemap.xml** file in the location you specified in the config file.

[[<< 3. Uploading the necessary files](Upload.md)] | [[5. Adding the generated sitemap>>](Add.md)]
### 1. Downloading the Perl Sitemap Generator program files ###
The Perl Sitemap Generator files are available in ZIP and GZ archive formats from the following location:

http://code.google.com/p/perlsitemapgenerator/downloads/list

Once you download the archive, extract it into a local directory. Locate the following files:

  * **README** —contains the latest information about this tool
  * **sitemap\_gen.pl** —the perl script that generates your Sitemap
  * **example\_config.xml** —the template configuration file you'll use to specify the configuration for your site
  * **example\_urllist.txt** —the template URL list you can use if you wish to create a Sitemap based on a set of URLs that you specify

### 2. Creating a configuration file ###

This section provides step-by-step instructions for creating a configuration file. It also provides a complete reference of the options available. If you are creating [Mobile Sitemaps](http://www.google.com/support/webmasters/bin/answer.py?answer=34627&topic=8493), see the additional mobile guidelines.

In order to create a configuration file for your site, you must have the following information:

  * The base URL for your site (such as `http://www.example.com/`). Only URLs that begin with this base URL can be included in the Sitemap. Ensure that you include the protocol (such as `http://`). For instance, `http://www.google.com` is a valid base url, but `www.google.com` is not.
  * The web server path to the location where you want to store the Sitemap. Generally, this is the path to the base URL as the Sitemap cannot contain URLs that are in a higher-level directory from the location of the Sitemap. When you run the Google Sitemap Generator, it creates the Sitemap and places it in the location you specify.
  * The methods you want the Sitemap Generator to use to create your Sitemap. You can use any combination of methods. The following methods are available:
    * **URL** —list individual URLs in this section of the configuration file, along with information about each URL. You would generally use this method in conjunction with another method to manually include additional URLs that other methods wouldn't pick up.
    * **URL list** —point the configuration file to a text file that contains a list of URLs. You might want to use this method if this text file already exists or if you use a script to generate a list of URLs.
    * **Directory paths** —specify the directory paths for your site and corresponding URLs to those paths. The Sitemap Generator will create a list of URLs based on the contents of those directories. You might want to use this method if your site consists of static HTML files.
    * **Access logs** —point to the path to your log files. The Sitemap Generator will create a list of URLs based on the URLs included in the logs. You might want to use this method if your site consists of dynamic pages.
    * **Sitemap** —point to existing Sitemaps that you have created with the Sitemap Generator. The Sitemap Generator will create a single Sitemap that includes the URLs contained in each Sitemap. You could use this method if you have already created several smaller Sitemaps that you want to combine into one larger Sitemap.

**Create the configuration file as follows:**

  1. Open the **example\_config.xml** file in a text editor. Save it as a new file (such as **config.xml** or **mysite\_config.xml**).
  1. Locate the site definition section:
```
      <site 
      base_url="http://www.example.com/" 
      store_into="/var/www/docroot/sitemap.xml.gz"
      verbose="1">
```
  1. Change the **base\_url** value to the URL for your site.
  1. Change the **store\_into** value to the path on your web server where you want to store the Sitemap and the filename you want to use for the Sitemap. Generally, this is the path to the base URL since Google can only accept URLs that are at the same level as or subdirectories of the directory that holds the Sitemap. You can specify a relative path from the directory where you upload the script or a complete path from the root of your web server. If you upload the script to your base URL directory, you can simply specify the filename.
  1. Locate the generation method sections that begin with  **MODIFY or DELETE** . Each of these sections corresponds to a method for generating a Sitemap.
  1. Delete the sections for the methods you aren’t going to use.
  1. Follow the instructions below for the methods you are going to use.

  * **URL**

> Locate the following section:
```
  <!-- ** MODIFY or DELETE ** 
  "url" nodes specify individual URLs to include in the map. <br>

  Required attributes: 
  href - the URL

  Optional attributes: 
  lastmod - timestamp of last modification (ISO8601 format) 
  changefreq - how often content at this URL is usually updated
  priority - value 0.0 to 1.0 of relative importance in your site 
  --> 

  <url href="http://www.example.com/stats?q=name" /> 
  <url 
  href="http://www.example.com/stats?q=age" 
  lastmod="2004-11-14T01:00:00-07:00" 
  changefreq="yearly" 
  priority="0.3"
  /> 
```
> This section gives two examples: the first includes only the required attribute and the second includes the required attribute as well as the optional attributes.

> Use this format for each of the URLs you want to include. The **changefreq** attribute gives Google a general idea of how often the URL is updated. This helps Google know how often to visit the page for new content. The **priority** attribute gives Google information about the relative importance of this page compared to the other pages of your site. This attribute has no effect on how Google compares your page to pages on other sites, it just helps Google know which pages of your site that you think are most important.

  * **URL List**

> Locate the following section:
```
  <!-- ** MODIFY or DELETE **
  "urllist" nodes name text files with lists of URLs. 
  An example file "example_urllist.txt" is provided. 

  Required attributes: 
  path - path to the file 

  Optional attributes: 
  encoding - encoding of the file if not US-ASCII 
  --> 
  <urllist path="example_urllist.txt" encoding="UTF-8" /> 
```
> Use this format to point to the path and name of the text file that contains your list of URLs. You can use the provided **example\_urllist.txt** file as a template for that text file. You can specify either a relative or complete path to your web server. For instance, if the Sitemap Generator and **urlist.txt** file are located in the same directory, you can simply specify the filename of the **.txt** file, If you create a text file with an encoding other than UTF-8, you can use the **encoding** attribute to indicate this encoding. If you have multiple .txt files, you can use wildcards. For instance:
```
  <urllist path="example_urllist*.txt" encoding="UTF-8" /> 
```
> For each URL you include in the text file, you can specify the last modification date, change frequency, and priority. See the URLlist text file reference section for complete information about the structure of this file.

  * **Directory paths**

> Locate the following section:
```
  <!-- ** MODIFY or DELETE ** 
  "directory" nodes tell the script to walk the file system and 
  include all files and directories in the Sitemap.

  Required attributes:
  path - path to begin walking from 
  url - URL equivalent of that path 

  Optional attributes:
  default_file - name of the index or default file for directory URLs

  --> 
  <directory  path="/var/www/icons"    url="http://www.example.com/images/" />
  <directory
     path="/var/www/docroot"
     url="http://www.example.com/"
     default_file="index.html"
  />
```
> This section gives two examples. If all of your pages are contained in subdirectories of one path, then you only need to include one entry. However, if you have multiple paths to pages on your site, include an entry for each.

> Remember that each URL must begin with the base URL you specified in step 3. For instance, the examples given in the **example\_config.xml** file both have URLs that begin with `http://www.example.com/`. Therefore, both URLs are valid.

> Replace the example entries with entries for your site. Many sites will only have one entry that points to the base URL. Ensure that **path** value is the complete path to the directory on your web server. Ensure that the **url** value is the complete URL, including the protocol (such as http) and a trailing slash, if required.

> You can use the **default\_file** parameter to specify the filename that your server uses as the default page for a directory. In the above example, **/var/www/docroot** resolves to `http://www.example.com/index.html`. You are not required to specify this. However, if you do, the Sitemap Generator will include the page that maps to each subdirectory only once (rather than list both the directory URL and filename URL) and will use the last modified date of the file (rather than the directory) to extract the lastmod attribute for that page.

  * **Access logs**

> Locate the following section:
```
  <!-- ** MODIFY or DELETE **
  "accesslog" nodes tell the script to scan webserver log files to
  extract URLs on your site.  Both Common Logfile Format (Apache's default 
  logfile) and Extended Logfile Format (IIS's default logfile) can be read.
				
  Required attributes:
   path - path to the file
  Optional attributes:
   encoding - encoding of the file if not US-ASCII
   -->
<accesslog path="/etc/httpd/logs/access.log" encoding="UTF-8" />
<accesslog path="/etc/httpd/logs/access.log.0" encoding="UTF-8" />
<accesslog path="/etc/httpd/logs/access.log.1.gz" encoding="UTF-8" />
```
> This section gives three examples. You should replace these entries and include an entry for each log file. Ensure that the path value is the complete path and filename on your web server. If the log files are not encoded as US-ASCII or UTF-8, then use the optional **encoding** attribute to specify the encoding. Rather than list each log file, you can use wildcards. For instance, in the above example, you could include the following entry that would include all three log files:
```
<accesslog path="/etc/httpd/logs/access.log*" encoding="UTF-8" /> 
```
> The Sitemap Generator assigns priority to URLs it finds in the logs based on how often each URL is accessed. For instance, a URL that has been accessed 100 times will be given a higher priority than a URL that has been accessed twice. The actual priority assignment is relative and depends on each URL as compared to other URLs in the site.

  * **Sitemap**

> Locate the following section:
```
  <!-- ** MODIFY or DELETE **
    
  "sitemap" nodes tell the script to scan other Sitemap files.  This can    
  be useful to aggregate the results of multiple runs of this script into
  a single Sitemap.
				 
  Required attributes:
   path - path to the file
   -->
  <sitemap path="/var/www/docroot/subpath/sitemap.xml" />
```
> This section gives one example. You should replace this entry and include an entry for each Sitemap you want to include. Ensure that the path value is the complete path and filename on your web server. You can list gzipped Sitemaps as well, as long as they have a .gz extension. Rather than list each Sitemap, you can use wildcards. For instance, the following entry would include any Sitemaps that begin with the word "sitemap" and have an .xml extension:
```
<sitemap path="/var/www/docroot/subpath/sitemap*.xml" /> 
```
> The Sitemap Generator extracts all URLs and the optional data listed for each URL for every Sitemap you list and creates one Sitemap with this information. At this time, we can't guarantee that this method will work Sitemaps created with tools other than the Sitemap Generator.

> 8. Locate the filter definition section:
```
  <!-- ********************************************************         
  FILTERS
				
  Filters specify wild-card patterns that the script compares
against all URLs it finds. Filters can be used to exclude
certain URLs from your Sitemap, for instance if you have
hidden content that you hope the search engines don't find.

  Filters can be either type="wildcard", which means standard
path wildcards (* and ?) are used to compare against URLs,
 or type="regexp", which means regular expressions are used
to compare.

  Filters are applied in the order specified in this file.
An action="drop" filter causes exclusion of matching URLs.
An action="pass" filter causes inclusion of matching URLs,
shortcutting any other later filters that might also match.
If no filter at all matches a URL, the URL will be included.
Together you can build up fairly complex rules.

  The default action is "drop".
  The default type is "wildcard".

  You can MODIFY or DELETE these entries as appropriate for
your site. However, unlike above, the example entries in
this section are not contrived and may be useful to you as
they are.
  ********************************************************* -->

  <!-- Exclude URLs that end with a '~' (IE: emacs backup files) -->
  <filter action="drop" type="wildcard" pattern="*~" />

  <!-- Exclude URLs within UNIX-style hidden files or directories -->
  <filter action="drop" type="regexp" pattern="/\.[^/]*" />
```
> > You can use filtering to exclude specific URLs from the generated Sitemap. You might want to do this to create a cleaner list, to reduce redundant listings, or to keep certain URLs from being indexed. Note that if you use a [robots.txt](http://www.robotstxt.org/wc/robots.html) file to keep URLs from being indexed, then even if the URLs are included in your Sitemap, Google will not search or index them.


> You can use any or all of the filtering methods. You can delete the entries you don’t need and can create additional entries, if desired. Below are sample usages.
```
  <filter action="drop" type="wildcard" pattern="*.jpg" />
```
> This filter excludes URLs that end in .jpg. You might want to include a similar filter if all of your site’s images are embedded within HTML pages and should not be accessed as standalone URLs.
```
  <filter action="pass" type="wildcard" pattern="*.htm*" />
  <filter action="drop" type="wildcard" pattern="*" />
```
> This filter includes all `.htm*` files but excludes everything else.

> 9. Once you have made all the changes for your site, save the file.

**Config File Syntax Reference**

A complete explanation of the config file syntax is below. Each tag begins with a code sample, followed by a description of the attributes.

**site**

Required tag at the beginning of each config file.
```
<site
base_url="http://www.example.com/"
store_into="/var/www/html/sitemap.xml.gz"
verbose="1"
supress_search_engine_notify="1"
default_encoding="UTF-8">
```

|base\_url|required|The HTTP path of the base of your website - only URLs that begin with this base can be included in the Sitemap|
|:--------|:-------|:-------------------------------------------------------------------------------------------------------------|
|store\_into|required|The web server path to the desired output file. The script will create this file - there's no need to create the file before running the script.|
|verbose  |optional|Enter a number from 0-3, with higher numbers corresponding to increased debug information                     |
|suppress\_search\_engine\_notify|optional|Disable search engine notification by entering "1" for testing purposes                                       |
|default\_encoding|optional|Specify a character encoding to be applied to file system paths and URLs                                      |

**url**

Optional tag that you can use to list each URL in your site.
```
<url
href="http://www.example.com/stats?q=age" 
lastmod="2004-11-14T01:00:00-07:00" 
changefreq="yearly" 
priority="0.3"
/> 
```

|href|required|The HTTP path of the base of your website - only URLs that begin with this base can be included in the Sitemap|
|:---|:-------|:-------------------------------------------------------------------------------------------------------------|
|lastmod|optional|The time the URL was last modified in [W3C Datetime](http://www.w3.org/TR/NOTE-datetime) format (YYYY-MM-DDThh:mm:ss+00:00). You may omit the time portion. Examples: "2005-02-21T18:00:15+00:00", "2005-02-21"|
|changefreq|optional|The frequency with which the URL is likely to change. This is considered a hint and not a command. The value must be one of "always", "hourly", "daily", "weekly", "monthly", "yearly", or "never".|
|priority|optional|The priority of this page relative to other pages on the same site. The value is a number between 0.0 and 1.0, where 0.0 is the lowest priority and 1.0 is the highest priority. The priority can affect the order that search engines select URLs to explore on your site. Since the priority is relative, it is only used to select between URLs within your own site; the priority of your pages will not be compared to the priority of pages on other sites.|

**urllist**

Optional tag that you can use to point to a text file that contains a list of the URLs in your site.
```
<urllist path="/var/www/html/urllist.txt" encoding="UTF-8" />
```

|path|required|The path and filename of the .txt file. You can specify either a relative or complete path.|
|:---|:-------|:------------------------------------------------------------------------------------------|
|encoding|optional|The encoding of the file, if not UTF-8.                                                    |

The **urllist.txt** file is a simple text file containing a list of URLs to map. You can also include optional attributes for each URL. Attributes are entered on the same line as the URL and are separated by a single space. For example:
```
http://www.example.com/abc/something
http://www.example.com/abc/xyy.pdf lastmod=2001-12-31T14:05:06+00:00
http://www.example.com/abc/def?x=12&y=23 changefreq=weekly priority=0.3
```

|lastmod|optional|The time the URL was last modified in W3C Datetime format (YYYY-MM-DDThh:mm:ss+00:00). You may omit the time portion. Examples: "2005-02-21T18:00:15+00:00", "2005-02-21"|
|:------|:-------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|changefreq|optional|The frequency with which the URL is likely to change. This is considered a hint and not a command. The value must be one of "always", "hourly", "daily", "weekly", "monthly", "yearly", or "never".|
|priority|optional|The priority of this page relative to other pages on the same site. The value is a number between 0.0 and 1.0, where 0.0 is the lowest priority and 1.0 is the highest priority. The priority can affect the order that search engines select URLs to explore on your site. Since the priority is relative, it is only used to select between URLs within your own site; the priority of your pages will not be compared to the priority of pages on other sites.|

**directory**

Optional tag that you can use to specify directories in your site so the Sitemap Generator can create a list of URLs from the files found in those directories.
```
<directory  path="/var/www/icons"    url="http://www.example.com/images/" />
<directory
   path="/var/www/docroot"
   url="http://www.example.com/"
   default_file="index.html"
/>
```

|path|required|States the initial path. Sitemap Generator will traverse this directory and all subdirectories.|
|:---|:-------|:----------------------------------------------------------------------------------------------|
|url |required|Specifies the URL equivalent of the path value.                                                |
|default\_file|optional|Specifies the default file for a directory on the server.                                      |

**accesslog**

Optional tag that you can use to specify the path and filename of IIS and Apache-style access logs so the Sitemap Generator can automatically pick up URLs from them.
```
<accesslog path="/etc/httpd/logs/access-0.log" encoding="UTF-8"/>
```

|path|required|States the path to the file.|
|:---|:-------|:---------------------------|
|encoding|optional|Specifies encoding of the file, if not UTF-8.|

**sitemap**

Optional tag that you can use to specify the path and filename of existing Sitemaps that you have created with the Sitemap Generator. The Sitemap Generator will create a single Sitemap that includes the URLs contained in each Sitemap.
```
<sitemap path="/var/www/docroot/subpath/sitemap.xml" />
```

|path|required|States the path to the Sitemap file.|
|:---|:-------|:-----------------------------------|

**filter**

Optional tag that you can use to build rules that include or exclude specific files. Filters are obeyed in the order in which they appear in the config.xml file. However, intermixing filter entries and input entries (url, urllist, directory, or accesslog) has no additional effect - every URL the Sitemap Generator adds to the Sitemap is first compared against every filter. If no filter matches a URL, the default is to include the URL in the Sitemap.
```
<filter action="drop" type="wildcard" pattern="*/internal/*" />
```

|action|optional|The action the filter should take. Valid values are: **drop** - excludes matching URLs. This is the default action, so if no action is specified, the generator assumes "drop". **pass** - includes matching URLs.|
|:-----|:-------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|type  |optional|The type of filtering. Valid values are: **wildcard** - standard path wildcards (`?` and `*`) are used to compare against URLs. This is the default type, so if no type is specified, the generator assumes "wildcard". **regexp** - regular expressions are used.|
|pattern|required|Specifies the pattern to match against.                                                                                                                                                                           |

**Encodings**

Files referenced by your configuration file, either URL lists or web server logs, can use encodings other than the default UTF-8. You can specify alternate encodings in config.xml to affect how the Sitemap Generator reads your files. Some common encodings are:

  * **encoding="utf-8"** is the assumed default
  * **encoding="ascii"** is a subset of UTF-8 so you don't have to specify it
  * **encoding="iso-8859-1"** is common for many west European languages

**Additional information for creating a mobile configuration file**

You create a configuration file for a Mobile Sitemap in the same way as for a non-mobile Sitemap. However, you must create a separate config file for each markup language and run the Sitemap Generator with each config file separately so that you create a separate Sitemap for each.

Each config file must:

  * Specify a different filename for the **store\_into** value.
  * Use filters to specify the URLs to exclude and include for the markup language. Remember that each Sitemap should include URLs for only one markup language. This means that the same URL may be included in multiple Sitemaps, if those URLs serve multiple markup languages.

**Examples of filtering**

Below are some examples of how you can use extension-based filters to generate Mobile Sitemaps for different markup languages. The specific filtering you use should be based on the types of markup languages used in your site, and how you specify each type. If you have implemented the details of your site differently (for instance, you may organize URLs with different markup languages in separate folders), you should filter based on the specifics of your site implementation. Remember that filters are applied in the order you list them in the config file. So, the first filter you should list is a "pass" action that specifies the URLs you want to include in the Sitemap.

To create a Sitemap for WML (WAP 1.2) content:
```
<filter action="pass" type="wildcard" pattern="*.wml" />
<filter action="drop" type="wildcard" pattern="*.*" />
```
To create a Sitemap for XHTML mobile profile (WAP 2.0) content:
```
<filter action="pass" type="wildcard" pattern="*.xhtml" />
<filter action="drop" type="wildcard" pattern="*.*" />
```

### 3. Uploading the necessary files ###

You should upload the following files to your web server in a location you can access from a command line:

  * **config.xml** —this is the configuration file you just created using **example\_config.xml**.
  * **sitemap\_gen.pl** —this is the Perl script that generates your Sitemap.
  * **urllist.txt** —this file is optional; you only need to include it if you used the text file method of generating a Sitemap.

The method you use to upload these files depends on your environment. Common methods include FTP and SCP. For more information, contact your web host.

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

### 5. Adding the generated sitemap ###

The Sitemap Generator creates a **sitemap.xml** file in the location you specified in the config file. Once this file is successfully created, make sure it is accessible through a web browser. Then, [add](http://www.google.com/support/webmasters/bin/answer.py?answer=34575&topic=8496) it to your [Google Sitemaps account](https://www.google.com/webmasters/sitemaps/siteoverview). This enables Google to provide you with useful status and statistical information. If Google reports problems with your Sitemap, you can correct the problems and resubmit it. You only have to add the Sitemap manually once. After that, you can use an HTTP request to notify Google about changes to your Sitemap (although you can also resubmit it through your Google webmaster tools account).

### 6. Setting up a recurring script (optional) ###

We suggest setting up the Perl Sitemap Generator to run as often as your content is changed, to a maximum frequency of once per hour.

Webmasters with a UNIX web server may consider setting this up as a [cron job](http://www.google.com/search?q=cron).

Webmasters using other platforms should contact their system administrator for help in configuring recurring scripts. You may also benefit from peer advice in the Google Sitemaps Group on [Google Groups](http://groups.google.com/group/Google_Webmaster_Help-Sitemap?tsc=1).

You can use an HTTP request to let Google know about changes to your Sitemap. However, please make sure that you log in to [Google webmaster tools](https://www.google.com/webmasters/sitemaps/siteoverview) with your Google Account once to manually [add your Sitemap](http://www.google.com/support/webmasters/bin/answer.py?answer=34575&topic=8496) to your Google webmaster tools account.
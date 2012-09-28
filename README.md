google-mini
===========

XSLT Templates to deliver Google Mini results in formats other than HTML

The three XSLT templates in this directory have been tested on a Google Mini search appliance (version 5.0.4), but should work just as well on a Google Enterprise search appliance.

Use these stylesheets by creating a new Front End on your search appliance (Serving > Front Ends).
Click on 'edit' for the entry for your new front end.
In the 'XSLT Stylesheet Editor' box, click 'Edit underlying XSLT code'.
Paste the contents of one of the templates in this repository into the edit box that appears.
Click 'Save XSLT Code'
Click on 'Ok' on the warning box that pops up to agree that you wish to proceed.
    

The Templates
=============

-------
id.xsl
-------
    This template will return the search results as XML in the native Google format.
    The template is an identity transformation so does not alter the XML in any way.
    
    For more details on how to interpret the XML returned, see:

    https://developers.google.com/search-appliance/documentation/614/
    
---------
json.xsl
---------
    This template will turn the search results into JSON formatted data. The structure of the data is as indicated in the example below:
    
    

{
	"query": "query-string",

	"results":
	[
    	{
    	    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"mime": "application/pdf"
		},

		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"size": "27k"
		},

		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"size": "58k"
		},
		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"size": "28k"
		},
		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"size": "34k"
		},
		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"size": "19k",
			"mime": "text/plain"
		},
		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"size": "36k"
		},
		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"mime": "application/pdf"
		},
		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"mime": "application/pdf"
		},
		{
		    "url": "http://your-site.com/url-to-search-result",
			"title": "Title of the page",
			"summary": "Summary of the page contents (May contain HTML tags)",
			"size": "15k",
			"mime": "text/plain"
		}
	],

	"results_nav":
	{
	    "total_results": "552",
	    "results_start": "12",
	    "results_end": "21",
	    "current_view": "11",
	    "have_prev": "1",
	    "have_next": "1"
	}
}

Description of data:
query: [string] Contains the query string that was passed to the search appliance
results: [array] Contains hashes corresponding to each search result returned (default max 10 results)
    url: [string] URL to the search result
    title: [string] The title of the page or content found
    summary: [string] A summary of the page or document content (N.B. This may contain HTML)
    size: [string] [optional] A human readable description of the document's size. May not be available (e.g. for PDF documents it is not returned)
    mime: [string] [optional] The MIME type of the document. This may not be returned (e.g. for HTML documents it is not returned)
results_nav: [hash] Contains information about where in the search results you currently are
    total_results: [integer] Google's guess at how many results there are. This is usually wildly inaccurate.
    results_start: [integer] The position of the first result in this set
    results_end: [integer] The position of the last result in this set
    current_view: [integer] The 'start' parameter that was passed to the search appliance to return this result set
    have_prev: [boolean] Is set to 1 if there are previous results available, omitted otherwise
    have_next: [boolean] Is set to 1 if there are more results available, omitted otherwise
    

----------
jsonp.xsl
----------
    This template returns data in a JSONP format. The body of data is as described for json.xsl above, but the data is wrapped in a callback function.

    When you query the search appliance, you can append a parameter of 'callback' to set the name of the JavaScript function that will process the returned results. For example:

http://search.yourcompany.com/search?output=xml_no_dtd&client=jsonp&proxystylesheet=jsonp&site=default_collection&q=search+query&callback=your_function_name

    If you do not specify a callback parameter, then the default callback function will be 'search_results_callback'.


Some comments on using html, markdown, mathjax, jekyll and whatnot:

	1) when writing down conditional probabilities inline in markdown, markdown inteprets them as part of a table; to solve this problem, simply write the paragraph with html adding <p> 
	2) site.url = https://ghostsandmachines.github.io	
	   site.base-url = this is not defined UNTIL you write it out explicitly in your config file. What is the base-url? It's whatever comes right after you site url, for instance https://ghostsandmachines.github.io{base-url} and usually we have something like https://ghostsandmachines.github.io/somename/ and /somename is the base url. Effectively you can ignore it altogether if you don't want anything other than the name of your website and the subsequent links
	3) {{ page.date }} gives the date of the page, ie, date: 2019-01-12, in the posts; if there is no date indicated it gives nothing as it should be
	4) note that in _site jekyll automatically creates more folder organized by year then month then day, without needing any gems actually, I tested it in an another branch. So it's nothing to do with jekyll-archives.
  <div class="trigger">
          {%- for path in page_paths -%}
            {%- assign my_page = site.pages | where: "path", path | first -%}
            {%- if my_page.title -%}
            <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
            {%- endif -%}
          {%- endfor -%}
        </div>


<ul> 
    <li><a class="page-link" href="/">Home</a></li>
    <li><a class="page-link" href="/about">About</a></li>
    <li><a class="page-link" href="/blog">Blog</a></li>
</ul>        


  {%- if page.title -%}
    <h1 class="page-heading">{{ page.title }}</h1>
  {%- endif -%}

  
  vertical-align: middle;

   <span class="page_number ">
    Page: {{ paginator.page }} of {{ paginator.total_pages }}
  </span>

  <div class="trigger">
          {%- for path in page_paths -%}
            {%- assign my_page = site.pages | where: "path", path | first -%}
            {%- if my_page.title == "Home" or my_page.title == "About" or my_page.title == "Blog" -%}
            <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
            {%- endif -%}
          {%- endfor -%}
        </div>

<p>The patterns by themselves are interesting and it is likely that some of them still need to be uncovered, especially moving beyond the analysis of the marginal statistics.

Going further, what exactly can we infer from such patterns? Do they actually reflect biophysical principles? Are they rather neutral effects of genome-level evolution dynamics? Even 'more neutrally', similar regularities have been observed in contexts rather different from biology. All such contexts have in common is a simple data structure in which we have realizations made up of certain categories. Then, are some of these patterns best seen as mere robust statistical artificats of the data structure? In particular, what is the statistical relationship relationship of these patterns with one another? How, if at all, do they imply one another? How do they constrain one another? So far, I've focused on what is neutral and null first, elaborating minimal evolutionary and statistical models of proteome organization.
</p>        
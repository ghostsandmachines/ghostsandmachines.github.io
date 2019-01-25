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
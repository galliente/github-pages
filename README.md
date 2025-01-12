<!doctype html>
<html lang="{{ shop.locale }}" class="color_scheme" {% if settings.rtl %}dir="rtl"{% endif %}>
	<head>
		<meta charset="utf-8">

		{% capture seo_title %}
			{{ page_title }}

			{% unless page_title contains shop.name %}
				&ndash; {{ shop.name }}
			{% endunless %}
		{% endcapture %}

		<title>{{ seo_title }}</title>

		<link rel="canonical" href="{{ canonical_url }}">

		{%- if settings.favicon.size > 0 -%}
			<link rel="shortcut icon" href="{{ settings.favicon | img_url: '32x32' }}" type="image/png">
		{%- endif -%}

		{%- if page_description -%}
			<meta name="description" content="{{ page_description | escape }}">
		{%- endif -%}

		<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />

		<!--[if IE]>
			<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
		<![endif]-->
		
		<!-- CSS -->
		{% include 'variables' %}
		{{ 'style.scss.css' | asset_url | stylesheet_tag }}
		{{ 'responsive.scss.css' | asset_url | stylesheet_tag }}
		{% if settings.rtl %}
			{{ 'rtl.scss.css' | asset_url | stylesheet_tag }}
		{% endif %}
		
		<!-- JS -->
		<script>
			var theme = {
				moneyFormat: {{ shop.money_format | json }},
			};
		</script>
		<script src="{{ 'assets.js' | asset_url }}"></script>
		<script src="{{ 'lazysizes.min.js' | asset_url }}" defer></script>
		<script src="{{ 'shop.js' | asset_url }}" defer></script>

		{%- if content_for_index contains 'index_section_slideshow__slide_video' -%}
			<script src="{{ 'YTPlayer.min.js' | asset_url }}" defer></script>			
		{%- endif -%}
					

		
		{%- if template contains 'customers' -%}
			<script src="{{ 'shopify_common.js' | shopify_asset_url }}" defer></script>
			<script src="{{ 'customer_area.js' | shopify_asset_url }}" defer></script>
		{%- endif -%}
		
		{%- unless template == 'password' or template == 'page.password' -%}
			{{ 'header-script.js' | asset_url | script_tag }}
		{%- endunless -%}

		<!-- SHOPIFY SERVICE SCRIPTS -->
		{{ content_for_header }}
	</head>

	<body class="template-{{ template | split: '.' | first }} {{ settings.color_scheme }} {% if settings.rtl %}rtl{% endif %}">
		<div class="page_wrapper">

			<div id="page_preloader__bg">
				<img id="page_preloader__img" src="{{ 'shopify_logo.gif' | asset_url }}" alt="">
			</div>

			<script>
				preloaderBg = document.getElementById('page_preloader__bg');
				preloaderImg = document.getElementById('page_preloader__img');

				window.addEventListener('load', function() {
					preloaderBg.classList.add("off");
					preloaderImg.classList.add("off");
				});

			</script>

			{% if template == 'page.sections'%}
				{% section 'sect_all' %}
			{% endif %}

			{% if template == 'password' or template == 'page.password' %}
				{{ content_for_layout }}
			{% else %}
				{% section 'helper' %}
				
				{% section 'header-2' %}

				<div class="page_container">
					{% unless template == 'index' or template == '404' %}
						{% include 'snippet-breadcrumbs' %}
					{% endunless %}
					
					
					{%- assign sidebar_on = false -%}
					{% case template %}
						{% when 'article', 'collection', 'search', 'page.wishlist', 'collection.right-sidebar', 'collection.loadmore' %}
							{% if settings.sidebar_toggle %}
								{%- assign sidebar_on = true -%}
							{% endif %}
					{% endcase %}
					
					{% if sidebar_on %}
						<div class="container">
							{% if template == 'collection' %}
								<div class="collection_info_wrapper">
									{% include 'collection_info' %}
								</div>

							{% endif %}
							<div class="row">	
					{% endif %}
							<div class="main_content {% if sidebar_on %}sidebar_on {% if template == 'article' %}col-md-9{% else %}col-md-9 col-lg-9{% endif %} {% unless template == 'collection.right-sidebar' %}{% if settings.sidebar_position == 'sidebar_left' %}left-sidebar{% endif %}{% endunless %}{% endif %}">
								{{ content_for_layout }} 
							    
							</div>

							{% if sidebar_on %}
								<div class="sidebar_small {% if template == 'article' %}col-md-3{% else %}col-md-3 col-lg-3{% endif %}">
									{% if template == 'blog' or template == 'article' %}
										{% section 'sidebar-blog' %}
									{% else %}
										{% section 'sidebar' %}
									{% endif %}
								</div>
							{% endif %}
					{% if sidebar_on %}
							</div>
						</div>
					{% endif %}
					

                    {% section 'footer-1' %}

				</div>

				<a id="back_top" href="#">
					<i class="fa fa-angle-up" aria-hidden="true"></i>
				</a>
			{% endif %}	
		</div>



		{% if settings.newsletter_popup_toggle %}
			{% include 'widget-newsletter-popup' %}
		{% endif %}


	</body>

</html>




<header>

<!--
  <<< Author notes: Course header >>>
  Include a 1280×640 image, course title in sentence case, and a concise description in emphasis.
  In your repository settings: enable template repository, add your 1280×640 social image, auto delete head branches.
  Add your open source license, GitHub uses MIT license.
-->

# GitHub Pages

_Create a site or blog from your GitHub repositories with GitHub Pages._

</header>

<!--
  <<< Author notes: Course start >>>
  Include start button, a note about Actions minutes,
  and tell the learner why they should take the course.
-->

## Welcome

With GitHub Pages, you can host project blogs, documentation, resumes, portfolios, or any other static content you'd like. Your GitHub repository can easily become its own website. In this course, we'll show you how to set up your own site or blog using GitHub Pages.

- **Who is this for**: Beginners, students, project maintainers, small businesses.
- **What you'll learn**: How to build a GitHub Pages site.
- **What you'll build**: We'll build a simple GitHub Pages site with a blog. We'll use [Jekyll](https://jekyllrb.com), a static site generator.
- **Prerequisites**: If you need to learn about branches, commits, and pull requests, take [Introduction to GitHub](https://github.com/skills/introduction-to-github) first.
- **How long**: This course takes less than one hour to complete.

In this course, you will:

1. Enable GitHub Pages
2. Configure your site
3. Customize your home page
4. Create a blog post
5. Merge your pull request

### How to start this course

<!-- For start course, run in JavaScript:
'https://github.com/new?' + new URLSearchParams({
  template_owner: 'skills',
  template_name: 'github-pages',
  owner: '@me',
  name: 'skills-github-pages',
  description: 'My clone repository',
  visibility: 'public',
}).toString()
-->

[![start-course](https://user-images.githubusercontent.com/1221423/235727646-4a590299-ffe5-480d-8cd5-8194ea184546.svg)](https://github.com/new?template_owner=skills&template_name=github-pages&owner=%40me&name=skills-github-pages&description=My+clone+repository&visibility=public)

1. Right-click **Start course** and open the link in a new tab.
2. In the new tab, most of the prompts will automatically fill in for you.
   - For owner, choose your personal account or an organization to host the repository.
   - We recommend creating a public repository, as private repositories will [use Actions minutes](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions).
   - Scroll down and click the **Create repository** button at the bottom of the form.
3. After your new repository is created, wait about 20 seconds, then refresh the page. Follow the step-by-step instructions in the new repository's README.

<footer>

<!--
  <<< Author notes: Footer >>>
  Add a link to get support, GitHub status page, code of conduct, license link.
-->

---

Get help: [Post in our discussion board](https://github.com/orgs/skills/discussions/categories/github-pages) &bull; [Review the GitHub status page](https://www.githubstatus.com/)

&copy; 2023 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

</footer>

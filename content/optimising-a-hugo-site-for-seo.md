---
title: Optimising A Hugo Site For SEO
date: 2024-10-24
---
# Optimising A Hugo Site for SEO 

Let this article serve as a reference and checklist. 

Hugo is a static site generator, which makes it fast and efficient, but it also means you have to ensure that you’re following best SEO practices manually:

### 1. **Configure Basic SEO in Hugo**
   - **Page Titles and Meta Descriptions**: 
     - Ensure each page has a unique, descriptive `<title>` tag and meta description.
     - Use Hugo’s templating system to dynamically generate meta tags in the head of each page. Add this to your `head.html` partial:
       ```html
       <title>{{ .Title }} - {{ .Site.Title }}</title>
       <meta name="description" content="{{ .Description }}">
       <meta name="keywords" content="H5P consultancy, H5P development, {{ .Keywords }}">
       ```
   - **Permalinks**: 
     - Ensure URLs are clean and readable by configuring permalinks in your `config.toml` or `config.yaml`.
       ```toml
       [permalinks]
       post = "/:title/"
       ```
     - Use descriptive URLs that reflect your content and keywords.
  
### 2. **Optimize Your Content**
   - **Keyword Research**: 
     - Conduct keyword research to find the most relevant keywords for each page or blog post.
     - Incorporate those keywords naturally into your title, headings (H1, H2), and body text.
   - **Structured Content**: 
     - Organize content with proper headings (`<h1>`, `<h2>`, `<h3>`) to enhance readability and improve search engines' understanding of your content.
   - **Internal Linking**: 
     - Link relevant pages or blog posts together. This helps search engines crawl your site and builds context around key topics.

### 3. **Optimize for Speed and Mobile**
   - **Page Speed**: 
     - Hugo-generated sites are usually very fast, but further optimize performance by compressing images, enabling lazy loading for images, and using a CDN.
     - Use minified CSS and JavaScript. You can do this in Hugo with:
       ```toml
       [minify]
       disableHTML = false
       disableCSS = false
       disableJS = false
       ```
     - Enable GZIP compression on your server for faster loading times.
	 
### 4. **Create an XML Sitemap**
   - Hugo has built-in support for generating a sitemap. Make sure your `config.toml` file includes this configuration:
     ```toml
     [outputs]
     home = ["HTML", "RSS", "SITEMAP"]
     ```
   - This will generate an `sitemap.xml` file at the root of your site, which helps search engines index your pages.

### 5. **Use Schema Markup**
   - Implement structured data to help search engines understand your content. For a blog post, you can add schema markup like this in your `head.html` partial:
     ```html
     <script type="application/ld+json">
     {
       "@context": "https://schema.org",
       "@type": "BlogPosting",
       "headline": "{{ .Title }}",
       "author": "{{ .Params.author }}",
       "datePublished": "{{ .Date }}",
       "description": "{{ .Description }}"
     }
     </script>
     ```
   - Schema.org provides additional schema types you can use for reviews, articles, events, etc.

### 6. **Set Up Canonical URLs**
   - Avoid duplicate content issues by setting canonical URLs in the head of your pages:
     ```html
     <link rel="canonical" href="{{ .Permalink }}">
     ```

### 7. **Create SEO-Friendly Blog Content**
   - Write high-quality, long-form content that answers user queries (figure out what users might ask in search engines)
   - Regularly update your blog with new content.
   - Use images with descriptive alt text 
   - Use "rich snippets" for things like FAQ or How-to content to increase visibility in search results (this might be a bit overkill when thinking about how to implement it in markdown)

### 8. **Optimize for Social Sharing (Open Graph and Twitter Cards)**
   - Add Open Graph and Twitter meta tags to control how your content appears when shared on social media. In `head.html`:
     ```html
     <meta property="og:title" content="{{ .Title }}">
     <meta property="og:description" content="{{ .Description }}">
     <meta property="og:image" content="{{ .Params.image }}">
     <meta name="twitter:card" content="summary_large_image">
     <meta name="twitter:title" content="{{ .Title }}">
     <meta name="twitter:description" content="{{ .Description }}">
     ```

### 9. **Robots.txt and Noindex**
   - Ensure that search engines are allowed to index your site by creating a `robots.txt` file.
   - Use the `noindex` meta tag on any pages you don’t want to be indexed, such as privacy policies or draft pages.

### 10. **Monitor and Adjust SEO**
   - **Google Search Console**: Submit your site and sitemap to Google Search Console to monitor performance and indexing issues.
   - **Analytics**: Use Google Analytics or another tool to track traffic, bounce rates, and keyword rankings.

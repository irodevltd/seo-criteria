# SEO criteria

**English** · [Türkçe](SEO.tr.md)

The 99 checks of the irodev.net SEO audit, each with why it matters, how to fix it and, where it helps, an example. Every one is measurable and backed by the search engines' own documentation; the sources are listed under each group. Things that are often counted but aren't real ranking criteria are in [MYTHS.md](MYTHS.md).

Run them on your own page with the [free SEO audit](https://irodev.net/ucretsiz-seo-analizi). The "Site crawl" group needs the whole site crawled.

- [Basics](#basics) (8)
- [Content](#content) (10)
- [Technical](#tech) (21)
- [Performance](#perf) (11)
- [Security](#security) (4)
- [Mobile & accessibility](#mobile) (7)
- [Social & schema](#social) (11)
- [Local SEO](#local) (6)
- [Core Web Vitals](#vitals) (5)
- [Links](#links) (3)
- [Site crawl](#site) (13)

<a name="basics"></a>

## Basics

What every page needs before anything else: a secure address, a title and description, a mobile viewport, a language and a character set.

### HTTPS secure connection

*Impact: high · Effort: easy*

Browsers mark plain-HTTP pages as "Not secure" and Google treats HTTPS as a ranking signal. Forms on HTTP also leak what visitors type.

**How to fix it**

1. Install a free certificate (Let's Encrypt) from your hosting panel.
2. Redirect every http:// address to https:// with a 301.
3. Update internal links, canonical tags and the sitemap to https.

```text
# .htaccess
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

### Valid SSL certificate

*Impact: high · Effort: easy*

An expired or mismatched certificate shows a full-page browser warning before visitors see anything, and most of them leave.

**How to fix it**

1. Renew the certificate and make sure it covers both example.com and www.example.com.
2. Install the full chain (intermediate certificates), not only the site certificate.
3. Turn on automatic renewal so it never lapses again.

### Page title

*Impact: high · Effort: easy*

The title is the blue headline in search results and the first thing people read. A clear title with your main service raises both rankings and clicks.

**How to fix it**

1. Keep it between 30 and 65 characters so it is not cut off.
2. Put the main keyword first, then your brand: "Service in City | Brand".
3. Give every page its own title; never repeat one.

```html
<title>Corporate Web Design in Ankara | Ardena</title>
```

### Meta description

*Impact: medium · Effort: easy*

The description is the grey text under your title in search results. Google does not rank on it, but a good one decides whether people click.

**How to fix it**

1. Write 70–165 characters that answer "why this page?".
2. Mention the service, the benefit and a call to action.
3. Write a unique description for each important page.

```html
<meta name="description" content="Fast, mobile-first corporate websites with a fixed quote. Get a proposal within one business day.">
```

### Mobile viewport

*Impact: high · Effort: easy*

Google ranks the mobile version of your site. Without a viewport tag phones show a zoomed-out desktop page.

**How to fix it**

1. Add the viewport tag inside <head>.
2. Check the page on a real phone: text must be readable without zooming.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### Language attribute

*Impact: low · Effort: easy*

Screen readers pick the pronunciation from the lang attribute, browsers use it for translation and hyphenation (WCAG 3.1.1), and Bing reads it. Google works out the language from the visible text instead.

**How to fix it**

1. Set it on the <html> element: tr for Turkish, en for English.

```html
<html lang="tr">
```

### Character encoding

*Impact: low · Effort: easy*

Without a declared encoding, Turkish characters such as ş, ğ and İ can turn into garbled symbols in some browsers and in search snippets.

**How to fix it**

1. Declare UTF-8 as the first element inside <head>.

```html
<meta charset="utf-8">
```

### Favicon

*Impact: low · Effort: easy*

Google shows the favicon next to your result on mobile, and browsers show it on tabs and bookmarks. A missing icon looks unfinished.

**How to fix it**

1. Add a square icon (at least 48×48 px; SVG or PNG).
2. Add an apple-touch-icon (180×180) for iPhones.

```html
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

**Sources:** [Title links](https://developers.google.com/search/docs/appearance/title-link) · [Snippets and meta descriptions](https://developers.google.com/search/docs/appearance/snippet) · [Mobile-first indexing](https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing) · [Favicons in Search](https://developers.google.com/search/docs/appearance/favicon-in-search) · [Page experience](https://developers.google.com/search/docs/appearance/page-experience)

<a name="content"></a>

## Content

The visible content: headings, text, images and links that tell people and search engines what the page is about.

### Main heading (H1)

*Impact: medium · Effort: easy*

The H1 is the headline visitors see first, and Google may use it when it writes the title link of your result. Several H1s are fine for Google; having none leaves the page without a clear main heading.

**How to fix it**

1. Give the page a clear main heading in an <h1>, with the main topic in it.
2. If your theme wraps only the logo in an <h1>, add a real headline as well.

```html
<h1>Corporate websites that bring in customers</h1>
```

### Heading structure

*Impact: low · Effort: easy*

Subheadings split long text into sections that visitors can scan and screen readers can jump between. Google says heading order does not matter for ranking, but a long page without a single subheading is hard to read.

**How to fix it**

1. Give each main section an <h2>, and its sub-points <h3>.
2. Do not skip levels (an <h4> right after the <h1>): screen-reader users navigate by them.
3. Use headings for structure, not for making text bigger.

### Text content

*Impact: medium · Effort: moderate*

Google has no minimum word count, but a page needs enough text to say what it offers and answer the searcher's question. With almost no text, search engines and AI assistants have nothing to understand or quote.

**How to fix it**

1. Say plainly what the page offers, for whom, and why to choose you.
2. Answer what customers ask before buying: price, process, timing, guarantees.
3. Write for the reader, not for a word count.

### Image alt text

*Impact: medium · Effort: easy*

Alt text describes an image to Google Images, to screen readers and to AI models. It is also an accessibility requirement.

**How to fix it**

1. Add a short, specific alt to every meaningful image.
2. Use alt="" for purely decorative images so screen readers skip them.
3. Describe the content, do not stuff keywords.

```html
<img src="team.webp" alt="Our design team reviewing a homepage layout" width="1200" height="800">
```

### Main topic in the title

*Impact: low · Effort: easy*

The words a page uses most are usually its topic. If none of them is in the title, the title may not describe the page, and Google may rewrite it or show the page for other searches.

**How to fix it**

1. Check the keyword table below and pick the term customers search for.
2. Put that term in the title and the H1 in natural wording.

### Internal links

*Impact: medium · Effort: easy*

Links to your own pages help visitors go deeper and let search engines find and value your other pages.

**How to fix it**

1. Link to related services, case studies and the contact page from the text.
2. Use descriptive anchor text ("corporate web design"), not "click here".

### Readability

*Impact: low · Effort: moderate*

Google does not use readability scores, but visitors skim: long sentences and heavy words lose them before they reach your offer, and plain text is easier for AI assistants to quote correctly.

**How to fix it**

1. Keep most sentences under 20 words; split long ones in two.
2. Prefer everyday words to jargon, and explain a technical term the first time you use it.
3. Use short paragraphs (2–4 sentences), subheadings and lists.

### Title and H1 match

*Impact: low · Effort: easy*

The title is what searchers click; the H1 is what they see when they land. When the two talk about different things people feel misled, and Google may replace your title with the H1 or other text from the page.

**How to fix it**

1. Make the H1 repeat the main topic of the title. It does not have to be identical.
2. Keep your main keyword in both.

```html
<title>Corporate Web Design in Ankara | Ardena</title>
<h1>Corporate web design for Ankara businesses</h1>
```

### Descriptive link text

*Impact: low · Effort: easy*

Link text tells visitors and search engines what is behind a link. "Click here" or "read more" says nothing, and screen-reader users jumping from link to link hear a list of identical phrases.

**How to fix it**

1. Replace generic phrases with what the reader gets: "See e-commerce prices" instead of "Click here".
2. Keep link text short (2–6 words) and different for each destination.

```html
<!-- before -->
<a href="/services">Click here</a>
<!-- after -->
<a href="/services">See all our services</a>
```

### Descriptive image file names

*Impact: low · Effort: easy*

A file name is one of the few clues search engines have about an image. IMG_4821.jpg says nothing; red-ceramic-vase.jpg helps it appear in image search.

**How to fix it**

1. Rename images before uploading: lowercase words separated by hyphens.
2. Describe what is in the picture, with your keyword where it fits.
3. Avoid spaces and Turkish characters in file names (c, s, g instead of ç, ş, ğ).

```text
IMG_4821.jpg   ->  red-ceramic-vase.jpg
DSC00093.png   ->  ankara-office-entrance.png
```

**Sources:** [SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide) · [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) · [Image SEO](https://developers.google.com/search/docs/appearance/google-images) · [Crawlable links](https://developers.google.com/search/docs/crawling-indexing/links-crawlable)

<a name="tech"></a>

## Technical

Whether search engines can fetch, index and understand the page: status codes, redirects, canonical, robots rules, sitemap, compression and server speed.

### HTTP status code

*Impact: high · Effort: moderate*

Only pages that answer with a 2xx code are indexed. Errors (4xx/5xx) drop the page from search and lose visitors.

**How to fix it**

1. Find out why the server answers this status code: a removed page, a server error or a firewall.
2. Restore the page or 301-redirect it to the closest working page.

### Redirect chain

*Impact: medium · Effort: easy*

Each extra redirect adds a round trip before the page starts loading, and Google stops following a chain after ten hops.

**How to fix it**

1. Point old addresses straight to the final URL in one 301.
2. Use the final URL (https, with or without www) in links, ads and the sitemap.

### Indexable

*Impact: high · Effort: easy*

A noindex instruction tells Google not to show the page at all. It is often left behind after a site goes live.

**How to fix it**

1. Remove "noindex" from the robots meta tag (and from the X-Robots-Tag header).
2. In WordPress, untick "Discourage search engines" under Settings › Reading.

```html
<meta name="robots" content="index, follow">
```

### Canonical tag

*Impact: medium · Effort: easy*

The same page is often reachable at several addresses (with parameters, with or without www). The canonical tag names the one that should rank.

**How to fix it**

1. Add a canonical link with the clean, final URL of the page.
2. Point it to the page itself unless it really is a copy of another page.

```html
<link rel="canonical" href="https://example.com/services/web-design">
```

### robots.txt reachable

*Impact: high · Effort: easy*

Google reads robots.txt before it crawls. A missing file (404) is fine: everything may be crawled. But if robots.txt answers with a server error or times out, Google stops crawling the whole site until it can read the file again.

**How to fix it**

1. Make /robots.txt return 200 with a text file, or a plain 404 if you do not need one.
2. If it errors, check the firewall, CDN or security plugin rules in front of it.

```text
User-agent: *
Allow: /
Disallow: /admin/

Sitemap: https://example.com/sitemap.xml
```

### XML sitemap

*Impact: medium · Effort: easy*

A sitemap lists every page you want indexed, so new and deep pages are found faster.

**How to fix it**

1. Generate /sitemap.xml (most CMSs and SEO plugins do this automatically).
2. Reference it in robots.txt and submit it in Google Search Console.

```html
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://example.com/</loc></url>
</urlset>
```

### Compression (gzip / Brotli)

*Impact: medium · Effort: easy*

Compression shrinks HTML, CSS and JavaScript by 60–80 %, so pages arrive faster, especially on mobile data.

**How to fix it**

1. Enable Brotli or gzip on the server or CDN (often one switch in the hosting panel).

```text
# .htaccess (Apache)
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/css application/javascript
</IfModule>
```

### Server response time

*Impact: high · Effort: moderate*

Nothing can appear on screen until the server answers. A slow first byte delays every other speed metric and Core Web Vitals.

**How to fix it**

1. Turn on page caching (or a CDN) so pages are not rebuilt for every visit.
2. Remove slow plugins and database queries; upgrade PHP to a current version.
3. Host close to your visitors (Europe for Türkiye and the UK).

### HTML size

*Impact: low · Effort: moderate*

A heavy HTML document (inlined images, huge menus, page builders) slows down parsing on phones.

**How to fix it**

1. Move inlined images and scripts to separate cached files.
2. Remove unused page-builder sections and duplicate menus.

### Lazy-loaded images

*Impact: low · Effort: easy*

On an image-heavy page, images below the first screen do not need to load before the visitor scrolls. Loading them later makes the first view appear sooner; the main image must still load first.

**How to fix it**

1. Add loading="lazy" to images below the first screen.
2. Never lazy-load the main hero image; it should load first.

```html
<img src="gallery-3.webp" alt="…" loading="lazy" width="800" height="600">
```

### Image dimensions

*Impact: medium · Effort: easy*

Without width and height the browser cannot reserve space, so the page jumps while images load (layout shift, a Core Web Vitals metric).

**How to fix it**

1. Add width and height attributes with the image's real proportions.
2. Keep CSS width:100%; height:auto so it still scales.

```html
<img src="hero.webp" alt="…" width="1600" height="900">
```

### HTTP to HTTPS redirect

*Impact: high · Effort: easy*

People and old links still arrive at http://. Without a permanent redirect that version stays open as a separate, insecure copy of your site and splits its ranking signals.

**How to fix it**

1. Redirect every http:// URL to the same https:// URL with a 301 (or 308).
2. Do it in one hop, without extra steps in between.
3. Keep 302 for temporary moves only.

```text
# .htaccess (Apache)
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

### www and non-www

*Impact: medium · Effort: easy*

example.com and www.example.com are two different addresses to Google. If both show the site, links and rankings are split between two copies.

**How to fix it**

1. Choose one version and 301-redirect the other to it.
2. Make sure the certificate covers both names.
3. Use the chosen version in canonical tags, the sitemap and internal links.

```text
# .htaccess: www.example.com -> example.com
RewriteEngine On
RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
RewriteRule ^ https://%1%{REQUEST_URI} [L,R=301]
```

### Real 404 for missing pages

*Impact: medium · Effort: easy*

When a missing page answers "200 OK", search engines index empty or duplicate pages (soft 404s) and waste crawl time, and visitors get no clear message.

**How to fix it**

1. Return status 404 (or 410 for removed content) for unknown URLs.
2. Show a helpful 404 page with search and links, but keep the 404 status.
3. Do not redirect every missing URL to the home page.

```text
# .htaccess
ErrorDocument 404 /404.php

<?php // 404.php: keep the status code
http_response_code(404);
```

### Clean URL structure

*Impact: low · Effort: moderate*

Short, readable, lowercase addresses are easier to share and to trust. Google says the words in a URL matter very little for ranking, but session IDs, mixed case and piles of parameters create duplicate addresses for the same page.

**How to fix it**

1. Use lowercase words separated by hyphens: /services/web-design.
2. Keep session ids and long parameter lists out of links you want indexed.
3. When you change a URL, 301-redirect the old one.

### Sitemap contents

*Impact: medium · Effort: easy*

A sitemap only helps if search engines can read it and it lists your real, current pages. Errors or other sites' URLs make Google ignore parts of it.

**How to fix it**

1. Validate the XML: one <url><loc> per page, absolute https URLs.
2. Add <lastmod> only where it is true: Google uses it when it is consistently accurate.
3. List only this site's indexable pages, and submit the sitemap in Search Console.

```html
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/services</loc>
    <lastmod>2026-10-01</lastmod>
  </url>
</urlset>
```

### robots.txt rules

*Impact: high · Effort: easy*

One wrong line in robots.txt can hide the whole site from Google, or stop it loading the CSS and JavaScript it needs to see pages the way visitors do.

**How to fix it**

1. Never leave "Disallow: /" on a live site.
2. Do not block theme, CSS or JavaScript folders.
3. Add a Sitemap: line with the full sitemap URL.

```text
User-agent: *
Disallow: /admin/
Allow: /

Sitemap: https://example.com/sitemap.xml
```

### Language alternates (hreflang)

*Impact: medium · Effort: easy*

hreflang tells Google which language version to show to whom. Invalid codes, a missing self-reference or duplicates can make it ignore the whole set, and the wrong language ranks.

**How to fix it**

1. Use ISO codes such as tr, en or en-GB, plus x-default for the fallback.
2. Every language version lists all versions, itself included.
3. Use absolute URLs and one entry per language code.

```html
<link rel="alternate" hreflang="tr" href="https://example.com/tr/">
<link rel="alternate" hreflang="en" href="https://example.com/">
<link rel="alternate" hreflang="x-default" href="https://example.com/">
```

### Meta refresh redirects

*Impact: low · Effort: easy*

A meta refresh reloads or forwards the page after a delay: visitors lose their place and the back button breaks. Google recommends a server-side 301 instead, and treats a delayed refresh only as a temporary redirect.

**How to fix it**

1. Replace it with a server-side 301 redirect.
2. For content that updates itself, refresh the data with JavaScript instead of reloading the page.

```html
<!-- remove this -->
<meta http-equiv="refresh" content="0; url=/new-page">
```

### Canonical details

*Impact: medium · Effort: easy*

A canonical that points to another page tells Google to index that page instead of this one. Two canonical tags, or a relative URL, can make Google ignore it.

**How to fix it**

1. Use exactly one canonical tag per page.
2. Use this page's absolute, preferred URL (https, your chosen host).
3. Point elsewhere only for true duplicates, such as print versions or filter pages.

```html
<link rel="canonical" href="https://example.com/services/web-design">
```

### Content without JavaScript

*Impact: high · Effort: hard*

Google runs JavaScript later and not always completely, and many AI crawlers do not run it at all. If the HTML is nearly empty until scripts run, your content may never be read.

**How to fix it**

1. Render the main content on the server (SSR) or pre-render it at build time.
2. At the very least, put the headline, intro text and key links in the HTML.
3. Check with "View page source": that is what crawlers get first.

**Sources:** [HTTP status codes and network errors](https://developers.google.com/search/docs/crawling-indexing/http-network-errors) · [Redirects](https://developers.google.com/search/docs/crawling-indexing/301-redirects) · [Canonical URLs](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) · [robots.txt](https://developers.google.com/search/docs/crawling-indexing/robots/intro) · [Blocking indexing with noindex](https://developers.google.com/search/docs/crawling-indexing/block-indexing) · [Building a sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) · [Localized versions (hreflang)](https://developers.google.com/search/docs/specialty/international/localized-versions) · [JavaScript SEO basics](https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics)

<a name="perf"></a>

## Performance

What makes a page load fast for real visitors.

### HTTP/2 or HTTP/3

*Impact: medium · Effort: easy*

HTTP/2 and HTTP/3 load many files over one connection at the same time; HTTP/1.1 queues them, which slows pages with many images and scripts.

**How to fix it**

1. Turn on HTTP/2 (and HTTP/3 if offered) in your hosting panel or CDN.
2. HTTP/2 needs HTTPS; most hosts switch it on together with the certificate.
3. A CDN such as Cloudflare provides it without any server changes.

### Number of files

*Impact: medium · Effort: moderate*

Every stylesheet, script and image is a separate download. Dozens of files slow the first view, especially on mobile networks.

**How to fix it**

1. Combine or remove the plugin CSS and JavaScript you do not use.
2. Lazy-load images below the fold.
3. Replace icon images with one SVG sprite.

### Render-blocking resources

*Impact: high · Effort: moderate*

The browser shows nothing until every stylesheet and synchronous script in <head> has downloaded. Each one delays the first paint.

**How to fix it**

1. Add defer to scripts in <head>, or move them to the end of <body>.
2. Merge small stylesheets and inline the critical CSS for the top of the page.
3. Load non-critical CSS (print styles, later sections) without blocking.

```html
<script src="/js/app.js" defer></script>
<link rel="stylesheet" href="/css/print.css" media="print">
```

### Browser caching

*Impact: medium · Effort: easy*

With long cache lifetimes, returning visitors load your CSS, JavaScript and images from their own device instead of downloading them again.

**How to fix it**

1. Send Cache-Control: max-age=31536000 for static files.
2. Put a version or hash in file names (app.3f9a.css) so updates still reach visitors.
3. Cache HTML briefly and assets for a long time.

```text
# .htaccess (Apache, mod_expires)
<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresByType text/css "access plus 1 year"
  ExpiresByType application/javascript "access plus 1 year"
  ExpiresByType image/webp "access plus 1 year"
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
</IfModule>
```

### Compressed CSS and JavaScript

*Impact: medium · Effort: easy*

Text files shrink by 70–80% with gzip or Brotli. Serving them uncompressed wastes bandwidth and slows every page view.

**How to fix it**

1. Enable Brotli or gzip for CSS and JavaScript on the server or CDN.
2. Check third-party files too, and host them yourself if their server does not compress.

```text
# .htaccess (Apache, mod_deflate)
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/css application/javascript application/json image/svg+xml
</IfModule>
```

### Modern image formats

*Impact: medium · Effort: easy*

WebP and AVIF are usually 25–50% smaller than JPEG and PNG at the same quality, which speeds up image-heavy pages.

**How to fix it**

1. Convert photos to WebP (or AVIF) when you upload them, or let your CMS or CDN do it.
2. Use <picture> with a JPEG fallback if you must support very old browsers.

```html
<picture>
  <source srcset="vase.avif" type="image/avif">
  <source srcset="vase.webp" type="image/webp">
  <img src="vase.jpg" width="800" height="600" alt="Handmade red ceramic vase">
</picture>
```

### Image file sizes

*Impact: high · Effort: easy*

A single 2 MB photo can take longer to load than the rest of the page. Large images are the most common reason for a slow Largest Contentful Paint.

**How to fix it**

1. Resize images to the size they are shown at (rarely wider than 1600 px).
2. Compress them: WebP at quality 75–85 looks the same and is far smaller.
3. Serve smaller versions to phones with srcset.

```html
<img src="hero-1200.webp"
     srcset="hero-800.webp 800w, hero-1200.webp 1200w, hero-1600.webp 1600w"
     sizes="(max-width: 800px) 100vw, 1200px"
     width="1200" height="600" alt="…">
```

### Web font loading

*Impact: low · Effort: easy*

Without font-display: swap, text stays invisible until the web font has downloaded, so on a slow connection visitors look at an empty page.

**How to fix it**

1. Add font-display: swap to every @font-face rule.
2. For Google Fonts, keep &display=swap in the URL.
3. Self-host and preload the one or two fonts used at the top of the page.

```text
@font-face {
  font-family: "Brand";
  src: url("/fonts/brand.woff2") format("woff2");
  font-display: swap;
}
```

### Page complexity (DOM size)

*Impact: medium · Effort: hard*

Thousands of HTML elements make the browser work harder on every scroll and tap, which slows interaction (INP) on mid-range phones.

**How to fix it**

1. Simplify page-builder layouts and remove nested wrapper elements.
2. Paginate long lists, and build mega menus only when they open.
3. Create tab and modal content when it is needed instead of shipping it all.

### Third-party scripts

*Impact: medium · Effort: moderate*

Every external widget, tracker and font host adds DNS lookups and code you do not control. Together they often cause slow, janky pages and privacy questions.

**How to fix it**

1. List what each one does and remove those nobody uses.
2. Load chat widgets and maps only when the visitor asks for them.
3. Self-host fonts and small libraries.

### Minified CSS and JavaScript

*Impact: low · Effort: easy*

Spaces, comments and long names help while coding, but in production they only add bytes.

**How to fix it**

1. Turn on minification in your build tool, CMS cache plugin or CDN.
2. Serve the .min version of libraries.

**Sources:** [Core Web Vitals](https://developers.google.com/search/docs/appearance/core-web-vitals) · [Web Vitals (web.dev)](https://web.dev/articles/vitals) · [Lazy loading and LCP (web.dev)](https://web.dev/articles/lcp-lazy-loading)

<a name="security"></a>

## Security

What keeps visitors safe and browsers free of warnings.

### HSTS (Strict-Transport-Security)

*Impact: low · Effort: easy*

HSTS makes browsers always use HTTPS for your site, so nobody can be pushed onto an insecure http:// connection on public Wi-Fi. It protects visitors; it is not a ranking factor by itself.

**How to fix it**

1. Once HTTPS works everywhere, send Strict-Transport-Security: max-age=31536000.
2. Add includeSubDomains only if every subdomain has HTTPS.

```text
# .htaccess (Apache, mod_headers)
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
```

### Security headers

*Impact: low · Effort: moderate*

Four response headers block common attacks on your visitors: a Content-Security-Policy limits which scripts may run, nosniff stops file-type guessing, frame protection prevents clickjacking and a referrer policy keeps URL details private. They are not ranking factors, but a hacked site gets a warning in Google results and loses its traffic.

**How to fix it**

1. Add the missing headers in your server or CDN settings; start the CSP in report-only mode.
2. Check the response headers in your browser's developer tools (Network tab).

```text
# .htaccess (Apache, mod_headers)
Header always set X-Content-Type-Options "nosniff"
Header always set X-Frame-Options "SAMEORIGIN"
Header always set Referrer-Policy "strict-origin-when-cross-origin"
Header always set Content-Security-Policy-Report-Only "default-src 'self'"
```

### Mixed content

*Impact: high · Effort: easy*

An HTTPS page that loads files over http:// is not fully secure. Browsers block insecure scripts and frames, which breaks the page, and flag insecure images.

**How to fix it**

1. Change every http:// resource link to https:// or a relative path.
2. After moving to HTTPS, search the database content for http:// links.
3. Add upgrade-insecure-requests to your CSP as a safety net.

```text
Header always set Content-Security-Policy "upgrade-insecure-requests"
```

### Certificate expiry

*Impact: high · Effort: easy*

When the certificate expires, every visitor gets a full-page security warning and most of them leave.

**How to fix it**

1. Turn on automatic renewal (Let's Encrypt renews every 60–90 days).
2. For a paid certificate, set a reminder two weeks before it expires.

**Sources:** [Page experience](https://developers.google.com/search/docs/appearance/page-experience)

<a name="mobile"></a>

## Mobile & accessibility

Mobile use and accessibility: what makes the page usable on a phone and with assistive technology.

### Zoom allowed

*Impact: medium · Effort: easy*

Blocking pinch-zoom (user-scalable=no, maximum-scale=1) locks out people with low vision, and it fails the WCAG accessibility guidelines.

**How to fix it**

1. Remove user-scalable=no and maximum-scale from the viewport tag.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### Form field labels

*Impact: medium · Effort: easy*

Screen readers announce a field by its label. Placeholder text disappears while typing and is not a label, and unlabeled forms lose leads.

**How to fix it**

1. Give every field a <label for="id">, or an aria-label if it really has no visible text.
2. Keep labels visible above the fields.

```html
<label for="email">Email</label>
<input id="email" name="email" type="email" autocomplete="email">
```

### Page landmarks

*Impact: low · Effort: easy*

<main>, <nav>, <header> and <footer> let screen-reader users jump straight to the content instead of listening to the whole menu first.

**How to fix it**

1. Wrap the main content in one <main> element.
2. Use <nav> for menus, and <header> and <footer> for the page frame.

```html
<header>…</header>
<nav>…</nav>
<main id="main">…</main>
<footer>…</footer>
```

### Buttons and links with names

*Impact: medium · Effort: easy*

An icon-only button, or an image link without alt, is announced as just "button" or "link". Nobody can tell what it does, and search engines get no anchor text.

**How to fix it**

1. Add visible text, or aria-label="…", to icon buttons such as menu, search and close.
2. Give images inside links an alt text that says where the link goes.

```html
<button type="button" aria-label="Open menu">
  <svg aria-hidden="true">…</svg>
</button>
```

### Meaningful alt texts

*Impact: low · Effort: easy*

An alt of "image" or a file name is as unhelpful as none: screen readers read it out, and image search learns nothing.

**How to fix it**

1. Describe what the image shows in a short sentence.
2. Use alt="" for purely decorative images.

```html
<img src="vase.webp" alt="Handmade red ceramic vase on a wooden table">
```

### Empty headings

*Impact: low · Effort: easy*

Empty <h1>–<h6> tags break the outline that screen readers and search engines use to understand the page structure.

**How to fix it**

1. Remove empty heading tags or put their text back; use CSS, not heading tags, for spacing and style.

### Valid language code

*Impact: low · Effort: easy*

A code such as lang="tr_TR" or lang="turkish" is not valid, so screen readers and browsers ignore it. Use tr, en, or a region form such as en-GB.

**How to fix it**

1. Use a BCP 47 code such as tr, en or en-GB (a hyphen, not an underscore).

```html
<html lang="tr">
```

**Sources:** [Mobile-first indexing](https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing) · [Decorative images (W3C)](https://www.w3.org/WAI/tutorials/images/decorative/)

<a name="social"></a>

## Social & schema

How the page looks when shared, and the structured data that describes it.

### Open Graph title and description

*Impact: low · Effort: easy*

When your link is shared on WhatsApp, LinkedIn or Facebook, these tags decide the preview text. Without them the preview looks broken.

**How to fix it**

1. Add og:title and og:description (they can match the title and description).

```html
<meta property="og:title" content="Corporate websites that bring in customers">
<meta property="og:description" content="Fast, mobile-first sites with a fixed quote.">
```

### Share image (og:image)

*Impact: low · Effort: easy*

Shared links with an image get far more clicks than plain text links.

**How to fix it**

1. Create a 1200×630 px image with your logo and message.
2. Reference it with an absolute https URL.

```html
<meta property="og:image" content="https://example.com/og.png">
```

### X (Twitter) card

*Impact: low · Effort: easy*

A twitter:card tag gives your links a large image preview on X.

**How to fix it**

1. Add twitter:card; X falls back to your Open Graph tags for the rest.

```html
<meta name="twitter:card" content="summary_large_image">
```

### Structured data (JSON-LD)

*Impact: medium · Effort: moderate*

Schema.org markup tells search engines and AI exactly what the page is: a company, a product, an article. It does not raise rankings by itself, but rich results such as review stars, prices and breadcrumbs need it.

**How to fix it**

1. Describe your organisation on the home page.
2. Add the type that fits each page: Product, Service, Article, LocalBusiness, BreadcrumbList.
3. Validate with the Rich Results Test.

```html
<script type="application/ld+json">
{"@context":"https://schema.org","@type":"Organization",
 "name":"Example Ltd","url":"https://example.com",
 "logo":"https://example.com/logo.png"}
</script>
```

### Organization schema

*Impact: medium · Effort: easy*

Organization or LocalBusiness markup on your home page ties your name, logo, address and profiles together; Google uses it for the logo and details it shows about you. One page is enough, usually the home page.

**How to fix it**

1. Add Organization (or LocalBusiness with address and opening hours).
2. List your social profiles in sameAs.

```json
{"@context":"https://schema.org","@type":"LocalBusiness","name":"Example",
 "address":{"@type":"PostalAddress","addressLocality":"Ankara"},
 "sameAs":["https://www.linkedin.com/company/example"]}
```

### Breadcrumb schema

*Impact: low · Effort: easy*

BreadcrumbList lets Google show the page's place in your site ("Home › Services › Web design") in desktop results instead of a long URL, and states your site structure plainly.

**How to fix it**

1. Add BreadcrumbList markup to inner pages that have a visible breadcrumb.

```json
{"@context":"https://schema.org","@type":"BreadcrumbList","itemListElement":[
 {"@type":"ListItem","position":1,"name":"Home","item":"https://example.com/"},
 {"@type":"ListItem","position":2,"name":"Services","item":"https://example.com/services"}]}
```

### Share image works

*Impact: medium · Effort: easy*

If the og:image is broken or badly shaped, links to your site are shared as a plain grey box or a cropped picture, and get far fewer clicks.

**How to fix it**

1. Use a 1200×630 px JPEG or PNG under 5 MB.
2. Use an absolute https URL that opens without a login.
3. Test it with LinkedIn's Post Inspector or Facebook's Sharing Debugger.

### Valid JSON-LD

*Impact: medium · Effort: easy*

One misplaced comma makes a JSON-LD block unreadable, and Google silently drops all the structured data in it.

**How to fix it**

1. Paste the block into the Schema Markup Validator (validator.schema.org) and fix the errors.
2. Generate JSON-LD in code (for example json_encode in PHP) instead of writing it by hand.

```html
<script type="application/ld+json">
<?= json_encode($schema, JSON_UNESCAPED_UNICODE | JSON_UNESCAPED_SLASHES) ?>
</script>
```

### Structured data fields

*Impact: medium · Effort: moderate*

Rich results (review stars, prices, events, breadcrumbs) only appear when the required properties are filled in; the recommended ones make them richer.

**How to fix it**

1. Add the missing properties listed here to your JSON-LD.
2. Check the result in Google's Rich Results Test.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Ardena",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png"
}
</script>
```

### Site name in search results

*Impact: low · Effort: easy*

Google shows a site name above your result. It reads it from WebSite structured data or og:site_name; without them it guesses or shows the bare domain.

**How to fix it**

1. Add WebSite JSON-LD with your brand name to the home page.
2. Add og:site_name to every page.

```html
<script type="application/ld+json">
{"@context": "https://schema.org", "@type": "WebSite", "name": "Ardena", "url": "https://example.com/"}
</script>
```

### Links to your profiles

*Impact: low · Effort: easy*

Linking your official social profiles, and listing them in sameAs, helps Google and AI assistants connect your site with your brand everywhere else.

**How to fix it**

1. Link your profiles from the footer.
2. List the same URLs in sameAs in your Organization schema.

```text
"sameAs": [
  "https://www.linkedin.com/company/your-company",
  "https://www.instagram.com/your-company"
]
```

**Sources:** [Structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) · [Organization markup](https://developers.google.com/search/docs/appearance/structured-data/organization) · [Site names](https://developers.google.com/search/docs/appearance/site-names) · [Breadcrumbs](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb) · [The Open Graph protocol](https://ogp.me/)

<a name="local"></a>

## Local SEO

For businesses that serve customers at a place or in an area. Not relevant to every page.

### Phone number

*Impact: medium · Effort: easy*

For a local business the phone call is often the conversion itself. A tap-to-call link turns calling into one tap, and the number confirms your listing details to Google.

**How to fix it**

1. Show the number in the header or footer as a tel: link.
2. Use the same number as on your Google Business Profile.

```html
<a href="tel:+902120000000">+90 212 000 00 00</a>
```

### Address

*Impact: medium · Effort: easy*

A visible address that matches your Google Business Profile and directories (name, address, phone: NAP) lets customers find you and keeps your business details consistent across the web.

**How to fix it**

1. Put the full address in the footer or the contact section, written the same way everywhere.
2. Mark it up with <address>, and with PostalAddress in JSON-LD.

```html
<address>Ardena, Atatürk Cad. No: 12, 06100 Çankaya/Ankara</address>
```

### LocalBusiness schema

*Impact: medium · Effort: easy*

LocalBusiness JSON-LD (or a subtype such as Dentist or Restaurant) states your address, phone and hours in a form that Google and AI assistants can trust and show.

**How to fix it**

1. Add LocalBusiness, using the most specific subtype, with name, address, telephone, openingHoursSpecification and geo.
2. Use exactly the details shown on your Google Business Profile.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Dentist",
  "name": "Ardena Dental",
  "telephone": "+90 212 000 00 00",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Atatürk Cad. No: 12",
    "addressLocality": "Ankara",
    "postalCode": "06100",
    "addressCountry": "TR"
  },
  "openingHoursSpecification": [{
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
    "opens": "09:00", "closes": "18:00"
  }]
}
</script>
```

### Map

*Impact: low · Effort: easy*

A map, or a link to your Google Maps listing, helps visitors plan the visit and find the right entrance.

**How to fix it**

1. Embed your Google Maps location on the contact page; load it on click to keep the page fast.
2. Or link to your Maps profile (maps.app.goo.gl/…).

### Opening hours

*Impact: low · Effort: easy*

People search for "open now". Hours on the site and in your schema cut wasted trips and calls, and they must match your Google profile.

**How to fix it**

1. List your hours on the contact page.
2. Add openingHoursSpecification to your LocalBusiness schema.

### Contact page link

*Impact: low · Effort: easy*

A clear contact link on every page is a trust signal for visitors and for Google's quality raters, and the shortest path to a lead.

**How to fix it**

1. Link "Contact" from the main menu and the footer.

**Sources:** [Local business markup](https://developers.google.com/search/docs/appearance/structured-data/local-business)

<a name="vitals"></a>

## Core Web Vitals

Google's Core Web Vitals and PageSpeed scores, measured with Google PageSpeed Insights.

### Mobile speed score (Google)

*Impact: high · Effort: moderate*

Google's Lighthouse score on a simulated mid-range phone sums up how fast the page loads and becomes usable. Most of your visitors are on phones.

**How to fix it**

1. Start with the biggest items in this report's speed opportunities list.
2. Compress and resize images, defer scripts and remove unused plugins.
3. Test again after each change; the score moves a few points between runs.

### Largest Contentful Paint (LCP)

*Impact: high · Effort: moderate*

LCP is the moment the main image or headline appears. Above 2.5 seconds visitors feel the page is slow, and it is one of Google's three Core Web Vitals.

**How to fix it**

1. Make the hero image small (WebP or AVIF at the right size) and give it fetchpriority="high".
2. Never lazy-load the main image at the top.
3. Speed up the server response with caching, better hosting or a CDN.

```html
<img src="hero.webp" width="1200" height="600" fetchpriority="high" alt="…">
```

### Responsiveness (INP)

*Impact: high · Effort: hard*

INP measures how quickly the page reacts to taps and clicks. Above 200 ms buttons feel sticky, and it is a Core Web Vital. Without real-user data the lab measure TBT stands in for it.

**How to fix it**

1. Cut heavy JavaScript: unused libraries, sliders and chat widgets that load at start-up.
2. Split long tasks, and load third-party scripts after the page is usable.

### Layout shift (CLS)

*Impact: medium · Effort: moderate*

CLS measures how much the page jumps around while it loads. Moving buttons cause mis-taps and look careless, and it is a Core Web Vital.

**How to fix it**

1. Give images and videos width and height attributes.
2. Reserve space for ads, embeds and cookie banners.
3. Use font-display: swap with a similar fallback font.

```html
<img src="team.webp" width="800" height="533" alt="…">
.embed { aspect-ratio: 16 / 9; }
```

### Desktop speed score (Google)

*Impact: medium · Effort: moderate*

The same Lighthouse test on a desktop connection. A low desktop score usually means heavy scripts or a slow server rather than the network.

**How to fix it**

1. Work through the speed opportunities list in this report.
2. Check the server response time and page caching.

**Sources:** [Core Web Vitals](https://developers.google.com/search/docs/appearance/core-web-vitals) · [Web Vitals (web.dev)](https://web.dev/articles/vitals)

<a name="links"></a>

## Links

Whether the links and images on the page work.

### Broken links

*Impact: high · Effort: easy*

Links to missing pages waste visitors' time, chip away at trust and waste the crawl budget Google spends on your site.

**How to fix it**

1. Fix or remove each link listed in this report.
2. When you delete a page, 301-redirect its URL to the closest replacement.

### Broken images

*Impact: medium · Effort: easy*

Missing images show empty boxes or broken icons and make a site look abandoned.

**How to fix it**

1. Upload the missing files again, or remove the references listed in this report.

### Links through redirects

*Impact: low · Effort: easy*

Internal links that pass through a redirect add a delay to every click and extra work for crawlers. Link straight to the final address.

**How to fix it**

1. Point internal links straight at the final URL; the cause is often a missing trailing slash or an old http:// link.

**Sources:** [Crawlable links](https://developers.google.com/search/docs/crawling-indexing/links-crawlable) · [HTTP status codes](https://developers.google.com/search/docs/crawling-indexing/http-network-errors)

<a name="site"></a>

## Site crawl

Checks that need the whole site crawled, page by page.

### Pages with errors

*Impact: high · Effort: moderate*

Pages that return 4xx or 5xx errors drop out of search results and frustrate visitors who arrive from your own menus.

**How to fix it**

1. Fix or remove the pages marked in the crawl table.
2. Server errors (5xx) usually mean a broken plugin or database connection: check the error log.

### Duplicate titles

*Impact: medium · Effort: easy*

When several pages share one title Google cannot tell which to show, often rewrites them, and the pages compete with each other.

**How to fix it**

1. Write a unique title for each page in the list.
2. In a CMS, build titles from the page name plus the brand, not from a fixed text.

### Duplicate descriptions

*Impact: low · Effort: easy*

The same meta description on many pages makes your results look identical in search, so people cannot see why to pick one.

**How to fix it**

1. Write a description for each important page that says what is special about it.
2. Leave the description empty rather than repeating a sitewide one.

### Pages without a title

*Impact: high · Effort: easy*

A page without a title shows its address, or a guess, in search results and almost never gets clicked.

**How to fix it**

1. Add a title of 30–65 characters to each page listed.

### Pages without a description

*Impact: medium · Effort: easy*

Without a meta description Google picks random text from the page for the snippet, which rarely sells it.

**How to fix it**

1. Write a 70–165 character description for the important pages listed.

### Pages without an H1

*Impact: medium · Effort: easy*

The H1 is the page's main heading for visitors and search engines; without it the topic of the page is less clear.

**How to fix it**

1. Give each page listed one H1 that states its topic.

### Pages with almost no text

*Impact: medium · Effort: moderate*

Google has no minimum word count, but pages with almost no text (empty categories, tag pages, placeholders) rarely help anyone, and many of them can weigh on how Google sees the whole site.

**How to fix it**

1. Expand the important ones with useful detail: questions customers ask, prices, examples.
2. Merge or noindex the pages that will never be useful in search.

### noindex pages

*Impact: high · Effort: easy*

A noindex tag removes a page from Google. That is right for thank-you pages, but a stray noindex on a service page silently costs traffic.

**How to fix it**

1. Check each page in the list and remove noindex from those that should rank.
2. Take noindex pages out of the sitemap.

### Sitemap coverage

*Impact: medium · Effort: easy*

Pages missing from the sitemap are found later, and sitemap URLs that redirect or fail send Google on a detour.

**How to fix it**

1. Add the indexable pages found in the crawl to the sitemap.
2. Remove URLs that redirect, fail or are noindex.

### Pages without internal links

*Impact: medium · Effort: easy*

These pages are in your sitemap, but no crawled page links to them. Google finds pages mainly through links, so orphan pages are discovered late, crawled rarely and get no internal link value; visitors cannot reach them at all.

**How to fix it**

1. Link each listed page from a relevant page: a menu, a category or a related article.
2. If a page is no longer needed, remove it from the sitemap or redirect it.

### Slow pages

*Impact: medium · Effort: moderate*

A slow server response on some pages usually points to heavy database queries or missing caching on those templates.

**How to fix it**

1. Turn on page caching for these templates.
2. Look for slow plugins or queries on the pages listed.

### Click depth

*Impact: low · Effort: moderate*

Pages more than three clicks away from the home page are crawled less often and receive less internal link value.

**How to fix it**

1. Link important pages from the menu, the footer or hub pages.
2. Add related-content links between pages.

### Alt texts across the site

*Impact: medium · Effort: easy*

Images without alt text are invisible to image search and to screen-reader users on every page they appear on.

**How to fix it**

1. Add alt text to the images on the pages listed; use alt="" for decoration.

**Sources:** [Building a sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) · [Canonical URLs](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) · [Blocking indexing with noindex](https://developers.google.com/search/docs/crawling-indexing/block-indexing)

---

Generated from the audit guide of the [irodev.net](https://irodev.net) tools on 2026-10-23. Licensed under [CC BY 4.0](LICENSE).

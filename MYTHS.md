# SEO and AI-search myths

**English** · [Türkçe](MYTHS.tr.md)

Things many audit tools count as problems, but that the search engines' own documentation doesn't support. We
leave them out of our audits, and here is why, with the source for each.

### 1. "Aim for a keyword density of 2–3%"

There is no target density. Google's spam policies treat *keyword stuffing* as spam, and its SEO Starter Guide
says the same. Write naturally and use the words your customers use.
Sources: [Spam policies](https://developers.google.com/search/docs/essentials/spam-policies) ·
[SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 2. "A page needs at least 300 (or 1,500) words"

Google's SEO Starter Guide says the length of the content alone doesn't matter for ranking, and that there is no
word-count target, minimum or maximum. Our audit only flags pages with almost no text, because visitors have
nothing to read there.
Source: [SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 3. "Exactly one H1, at least two H2s, in strict order"

The same guide says headings in semantic order help screen readers, but for Google Search it doesn't matter if
they are out of order. Nothing in Google's documentation requires a single H1. We only warn when a page has no main
heading at all, because it's harder to scan.
Source: [SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 4. "Fill in the meta keywords tag"

Google's SEO Starter Guide states that Google Search doesn't use the keywords meta tag.
Source: [SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 5. "Put the keyword in the first 100 words" and "improve your text-to-HTML ratio"

Neither appears anywhere in Google's documentation. Make the opening answer the reader's question instead, which
helps people and AI answers alike.

### 6. "The lang attribute tells Google your page's language"

Google says it works out a page's language from its visible content and doesn't use code-level information such as
lang attributes or the URL. Keep a correct `lang` anyway: screen readers need it to pronounce the page. That is why our audit
checks it, as an accessibility point.
Source: [Managing multi-regional and multilingual sites](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)

### 7. "Titles must be under 60 characters"

Google says there is no limit on the length of a `<title>` element; the title link is cut as needed, usually to fit
the device's width. Truncation goes by width, not by a character count. Our
audit suggests 30–65 characters as a practical range, not as a rule.
Source: [Title links](https://developers.google.com/search/docs/appearance/title-link)

### 8. "Add FAQ markup to get rich results"

Since August 2023, Google shows FAQ rich results only for well-known, authoritative government and health sites.
FAQ markup won't add them for a business site.
Source: [Changes to HowTo and FAQ rich results](https://developers.google.com/search/blog/2023/08/howto-faq-changes)

### 9. "The home page needs breadcrumb markup"

A breadcrumb trail shows where a page sits in a site. The home page is where every trail starts, so it has nothing to
show. Breadcrumbs belong on inner pages.
Source: [Breadcrumb structured data](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb)

### 10. "An empty alt attribute is a missing alt text"

For purely decorative images, `alt=""` is the correct markup: it tells screen readers to skip the image. Only
images that carry meaning need a description.
Source: [W3C: Decorative images](https://www.w3.org/WAI/tutorials/images/decorative/)

### 11. "Every site needs hreflang"

hreflang tells Google about *localized versions* of a page. A site in one language has none to declare.
Source: [Localized versions of your pages](https://developers.google.com/search/docs/specialty/international/localized-versions)

### 12. "Lazy-load every image"

Lazy-loading the main image at the top of the page delays it and hurts Largest Contentful Paint. Lazy-load images
further down the page, never the one that is visible on arrival.
Source: [web.dev: Lazy loading and LCP](https://web.dev/articles/lcp-lazy-loading)

### 13. "Every page needs a video"

No search engine documents video as a requirement. Add a video when it helps the visitor, a product demo for
example, and describe it with `VideoObject` markup. Don't add one to tick a box.

### 14. "`<lastmod>` is required in a sitemap"

In the sitemaps protocol, `<lastmod>` is optional. When you use it, keep it accurate: change it only when the page's
content changes.
Source: [sitemaps.org protocol](https://www.sitemaps.org/protocol.html)

### 15. "HTTP/2 and security headers are ranking factors"

Google documents neither as a ranking factor. They make pages faster and safer, which is reason enough, and HTTPS is
part of page experience. Our audit checks them for those reasons and says so.
Source: [Page experience](https://developers.google.com/search/docs/appearance/page-experience)

### 16. "You need llms.txt (or special files) to appear in AI answers"

Google says you don't need new machine-readable files, AI text files or special markup to appear in its AI
features. No major engine documents reading llms.txt. It is a courtesy for AI tools that look for it, which is why our AI
visibility test reports it but doesn't count a missing file against you.
Sources: [AI features and your website](https://developers.google.com/search/docs/appearance/ai-features) ·
[The llms.txt proposal](https://llmstxt.org/)

### 17. "Block GPTBot and ChatGPT can't find you" (or "allow GPTBot to appear in ChatGPT")

OpenAI runs separate crawlers: OAI-SearchBot for search, GPTBot for model training. It says each setting is
independent, so you can allow search and refuse training. The same split exists at Anthropic, Apple, Google
(Google-Extended) and others. Our AI visibility test scores only the search crawlers.
Source: [OpenAI crawlers](https://platform.openai.com/docs/bots)

---

Found a myth we missed, or a source that changed? [Open an issue](https://github.com/irodevltd/seo-criteria/issues).
Licensed under [CC BY 4.0](LICENSE).

# AI visibility criteria

**English** · [Türkçe](AI-VISIBILITY.tr.md)

The 46 checks of the irodev.net AI visibility test: can ChatGPT, Gemini, Perplexity, Claude, Copilot and Google's AI features reach, read, understand and quote a page? Each criterion comes from the engines' own documentation or a named study, listed under each group. None of them guarantees being cited: they remove the obstacles.

Training crawlers (GPTBot, ClaudeBot, CCBot and others) are listed in the test but never scored: whether your pages may train future models is your choice and doesn't hide you from AI search. Run the checks on your own page with the [free AI visibility test](https://irodev.net/geo-ai-gorunurluk).

- [AI access](#access) (15)
- [Entity & structured data](#entity) (8)
- [Citability](#content) (14)
- [Trust](#trust) (3)
- [Site-wide readiness](#site) (6)

<a name="access"></a>

## AI access

Can AI search and answer engines reach and read the page at all: robots.txt rules per crawler, firewalls, indexing and quoting directives, text without JavaScript.

### robots.txt answers

*Impact: high · Effort: easy*

Every well-behaved crawler asks for /robots.txt before anything else. The robots.txt standard (RFC 9309) says that if the file can't be reached because of a server error, crawlers must assume nothing may be crawled. A missing file (404) is fine: it means everything may be crawled.

**How to fix it**

1. Make /robots.txt answer quickly with 200 (or 404 if you don't need one), never with a 5xx error.
2. Make sure your firewall or CDN doesn't rate-limit or challenge requests for it.

### ChatGPT search (OAI-SearchBot)

*Impact: high · Effort: easy*

OpenAI uses OAI-SearchBot to show websites in ChatGPT's search results and recommends allowing it to appear there. It is separate from GPTBot, which only collects training data, so you can keep training out and still be found.

**How to fix it**

1. Allow OAI-SearchBot in robots.txt. OpenAI says changes take about 24 hours to reach ChatGPT search.
2. If a firewall or CDN sits in front of the site, also allow the IP ranges OpenAI publishes.

```text
User-agent: OAI-SearchBot
Allow: /

# optional: keep model training out
User-agent: GPTBot
Disallow: /
```

### Perplexity (PerplexityBot)

*Impact: high · Effort: easy*

Perplexity uses PerplexityBot to show and link websites in its search results, and says it isn't used to train AI models. Perplexity lists its sources under every answer, so blocking the bot removes you from that list.

**How to fix it**

1. Allow PerplexityBot in robots.txt.
2. If a firewall or CDN sits in front of the site, allow Perplexity's published IP ranges too.

```text
User-agent: PerplexityBot
Allow: /
```

### Claude search (Claude-SearchBot)

*Impact: medium · Effort: easy*

Anthropic's Claude-SearchBot crawls the web to improve Claude's search results; Anthropic says blocking it may reduce your visibility and accuracy in them. ClaudeBot is a different crawler that only collects training data.

**How to fix it**

1. Allow Claude-SearchBot in robots.txt (you can still disallow ClaudeBot if you don't want your pages used for training).

```text
User-agent: Claude-SearchBot
Allow: /
```

### Google AI Overviews and AI Mode (Googlebot)

*Impact: high · Effort: easy*

AI Overviews and AI Mode are part of Google Search. Google says a page can appear as a source when Googlebot may crawl it and it's indexed and eligible for a snippet; there is no separate AI crawler to allow and no special file or markup to add.

**How to fix it**

1. Remove the robots.txt rule that blocks Googlebot from this page.
2. Check the page in Google Search Console (URL inspection).

```text
User-agent: Googlebot
Allow: /
```

### Microsoft Copilot (Bingbot)

*Impact: high · Effort: easy*

Copilot grounds its answers in Bing's index, which Bingbot builds. If Bingbot may not crawl a page, Bing can use it neither in search nor in Copilot answers.

**How to fix it**

1. Allow Bingbot in robots.txt.
2. Verify the site in Bing Webmaster Tools: it shows how your pages are indexed and how often Copilot cites them.

```text
User-agent: Bingbot
Allow: /
```

### Firewall lets AI crawlers in

*Impact: high · Effort: moderate*

robots.txt is only half of access: a CDN or firewall can turn crawlers away before they reach the page. Google lists crawling allowed "by any CDN or hosting infrastructure" among its best practices for AI features, and OpenAI asks sites to allow its IP ranges. We requested this page with the user agents of OpenAI's, Perplexity's and Anthropic's search crawlers.

**How to fix it**

1. Open the bot settings of your CDN or firewall (for example Cloudflare's AI crawler controls) and allow the search crawlers you want.
2. Allow them by the IP ranges each vendor publishes, not by user agent alone: anyone can fake a user agent.

### The page can be indexed

*Impact: high · Effort: easy*

AI Overviews, AI Mode and Copilot pick their sources from a search index. A page with noindex (in a meta tag or the X-Robots-Tag header), or one that answers with an error, isn't in the index and can't be cited.

**How to fix it**

1. Remove noindex from pages you want found (check SEO plugin settings and server headers).
2. Make the page answer with 200.

### AI answers may quote the text

*Impact: high · Effort: easy*

Google applies its snippet controls to AI Overviews and AI Mode: nosnippet or max-snippet:0 stops it from showing your text. Bing says NOARCHIVE keeps a page out of Copilot answers and NOCACHE limits Copilot to the URL, title and snippet.

**How to fix it**

1. Remove nosnippet, max-snippet:0 and noarchive unless you mean to stay out of AI answers.
2. To hide one part only (a price table, a disclaimer), wrap it in data-nosnippet instead.

```html
<!-- keep one part out of snippets, not the whole page -->
<div data-nosnippet>…</div>
```

### Text without JavaScript

*Impact: high · Effort: hard*

A 2024 study by Vercel and MERJ found that the major AI crawlers (OpenAI's, Anthropic's, Perplexity's and others) don't run JavaScript; Google's and Apple's do. If your text only appears after scripts run, those crawlers see an empty page.

**How to fix it**

1. Render the page on the server (SSR) or generate it ahead of time (static or pre-rendered pages).
2. Check by viewing the page source (not the inspector): the text should be there.

### Gemini apps (Google-Extended)

*Impact: medium · Effort: easy*

Google-Extended is a robots.txt token, not a crawler. It decides whether Google may use your pages to train Gemini and to ground answers in the Gemini apps; Google says it doesn't affect Google Search or rankings. Blocking it is a fair choice if you object to training, but it also keeps you out of Gemini app answers.

**How to fix it**

1. Decide deliberately: remove the Google-Extended block if appearing in Gemini apps matters more to you than staying out of training.

```text
User-agent: Google-Extended
Allow: /
```

### Siri and Spotlight (Applebot)

*Impact: low · Effort: easy*

Applebot powers search in Siri, Spotlight and Safari. Apple says pages that block Applebot-Extended, its training token, can still appear in those results. When robots.txt has no Applebot rules, Applebot follows your Googlebot rules.

**How to fix it**

1. Allow Applebot; block Applebot-Extended instead if you only want to keep training out.

```text
User-agent: Applebot
Allow: /

# optional: keep Apple model training out
User-agent: Applebot-Extended
Disallow: /
```

### DuckDuckGo AI answers (DuckAssistBot)

*Impact: low · Effort: easy*

DuckAssistBot fetches pages in real time for DuckDuckGo's AI-assisted answers, which cite their sources. DuckDuckGo says the data isn't used to train AI models and that blocking the bot doesn't affect organic rankings.

**How to fix it**

1. Allow DuckAssistBot in robots.txt.

```text
User-agent: DuckAssistBot
Allow: /
```

### Sitemap with update dates (Bing, Copilot)

*Impact: medium · Effort: easy*

Bing calls the sitemap's lastmod date a key signal in AI-powered search: it decides which pages to re-read, so Copilot doesn't answer from an old version. The date has to be honest: change it only when the content changes. IndexNow can tell Bing the moment a page changes.

**How to fix it**

1. Publish an XML sitemap and declare it in robots.txt.
2. Give each URL a lastmod in ISO 8601 with the time, updated only when the content changes.
3. Optionally add IndexNow (most SEO plugins and CDNs offer it).

```html
<url>
  <loc>https://example.com/services</loc>
  <lastmod>2026-10-21T09:30:00+03:00</lastmod>
</url>
```

### llms.txt (optional)

*Impact: low · Effort: easy*

llms.txt is a proposed Markdown summary of a site for AI tools. No major AI search engine has said it reads one, and Google says no special AI text files are needed for AI Overviews. It does no harm and some AI assistants and coding tools read it, so we only check the format when you have one: a # title and links to your key pages.

**How to fix it**

1. If you keep one, start with "# Name", add a one-line summary and link your key pages in Markdown.

```text
# Example Ltd
> Corporate web design studio in Ankara.

## Services
- [Web design](https://example.com/web-design): sites for small firms
```

**Sources:** [Google: AI features and your website](https://developers.google.com/search/docs/appearance/ai-features) · [Google common crawlers (incl. Google-Extended)](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers) · [OpenAI crawlers](https://platform.openai.com/docs/bots) · [Perplexity crawlers](https://docs.perplexity.ai/guides/bots) · [Anthropic crawlers](https://support.claude.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler) · [Applebot](https://support.apple.com/en-us/119829) · [DuckAssistBot](https://duckduckgo.com/duckduckgo-help-pages/results/duckassistbot) · [Bing Webmaster Guidelines](https://www.bing.com/webmasters/help/webmaster-guidelines-30fba23a) · [Robots meta tag (nosnippet, max-snippet)](https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag) · [The llms.txt proposal](https://llmstxt.org/)

<a name="entity"></a>

## Entity & structured data

Whether engines can tell who is behind the site: structured data, organization details, links to official profiles, one consistent name.

### Structured data (JSON-LD)

*Impact: medium · Effort: moderate*

Structured data states facts so machines don't have to guess: who you are, what you offer, what a page is about. Google says no special markup is needed for AI Overviews, but it does use structured data to understand pages and the entities in them, and Microsoft says schema helps label content as a product, review, FAQ or event.

**How to fix it**

1. Add JSON-LD for what the page really is: Organization or LocalBusiness on the home page, Product, Service, Article or FAQPage where they fit.
2. Test it with Google's Rich Results Test or the Schema Markup Validator.

```html
<script type="application/ld+json">
{"@context":"https://schema.org","@type":"Organization","name":"Example Ltd","url":"https://example.com/","logo":"https://example.com/logo.png"}
</script>
```

### Organization markup

*Impact: high · Effort: easy*

Organization or LocalBusiness markup on the home page states your official name, logo, address and profiles. Google uses it to understand your organization and tell it apart from others; it's how an engine knows which of two similar names is you.

**How to fix it**

1. Add Organization (or the closest LocalBusiness type) to the home page with name, url, logo and sameAs.

```json
{"@context":"https://schema.org","@type":"Organization","name":"Example Ltd","url":"https://example.com/",
 "logo":"https://example.com/logo.png","sameAs":["https://www.linkedin.com/company/example"]}
```

### Linked profiles (sameAs)

*Impact: medium · Effort: easy*

sameAs lists other pages about you: LinkedIn, Wikipedia or Wikidata, social profiles, business directories. Google's Organization documentation recommends it; it joins up what engines find about you elsewhere.

**How to fix it**

1. Add the URLs of your official profiles to sameAs in the Organization markup.

```text
"sameAs": ["https://www.linkedin.com/company/example", "https://www.instagram.com/example"]
```

### Organization details

*Impact: medium · Effort: easy*

Google's Organization and LocalBusiness documentation recommends name, url and logo, and address and telephone for local businesses. These are the facts AI answers repeat when someone asks about you, so they should come from you.

**How to fix it**

1. Fill in the missing properties in your Organization or LocalBusiness markup.

### Structured data matches the page

*Impact: medium · Effort: easy*

Google's best practices for AI features include making sure structured data matches the visible text, and its general guidelines forbid marking up content visitors can't see. Markup that names things the page doesn't show looks unreliable.

**How to fix it**

1. Make each name and headline in the markup appear on the page as written, or correct the markup.

### Wikidata entry

*Impact: low · Effort: moderate*

Wikidata is the open knowledge base behind many knowledge panels and AI datasets. An item whose official website is your domain ties your name to your site in a source engines trust. Create one only if your organization meets Wikidata's notability policy; promotional items get deleted.

**How to fix it**

1. If you qualify, create an item with "official website" (P856) set to your domain and add independent references.
2. Then add the item's URL to sameAs in your Organization markup.

### Site name (WebSite markup)

*Impact: low · Effort: easy*

WebSite markup or og:site_name on the home page states the name of the site. Google uses it for the site name in results; engines need it to name you when they cite the site.

**How to fix it**

1. Add WebSite markup with your name to the home page.

```json
{"@context":"https://schema.org","@type":"WebSite","name":"Example","url":"https://example.com/"}
```

### One brand name everywhere

*Impact: medium · Effort: easy*

Bing's guidelines ask for consistent entity names. If the markup, the site name and the page use different names, engines may treat them as different businesses or pick the wrong one.

**How to fix it**

1. Use the same name in the Organization markup, og:site_name, the title and the page text (legal suffixes like Ltd may differ).

**Sources:** [Organization markup](https://developers.google.com/search/docs/appearance/structured-data/organization) · [Site names](https://developers.google.com/search/docs/appearance/site-names) · [Structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data)

<a name="content"></a>

## Citability

Whether the text is easy to quote: questions with direct answers, clear structure, figures, quotations and sources.

### Main heading (H1)

*Impact: medium · Effort: easy*

Microsoft's guidance for AI answers says the H1 should match or closely reflect the page title. It is the first statement of what the page is about.

**How to fix it**

1. Give the page one clear H1 that says what it offers, in the words of the title.

```html
<h1>Corporate web design in Ankara</h1>
```

### Key information near the top

*Impact: medium · Effort: easy*

Bing's guidelines for AI answers ask for the key information near the top of the page. Open with a sentence or two that says what this is, for whom and where: a summary an engine can use on its own.

**How to fix it**

1. Put a short paragraph (two sentences, plain words, with your service and place) right under the H1.

```html
<h1>Corporate web design in Ankara</h1>
<p>We design and build fast, bilingual websites for small firms in Ankara, from a first sketch to launch in four weeks.</p>
```

### Questions as headings

*Impact: medium · Effort: easy*

Microsoft points out that questions with clear answers match the way people ask AI assistants. A heading phrased as the question a customer would ask, with the answer under it, is a passage that fits that question.

**How to fix it**

1. Turn some headings into the questions customers really ask ("How long does a website take?").
2. Answer each one in the first sentence under it.

### Sections with subheadings

*Impact: medium · Effort: easy*

AI assistants split pages into smaller pieces and judge each one; Microsoft says H2 and H3 headings define those pieces, and that lists and tables work well for steps and comparisons. A long page without subheadings is one block that's hard to quote from.

**How to fix it**

1. Split the text into sections with descriptive H2 and H3 headings.
2. Use a list for steps and a table for comparisons.

### Enough text to cite

*Impact: high · Effort: moderate*

An engine can only cite what's written on the page, and Google's AI-features guidance stresses text content. There's no magic word count: near-empty pages are the problem, because they give an answer nothing to quote.

**How to fix it**

1. Write the facts a customer needs on the page itself: what, for whom, where, how much, how long.

### Short answers right after questions

*Impact: medium · Effort: easy*

Microsoft recommends one- to two-sentence answers right under the question, in sentences that still make sense when quoted on their own. We look for 8 to 80 words, or a list, right after each question heading.

**How to fix it**

1. Start each answer with the direct answer ("Usually four weeks."), then add the detail.

### No walls of text

*Impact: low · Effort: easy*

Microsoft lists long walls of text among the mistakes that keep content out of AI answers. A paragraph over 150 words packs several points together; split it so each paragraph makes one point.

**How to fix it**

1. Break long paragraphs up: one point per paragraph, a list where you enumerate.

### Images described in text

*Impact: low · Effort: easy*

Microsoft warns against putting key information only in images: give each image alt text and keep important facts in the HTML text. Alt text is also an accessibility requirement.

**How to fix it**

1. Add an alt attribute to every image (alt="" for purely decorative ones).
2. Never put prices, opening hours or other facts only inside an image.

### Specific numbers

*Impact: medium · Effort: easy*

In the 2024 GEO study (Aggarwal et al., KDD 2024), adding statistics was among the changes that raised a page's visibility in generative-engine answers most. Microsoft also asks for claims anchored in measurable facts instead of words like "innovative". Use only numbers you can stand behind.

**How to fix it**

1. Replace vague claims with facts: delivery times, prices, sizes, years in business, numbers of projects.

### Quotations

*Impact: low · Effort: easy*

The same GEO study found that adding quotations from credible sources was one of the most effective changes. Quote a named expert, a standard or a genuine customer where it helps, marked up as a quotation. Never invent quotes or testimonials.

**How to fix it**

1. Use <blockquote> (with the source named) for a quotation.

```html
<blockquote>
  <p>The site went live in three weeks.</p>
  <footer>Ayşe K., owner of Example Bakery</footer>
</blockquote>
```

### Cited sources

*Impact: low · Effort: easy*

Citing sources was the third of the methods that helped most in the GEO study. Linking to the standards, studies or official pages behind your claims lets readers and engines check them.

**How to fix it**

1. Link the sources behind your numbers and claims from the text itself.

### Visible date on articles

*Impact: medium · Effort: easy*

Microsoft names freshness among the qualities AI answers look for, and Google recommends showing a visible date and adding datePublished and dateModified to the markup. A date tells engines how current the information is.

**How to fix it**

1. Show the publish date (and the update date when you revise) near the title, and add both to the Article markup.

```html
<time datetime="2026-10-21">21 October 2026</time>
```

### Author on articles

*Impact: low · Effort: easy*

Google's guidance on helpful content asks "who created the content?" and recommends a byline where readers expect one. A named author with a profile page makes an article easier to trust and to attribute.

**How to fix it**

1. Add a byline with the author's name linking to a short profile, and author in the Article markup.

### FAQ markup

*Impact: low · Effort: easy*

When a page has several questions and answers, FAQPage markup labels each pair for machines; Microsoft lists FAQ among the content types schema can label. Don't expect a rich result in Google: it stopped showing FAQ rich results on 7 May 2026.

**How to fix it**

1. Mark the questions and answers that are visible on the page with FAQPage, word for word.

```json
{"@context":"https://schema.org","@type":"FAQPage","mainEntity":[{"@type":"Question","name":"How long does a website take?",
 "acceptedAnswer":{"@type":"Answer","text":"Usually four weeks from the first meeting."}}]}
```

**Sources:** [GEO: Generative Engine Optimization (Aggarwal et al., KDD 2024)](https://arxiv.org/abs/2311.09735) · [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)

<a name="trust"></a>

## Trust

Signals that a real, reachable business stands behind the page.

### About and contact pages

*Impact: medium · Effort: easy*

Google's guidance on helpful content asks whether it's clear who is behind a site, and its quality rater guidelines look for who is responsible for it and how to contact them. People who find you through an AI answer check exactly that before getting in touch.

**How to fix it**

1. Link an about page and a contact page from the menu or the footer of every page.

### Contact details

*Impact: medium · Effort: easy*

A phone number, email and address on the page (as links, or in your Organization markup) give engines the facts they repeat when someone asks how to reach you, from your own site rather than an outdated directory.

**How to fix it**

1. Show your phone as a tel: link and your email as a mailto: link, and add them to the Organization markup.

```html
<a href="tel:+903120000000">+90 312 000 00 00</a> · <a href="mailto:info@example.com">info@example.com</a>
```

### Privacy policy

*Impact: low · Effort: moderate*

A privacy policy is required by law (GDPR, KVKK) as soon as a site collects personal data, even through a contact form. It's also part of what makes a business look accountable to the people an AI answer sends your way.

**How to fix it**

1. Publish a privacy policy that fits what you collect and link it from the footer.

**Sources:** [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) · [Bing Webmaster Guidelines](https://www.bing.com/webmasters/help/webmaster-guidelines-30fba23a)

<a name="site"></a>

## Site-wide readiness

Checks that need the whole site crawled the way AI crawlers read it.

### Every page readable without JavaScript

*Impact: high · Effort: hard*

The same test as "Text without JavaScript", on every crawled page: the major AI crawlers other than Google's and Apple's don't run scripts.

**How to fix it**

1. Render these pages on the server or pre-render them.

### Structured data across the site

*Impact: medium · Effort: moderate*

Pages without any JSON-LD leave engines to guess what they are. The home page needs Organization markup; service, product and article pages need their own types.

**How to fix it**

1. Add JSON-LD templates per page type in your CMS, so every new page gets it.

### Pages kept out of the index

*Impact: high · Effort: easy*

noindex keeps a page out of search and out of the AI answers built on it. That's right for thank-you or account pages, but a mistake on pages you list in the sitemap.

**How to fix it**

1. Remove noindex from pages you want found, or take them out of the sitemap.

### Pages AI answers may not quote

*Impact: high · Effort: easy*

nosnippet or max-snippet:0 keeps a page's text out of Google's AI features; NOARCHIVE keeps it out of Copilot answers.

**How to fix it**

1. Remove these directives from pages you want quoted (often a site-wide SEO plugin setting).

### Pages that answer with errors

*Impact: medium · Effort: easy*

A page that answers 404 or 5xx can't be crawled, indexed or cited, and links to it waste the crawl.

**How to fix it**

1. Fix or redirect (301) the broken pages and update the links that point to them.

### Pages blocked for AI search crawlers

*Impact: high · Effort: easy*

robots.txt rules can block AI search crawlers from parts of a site without anyone noticing: a rule meant for an admin folder that also covers your services, for example.

**How to fix it**

1. Review the rules that match these pages and narrow them down.

**Sources:** [Google: AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)

---

Generated from the audit guide of the [irodev.net](https://irodev.net) tools on 2026-10-23. Licensed under [CC BY 4.0](LICENSE).

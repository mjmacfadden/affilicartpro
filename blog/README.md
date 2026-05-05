# AffiliCart Blog Structure & Guidelines

This blog is a pure HTML/CSS implementation designed for lightweight performance and easy maintenance. This guide explains how the blog works and how to add new content.

## Directory Structure

```
/blog/
  index.html                          # Main blog listing
  category/
    /getting-started/
      index.html                      # All "Getting Started" posts
    /tutorials/
      index.html                      # All "Tutorials" posts
    /strategy/
      index.html                      # All "Strategy" posts
    /tools/
      index.html                      # All "Tools" posts
  /how-affilicart-turns-wordpress-blog.html
  /step-by-step-installation-guide.html
  /boost-amazon-affiliate-commissions.html
  /asin-copier-chrome-extension.html
  (individual blog post files)
```

## How to Add a New Blog Post

### Step 1: Create the Post HTML File

1. Create a new file in `/blog/` with a descriptive slug: `your-post-slug-here.html`
   - Use hyphens to separate words (kebab-case)
   - Keep it under 60 characters
   - Example: `keyword-rich-affiliate-strategy.html`

2. Use this template as a starting point. Copy from an existing post (e.g., `how-affilicart-turns-wordpress-blog.html`) and update:
   - `<title>` - Exact post title (60 chars or less for SEO)
   - `<meta name="description">` - 150-160 chars, includes keywords
   - `<link rel="canonical">` - Update URL to match your slug
   - `<meta property="og:url">` - Same as canonical
   - `<h1>` - Post title
   - Reading time estimate (in blog-meta-info)
   - BlogPosting schema `datePublished` (use 2026-05-XX format)
   - Actual post content in the `<article>` section
   - Related posts links at the bottom

3. Key HTML sections to customize:
   ```html
   <!-- Head section metadata -->
   <title>Your Post Title Here</title>
   <meta name="description" content="150-160 character description with keywords">
   <meta name="keywords" content="keyword1, keyword2, keyword3">
   <link rel="canonical" href="https://affilicartpro.com/blog/your-post-slug.html">
   
   <!-- Blog header -->
   <h1>Your Post Title</h1>
   <a href="category/category-slug/" class="blog-category">Category Name</a>
   <div class="blog-meta-info">
     <span>⏱️ X min read</span>
   </div>
   
   <!-- Content sections - use h2 for main sections, h3 for subsections -->
   <h2>Section Title</h2>
   <p>Content here...</p>
   
   <!-- Related posts (link to 2-3 other posts) -->
   <a href="other-post-slug.html" class="related-post-link">Other Post Title →</a>
   ```

### Step 2: Choose a Category

Posts must belong to ONE of these categories:
- **Getting Started** - Introductory guides, overviews, "why you should use AffiliCart"
- **Tutorials** - Step-by-step how-tos, setup guides, installation
- **Strategy** - Tips, tactics, optimization, commission strategies
- **Tools** - Features, extensions, integrations, tooling

### Step 3: Update the Blog Index

1. Open `/blog/index.html`
2. Add a new `<div class="col-md-6 col-lg-4">` card ABOVE the existing posts (new posts go to the top):
   ```html
   <div class="col-md-6 col-lg-4">
   <div class="blog-card">
     <div class="blog-date">X min read</div>
     <h3 class="blog-title"><a href="your-post-slug.html">Your Post Title</a></h3>
     <a href="category/your-category/" class="blog-category">Category Name</a>
     <p class="blog-excerpt">Brief 1-2 sentence excerpt from the post</p>
   </div>
   </div>
   ```

### Step 4: Update the Category Page

1. Navigate to the appropriate category folder (e.g., `/blog/category/tutorials/`)
2. Open `index.html`
3. Add your post card to the top of the post list:
   ```html
   <div class="col-md-6 col-lg-4">
   <div class="blog-card">
     <div class="blog-date">X min read</div>
     <h3 class="blog-title"><a href="../../your-post-slug.html">Your Post Title</a></h3>
     <span class="blog-category">Category Name</span>
     <p class="blog-excerpt">Brief excerpt</p>
   </div>
   </div>
   ```
4. Category pages show ALL posts in that category

### Step 5: Update Related Posts Links

In your new post's HTML file, add links to 2-3 related existing posts:
```html
<div class="related-posts">
  <h3>Read More</h3>
  <a href="other-post-slug.html" class="related-post-link">Related Post Title →</a>
  <a href="another-post-slug.html" class="related-post-link">Another Related Post →</a>
</div>
```

Also, update existing related posts sections to link back to your new post where appropriate.

### Step 6: Update sitemap.xml

Add your new post to `/sitemap.xml`:
```xml
<url>
  <loc>https://affilicartpro.com/blog/your-post-slug.html</loc>
  <lastmod>2026-05-XX</lastmod>
  <changefreq>monthly</changefreq>
  <priority>0.7</priority>
</url>
```

## Future Scaling: Archive & Pagination

When the blog grows to 50+ posts, consider implementing:
- Archive page with pagination (`/blog/archive/`, `/blog/archive/page/2/`, etc.)
- "View All Posts" button on main index
- Previous/Next navigation on archive pages

## Post Content Guidelines

### Length
- Aim for 4-8 minutes of reading time
- Roughly 800-2000 words depending on density
- Shorter is better than fluff

### Structure
- **Intro (1 paragraph):** Hook with problem or benefit
- **Main sections (h2):** 2-4 main topics, each with h3 subsections
- **Lists:** Use `<ul>` for benefits, `<ol>` for steps
- **Callouts:** Use `.highlight-box` divs for tips, warnings, pro tips
- **Conclusion:** Brief wrap-up + CTA linking back to product

### Tone
- Friendly, conversational (not formal)
- Focus on reader benefits, not just features
- Include practical examples
- Avoid corporate jargon

### Links
- Link to other blog posts for internal navigation
- Link to support.html for documentation
- Link to index.html#pricing for CTAs
- Include 2-3 related post links at the bottom

## SEO Best Practices

1. **Title Tags (60 chars max):** Include keyword near start
   - ✅ "Boost Amazon Affiliate Commissions with Multi-Product Carts"
   - ❌ "How I Increased My Affiliate Income by 300%"

2. **Meta Description (150-160 chars):** Include keyword + value prop
   - ✅ "Learn how the AffiliCart shopping cart feature lets Amazon Associates display multiple products and increase average order value."

3. **Canonical URLs:** Always use the exact blog post URL
   - ✅ `https://affilicartpro.com/blog/your-post-slug.html`

4. **Slugs (kebab-case):** Use target keywords
   - ✅ `amazon-affiliate-strategy-2026.html`
   - ❌ `blog-post-1.html`

5. **Headings:** Use h2 for main sections (1 per post), h3 for subsections
   - Include keywords naturally

6. **Schema Markup:** BlogPosting JSON-LD is already in template
   - Update `datePublished` to actual publish date

## Testing Checklist Before Publishing

- [ ] Links to all other blog posts work (no 404s)
- [ ] Internal links to support.html and index.html work
- [ ] Related posts section has 2-3 active links
- [ ] Category link works (links to category page)
- [ ] Post appears in blog/index.html
- [ ] Post appears in correct category page
- [ ] sitemap.xml includes new post URL
- [ ] Title is under 60 characters
- [ ] Meta description is 150-160 characters
- [ ] Reading time estimate is accurate
- [ ] No broken internal links
- [ ] Mobile responsive (test on phone/tablet)

## Quick Reference: File Locations

| Page | File Path | Purpose |
|------|-----------|---------|
| Main Blog | `/blog/index.html` | Lists all current posts |
| Getting Started | `/blog/category/getting-started/index.html` | All intro posts |
| Tutorials | `/blog/category/tutorials/index.html` | All tutorial posts |
| Strategy | `/blog/category/strategy/index.html` | All strategy posts |
| Tools | `/blog/category/tools/index.html` | All tool/feature posts |
| Individual Post | `/blog/post-slug.html` | Single blog post |

## Future Enhancements

When the blog grows, consider:
- [ ] Search functionality (JavaScript-based)
- [ ] Tags in addition to categories
- [ ] "Popular Posts" section
- [ ] Newsletter signup callouts
- [ ] Blog post comments (via Disqus/similar)
- [ ] Author bios (if expanding authorship beyond AffiliCart)

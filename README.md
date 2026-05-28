# Refinance LO Resource Portal

A responsive, single-page training and resource portal for Mortgage Loan Originators. The portal includes training modules, scripts, objection-handling resources, UWM-specific video training, downloadable documents, dark/light mode, engagement tracking, and a mobile-friendly navigation layout.

## Overview

This project is designed as an internal LO command center for refinance training and operational resources. It is built as a static HTML website, making it easy to host on GitHub Pages or any static hosting provider.

The current version includes:

- Responsive desktop, tablet, and mobile layout
- Light mode and dark mode
- Mobile slide-out navigation drawer
- Training module navigation
- UWM-specific video library
- Upload interface for call clips
- Engagement counters for views and likes
- Download links for document assets
- Header logo responsiveness
- Search bar hidden at smaller widths to avoid layout overlap

## Important Security Note

This site is currently a static front-end website. If hosted on GitHub Pages, any password, password hash, or client-side login logic included in the HTML, CSS, or JavaScript can be viewed by users through the browser source.

For real access control, use one of the following:

### Recommended

Use **Cloudflare Access** in front of the GitHub Pages site.

Recommended structure:

```text
GitHub Pages
→ Custom domain
→ Cloudflare DNS proxy
→ Cloudflare Zero Trust / Access
```

This protects the site before visitors reach the HTML files.

### Alternative

Use Cloudflare Pages with a Cloudflare Worker for custom server-side authentication.

This is the better option if you need a fully custom login page while keeping secrets out of the HTML source.

## Hosting on GitHub Pages

1. Create a GitHub repository.
2. Add the HTML file to the repository.
3. Rename the main HTML file to:

```text
index.html
```

4. Upload your supporting folders, such as:

```text
videos/
documents/
UML_logo.png
```

5. Go to:

```text
Repository Settings
→ Pages
```

6. Set the source branch, usually:

```text
main
```

7. Save and wait for GitHub Pages to publish the site.

## Recommended Folder Structure

```text
project-root/
├── index.html
├── UML_logo.png
├── documents/
│   ├── Gates To a Sale 2026 1.pdf
│   ├── new development guide.pdf
│   ├── uml-employee-handbook.pdf
│   └── other-downloadable-docs.pdf
└── videos/
    ├── Mortgage Industry 101.mp4
    ├── Introduction To Conventional vs. FHA Loans.mp4
    ├── How To Review A Credit Report.mp4
    ├── Understanding LTV.mp4
    └── other-training-videos.mp4
```

## Customizing Content

Most portal content is controlled inside the `portalRegistry` JavaScript object.

Each module looks like this:

```js
module_key: {
    title: "Module Title",
    video: "videos/example-video.mp4",
    hideVideo: false,
    desc: "Module description goes here.",
    assets: "<ul class='asset-list'><li>Resource item</li></ul>"
}
```

To add a new module:

1. Add a new entry to `portalRegistry`.
2. Add a matching navigation button.
3. Use `changeModule('your_module_key')` as the button action.

Example:

```html
<button class="nav-btn" data-mod="new_module" onclick="changeModule('new_module')">
    New Module
</button>
```

## Updating the Logo

The header logo uses:

```html
<img src="./UML_logo.png" alt="UML Logo">
```

To replace the logo:

1. Add your new logo file to the project root.
2. Rename it to `UML_logo.png`, or update the `src` path in the HTML.
3. Use a transparent PNG for the cleanest result.

## Search Bar Behavior

The header search bar is intentionally hidden at smaller screen widths to prevent it from colliding with the logo.

Current behavior:

- Search bar displays on large desktop widths.
- Search bar disappears at `1223px` and below.
- Logo remains centered and responsive.

To change the breakpoint, update this CSS rule:

```css
@media (max-width: 1223px) {
    .header-search {
        display: none !important;
    }
}
```

## Dark Mode

The portal supports light and dark mode using CSS variables and local storage.

Theme preference is stored under:

```js
refiPortalTheme
```

The dark mode toggle updates both the login/landing area, if present, and the main portal UI.

## Engagement Tracking

Views and likes are stored in the browser using local storage.

Storage key:

```js
refiPortalEngagement
```

This is local to the browser. It is not shared across users or devices.

For centralized tracking, connect the portal to a backend database or analytics platform.

## Video Notes

The video library expects files to exist in the `videos/` folder.

Example:

```js
{
    title: "Mortgage Industry 101",
    src: "videos/Mortgage Industry 101.mp4",
    category: "Mortgage Foundations"
}
```

Make sure the file name in the code exactly matches the uploaded file name, including spaces, capitalization, and punctuation.

## Document Notes

Download links expect files to exist in the `documents/` folder.

Example:

```html
<a href="documents/submission-checklist.pdf" class="download-action" download>
    Download Submission Assets
</a>
```

Make sure document names match exactly.

## Browser Support

This portal is designed for modern browsers, including:

- Chrome
- Edge
- Safari
- Firefox

The layout uses CSS Grid, Flexbox, CSS variables, and modern JavaScript.

## Development Notes

This is currently a single-file HTML app. That makes it easy to deploy, but as the project grows, consider splitting it into:

```text
index.html
styles.css
app.js
```

Suggested future improvements:

- Real backend authentication
- Admin panel for adding modules
- Centralized user analytics
- Search index for all module content
- Video completion tracking
- Role-based access control
- Cloudflare Access protection

## License

Internal use only unless otherwise specified.

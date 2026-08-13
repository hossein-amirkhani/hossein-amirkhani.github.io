---
layout: single
permalink: /gallery/
title: "Gallery"
author_profile: true
redirect_from:
  - /gallery
  - /gallery.html
meta_gallery:
  - image_path: /images/gallery/meta/photo-1.jpg
    alt: "Meta office building"
    title: "Meta office building"
---

<!--
  HOW TO ADD PHOTOS
  ------------------
  1. Drop image files into the /images/gallery/ folder in this repo.
  2. Add one entry per image to the `gallery` list in this page's front matter, e.g.:

     gallery:
       - image_path: /images/gallery/photo-1.jpg
         alt: "short description"
         title: "short description"
       - image_path: /images/gallery/photo-2.jpg
         alt: "short description"
         title: "short description"

  3. Below, call the include: {% raw %}{% include gallery %}{% endraw %}
     (it reads the `gallery` list above automatically).

  For named sub-galleries (like Meta below), add a separate list to the front
  matter (e.g. `meta_gallery`) and include it with an id:
  {% raw %}{% include gallery id="meta_gallery" %}{% endraw %}
-->

## Meta

I'm always curious about how a company's physical space reflects its culture — the layout, the details, the way a building is designed to say something about how people work and think together. Meta's offices are a great example of this, so I'm collecting photos of their buildings here.

{% include gallery id="meta_gallery" %}

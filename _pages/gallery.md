---
layout: single
permalink: /gallery/
title: "Gallery"
author_profile: true
redirect_from:
  - /gallery
  - /gallery.html
meta_gallery:
  - image_path: /images/gallery/meta/IMG_4858.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4860.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4861.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4863.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4916.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4917.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4918.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4919.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4920.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4921.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4922.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4923.jpeg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4963.jpg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4964.jpg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_4976.jpg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_5016.jpg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_5017.jpg
    alt: "Meta MPK"
  - image_path: /images/gallery/meta/IMG_5018.jpg
    alt: "Meta MPK"
---

<!--
  HOW TO ADD PHOTOS
  ------------------
  1. Drop image files into the /images/gallery/<sub-folder>/ folder in this repo.
  2. Add one entry per image to the relevant gallery list in this page's front
     matter (e.g. `meta_gallery`), e.g.:

     meta_gallery:
       - image_path: /images/gallery/meta/photo-1.jpg
         alt: "short description"

     image_path is the FULL site-relative path (starting with /images/...).
     alt is kept for accessibility only — nothing is shown visually on
     hover, and no caption/title appears in the click-to-zoom lightbox.

  3. The custom .mpk-gallery grid below reads straight from that front-matter
     list — no need to touch the HTML/CSS unless you're adding a new
     named sub-gallery (copy the "Meta" block and swap in the new list name).
-->

<style>
.mpk-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 16px;
  margin: 1.5em 0 2.5em;
  padding: 0;
  list-style: none;
}

.mpk-gallery__item {
  position: relative;
  display: block;
  aspect-ratio: 4 / 3;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.12);
  cursor: zoom-in;
  text-decoration: none;
}

.mpk-gallery__item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  margin: 0;
  border-radius: 0;
  transition: transform 0.45s ease;
}

.mpk-gallery__item:hover img,
.mpk-gallery__item:focus img {
  transform: scale(1.06);
}
</style>

## Meta (MPK 2026)

I'm always curious about how a company's physical space reflects its culture — the layout, the details, the way a building is designed to say something about how people work and think together. Meta's offices are a great example of this, so I'm collecting photos of their buildings here.

<div class="mpk-gallery">
  {% for photo in page.meta_gallery %}
  <a class="mpk-gallery__item image-popup" href="{{ photo.image_path | relative_url }}">
    <img src="{{ photo.image_path | relative_url }}" alt="{{ photo.alt }}" loading="lazy">
  </a>
  {% endfor %}
</div>

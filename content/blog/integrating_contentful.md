+++
title = "Incrementally Adopting Contentful"
date = ""
description = "Showcasing strategy for adding Contentful incrementally into an existing front-end project"
tags = [
    "Jamstack",
    "Contentful",
    "GCP",
]
+++

Let's say you are working on an existing codebase for someone's website. It's an old
website - some HTML and CSS on a server, no JS and no front-end framework to speak of
(not even a templating library). Let's also say that you are non-committal and don't
want to spend time migrating the site to a modern framework like Next.js -- it doesn't
seem valuable yet, you'd rather work with the code you have and focus on implementing
a CMS first, which will be agnostic of whichever framework you eventually end up choosing.
Plus, enabling non-technical users to make site updates is what your client is interested
in the most, so focusing on the CMS first makes sense from a priorities standpoint.

This is the situation I found myself in with a side project. I wanted a CMS with
a good free tier that I could adopt over time, I chose Contentful for its generous
free tier and premier usability. Integrating Contentful into a Gatsby or Next.js
project is a well-trod path, but what about this dead-simple HTML + CSS project? I wondered
if I could cobble together low-level tools to create something custom while getting
away with minimal changes to the existing codebase.

Enter Handlebars -- the (almost) lowest-level templating framework available. It
seems great for my use case, I just want to dynamically pre-render HTML files depending
on some JSON that I get from Contentful, all I need to do is write a simple build
script/process to piece things together.

## Tools

- Contentful - CMS
- Handlebars - HTML templating
- Marked - Rendering markdown from Contentful
- Contentful.js - Rendering Contentful-flavor rich text
- GraphQL Requests - Making barebones GraphQL requests to Contentful's API

Check out the example repository for the finished product

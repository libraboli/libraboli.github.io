---
layout: page
title: vivo BlueImage Lab
description: Public research agenda and project links from vivo Camera Research.
permalink: /blueimage/
---

vivo BlueImage Lab explores mobile imaging, computational photography, content generation, agents, and foundation models. The lab's public research presence is visible through the [vivo Camera Research GitHub organization](https://github.com/vivoCameraResearch), which publishes projects spanning diffusion-based imaging, matting, bokeh rendering, visual grounding, photo editing, and video generation.

vivo's public BlueImage material describes an imaging stack that brings together self-developed sensing, algorithm, and imaging-chip technologies, while exploring AIGC and 3D imaging for future mobile imaging experiences.

<div class="project-grid">
{% for project in site.data.projects %}
  <article>
    <p class="venue">{{ project.area }}</p>
    <h3><a href="{{ project.url }}">{{ project.name }}</a></h3>
    <p>{{ project.description }}</p>
  </article>
{% endfor %}
</div>

## Source Links

- [vivo Camera Research GitHub](https://github.com/vivoCameraResearch)
- [vivo BlueImage public news](https://www.vivo.com.cn/brand/news/detail?id=1261&type=1)
- [vivo BlueImage product coverage](https://www.pingwest.com/w/312350)


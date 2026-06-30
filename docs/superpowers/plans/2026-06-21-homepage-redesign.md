# Homepage Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild `libraboli.github.io` into an al-folio-based research leadership homepage for Bo Li, presenting dual authority as an academic AI imaging researcher and vivo BlueImage Lab research leader.

**Architecture:** Use al-folio's Jekyll conventions for pages, publications, news, projects, and bibliography. Preserve current homepage assets as source material, but replace the W3layouts static site with a structured academic/research-leadership site. Keep public claims source-backed and isolate uncertain claims such as the exact CVPR finalist link for manual confirmation.

**Tech Stack:** GitHub Pages, Jekyll, al-folio, BibTeX, Markdown, SCSS/CSS, Ruby Bundler.

---

## File Structure

- Modify: `_config.yml` — site identity, navigation, social links, theme settings, collections.
- Create/Modify: `_pages/about.md` — customized homepage hero and research-leadership sections.
- Create/Modify: `_pages/cv.md` — education, appointments, awards, service.
- Create/Modify: `_pages/publications.md` — al-folio publication listing page.
- Create/Modify: `_pages/projects.md` — BlueImage Lab / research agenda and public project links.
- Create/Modify: `_pages/service.md` — NeurIPS/ICLR/service and awards page if al-folio navigation needs a separate service page.
- Create/Modify: `_bibliography/papers.bib` — curated publication records.
- Create/Modify: `_news/*.md` — recent publication and service news.
- Create/Modify: `_projects/*.md` — selected BlueImage Lab public projects.
- Create/Modify: `assets/img/` — migrate current portrait, vivo/NJU/Youtu logos, paper thumbnails.
- Create/Modify: `assets/css/custom.scss` or al-folio custom style entry — restrained industrial research director visual layer.
- Preserve: `legacy/` — current HTML/CSS site copied for rollback/reference.
- Modify: `.gitignore` — keep `.superpowers/` and local build artifacts out of commits.

## Task 1: Create a Safe Migration Branch and Preserve the Existing Site

**Files:**
- Modify: `.gitignore`
- Create: `legacy/README.md`
- Move/copy existing static files into `legacy/original-site/`

- [ ] **Step 1: Create the implementation branch**

```bash
git switch -c codex/al-folio-homepage
```

Expected: branch changes from `main` to `codex/al-folio-homepage`.

- [ ] **Step 2: Preserve the current static site**

```bash
mkdir -p legacy/original-site
cp -R README.md index.html bio.html pub.html contact.html css fonts image images legacy/original-site/
```

Expected: `legacy/original-site/index.html` exists and opens as the current homepage.

- [ ] **Step 3: Add rollback documentation**

Create `legacy/README.md`:

```markdown
# Legacy Homepage

This folder preserves the previous static `libraboli.github.io` site before the al-folio redesign.

The preserved site includes:

- `index.html`
- `bio.html`
- `pub.html`
- `contact.html`
- `css/`
- `fonts/`
- `image/`
- `images/`

Use it only as content and asset reference during the redesign.
```

- [ ] **Step 4: Commit the preservation step**

```bash
git add .gitignore legacy
git commit -m "Preserve legacy homepage"
```

Expected: commit created with only `.gitignore` and `legacy/` changes.

## Task 2: Import the al-folio Skeleton

**Files:**
- Create/replace: al-folio Jekyll root files and directories listed in File Structure.
- Preserve: `legacy/`.

- [ ] **Step 1: Fetch al-folio using a blobless clone**

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 --filter=blob:none https://github.com/alshedivat/al-folio.git "$tmpdir/al-folio"
```

Expected: `$tmpdir/al-folio/_config.yml`, `$tmpdir/al-folio/_pages/about.md`, and `$tmpdir/al-folio/_bibliography/papers.bib` exist.

- [ ] **Step 2: Copy the al-folio skeleton into the repo**

```bash
rsync -a \
  --exclude='.git' \
  --exclude='.github' \
  --exclude='.agents' \
  --exclude='.claude' \
  --exclude='.codex' \
  --exclude='.gemini' \
  --exclude='docs' \
  --exclude='lighthouse_results' \
  --exclude='readme_preview' \
  "$tmpdir/al-folio/" ./
```

Expected: `_config.yml`, `_pages/`, `_bibliography/`, `_news/`, `_projects/`, `_posts/`, `assets/`, `Gemfile`, and `package.json` exist in the homepage repo.

- [ ] **Step 3: Restore local planning docs after skeleton copy**

```bash
git checkout -- docs/superpowers/specs/2026-06-21-homepage-redesign-design.md docs/superpowers/plans/2026-06-21-homepage-redesign.md
```

Expected: both planning docs remain present.

- [ ] **Step 4: Remove sample al-folio content that should not ship**

```bash
rm -rf _books _teachings
rm -f _pages/about_einstein.md _pages/books.md _pages/dropdown.md _pages/plugins.md _pages/profiles.md _pages/repositories.md _pages/teaching.md
rm -rf _posts/*
```

Expected: no Einstein/sample teaching/book pages remain in navigation.

- [ ] **Step 5: Commit the imported skeleton**

```bash
git add .
git commit -m "Import al-folio site skeleton"
```

Expected: commit contains al-folio structure and legacy site remains under `legacy/`.

## Task 3: Configure Site Identity, Navigation, and Assets

**Files:**
- Modify: `_config.yml`
- Create/Modify: `assets/img/bo-li.jpeg`
- Create/Modify: `assets/img/logos/vivo.png`, `assets/img/logos/youtu.png`, `assets/img/logos/nju.jpg`
- Create/Modify: `assets/img/publications/*.png`

- [ ] **Step 1: Copy source assets into al-folio asset locations**

```bash
mkdir -p assets/img/logos assets/img/publications
cp legacy/original-site/image/libo.jpeg assets/img/bo-li.jpeg
cp legacy/original-site/image/vivo.png assets/img/logos/vivo.png
cp legacy/original-site/image/youtu.png assets/img/logos/youtu.png
cp legacy/original-site/image/nju.jpg assets/img/logos/nju.jpg
cp legacy/original-site/image/CVPR2024-ASAM.png assets/img/publications/cvpr2024-asam.png
cp legacy/original-site/image/IJCV2024-IPSeg.png assets/img/publications/ijcv2024-ipseg.png
cp legacy/original-site/image/MM2024-CoVP.jpg assets/img/publications/mm2024-covp.jpg
cp legacy/original-site/image/CVPR2024-revisting.png assets/img/publications/cvpr2024-reflection-removal.png
cp legacy/original-site/image/CVPR2022-COD.png assets/img/publications/cvpr2022-cod.png
```

Expected: all copied files exist under `assets/img/`.

- [ ] **Step 2: Configure `_config.yml`**

Set these fields in `_config.yml`:

```yaml
title: Bo Li
first_name: Bo
middle_name:
last_name: Li
description: Research leader in AI imaging, multimodal vision, and device-native intelligence.
url: "https://libraboli.github.io"
baseurl: ""
lang: en
icon: assets/img/bo-li.jpeg
github_username: vivoCameraResearch
scholar_userid: NVzQ87sAAAAJ
orcid_id: 0000-0000-0000-0000
twitter_username: BoLi_CV
```

For `orcid_id`, replace the temporary value with the ID from the OpenReview ORCID link before publishing. If the ORCID ID cannot be verified, omit the field rather than publishing an unverified value.

- [ ] **Step 3: Configure header navigation**

Ensure navigation exposes only these pages:

```yaml
- title: About
  url: /
- title: Publications
  url: /publications/
- title: BlueImage Lab
  url: /projects/
- title: Service
  url: /service/
- title: CV
  url: /cv/
- title: Writing
  url: /blog/
```

Expected: sample al-folio pages are not visible in the site header.

- [ ] **Step 4: Commit configuration and assets**

```bash
git add _config.yml assets/img
git commit -m "Configure site identity and assets"
```

Expected: commit contains site config and migrated assets.

## Task 4: Build the Homepage Content

**Files:**
- Modify: `_pages/about.md`
- Modify/Create: `assets/css/custom.scss`

- [ ] **Step 1: Replace `_pages/about.md` with the dual-authority homepage**

Use this content:

```markdown
---
layout: about
title: about
permalink: /
subtitle: Principal Researcher, vivo BlueImage Lab
profile:
  align: right
  image: bo-li.jpeg
  image_circular: false
  more_info: >
    <p>vivo BlueImage Lab</p>
    <p>Camera Research Department, vivo</p>
selected_papers: true
social: true
announcements:
  enabled: true
  scrollable: true
  limit: 6
latest_posts:
  enabled: false
---

I am a Principal Researcher in the Camera Research Department at vivo, where I work with vivo BlueImage Lab on AI imaging, multimodal vision, computational photography, content generation, agents, and device-native intelligence.

Before vivo, I was a researcher at Tencent Youtu Lab. I received my B.Sc. and Ph.D. degrees from the Department of Computer Science at Nanjing University.

My research connects academic computer vision with industrial imaging systems: from robust segmentation, salient and camouflaged object detection, and adversarial robustness to diffusion-based imaging, MLLMs, AIGC, and camera intelligence for mobile devices.

<div class="research-trust-strip">
  <span>NeurIPS SAC</span>
  <span>ICLR AC</span>
  <span>CVPR Finalist</span>
  <span>Google Scholar</span>
  <span>OpenReview</span>
  <span>vivo BlueImage Lab</span>
</div>

## Research Agenda

**AI imaging and computational photography.** I am interested in imaging algorithms that improve how mobile devices capture, restore, understand, and generate visual content.

**Multimodal vision, MLLM, and AIGC.** Recent work from our group explores diffusion models, dense prediction, visual grounding, content generation, matting, bokeh rendering, and intelligent photo editing.

**Device-native intelligence.** I care about research that can move from papers into real camera and album experiences, connecting data, models, evaluation, deployment, and product use.

## vivo BlueImage Lab

vivo BlueImage Lab explores mobile imaging, computational photography, content generation, agents, and foundation models. Public work from vivo Camera Research includes projects such as MagicBokeh, SmartPhotoCrafter, Any-to-Bokeh, SDMatte, PPC, MagicTryOn, Hyper-Motion, and Magic-World.

## Selected Recognition and Service

- Senior Area Chair, NeurIPS.
- Area Chair, ICLR.
- CVPR finalist, exact public link pending confirmation.
- Jiangsu Provincial Outstanding Doctoral Thesis.
- Outstanding Doctoral Graduate, Nanjing University.
```

Expected: homepage copy foregrounds dual authority without developer-portfolio language.

- [ ] **Step 2: Add custom visual treatment**

Create or extend `assets/css/custom.scss`:

```scss
.research-trust-strip {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin: 1.5rem 0 2rem;
}

.research-trust-strip span {
  border: 1px solid var(--global-divider-color);
  border-radius: 999px;
  padding: 0.35rem 0.7rem;
  font-size: 0.85rem;
  color: var(--global-text-color-light);
  background: var(--global-bg-color);
}

.post-description,
.profile .more-info {
  font-size: 0.95rem;
}
```

Expected: trust strip reads as restrained professional metadata, not developer badges.

- [ ] **Step 3: Commit homepage content**

```bash
git add _pages/about.md assets/css/custom.scss
git commit -m "Create research leadership homepage"
```

Expected: commit contains homepage and custom styling only.

## Task 5: Structure Publications, Projects, News, and Service

**Files:**
- Modify: `_bibliography/papers.bib`
- Modify: `_pages/publications.md`
- Modify/Create: `_pages/service.md`
- Modify/Create: `_projects/*.md`
- Modify/Create: `_news/*.md`

- [ ] **Step 1: Replace `_bibliography/papers.bib` with curated seed records**

Use BibTeX entries for the current verified seed papers:

```bibtex
@inproceedings{zhong2022cod,
  title={Detecting Camouflaged Object in Frequency Domain},
  author={Zhong, Yijie and Li, Bo and Tang, Lv and Kuang, Senyun and Wu, Shuang and Ding, Shouhong},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2022},
  selected={true},
  preview={cvpr2022-cod.png},
  html={https://openaccess.thecvf.com/content/CVPR2022/html/Zhong_Detecting_Camouflaged_Object_in_Frequency_Domain_CVPR_2022_paper.html}
}

@inproceedings{li2024asam,
  title={ASAM: Boosting Segment Anything Model with Adversarial Tuning},
  author={Li, Bo and Xiao, Haoke and Tang, Lv},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2024},
  selected={true},
  preview={cvpr2024-asam.png},
  html={https://openaccess.thecvf.com/content/CVPR2024/html/Li_ASAM_Boosting_Segment_Anything_Model_with_Adversarial_Tuning_CVPR_2024_paper.html}
}

@article{tang2024ipseg,
  title={Towards Training-Free Open-World Segmentation via Image Prompting Foundation Models},
  author={Tang, Lv and Jiang, Peng-Tao and Xiao, Haoke and Li, Bo},
  journal={International Journal of Computer Vision},
  year={2024},
  selected={true},
  preview={ijcv2024-ipseg.png},
  html={https://link.springer.com/article/10.1007/s11263-024-02185-6}
}

@inproceedings{tang2024covp,
  title={Chain of Visual Perception: Harnessing Multimodal Large Language Models for Zero-Shot Camouflaged Object Detection},
  author={Tang, Lv and Jiang, Peng-Tao and Shen, Zhi-Hao and Zhang, Hao and Chen, Jinwei and Li, Bo},
  booktitle={Proceedings of the ACM International Conference on Multimedia},
  year={2024},
  selected={true},
  preview={mm2024-covp.jpg},
  html={https://arxiv.org/abs/2311.11273}
}

@inproceedings{zhu2024reflection,
  title={Revisiting Single Image Reflection Removal in the Wild},
  author={Zhu, Yurui and Fu, Xueyang and Jiang, Peng-Tao and Zhang, Hao and Sun, Qibin and Chen, Jinwei and Zha, Zheng-Jun and Li, Bo},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2024},
  selected={true},
  preview={cvpr2024-reflection-removal.png},
  html={https://openaccess.thecvf.com/content/CVPR2024/papers/Zhu_Revisiting_Single_Image_Reflection_Removal_In_the_Wild_CVPR_2024_paper.pdf}
}
```

Expected: selected papers render on homepage and publications page.

- [ ] **Step 2: Add BlueImage Lab project cards**

Create `_projects/blueimage-lab.md`:

```markdown
---
layout: page
title: vivo BlueImage Lab
description: AI imaging, computational photography, content generation, agents, and foundation models.
img: assets/img/logos/vivo.png
importance: 1
category: lab
---

vivo BlueImage Lab explores mobile imaging, computational photography, content generation, agents, and foundation models.

Public project links:

- [vivo Camera Research GitHub](https://github.com/vivoCameraResearch)
- [MagicBokeh](https://github.com/vivoCameraResearch/MagicBokeh)
- [SmartPhotoCrafter](https://github.com/vivoCameraResearch/SmartPhotoCrafter)
- [Any-to-Bokeh](https://github.com/vivoCameraResearch/any-to-bokeh)
- [SDMatte](https://github.com/vivoCameraResearch/SDMatte)
- [PPC](https://github.com/vivoCameraResearch/PPC-Official)
- [MagicTryOn](https://github.com/vivoCameraResearch/Magic-TryOn)
```

Expected: projects page has a lab card with public links.

- [ ] **Step 3: Add service page**

Create `_pages/service.md`:

```markdown
---
layout: page
title: service
permalink: /service/
nav: true
nav_order: 4
---

## Conference Service

- Senior Area Chair, NeurIPS.
- Area Chair, ICLR.

## Recognition

- CVPR finalist, exact public source link pending confirmation.
- Jiangsu Provincial Outstanding Doctoral Thesis, 2021.
- Outstanding Doctoral Graduate, Nanjing University, 2020.
- First prize for postgraduate doctoral scholarship, Nanjing University, 2015-2018.
- First prize for Top Student scholarship, Nanjing University, 2013-2014.
```

Expected: service page exists and does not overclaim unverified details.

- [ ] **Step 4: Add current news items**

Create `_news/2025-08-22-iclr-ac.md`:

```markdown
---
layout: post
date: 2025-08-22 00:00:00-0000
inline: true
related_posts: false
---

I will serve as an Area Chair for ICLR 2026.
```

Create `_news/2025-04-09-neurips-ac.md`:

```markdown
---
layout: post
date: 2025-04-09 00:00:00-0000
inline: true
related_posts: false
---

I will serve as an Area Chair for NeurIPS 2025.
```

Expected: homepage announcement section shows high-signal service news.

- [ ] **Step 5: Commit structured content**

```bash
git add _bibliography _pages/publications.md _pages/projects.md _pages/service.md _projects _news
git commit -m "Add publications projects and service content"
```

Expected: content commit is separate from visual/theme work.

## Task 6: Build, Verify, and Prepare Deployment

**Files:**
- Modify as needed: `Gemfile`, `Gemfile.lock`, `_config.yml`, `assets/css/custom.scss`

- [ ] **Step 1: Install dependencies**

```bash
bundle config set --local path vendor/bundle
bundle install
```

Expected: dependencies install without global Ruby permission errors.

- [ ] **Step 2: Build the site**

```bash
bundle exec jekyll build
```

Expected: `_site/index.html` is generated and the command exits 0.

- [ ] **Step 3: Run a local server**

```bash
bundle exec jekyll serve --host 127.0.0.1 --port 4000
```

Expected: `http://127.0.0.1:4000/` serves the new homepage.

- [ ] **Step 4: Browser QA**

Open the local site and check:

- Hero has Bo Li, role, profile photo, and high-signal links.
- Homepage does not look like a developer portfolio.
- Publications page renders selected papers and thumbnails.
- Projects page links to vivo Camera Research public projects.
- Service page renders without unverified claims.
- Mobile viewport has no overlapping text or broken navigation.

- [ ] **Step 5: Commit build fixes**

```bash
git status -sb
git add _config.yml Gemfile Gemfile.lock assets _pages _bibliography _projects _news
git commit -m "Verify al-folio homepage build"
```

Expected: final implementation commit includes only source files required for the site, not `_site/`, `vendor/`, or `.superpowers/`.

## Task 7: Publish Workflow

**Files:**
- No source changes unless verification finds a deployment-specific issue.

- [ ] **Step 1: Confirm final branch diff**

```bash
git status -sb
git log --oneline --decorate -5
git diff --stat origin/main...HEAD
```

Expected: clean working tree and a readable sequence of redesign commits.

- [ ] **Step 2: Push branch**

```bash
git push -u origin codex/al-folio-homepage
```

Expected: branch appears on GitHub.

- [ ] **Step 3: Open a draft PR**

```bash
gh pr create --draft --title "[codex] redesign academic research homepage" --body "Redesigns libraboli.github.io as an al-folio-based research leadership homepage. Includes source-backed academic, service, publication, and vivo BlueImage Lab content. Local verification: bundle exec jekyll build."
```

Expected: draft PR opens against `main`.

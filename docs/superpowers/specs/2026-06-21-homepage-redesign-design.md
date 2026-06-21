# Bo Li Homepage Redesign Design

## Objective

Rebuild `libraboli.github.io` as a research leadership homepage based on al-folio, customized for Bo Li's dual identity:

- Academic influence in computer vision, multimodal AI, and imaging research.
- Industrial research leadership as Principal Researcher at vivo BlueImage Lab / Camera Research Department.

The site should not feel like a student academic page, a professor-only publication archive, or a developer portfolio. It should read as the homepage of a senior industrial AI imaging research leader.

## Positioning

Primary positioning:

> Research leader in AI imaging, multimodal vision, and device-native intelligence.

Expanded positioning:

> Principal Researcher at vivo BlueImage Lab, working at the intersection of AI imaging, multimodal vision, computational photography, content generation, agents, and device-native intelligence.

## Audience

The homepage should work for:

- Academic peers, collaborators, and program chairs.
- Senior industry researchers and AI/product leaders.
- Candidates or partners evaluating vivo BlueImage Lab.
- Media, conference organizers, and invited-talk hosts.

## Homepage Structure

### 1. Hero

Content:

- Name: Bo Li / 李博.
- Role: Principal Researcher, vivo BlueImage Lab / Camera Research Department, vivo.
- One-sentence positioning around AI imaging, multimodal vision, computational photography, and device-native intelligence.
- High-signal links: Google Scholar, OpenReview, DBLP, ORCID, GitHub/vivo Camera Research, X.

Trust strip:

- NeurIPS SAC.
- ICLR AC.
- CVPR finalist, pending exact public source link.
- Google Scholar citation count, sourced from public Google Scholar page when refreshed.
- vivo BlueImage Lab.

### 2. Research Agenda

Three pillars:

- AI Imaging and Computational Photography.
- Multimodal Vision, MLLM, and AIGC.
- Device-Native Intelligence, Agents, and Research-to-Product Systems.

This section should explain the research agenda in plain language, not as keyword tags.

### 3. Selected Publications

Use al-folio's publications system, but curate the homepage to show only selected work.

Seed publications from the current site and public Google Scholar/OpenReview/vivo Camera Research data:

- Detecting Camouflaged Object in Frequency Domain, CVPR 2022.
- Multi-task Dense Prediction via Mixture of Low-Rank Experts, CVPR 2024.
- ASAM: Boosting Segment Anything Model with Adversarial Tuning, CVPR 2024.
- Revisiting Single Image Reflection Removal in the Wild, CVPR 2024.
- Towards Training-Free Open-World Segmentation via Image Prompt Foundation Models, IJCV 2024.
- Chain of Visual Perception / CoVP, ACM Multimedia 2024.
- Selected ICLR / NeurIPS / ICCV / TPAMI / CVPR 2025-2026 BlueImage Lab works after source verification.

Each selected paper card should include:

- Venue and year.
- Author role where clear, such as first author or corresponding author.
- Paper link.
- Code/project link when public.
- Thumbnail when already available or sourced from project pages.

### 4. BlueImage Lab and Industrial Impact

This section should link the personal academic identity with the lab agenda.

Source-backed facts to use:

- vivo Camera Research GitHub organization identifies vivo BlueImage Lab as exploring mobile imaging, computational photography, content generation, agents, and foundation models.
- vivo public material describes BlueImage as combining sensors, algorithm matrix, and imaging chip technologies while exploring AIGC and 3D imaging.
- vivo Camera Research public repositories include works such as MagicBokeh, SmartPhotoCrafter, Any-to-Bokeh, SDMatte, PPC, MagicTryOn, Hyper-Motion, and Magic-World.

Tone:

- Avoid corporate marketing copy.
- Present lab work as research agenda plus product translation.

### 5. Service and Recognition

Dedicated section for academic service and recognition:

- NeurIPS SAC.
- ICLR AC.
- Conference/journal reviewing or area-chair roles if verified.
- CVPR finalist once the exact public source is linked.
- Awards from Nanjing University and Jiangsu Outstanding Doctoral Thesis from the existing homepage.

### 6. Writing / Notes

Use al-folio blog or news pages for:

- Research notes on AI-native phone imaging.
- Technical essays on MLLM/AIGC for mobile imaging.
- Reflections on research-to-product loops.
- Talks and invited presentations.

### 7. CV / Biography

Keep a concise bio:

- B.Sc. and Ph.D., Department of Computer Science, Nanjing University.
- Senior Researcher, Tencent Youtu Lab, 2020-2023/2024 depending on source chosen.
- Principal Researcher / Lead Researcher, vivo Camera Research Department / vivo BlueImage Lab.

If source years differ, prefer OpenReview for public profile dates or show less precise wording.

## Visual Direction

Use al-folio as the content engine, but customize the homepage visual hierarchy:

- Editorial, restrained, and research-director focused.
- Light background, strong typography, generous spacing.
- Use small accent color inspired by vivo/BlueImage, not a dominant blue gradient.
- Avoid skill badges, animated particle backgrounds, 3D hero visuals, and generic developer cards.
- Use publication/project thumbnails sparingly and only where they add credibility.

## Source Policy

Only put source-backed claims on the live homepage.

Source-backed now:

- Existing `libraboli.github.io` content for education, Tencent/vivo history, selected publications, current photo, Google Scholar link, and X link.
- Google Scholar public page for profile, topics, citation count, and high-citation papers.
- OpenReview public profile for role, links, career history, expertise, and publication entries.
- vivo Camera Research GitHub organization for BlueImage Lab description and public project list.
- vivo public news and third-party tech media for BlueImage product/strategy context.

Needs confirmation before publishing:

- Exact wording and link for CVPR finalist.
- Whether to use "Principal Researcher", "Lead Researcher", "Algorithm Expert", or "Head of vivo BlueImage Lab" as the primary title.
- Whether to show citation count as a fixed number or omit the number to avoid staleness.

## Implementation Boundary

Implementation should be done on a new branch in the local clone, then reviewed locally before push.

The first implementation target is a working al-folio-based site with:

- Homepage.
- About/CV.
- Publications.
- BlueImage Lab / Research Agenda.
- Service.
- News or Writing.

Deployment target remains GitHub Pages at `https://libraboli.github.io/`.

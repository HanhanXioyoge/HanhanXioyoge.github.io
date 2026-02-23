---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* M.S. in Bioengineering, Zhejiang University of Technology, 2026 (expected)
* B.S. in Animal Science, Southwest University, 2022

Skills
======
* 生物信息与代谢建模
  * 蛋白组学分析
  * 基因组规模代谢模型（GEM）建模与模拟
  * 酶约束代谢模型（ecGEMs）构建
* 编程语言
  * python
  * Matlab
  * R
* AI工具
  * Claude code + minimax
  * Agent skills

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

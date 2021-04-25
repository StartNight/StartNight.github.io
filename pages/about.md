---
layout: page
title: About
description: 打码改变世界
keywords: Felix, 康
comments: true
menu: 关于
permalink: /about/
---

游戏是科技与艺术的结合。

仰慕「优雅编码的艺术」。

坚信熟能生巧，努力改变人生。

## 联系




## Skill Keywords

{% for skill in site.data.skills %}
### {{ skill.name }}
<div class="btn-inline">
{% for keyword in skill.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}

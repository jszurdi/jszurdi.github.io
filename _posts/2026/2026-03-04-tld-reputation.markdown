---
layout: post
title: 'Not What It Used To Be: Generational Analysis of Top-level Domain Reputation'
date: '2026-03-04 04:00'
comments: false
tags: ['DNS', 'domain names', 'security', 'cybercrime']
thumbnail-img: "/assets/img/blog/2026/tld-reputation/cover.png"
share-img: "/assets/img/blog/2026/tld-reputation/cover.png"
permalink: /blog/tld-reputation/
---

Over the past few decades, researchers from both academia and industry have significantly increased the number and quality of malicious domain detectors. From a few early heuristic-based detection methods, today there are hundreds of papers on machine learning- and AI-based detectors, matched by industry capabilities.

One would expect that such incredible improvement in malicious domain detection would lead to a decrease in the number of malicious domain registrations. Unfortunately, we observe the opposite; cybercriminals nowadays register vastly more malicious domains than before. The main reason is that domain registration policies have a considerably greater effect on the number of malicious domain registrations than detection capabilities do.

In our paper, we explore how new generations of generic  top-level domains (gTLDs) are utilized for malicious and benign use, finding that:
* Newer gTLD generations have vastly worse malicious ratios compared to legacy gTLDs and ccTLDs
* These new gTLD generation’s malicious use deteriorates faster over time compared to legacy gTLDs and ccTLDs
* They are used much less frequently for benign purposes.

![Malicious Ratio of TLD generations.](/assets/img/blog/2026/tld-reputation/cover.png)

These findings question the value of [ICANN’s DNS Abuse Mitigation Program](https://www.icann.org/resources/pages/dns-security-threat-mitigation-2025-11-21-en) for the Internet community at large and whether new domain registration policies are needed to curb malicious registrations in these new TLD generations. We argue that **ICANN’s current DNS abuse mitigation program** will not help and that policy proposals from researchers should be taken seriously. In particular, the extremely low pricing of new gTLDs enables massive malicious domain registration campaigns. Therefore, at least a **mandatory minimum domain registration price** would be a great first step to improve the current state of the domain landscape.

Our paper can be found here and [here](https://janos.szurdi.com/content/academicpapers/madweb26-tldreputation.pdf).

My presentation at MADWeb 2026 can be found [here](https://janos.szurdi.com/content/presentations/tld-reputation-presentation.pdf).

Palo Alto Networks publishes our data [here](https://github.com/PaloAltoNetworks/tld-metrics).

Feel free to reach out to me about our research via [LinkedIn](https://www.linkedin.com/in/szurdi/) or [email](https://janos.szurdi.com/aboutme/).







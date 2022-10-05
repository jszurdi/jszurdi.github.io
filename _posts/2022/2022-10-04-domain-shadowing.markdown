---
layout: post
title: 'Domain Shadowing'
date: '2022-10-04 22:00'
comments: true
tags: ['computer security', 'DNS security']
thumbnail-img: "/assets/img/blog/2022/domain-shadowing/cover.jpeg"
share-img: "/assets/img/blog/2022/domain-shadowing/cover.jpeg"
permalink: /blog/domain-shadowing/
---

In the very first post in this blog, I explain domain shadowing using a few examples and summarize results from our [Unit42 blog post](https://unit42.paloaltonetworks.com/domain-shadowing/).

Domain shadowing is a stealthy variant of [domain hijacking](https://en.wikipedia.org/wiki/Domain_hijacking) where attackers make sure to leave the original DNS records intact not to be detected by the compromised domain’s owners. Instead, they create new malicious subdomains under the compromised domain.

If we take a benign domain *barwonbluff.com[.]au*, the domain and its subdomain often have the same IP address:  

    barwonbluff.com[.]au 27.131.74[.]5  
    www.barwonbluff.com[.]au 27.131.74[.]5

When we think of DNS/domain hijacking, we usually imagine attackers modifying the records of the main domain:

    barwonbluff.com[.]au 62.204.41[.]247

Cybercriminals change the main domain’s IP address to launch attacks on the users of the domain name, including phishing, men-in-the-middle, or malware distribution. Crooks compromise domain names by stealing login credentials of the domain owners at their [registrar](https://en.wikipedia.org/wiki/Domain_name_registrar), compromising registrars or infiltrating a DNS server directly.

However, targeting a compromised domain’s users is often not lucrative for criminals. In that case, they can leverage compromised domains as part of their infrastructure for other malicious campaigns. For domain shadowing, attackers make sure not to modify the original DNS records, but instead, they create many inconspicuous malicious subdomains – called shadowed domains – under the compromised domain name. These domains are valuable for criminals as they provide them with a large number of domains that have a benign reputation. In the case of *barwonbluff.com[.]au*, we observed  attacker creating shadowed domains, as shown in the below examples:   

    bancobpmmavfhxcc.barwonbluff.com[.]au 62.204.41[.]247  
    tomsvprfudhd.barwonbluff.com[.]au 62.204.41[.]77

As traditional approaches are not very good at detecting shadowed domains, we designed a detection pipeline using supervised machine learning that processes terabytes of DNS logs daily. The detector has identified thousands of shadowed domains used in multiple malicious campaigns, including ones used for phishing - as shown in the example below (source: [Unit42 blog](https://unit42.paloaltonetworks.com/domain-shadowing/)). 

![Phishing campaign example using domain shadowing](/assets/img/blog/2022/domain-shadowing/cover.jpeg)

We see how vital these specialized detectors are when we find that VirusTotal vendors only detect 2% of the domains flagged by our model. We share more details on domain shadowing, our model and the detections in our [Unit42 blog post](https://unit42.paloaltonetworks.com/domain-shadowing/).


---
layout: post
title: 'Domain Wars: Detecting Stockpiled Domains'
date: '2023-12-18 9:00'
comments: true
tags: ['DNS', 'domain names', 'security', 'cybercrime']
thumbnail-img: "/assets/img/blog/2023/stockpiled-detector/cover.png"
share-img: "/assets/img/blog/2023/stockpiled-detector/cover.png"
permalink: /blog/stockpiled-detector/
---

Cybercriminals register domain names for various malicious and illicit endeavors, including:

* Malware distribution
* Potentially Unwanted Program ([PUP](https://en.wikipedia.org/wiki/Potentially_unwanted_program)) Distribution
* Scams
* Phishing
* Command and Control (C2)
* Hosting illicit adult, gambling and pirated movie websites
* Blackhat Search Engine Optimization (SEO)

Defenders from early on tried to take down these domains or provided solutions to block them. Eventually, the struggle between criminals and defenders turned into the **Domain Wars**. On the one hand, cybercriminals started registering domain names at scale and employed [techniques](https://dl.acm.org/doi/10.1145/3442381.3450071) to make the detection of their domains harder, such as:

* [Aging domain names](https://unit42.paloaltonetworks.com/strategically-aged-domain-detection/) - not using domain names for attacks until they reach a certain age
* Cloaking - where malicious sites present benign content to suspected web crawlers instead of the malicious content.
* User targeting - showing malicious content to a subset of users and vulnerable users who can be tricked.

On the other hand, defenders built increasingly sophisticated apparatus and models to identify malicious domain names. To have a fighting chance in the Domain Wars, various defenders started collaborating, including academic researchers, law enforcement, cybersecurity professionals, policymakers, and volunteers.

Automation employed by attackers to help in operating many domains leaves traces of information about their campaigns in various data sources. Security defenders can find these traces in locations such as [certificate transparency logs](https://certificate.transparency.dev/howctworks/) (e.g., certificate field reputation or timing information) and [passive DNS](https://www.enyo.de/fw/software/dnslogger/first2005-paper.pdf) (pDNS) data (e.g., infrastructure reuse or characteristics). 

Leveraging these crumbs of information, we built a detector to identify stockpiled domains. The two main advantages of detecting stockpiled domains are expanding coverage of malicious domains and providing patient-zero detections as attackers stock up on domains for future use.

To detect stockpiled domains, we engineered over 300 features in six categories. Our feature categories include the following:

* Certificate reputation and aggregation
* Certificate domain aggregation
* Domain name lexical
* Certificate lexical
* pDNS reputation and aggregation
* Combined pDNS and certificate aggregate features

We processed many terabytes of data and billions of pDNS and certificate records to calculate these features. We used a knowledge base of millions of malicious and benign domains to calculate certificate and pDNS reputation and to train and test a random forest machine learning algorithm. Even though not all malicious domains are stockpiled, and not all attackers leave traces of information for us to use, our model has still achieved 99% precision with 48% recall.

As of July 2023, **our detection pipeline has found 1,114,499 unique stockpiled root domain names and identifies tens of thousands of malicious domains weekly.** Our other detectors later classified 5% of the stockpiled domains as malicious, finding 45,862 malware, 8,989 phishing and 844 C2 domains. **Our model, on average, found stockpiled domains 34.4 days earlier compared to vendors on VirusTotal.** We expect the average delay to grow over time as vendors keep finding already identified stockpiled domains. 

The stockpiled detector continuously picks up a wide variety of scam, phishing, malware distribution, C2 and other campaigns. Some of these phishing campaigns target the largest software companies, online retail shops, banks, streaming services, and more. In our [Unit42 article](https://unit42.paloaltonetworks.com/detecting-malicious-stockpiled-domains/), we share both large campaigns leveraging thousands of domains and small campaigns involving just a few domains. 

In a high-yield investment scam campaign, we detected domains more than a month earlier than VirusTotal vendors and detected domains they did not catch. For another campaign, our detector unearthed thousands of domains redirecting to a malicious landing page. The detector discovered a phishing campaign based on the threat actors automatically setting up a certificate used for the domains they owned.

**The success of our approach emphasizes the need to combine multiple large datasets, such as passive DNS and certificate logs, to detect malicious campaigns.**

For more details, see our [Unit42 article](https://unit42.paloaltonetworks.com/detecting-malicious-stockpiled-domains/).

# php hosting: what your PHP app actually needs, and how Sharktech's VPS, cloud, and PaaS plans compare on price

Searching "php hosting" usually means one of two things. Either you're about to launch a PHP site or app and need somewhere to put it, or you're already hosted somewhere and your current setup is slow, restrictive, or both. The annoying part is that "PHP hosting" spans everything from a $2/month shared plan to a cluster of cloud servers, and most articles never explain which one you actually need.

So this guide does two things. First, it breaks down what a PHP environment has to get right — versions, databases, tooling, I/O — because that's what separates a site that loads in 400ms from one that crawls. Second, it looks at how one specific provider, Sharktech, handles PHP workloads across its three product lines: Smart VPS, Public Cloud, and the Cloud Applications Platform (CAP). Sharktech doesn't sell shared hosting at all, which makes it an interesting case for anyone whose PHP project has outgrown the $2/month tier.

## What a PHP environment has to get right

PHP is forgiving, but it's not magic. Whether you're running WordPress, a Laravel app, or a 15-year-old custom codebase, a few things determine whether your hosting works out.

**PHP version support.** WordPress.org currently recommends PHP 8.3 or greater, and modern Laravel versions require PHP 8.x as well. Older PHP 7.4 sites still run, but they're missing real performance gains — PHP 8's JIT and opcache improvements are substantial — and security patches are gone. Whatever you buy, you need the ability to run a current PHP release, and ideally to switch versions without a support ticket.

**Database access.** Almost every PHP app leans on MySQL or MariaDB, some use PostgreSQL or MongoDB. You want unrestricted database access and tools like phpMyAdmin, or the freedom to install your own stack.

**Developer tooling.** SSH access, Git deployment, cron jobs, and a control panel (cPanel or similar) are the baseline for anything beyond a static brochure site. If you're doing real development, staging environments matter too.

**Disk I/O.** This one gets ignored constantly. PHP apps are database-heavy, and databases are random-I/O-heavy. An environment that does 1,000 random IOPS versus 6,000 IOPS is the difference between a WooCommerce checkout that feels instant and one that makes customers leave.

**Security.** Free SSL, firewalls, and — increasingly relevant for PHP sites — actual DDoS protection. WordPress sites get scanned and attacked by bots from day one.

If a host nails those five things, the rest is mostly pricing and scale.

## Three ways to run PHP: shared, VPS, and PaaS

The "php hosting" market really splits into three models, and picking the wrong one is the most common mistake.

**Shared hosting** puts your site on a server with hundreds of others. It's cheap — typical entry plans run $1–4/month — and fully managed, but you get a fixed PHP version (maybe a choice of two), limited resources, and neighbors who can drag your performance down. Fine for one small WordPress site; frustrating for anything real.

**A VPS** gives you a slice of a server with reserved CPU, RAM, and storage, plus root access. You install your own LEMP or LAMP stack, pick any PHP version, run any database, and configure everything exactly how your app wants it. The trade-off: you're the sysadmin. Updates, firewall rules, and security hardening are on you unless you pay for management.

**A PaaS (platform as a service)** sits in between. You push code via Git, the platform builds and runs it in containers, and it scales resources automatically. No server patching, no nginx config files. You pay for what you actually use instead of a fixed monthly allocation.

Sharktech sells the second and third models, plus larger OpenStack-based cloud tiers for apps that need to scale horizontally. It does not sell shared hosting — there is no $2/month plan here, and that's worth knowing before you read further.

## Where Sharktech fits

Sharktech has been around since 2003, operating as its own ISP (AS46844) with direct peering at major internet exchange points. It runs five data centers — Denver, Chicago, Los Angeles, Las Vegas, and Amsterdam — and every product it sells ships with DDoS protection included, which is genuinely unusual at these price points. The company's whole positioning is "flat pricing, no gimmicks," and it serves everyone from hobbyists to game-server companies that get hit with multi-gigabit attacks daily.

For a PHP developer, the relevant details are these: full root access on the VPS line, Proxmox-based virtualization, NVMe storage across the board, and a container-native PaaS that lists PHP among its first-class languages.

## Running PHP on a Smart VPS

Smart VPS is Sharktech's flagship product for individual developers and small teams, and it's the natural home for most PHP projects.

The pricing model is different from typical VPS shops. Instead of picking a fixed "2GB plan," you buy a pool of resources — anywhere from 2 to 128 vCPU cores, 4 to 256 GB of DDR4 RAM, 40 GB to 2 TB of NVMe storage, and 4 to 304 TB of bandwidth on a 1Gbps port — and then you carve that pool into as many virtual machines as you like, deployed in any of the five data centers. One big production VM, or a production VM plus a staging VM plus a scratch VM for experiments. For an agency running client sites, or a Laravel shop that wants isolated dev/staging/prod environments, that's a materially better deal than buying three separate VPS plans.

The entry point is $7.95/month, and the billing-cycle discounts are steep: 25% off quarterly, 35% off semi-annually, and 50% off annually, which brings the entry tier down to an effective $3.98/month. HostAdvice's 2026 review of the service listed tier presets roughly as: 2 cores/4 GB, 4 cores/8 GB, 8 cores/16 GB, 16 cores/32 GB, and 32 cores/64 GB, all starting with 40 GB of NVMe — but since pricing updates live in the configurator as you move the resource sliders, treat the order page as the source of truth: 👉 configure a Smart VPS and see live pricing.

For PHP specifically, here's what you get on the technical side:

- **Any Linux distro** — Ubuntu, Debian, AlmaLinux, and others — so you install exactly the PHP version your app needs, plus whatever extensions (Redis, Imagick, intl, opcache) your stack requires. Windows Server is available via ISO install if you bring your own license.
- **Any database**, including multiple databases on a single instance. No arbitrary provider limits.
- **cPanel available as an option** if you want a familiar control panel instead of pure command-line administration.
- **60 Gbps DDoS protection included** — relevant for PHP sites, since public WordPress endpoints are constant bot targets.
- **A 99.999% uptime platform** built on redundant Proxmox clusters with 40G interconnects, so a hardware failure doesn't take your VM down with it.

Performance-wise, the third-party numbers are strong. HostAdvice's benchmark testing of a Smart VPS instance recorded 6,000+ random IOPS on the NVMe storage (roughly 2–3× what typical budget VPS providers deliver, and directly relevant to database-heavy PHP workloads), about 19 GB/sec of memory throughput, 5.33 Gbps download speed, and sub-millisecond latency to major network infrastructure. Their overall rating landed at 9.3/10, with the explicit caveat that the service assumes you know what you're doing — this is an unmanaged product aimed at people comfortable with SSH.

## Cloud Applications Platform: PHP without the server admin

If the phrase "configure PHP-FPM pool settings" makes you want to close your laptop, Sharktech's Cloud Applications Platform (CAP) is the other path. CAP is a container-based PaaS where PHP is a supported language alongside Java, Python, Node.js, Ruby, Go, and .NET.

You deploy via Git, SVN, or archives, and the platform handles the infrastructure — including one-click deployment of PHP applications like WordPress and Magento, plus MySQL, MariaDB, PostgreSQL, Redis, and MongoDB without manual configuration. Load balancers and application servers are provisioned from the panel, and there's a marketplace of prepackaged applications.

The billing model is the interesting part. Resources are measured in "cloudlets" — each cloudlet is 400 MHz of CPU plus 128 MiB of RAM — assigned to your containers in real time based on actual consumption. You're billed hourly for what your app used, not for limits you set. The platform's sample environment (2 cloudlets, 20 GB storage, 100 GB bandwidth) works out to $0.007/hour, roughly $5/month, and the math favors idle or spiky workloads: if your average CPU use equals 10 cloudlets but your peak RAM equals 12, you're billed for 12, not the sum of 22.

For a low-traffic PHP site or a development environment, that means a running bill near $5/month with zero server administration. For a production app with a marketing-driven traffic spike — a product launch, a viral post — automatic scaling absorbs the spike without you pre-paying for peak capacity. If that sounds like your situation, 👉 check out the Cloud Applications Platform.

## Public Cloud: when one PHP app outgrows a single VPS

The third option is Sharktech's OpenStack-based Public Cloud, which is the choice when you're running high-availability production systems, multi-server architectures, or workloads that need to scale compute and storage independently.

These tiers are bigger and more expensive — starting at $39/month and running up to $499/month — but they include unlimited incoming bandwidth plus 5,000 GB of outgoing (extra egress at $0.002/GB, additional IPv4 addresses at $1.50/month each), and the platform claims 99.999% uptime on hyperconverged, high-availability infrastructure. For a PHP application at genuine scale — a busy e-commerce platform, a SaaS product — this is the tier where you'd land after outgrowing a single VPS. Beyond even this, Sharktech sells bare-metal dedicated servers (listed from around $189/month with the same DDoS protection), colocation, object storage, CDN, and backup services.

## All Sharktech hosting plans at a glance

Here are the compute plans currently shown on Sharktech's order portal, with starting prices and verified product pages. Note that Smart VPS and CAP are billed on their own models — resource pool and pay-per-use respectively — while Public Cloud tiers are conventional monthly plans.

| Plan | Best for | CPU | RAM | Storage | Bandwidth | Starting price | Purchase |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Smart VPS | PHP sites & apps needing root control | 2–128 vCPU (Xeon Gold) | 4–256 GB DDR4 | 40 GB–2 TB NVMe | 4–304 TB, 1Gbps port | $7.95/mo ($3.98/mo on annual billing) | [Configure Smart VPS](https://portal.sharktech.net/index.php?rp=/store/smart-vps-2/smart-vps&aff=1611) |
| Cloud Applications Platform | PHP apps without server admin | Auto-scaled cloudlets (400 MHz + 128 MiB each) | Auto-scaled | Billed as used | Billed as used | ~$5/mo (usage-based, $0.007/hr sample) | [Try CAP](https://portal.sharktech.net/index.php?rp=/store/cloud-applications-platform&aff=1611) |
| Public Cloud – Small | Small production apps, HA hosting | 4–16 vCPU | 8–32 GB | 300–2,400 GB SSD (+HDD/NVMe options) | 20 TB+ (5000 GB outgoing included) | $39/mo | [Order Small](https://portal.sharktech.net/index.php?rp=/store/public-cloud-hosting/public-cloud-hosting-los-angeles-small&aff=1611) |
| Public Cloud – Medium | Growing apps, multiple services | 8–32 vCPU | 16–64 GB | 800–6,400 GB SSD | 20 TB+ | $79/mo | [Order Medium](https://portal.sharktech.net/index.php?rp=/store/public-cloud-hosting/public-cloud-hosting-los-angeles-medium&aff=1611) |
| Public Cloud – Large | High-traffic PHP platforms | 32–128 vCPU | 64–256 GB | 1,500–12,000 GB SSD | 20 TB+ | $249/mo | [Order Large](https://portal.sharktech.net/index.php?rp=/store/public-cloud-hosting/public-cloud-hosting-los-angeles-large&aff=1611) |
| Public Cloud – Enterprise | Large-scale distributed systems | 64+ vCPU | 128+ GB | 5,000+ GB SSD | 20 TB+ | $499/mo | [Order Enterprise](https://portal.sharktech.net/index.php?rp=/store/public-cloud-hosting/public-cloud-hosting-los-angeles-enterprise&aff=1611) |

All tiers include the 60 Gbps DDoS protection, run in your choice of the five data centers (US and Amsterdam), and can be upgraded through the customer portal without redeploying. To compare everything on one page, 👉 browse the full Sharktech plan catalog.

## How to pick between them

The honest answer depends on what you're running and how much server work you want to do.

**One WordPress site, minimal traffic, no interest in sysadmin work.** CAP at roughly $5/month, with one-click WordPress deployment, automatic scaling, and zero patching. This is the closest thing Sharktech has to traditional "php hosting" — managed, simple, cheap at small scale.

**A Laravel/Symfony app, an agency with client sites, or a developer who wants dev/staging/prod isolation.** Smart VPS. Splitting one resource pool into multiple VMs is exactly the right shape for this, you control your exact PHP version and extensions, and the NVMe I/O numbers matter for ORM-heavy apps. The entry point at $3.98/month effective (annual billing) undercuts a lot of shared hosting while delivering dramatically more capability — provided you can handle the Linux administration.

**A production PHP platform with real traffic, compliance needs, or horizontal scaling.** Public Cloud, starting at the Small tier. OpenStack, high availability, and independent scaling of compute and storage are what you want when downtime costs money.

**You just want the cheapest possible WordPress host and nothing else.** Then be honest about it: a $2/month shared plan from a traditional shared host is the right tool, and Sharktech doesn't sell one. HostAdvice's PHP hosting roundup lists entry shared plans from providers like Verpex, IONOS, and Webdock in the $0.59–$4.00/month range. You trade control and performance for price and simplicity — a legitimate trade for a hobby blog.

## The fine print worth knowing

A few things about Sharktech that you should walk in knowing, because they're unusual:

- **No refunds, no free trial.** All payments are non-refundable, including setup fees. Billing errors can be disputed within 30 days for account credit. This is the single biggest reason to size your plan conservatively at first — resources can be upgraded instantly through the portal, so starting small carries no penalty.
- **It's unmanaged.** Nobody is going to update your PHP version or configure your firewall for you on the VPS line. If that's a dealbreaker, use CAP instead, where the platform handles it.
- **Windows costs extra.** Linux distros are free; Windows Server requires bringing your own license or buying one.
- **No residential IPs.** If your use case depends on residential-classified IP addresses (some streaming or scraping scenarios), that's not available here.
- **Payment options are broad.** Cards, PayPal, Alipay, Apple Pay, Google Pay, bank transfers, SEPA, and ACH are all accepted.

Support is real humans on 24/7 ticket — HostAdvice's test got a technically accurate reply in 12 minutes — and the knowledge base covers common administration tasks for both Linux and Windows. Customer reviews on the official site skew toward infrastructure operators, including game-server companies that specifically chose Sharktech for its attack resilience, which tells you something about the customer base this provider has built over two decades.

## Quick FAQ

**Can I run WordPress on Sharktech?** Yes, on either Smart VPS (you install the LEMP/LAMP stack and WordPress yourself, with any PHP version 8.3+ available) or CAP (one-click WordPress deployment, fully managed).

**Is Sharktech good PHP hosting for beginners?** The Smart VPS line assumes comfort with SSH and basic server administration. CAP is the beginner-friendly option. If you've never touched a terminal and don't want to, start with CAP or a traditional shared host.

**How much does the cheapest setup cost?** The Smart VPS entry tier is $7.95/month, or $3.98/month effective with annual billing (50% off). CAP's sample environment runs about $5/month with usage-based billing.

**Can I host multiple PHP sites on one plan?** Yes. On Smart VPS, you can create unlimited VMs from your resource pool, each running its own stack — multiple sites, multiple PHP versions, isolated from each other.

**What if my PHP app gets popular?** Upgrade CPU, RAM, disk, and bandwidth instantly from the customer portal without redeploying, or move up to Public Cloud tiers when you need high-availability infrastructure rather than a single VM.

The short version: "php hosting" stops being a commodity purchase the moment your app needs a specific PHP version, real database performance, or isolated environments. That's the territory where Sharktech's VPS-plus-pool model and its usage-based PaaS make sense — 👉 compare the plans and pricing yourself and see which shape fits your project before committing, because the no-refund policy means the cheap entry tier is the smart first step.

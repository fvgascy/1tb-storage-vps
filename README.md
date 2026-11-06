# 1tb storage vps: real prices, hidden limits, and how to pick one for backups or a media server

A 1TB storage VPS is one of the cheapest ways to park backups, a media library, or a private cloud off your own hardware, and right now the realistic price range is wide: about $3 per month on US monthly plans, or $45 per year on GreenCloud's Storage-1 plan if you're fine committing annually. The catch is that these plans differ a lot in bandwidth, location, refund terms, and what "1TB" actually means once you read the fine print. This piece walks through GreenCloud's current storage lineup, what a year of 1TB really costs, and how it stacks up against InterServer, Contabo, and the annual HDD promos floating around.

> **Quick pick:** most people searching for a 1TB storage VPS want cheap, set-and-forget space for backups, Nextcloud, or a Plex/Jellyfin library. GreenCloud's **Storage-1** (1TB SATA, 2 cores, 3GB RAM, 6TB bandwidth in the US/EU) at **$45/year** fits that brief, and it's one of the few budget storage plans that also comes in Tokyo and Singapore. 👉 [Check GreenCloud's storage plans and current pricing](https://greencloudvps.com/billing/aff.php?aff=6679)

## What a 1TB storage VPS is actually good for

Storage VPS plans trade disk speed for capacity. GreenCloud's storage line runs on enterprise SATA drives in a hardware RAID-10 array behind a 10Gbps port, with KVM virtualization and full root access. That combination is built for sequential reads and writes: rsync or BorgBackup jobs, Restic repositories, Nextcloud or Seafile, cold archives, and media servers.

It is a poor fit for workloads that hammer the disk with small random reads. Databases, busy WordPress sites, and anything latency-sensitive belong on an NVMe plan instead. Contabo says the same thing about its own storage line, and InterServer's product page flat-out recommends its SSD Cloud VPS for high I/O needs. The rule of thumb across every provider in this niche: if your app cares about IOPS, don't buy a big-disk VPS.

One thing worth knowing about GreenCloud's newer storage configurations: the system runs on a small NVMe boot disk (20–60GB depending on the tier) while your data sits on the large SATA array. That split matters in practice. Your OS and applications load fast, and only the bulk data lives on slower disks, which is exactly how a backup or media box gets used.

## GreenCloud's storage VPS plans: the full current lineup

The official storage page currently lists six plans, split into a US/EU group and an APAC group. Same prices, same hardware capacity, half the bandwidth in Asia.

| Plan | Storage | CPU / RAM | Bandwidth | Price | Order |
| --- | --- | --- | --- | --- | --- |
| Storage-0.5TB | 500GB SATA | 1 core / 2GB | 3TB | $25/year | [ Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| Storage-1 | 1024GB SATA | 2 cores / 3GB | 6TB | $45/year | [ Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| Storage-2 | 2048GB SATA | 4 cores / 6GB | 10TB | $80/year | [ Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| StorageAPAC-0.5TB | 500GB SATA | 1 core / 2GB | 1TB | $25/year | [ Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| StorageAPAC-1 | 1024GB SATA | 2 cores / 3GB | 2TB | $45/year | [ Order](https://greencloudvps.com/billing/aff.php?aff=6679) |
| StorageAPAC-2 | 2048GB SATA | 4 cores / 6GB | 4TB | $80/year | [ Order](https://greencloudvps.com/billing/aff.php?aff=6679) |

All plans are Linux-only, come with 1 IPv4 and IPv6, run on a 10Gbps port, and include 24/7 support. US/EU plans are hosted in Phoenix (AZ), Ogden (UT), and Amsterdam; APAC plans run out of Tokyo and Singapore.

GreenCloud also runs a separate **Storage KVM Sale** section in its store with slightly different configurations: NVMe boot disk plus SATA RAID-10 data disk, Virtfusion control panel, and a choice of locations including Tokyo (Softbank and IIJ upstreams), Singapore, Ogden, Staten Island (both EPYC Milan), and Chicago (Xeon Gold). Two things stand out on that page. Stock is thin and lopsided, with several location/tier combinations showing zero availability. And every sale plan carries an explicit note: **"No refund/money back on this plan."** More on why that matters below.

## What a year of 1TB actually costs

The headline number is simple: Storage-1 costs **$45/year**, which works out to $3.75 per month for 1TB. Billing is annual, so there's no monthly option on this line, and there's no published renewal rate that differs from the listed price. What you see is what you pay each year.

The comparison that matters is InterServer's storage VPS, which sells 1TB SATA, 2GB RAM, and 2TB of transfer as a $3/month slice. That's $36 a year, cheaper than GreenCloud, and you can cancel any month. In exchange, GreenCloud's US tier gives you three times the bandwidth (6TB vs 2TB), a choice of Phoenix, Ogden, or Amsterdam instead of three US cities, and the APAC option InterServer simply doesn't have.

Where the real cost differences hide is bandwidth overages. GreenCloud sells extra transfer at **$3/TB/month in the US/EU but $15/TB/month in APAC**, a fivefold gap that reflects actual Asian bandwidth costs. If your backup jobs move multiple terabytes a month, an APAC plan can get expensive quietly. The US/EU plans with 6–10TB included are the safer bet for heavy transfer.

There's also a trap in the expansion math. Extra storage costs **$5/TB/month**, so adding 1TB to a Storage-1 would run $45/year on top of the base plan, for $90/year total. Storage-2 gives you 2TB for $80/year. If you can already see yourself needing 2TB within a year, buy the bigger tier upfront and save $10 a year plus a configuration headache.

## Things to check before you order

This is the part most comparison posts skip, and it's where the actual regret happens.

1. **Refunds are effectively none on storage plans.** GreenCloud's general marketing has advertised a 7-day money-back guarantee, but the current storage sale plans are each marked "No refund/money back on this plan." Treat any storage purchase as final. If you want to test the service first, a cheaper KVM plan or a short trial on the smallest tier is the rational move.

2. **Stock is per location and moves constantly.** On the sale store, combinations like Tokyo Softbank 0.5TB or Singapore DC1 showed zero availability, while Staten Island and Chicago had open slots. If a specific location matters to you, expect to check back or pick an alternative city.

3. **The CPU you get may not match the listing.** A community test of GreenCloud's $168/3-year 4TB storage promo in late 2026 found different actual processors across Tokyo Softbank, Tokyo IIJ, New York, and Singapore nodes, with EPYC Milan nodes clearly outperforming the rest (a Geekbench 5 single-core score of 1003 in New York versus 671 in Singapore). For a backup box this hardly matters. If you plan to transcode video on the same machine, it does.

4. **These are HDD arrays behind a fast port.** One tested node showed sequential reads around 575MB/s on the SATA data disk but only 5.37MB/s in 4K random reads. Great for streaming a movie or syncing an archive, painful for a busy database.

5. **APAC IPs come with caveats.** The same community testing flagged the Tokyo Softbank upstream as having a higher risk of the IP getting blocked in China (changing it costs $2), while the IIJ line came back clean. If you're serving content to mainland-adjacent users, that distinction is worth more than a few dollars of CPU performance.

## How it compares with the other big names

Keeping this to verified, current facts:

- **InterServer** sells storage as $3/month slices (1TB SATA, 2GB RAM, 2TB transfer each), backed by ZFS storage arrays, from three US data centers near New York, Dallas, and Los Angeles. Monthly billing, cancel anytime, managed support included from 4 slices up. It's the flexibility pick, and scaling to 8TB is as simple as buying 8 slices at $24/month.
- **Contabo** is the odd one out: its Storage VPS line is all-SSD, up to 1.4TB, with unlimited traffic under a fair-use policy and 11 locations. Its 1TB tier (6 vCPU, 18GB RAM, 600 Mbit/s port) lists at €14.00 with a lower promo rate shown for the first 24 months. You pay several times more per terabyte than the HDD-based plans, but you get genuine SSD speed and European/Asian locations.
- **DediRock** runs aggressive annual HDD storage promos out of New York (the kind that circulate through LowEndBox), with RAID5 arrays and 1Gbps ports. Prices there undercut almost everyone, but it's a single US location, and the same caveats about HDD performance apply.

The honest summary: GreenCloud isn't the absolute cheapest per terabyte in the US, and InterServer beats it on billing flexibility. Where GreenCloud earns its slot is the combination of annual locked pricing, generous included bandwidth, and Tokyo/Singapore availability at a price the others don't offer. If you specifically need an Asian location for a backup node, the shortlist is basically one item long. 👉 [See GreenCloud's storage plans for Tokyo and Singapore](https://greencloudvps.com/billing/aff.php?aff=6679)

## What actual users and tests say

The reputation picture is genuinely mixed, and it's worth going in with open eyes.

On the positive side, GreenCloud has been operating since 2013, claims over 16,000 active customers across 150+ countries, and has long-term reviewers, including one hosting blog that describes using the company continuously since 2013 and praises its support responsiveness. Its general advertising promises 99.9% network uptime and an average ticket response of around 20 minutes.

On the negative side, a Trustpilot reviewer in 2026 described paying, being asked to switch to cryptocurrency payment, and then having servers suspended without refund. Community testers of the storage promo noted visible overselling on the budget lines and CPU specifications that don't always match the listing. None of this is unusual for a budget host, but it leads to a sensible rule: **don't keep the only copy of anything important on a budget storage VPS.** The whole point of a backup box is redundancy, so keep at least one more copy elsewhere and the worst-case scenario stops being scary.

## Quick answers

**Is 1TB enough for a media server?** For most personal libraries, comfortably. Direct playing and a couple of concurrent streams from HDD storage work fine; heavy 4K transcoding won't, both because of the disks and because these tiers only carry 1–4 cores.

**Can I start small and expand later?** Yes, up to 20TB extra at $5/TB/month, but as shown above, upgrading to the next tier is almost always cheaper than stacking add-ons once you know you'll need the space.

**Will I get my money back if I change my mind?** Assume no. The storage sale plans are explicitly non-refundable, and the safer assumption is that anything in this line is a final purchase.

**Do I need to be technical?** Yes. You get a Linux machine with root access and a Virtfusion panel; setting up rsync, Borg, Nextcloud, or Jellyfin is on you.

## So which one should you buy

If you want month-to-month flexibility and US-only is fine, InterServer's $3 slice does the job and you can walk away any time. If you need SSD speed in Europe, Contabo's storage line is the option, at a correspondingly higher price. If you want a cheap 1TB that renews at the same rate, includes real bandwidth headroom, and can sit in Tokyo or Singapore, GreenCloud's Storage-1 at $45/year is the plan, with Storage-2 at $80/year as the right call the moment 2TB is on the horizon.

Before you click order, two last checks: confirm the location you want actually has stock, and remember the no-refund terms on the storage sale plans. If both look fine, 👉 [order the GreenCloud Storage-1 plan and get your backup node running tonight](https://greencloudvps.com/billing/aff.php?aff=6679).

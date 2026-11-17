# Cheap KVM VPS: What $3–$10 a Month Really Buys, Which Tier Fits Your Workload, and the Renewal Traps to Check Before You Order

A real KVM VPS starts at roughly $3 a month in 2026, and at that price you get 1 or 2 shared vCPUs, 2 to 4 GB of RAM and 30 to 50 GB of SSD or NVMe storage, provided you pay for a year up front. Almost everyone searching for a cheap KVM VPS needs the bottom tier. Moving up to 4 vCPUs and 8 GB is for people who already know why they need it.

RackNerd sells its KVM plans directly through its own client portal, and the live plan list, with the price for each billing term, is on the order page that the links below point to. What follows is about reading a plan list properly: what the headline price covers, where the second-year bill comes from, and how to confirm in three commands that you received a real KVM guest rather than a container.

> **Quick pick:** running one site, a VPN endpoint, a bot, or a handful of Docker containers? Take the smallest plan on the list and put the savings toward off-server backups. 👉 [See RackNerd's current KVM VPS plans and prices](https://bit.ly/RacKnerd)

## What “cheap” means for a KVM VPS right now

The floor is set by annual billing and by slice-based plans, not by the word “cheap” on a landing page. These are entry configurations read from each provider's own site.

| Provider | Entry plan | vCPU / RAM / Disk | Transfer | Price |
| --- | --- | --- | --- | --- |
| InterServer | Linux KVM, 1 slice | 2 GB / 30 GB SSD | 2 TB per slice | $3/mo, monthly billing |
| Ucartz | VPS Lite | 1 vCPU / 4 GB / 50 GB NVMe | Unmetered | $10/mo, or $36/yr |
| Luxvps | Xeon KVM, Frankfurt | 1 vCore / 4 GB / 30 GB NVMe | 5 TB | €4.50/mo |
| Luxvps | EPYC Tiny | 2 vCores / 8 GB / 60 GB NVMe | 10 TB | €6.95/mo |
| Liquid Web | Memory VPS | 1 vCPU / 4 GB / 120 GB | 2 TB | $17/mo |

Read the price column together with the configuration beside it. InterServer's $3 is one slice: 2 GB of RAM, 30 GB of SSD, 2 TB of transfer, billed monthly, and you add slices to grow. Ucartz's $10 buys 4 GB and 50 GB of NVMe with unmetered bandwidth, and drops to $36 for a year, which works out to $3 a month. Luxvps starts at €4.50 for 4 GB and 30 GB of NVMe on a 1 Gbit port with 5 TB of traffic.

The same three letters cover a five-fold price spread. A German host's KVM page, last updated in 2022 and still online, lists 1 vCPU, 2 GB of ECC RAM and 20 GB of RAID SSD at €25 a month. KVM describes how the machine is virtualized, not what it costs, so the label alone tells you nothing about value.

Cross-border price comparisons need one more caution. Luxvps quotes final prices with tax included. Hetzner, Contabo and OVH publish net prices and add your local VAT at checkout, and Contabo renders prices in whichever country's tax rate it detects. Line those numbers up in a single column and you produce a ranking that does not exist. Compare what leaves your bank account.

## Pick the tier by RAM, not by vCPU count

Cheap plans advertise vCPU counts that are shared and bursty, so a “4 vCPU” entry plan is not four dedicated cores. RAM is what you actually run out of, and disk fills up second.

| Workload | RAM | vCPU | Disk |
| --- | --- | --- | --- |
| WireGuard or OpenVPN endpoint, uptime monitor, chat bot | 1 GB | 1 | 20–25 GB |
| One WordPress site with a page cache, small PostgreSQL | 2 GB | 1–2 | 30–40 GB |
| 3–5 Docker containers, CI runner, staging environment | 4 GB | 2 | 50–60 GB |
| A small production app with its database and Redis | 8 GB | 4 | 80–100 GB |
| Windows Server with RDP | 4 GB minimum | 2 | 60 GB |

A 20 GB disk is gone after two container images and a month of logs, and that is the upgrade nobody plans for. If you are within 30% of the RAM figure in the row above yours, buy the larger tier now; migrating later costs an evening.

Windows is its own case. InterServer prices its Windows VPS at $10 a month because it enforces a two-slice minimum, giving 60 GB of storage and 4 TB of transfer, while the Linux slice next to it starts at $3. Plan for that multiplier before you compare Windows hosts.

## Three commands that prove it's a real KVM VPS

Run these after the first SSH login, before you install anything:


systemd-detect-virt
nproc
df -h /


The first should print `kvm`. If it prints `lxc`, `openvz` or `docker`, you have a container sharing the host kernel: no custom kernel, no kernel modules, and some Docker and VPN setups simply will not run. The second prints the vCPU count the guest sees and should match the plan you paid for. The third shows the root filesystem size, which should match the advertised disk.

The other half of KVM is what you can do when SSH stops answering. Ucartz exposes a VNC console through Virtualizor and lets you reinstall the OS from the client area. Luxvps runs its own panel with NoVNC and supports mounting a custom ISO. MaxterHost's SolusVM gives you a serial console, a reinstall button and bandwidth statistics. A plan with no console at all turns a broken fstab into a support ticket and a wait, which is a strange thing to save $2 a month on.

## The first-year price is not the price

Annual billing is where most of the discount sits, and the gap is larger than most people expect. On Ucartz's four plans, paying monthly for a year costs $120, $240, $360 and $480. Paying yearly costs $36, $120, $180 and $240. The saving runs from $84 on the entry plan to $240 on the top one, and Ucartz states that these renew at the same price, which makes year two identical to year one.

Not every host writes that sentence. The common pattern is a discounted first invoice and a renewal at list price, with the difference arriving on month thirteen. Two questions before you pay: what will the second invoice cost, and is the discount tied to the billing term or to the account.

There is a second, subtler trap. A plan advertised at “$3 a month” is usually an annual price divided by twelve, and the monthly option for the same machine costs more. Decide the term first, then compare providers on that term. 👉 [Compare RackNerd's monthly and annual prices side by side](https://bit.ly/RacKnerd)

Luxvps runs its discounts the other way: the listed price is the price, quarterly, six-month and annual terms take up to 15% off at checkout, and the company says it has not raised prices on existing customers since 2022.

## Five things a cheap KVM plan usually leaves out

**DDoS filtering.** Ucartz states plainly that DDoS mitigation is not part of its standard KVM plans and sends game-server customers to a separate product line. Luxvps includes 3.2 Tbit/s of filtering on every plan, backups too. If you are hosting a game server, a public API or anything that has annoyed someone online, read that line before the price line.

**Backups.** On a self-managed plan the backups are yours to make, and Ucartz says so in its SLA. Luxvps bundles four daily backups. Either way, budget storage somewhere else, because a rebuild from scratch costs more than a small object-storage bucket.

**A Windows licence.** Ucartz installs Windows Server as an evaluation edition on its Pro and Elite plans and sells the full licence by ticket. A $3 plan does not include a licence that retails for over $100, and any listing that implies otherwise deserves a second read.

**Managed support.** Free support on cheap plans covers short jobs. Ucartz defines it as best-effort help with tasks of about five minutes: console checks, OS reinstalls, DNS pointing, first-level troubleshooting. Past that, engineer time runs $8 per 15 minutes or $28 an hour. If you cannot fix a broken nginx config at 2 a.m., price that in before choosing.

**A generous refund window.** Ucartz offers 30 days. Luxvps offers 48 hours. Both exclude domain fees and third-party licences. A short window is fine if you test properly on day one; it is not fine if the box sits idle for a week.

## Who each of these actually suits

**InterServer** sells in slices on monthly billing, so you can add or remove CPU, RAM, disk and transfer as a project changes. Best if you refuse to prepay a year, or expect to resize often.

**Ucartz** runs a US datacenter with NVMe and unmetered bandwidth, and puts Windows on the top two tiers. Best if your audience is mostly North American and you move a lot of bytes.

**Luxvps** is in Frankfurt with DDoS filtering and four daily backups included from €4.50. Best for a European audience, or for anything that needs attack filtering by default rather than as an add-on.

**Liquid Web** starts at $17 a month for the memory tier and $22 for the CPU tier, on Dell and Cisco hardware with 24/7 support and a 100% network uptime claim. Best if you would rather pay triple than debug alone.

RackNerd sits in the same bracket as the first three. Take the table above, hold it next to its order page, and compare line by line: RAM per dollar, whether backups and filtering are included, and what the same configuration costs on the term you actually want.

## Before you pay: the checklist

1. The renewal price for the exact term you are buying, not just the first invoice.
2. The datacenter location, plus a ping or download test from where your users are.
3. Whether transfer is metered, unmetered or fair-use, and what the port speed is.
4. Whether DDoS filtering and backups are included, extra, or absent.
5. The refund window and what it excludes.
6. IPv4 included, IPv6 included, and how many of each.
7. Whether the control panel has a console and a self-service OS reinstall.
8. Whether an order can be held for fraud review. Ucartz notes that flagged orders can take 4 to 6 business days, which matters if the server is needed today.

## Which one to take

Running a VPN, a single low-traffic site or a bot? The smallest tier on the list, annual term, with backups stored somewhere else.

Running three to five containers or a small database? 4 GB and 2 vCPUs is the sweet spot, and it is where the price-per-gigabyte stops improving.

Serving users in Europe? Start with a Frankfurt host. Serving North America on a tight budget? Compare the US options first.

Hosting a game server or anything that attracts traffic you did not ask for? Filtering is a requirement, not an upgrade.

Once the machine is up, run `systemd-detect-virt`, `nproc` and `df -h /` before you install a single package. It takes twenty seconds and settles every argument about what you were sold. 👉 [Start with RackNerd's entry KVM plan and check the current term pricing](https://bit.ly/RacKnerd)

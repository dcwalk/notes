By no means complete, this is just some notes about hosted vs. self-hosted email.

# Considerations

Some guide posts and boundaries to keep in mind during research:

 - Keeping everything as Canadian as possible in terms of hosting and residency
 - Low-overhead to avoid administrative load
 - Relatively low-cost per inbox
 - Consideration for potentially high-volume notifications from Mastodon, etc
 
Open questions:

 - How many mailboxes do we expect to need?
 - is webmail good enough (roundcube, horde, etc) or do we expect IMAP?
 - How many team members have email admin experience (postfix, exim. dovecot, ...)?
 
# Two Approaches

## Fully hosted

A full service hosting solution would be the easiest to deal with and require the least skills from the team. It's possible that we already have the service available (namecheap has a decent email offering) which would help keep the number of managed accounts low. The costs would probably be the only major downside, with 20 inboxes/addresses being the in the range of $50/month. Not all hosted email solutions provide the best of account security (e.g. 2FA).

__Pros:__

 - Easy to manage and maintain, relatively non-technical
 - Probably already available from DNS provider
 - My include hosting of other services of interest to CoSocial (NextCloud, Wordpress, etc)
 
__Cons:__

 - A bit more expensive than self-hosted, particularly for a lot of addresses
 - Account security is potentially low for some services.
 - Not all provide DKIM signing
 

## Self Hosted

Self-hosting definitely keeps costs down (could be done with a small droplet/VM) at the expense of increased skills requirements. Initial set up is a bit daunting so we would want a couple of folks with experience. Security is less of a concern in that we would have full control over access and storage. Unfortunately DigitalOcean is reluctant to open port 25, but they might be convinced.

__Pros:__

 - Cheap, about as low-cost as it can get
 - Full control over the tech stack, including DKIM
 
__Cons:__

 - Technically complex, requiring some specialized skills for install and troubleshooting (normal operation is pretty hands-off, though)
 - Only a few hosting providers permit it these days
 
## A Note About Notifications

Since notifications sent from Mastodon (and other ActivityPub apps) can be high-volume at times and prone to bursts, we might consider keeping mailgun or sendgrid for those uses. This is a way to avoid suddenly finding our mail host blocklisted. This is especially true for self-hosting.

## DNS requirements

In either case of managed or self-hosted, the DNS requirements for spam control, etc, are the same. We'll want SPF, DKIM and DMARC.

# Potential Solutions

## Managed/Hosted

### namecheap

Namecheap has the advantage of being a provider that we already use. Their very basic package is about $1 per mailbox with 5GB storage per. This is pretty reasonable but comes with very few bells and whistles. The other packages come out to more like $3 mailbox. All packages have solid 2FA and anti-spam features. Also has wordpress hosting among others. Does not appear to have NextCloud.

Namecheap is US based.

### HostPapa

Affordable email hosting with webmail and IMAP, starting at $1-$2 per mailbox. Their higher packages are basically Google and Microsoft reseller accounts. Nothing to magical here, just basic email. I could not find any 2FA options. Hosted wordpress is an add-on and NwextCloud doesn't seem to be available.

HostPapa is Canadian but I'm not sure we have a choice as to location of mailboxes.

### SilverServers

It's a bit tricky to get pricing, you have to ask. However, SilverServers is a Canadian company with a BC data center and they offer the Zimbra suite for email and office. Not sure if this is really a contender but it's very Canadian at least.

### ProtonMail

It's hard to beat protonmail when it comes to privacy and security. It's Swiss based rather than Canadian but privacy protection is even better there than in Canada. At ~$7 per user, the business accounts are pricey but permit multiple domains. Top of the heap for security and functionality but also top of the heap for pricing.

### Tutanota

Similar features and security as protonmail but German based. ~2.40 Euros per user so still not cheap. 

### Coops

Boris' notes on Canadian tech coops include a couple that have email accounts as part of the service. CanTrust might be the most interesting of the two with NextCloud based sharing and collaboration.

## Self-hosted

There are a couple of recipes for this out there, using Linux or BSD and a collection of related mail transfer and delivery agents. Personally I have years of experience with Postfix+Dovecot with OpenDKIM. The details of each of these recipies are probably too much for this note but can be sorted out based on the skillset of the techops crew.

The biggest barrier to self-hosting is finding a cloud or VPS provider that will permit it. The spammers have ruined all the nice things for the rest of us and many providers simply won't allow it. DigitalOcean, for example, won't open port 25 even if you ask nicely. Vultr will, if you convince them you're a good citizen and AWS will upon request. Once that's sorted, one can host dozens of email accounts without a lot of resource usage.

### Vultr

Vultr isn't specifically Canadian, but they do have a Toronto datacenter. Based on the general requirements for Postfix + Dovecot + Apache/nginx the self-hosted service could be run on a $12 virtual server. 

### Digital Ocean

DO has become more reluctant to open enail ports in recent years. If your account is more that 60 days old and has been well-behaved they should grant the request, however. A $12 droplet is a good start for a dozen or so accounts.

### Ovhcloud

Ovh has port 25 open by default, but all their VPSs are in the US. A ~$15 virtual server could handle a mailserver easily.

### TurnKey Internet

A small-ish provider that has port 25 open by default. Their one datacenter is in NY. A ~$20 virutal server would do the trick.

### AWS 

Obviously a US company but they do have datacenters in Canada for hosting EC2. Email restrictions can be lifted upon request. EC2 instances that could run the mail service will range in the $25-$35 per month, half that with reserved pricing.

### Azure

Similar to AWS in pricing and restrictions.  They are a little tougher on port 25 requests, though.

### Linode

Linode started blocking email ports in 2019 but will open them upon request if you provide some details about your intended use. ~$12 virtual server would do for a start and a ~$24 virtual server would handle a large load.

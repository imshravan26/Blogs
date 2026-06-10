---
title: "How DNS Resolution works?"
seoDescription: "Learn how DNS translates domain names into IP addresses, the role of DNS servers, and how to inspect queries using the dig tool"
datePublished: 2026-02-05T07:29:15.389Z
cuid: cml94yc8t000y02l30u8t3vyo
slug: how-dns-resolution-works
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1770276492688/64ac79f5-97fd-462e-91d0-c3649a8fa4e9.png
tags: dns, dns-records, dns-resolver, dns-resolution

---

## What is DNS?

The Domain Name System (DNS) is the phonebook of the internet. We can access information online through domain names, like google.com or netflix.com. Web browsers interact through IP addresses. DNS’s job is to translate the domain names to ip addresses.

Each device connected to the internet has a unique ip address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770275058703/6a14aaf1-748f-46da-a389-511c4c82276b.png align="center")

## What is Dig?

Dig is command line dns quering tool that allows you diagnose and inspect the dns resolution.

## How does this DNS resolution works?

The process of DNS resolution involves converting a hostname (google.com) into computer-friendly IP address (142.251.222.78).

Inorder to understand the process behind the DNS resolution, it’s important to learn about the different hardware components a DNS query must passes between.

### These are the 4 DNS servers involved in loading a webpage:

1. **DNS Recursor:** The recursor is a server who receives queries from client machines through application such as web browsers. Typically recursor is then responsible for making additional request in order to satisfy the client’s DNS query.
    
2. **Root nameserver:** The root server is the first step translating human readable host names into IP addresses.
    
3. **TLD Nameserver:** This nameserver is the next step in the search for a specific IP address, and it hosts the last portion of a hostname (In google.com, the TLD server is “com“).
    
4. **Authoritative nameserver:** The authoritative nameserver is the last stop in the nameserver query. If the authoritative name server has access to the requested record, it will return the IP address for the requested hostname back to the DNS Recursor that made the initial request.
    
5. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770275084057/22ee4eba-300a-41d6-95bc-6c925771dc20.png align="center")
    

## How to use dig tool to inspect the DNS query?

DNS resolution happens step by step.

Each dig command below represents **one stage** of the DNS hierarchy that a recursive resolver walks through.

### Step 1: Start at the root

```bash
dig . NS
```

This query lists all the root names.

It looks something like this

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770270355243/521cff16-6c7d-4114-912a-eab48dfd7e5b.png align="center")

### Step 2: Move to the TLD layer

```bash
dig com NS
```

This query asks:

> Who manages .com domains?

TLD nameservers stores ip addresses of authorative nameservers.

### Step 3: Reach the authorative name server

```bash
dig google.com NS
```

This query returns the authorative name servers for google.com

These servers are the **source of truth** for the domain and are allowed to give final answers.

### Step 4: Get the final answer

```bash
dig google.com
```

This query returns the IP address for `google.com`

## What NS Records Represent and Why They Matter

**NS (Name Server) records define authority in DNS.**  
They specify **which name servers are responsible for a domain** and are allowed to provide DNS answers for it.

For example, the NS records of [`google.com`](http://google.com) indicate which servers are authoritative for that domain.

### What NS Records Represent

* They do **not** store IP addresses
    
* They define **who can answer DNS queries** for a domain
    
* They enable DNS to be **delegated layer by layer**
    

In simple terms:

> NS records tell DNS *where to ask next*.

### Why NS Records Matter

* **Delegation:** Root and TLD servers use NS records to delegate control without centralization
    
* **Trust:** Only authoritative servers listed in NS records are accepted as valid sources
    
* **Scalability:** DNS can scale globally by distributing responsibility across domains
    
* **Redundancy:** Multiple NS records improve availability and fault tolerance
    

### System Design Insight

DNS works because **authority is separated from resolution**.  
NS records define authority, while resolvers use that information to fetch actual records like `A` or `AAAA`.

Without NS records, DNS would have no reliable way to determine **which answers are valid**.

## How Recursive Resolvers Use This Information Behind the Scenes

When a user queries a domain, the system does **not** contact root or TLD servers directly.  
Instead, a **recursive resolver** (ISP DNS or public DNS like Google/Cloudflare) does the work.

Behind the scenes, the resolver:

1. Checks its **cache** for an existing answer
    
2. If missing, queries **root servers** to find the TLD
    
3. Queries **TLD servers** to find authoritative servers
    
4. Queries the **authoritative server** for the final record
    
5. Caches the result using the TTL value
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770275273789/014ac7f0-a2b8-4229-a22e-4719934cff74.png align="center")

## Connecting `dig` [`google.com`](http://google.com) to Real-World Browser Requests

Running:

```bash
dig google.com
```

shows the **final result** of DNS resolution — the IP address.

In a real browser:

1. The browser asks the OS for DNS resolution
    
2. The OS queries a recursive resolver
    
3. The resolver returns an IP address
    
4. The browser opens a TCP connection to that IP
    
5. TLS handshake and HTTP request follow
    

DNS resolution ends **before** any web request is sent.
# DNS Cheat Sheet

A comprehensive guide to DNS (Domain Name System), covering its main components and providing in-depth descriptions and examples.

---

## DNS Overview
- **DNS (Domain Name System)**: Translates domain names (like `example.com`) into IP addresses for computers. It’s a distributed database system that operates hierarchically.

---

## DNS Components

1. **Domain Names**
    - **Root Domain**: The highest level in the DNS hierarchy, represented as a dot (`.`).
    - **Top-Level Domain (TLD)**: Next level, such as `.com`, `.org`, or country codes like `.uk`.
    - **Second-Level Domain (SLD)**: Directly below the TLD, such as `example` in `example.com`.
    - **Subdomain**: Optional components added before the SLD, such as `www` in `www.example.com`.

2. **DNS Zones**
    - **Zone**: A segment of the DNS namespace managed by an authoritative server, containing records for all domains and subdomains under a specific domain.

---

## DNS Records

DNS records are entries in a DNS zone that map domain names to IP addresses or provide additional information. Here are the most common DNS records:

### 1. Start of Authority (SOA) Record
- **Description**: Defines the primary DNS server for a domain, sets administrative properties, and contains important information like the domain’s serial number, refresh interval, and retry timing.
- **Format**: SOA records have several fields: Primary NS, Hostmaster Email, Serial Number, Refresh, Retry, Expire, and Minimum TTL.
- **Example**:
  ```plaintext
  example.com.    IN SOA   ns1.example.com. admin.example.com. (
                      2023101001 ; Serial number
                      86400      ; Refresh (1 day)
                      7200       ; Retry (2 hours)
                      3600000    ; Expire (6 weeks)
                      300 )      ; Minimum TTL (5 minutes)
  ```
- **Explanation**:
    - **Primary NS**: Main name server for the domain (`ns1.example.com.`).
    - **Hostmaster Email**: Email of the domain administrator (`admin@example.com`).
    - **Serial Number**: Unique number incremented with each DNS change.
    - **Refresh, Retry, Expire, Minimum TTL**: Set timing intervals for DNS synchronization.

### 2. A Record
- **Description**: Maps a domain name to an IPv4 address.
- **Format**: `<Domain Name> IN A <IPv4 Address>`
- **Example**:
  ```plaintext
  example.com.    IN A     192.0.2.1
  www.example.com IN A     192.0.2.1
  ```
- **Explanation**: Maps `example.com` to IP `192.0.2.1`. Subdomains (e.g., `www`) can have their own `A` records or share the main IP.

### 3. AAAA Record
- **Description**: Maps a domain name to an IPv6 address.
- **Format**: `<Domain Name> IN AAAA <IPv6 Address>`
- **Example**:
  ```plaintext
  example.com.    IN AAAA  2001:0db8:85a3:0000:0000:8a2e:0370:7334
  ```
- **Explanation**: Allows for IPv6 support, mapping `example.com` to an IPv6 address.

### 4. CNAME Record
- **Description**: Canonical Name Record; maps an alias to another domain name.
- **Format**: `<Alias> IN CNAME <Canonical Domain>`
- **Example**:
  ```plaintext
  blog.example.com. IN CNAME www.example.com.
  ```
- **Explanation**: Redirects `blog.example.com` to `www.example.com`. `CNAME` records cannot coexist with other records for the same domain.

### 5. MX (Mail Exchange) Record
- **Description**: Specifies the mail server responsible for receiving emails for a domain.
- **Format**: `<Domain Name> IN MX <Priority> <Mail Server>`
- **Example**:
  ```plaintext
  example.com. IN MX 10 mail1.example.com.
  example.com. IN MX 20 mail2.example.com.
  ```
- **Explanation**: Email is first directed to the server with the lowest priority value (`10`). `mail2.example.com` is a backup.

### 6. TXT Record
- **Description**: Stores text data for various purposes, often for email verification, security protocols, and general notes.
- **Format**: `<Domain Name> IN TXT "<Text Data>"`
- **Example**:
  ```plaintext
  example.com. IN TXT "v=spf1 ip4:192.0.2.1 -all"
  ```
- **Explanation**: This TXT record is used for Sender Policy Framework (SPF) to define which IPs can send mail for `example.com`.

### 7. NS (Name Server) Record
- **Description**: Specifies the authoritative name servers for a domain.
- **Format**: `<Domain Name> IN NS <Name Server>`
- **Example**:
  ```plaintext
  example.com. IN NS ns1.example.com.
  example.com. IN NS ns2.example.com.
  ```
- **Explanation**: Directs queries to `ns1.example.com` and `ns2.example.com` for authoritative responses.

### 8. PTR (Pointer) Record
- **Description**: Used in reverse DNS lookups, mapping an IP address to a domain name.
- **Format**: `<Reversed IP>.in-addr.arpa. IN PTR <Domain Name>`
- **Example**:
  ```plaintext
  1.2.0.192.in-addr.arpa. IN PTR example.com.
  ```
- **Explanation**: Maps `192.0.2.1` back to `example.com`, useful for identifying IP origin in logs.

### 9. SRV (Service) Record
- **Description**: Defines the location of servers for specific services.
- **Format**: `<Service>.<Protocol>.<Domain> IN SRV <Priority> <Weight> <Port> <Target>`
- **Example**:
  ```plaintext
  _sip._tcp.example.com. IN SRV 10 60 5060 sipserver.example.com.
  ```
- **Explanation**: Used for VoIP, mapping the SIP service (`_sip._tcp`) to `sipserver.example.com`.

---

## DNS Process

1. **DNS Query**: The client (e.g., a browser) requests the IP address for `example.com`.
2. **DNS Resolver**: Queries the DNS hierarchy until it reaches the authoritative name server for the domain.
3. **Response**: The authoritative server responds with the requested records (e.g., `A`, `MX`).

---

## Example DNS Zone File

A zone file consolidates the DNS records for a domain and typically includes:

```plaintext
$TTL 86400
@    IN SOA ns1.example.com. admin.example.com. (
           2023101001 ; Serial
           3600       ; Refresh
           900        ; Retry
           1209600    ; Expire
           86400 )    ; Minimum TTL

     IN NS   ns1.example.com.
     IN NS   ns2.example.com.

example.com.     IN A     192.0.2.1
www              IN CNAME example.com.
mail             IN A     192.0.2.2
                 IN MX    10 mail.example.com.

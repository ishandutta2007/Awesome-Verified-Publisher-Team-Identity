# Awesome-Verified-Publisher-Team-Identity

# Awesome Verified Publisher & Team Identity

> A curated list of top Verified Publisher and Team Identity platforms — both SaaS/Hosted commercial verification services and open-source alternatives for establishing organizational identity, domain ownership, and publisher trust.  
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [GitHub Verified Organization](#github-verified-organization)
  - [Postman Domain Verification](#postman-domain-verification)
  - [X Verified Organizations](#x-verified-organizations)
  - [Trustpilot Business Verification](#trustpilot-business-verification)
  - [Dun & Bradstreet D-U-N-S](#dun--bradstreet-d-u-n-s)
  - [Sectigo EV SSL Validation](#sectigo-ev-ssl-validation)
- [Open-Source Software](#-open-source-software)
  - [Keybase](#keybase)
  - [DIAP (Decentralized Intelligent Agent Protocol)](#diap-decentralized-intelligent-agent-protocol)
  - [domainverifier (Go)](#domainverifier-go)
  - [OpenID Connect (OIDC) Trusted Publishing](#openid-connect-oidc-trusted-publishing)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Verified Publisher and Team Identity platforms. These are not open-source but are included as reference points for feature comparison.

### GitHub Verified Organization
**Type:** Domain-based organization verification  
GitHub allows organization owners to verify domain ownership by adding a DNS TXT record. Once verified, a "Verified" badge displays on the organization's profile, and email notifications can be restricted to verified domains . The process requires access to modify DNS records; verification may take up to 72 hours to propagate. If the organization's website and email use different domains (or variants), both must be verified for the badge to appear . Enterprise accounts can also approve domains across owned organizations.  
**Best for:** Open-source projects and organizations wanting a visible trust signal on GitHub without additional vendor relationships.

### Postman Domain Verification
**Type:** Domain ownership verification for team management  
Postman offers domain verification on Team and Enterprise plans (contact support to enable). Verified domains enable domain capture (Enterprise + Advanced Security Administration add-on), which consolidates all user accounts matching the domain into a single team . Prerequisites include SSO with SAML, disabling alternative auth methods, and adding a domain or subdomain. SCIM provisioning is recommended for onboarding. Domain users who are not yet team members appear with masked email addresses unless a CSV of known emails is uploaded to unmask them .  
**Best for:** Enterprise organizations needing to consolidate shadow Postman accounts and enforce team membership by email domain.

### X Verified Organizations
**Type:** Paid organizational verification with affiliate badges  
X (formerly Twitter) offers Verified Organizations with gold checkmarks for businesses and grey checkmarks for government/multilateral organizations . Eligibility requires a matching active X account, a current organization email address, and a current website domain. Once approved, organizations can add affiliated accounts, which receive affiliation badges linking them to the verified organization . The verification does not involve independent identity proofing — it is a paid subscription tied to domain/email matching and manual review.  
**Best for:** Brands and organizations wanting a visible verification signal and affiliate management on X.

### Trustpilot Business Verification
**Type:** Business identity verification for review platforms  
Trustpilot verifies business information to display a transparency badge on company profiles. Automatic verification occurs through domain name ownership and bank account registration during signup . Additional verification options include uploading a government-issued ID for an admin (passports from all countries; select ID cards/driver's licenses per country) and syncing a verified Google Business Profile for contact details . At least one verified item is required to display the "Verified additional business information" badge .  
**Best for:** Businesses wanting to build consumer trust on Trustpilot through verified identity signals.

### Dun & Bradstreet D-U-N-S
**Type:** Global business identifier and verification  
The D-U-N-S Number is a unique nine-digit identifier for businesses, widely used in procurement, trade, and compliance. Verification is performed through Dun & Bradstreet's portal, where businesses can search for an existing D-U-N-S, request a new one, or update associated information . It is frequently required for government contracting, international trade, and as a prerequisite for EV SSL certificate validation (Sectigo lists the D-U-N-S Number as a required field for EV validation) .  
**Best for:** Organizations needing a globally recognized business identity credential for B2B trust and regulatory requirements.

### Sectigo EV SSL Validation
**Type:** Extended Validation certificate identity verification  
Extended Validation (EV) SSL certificates require rigorous organizational verification beyond domain validation. Sectigo's EV validation collects the organization's legal name, DBA name, address, D-U-N-S Number, company registration number, jurisdiction and date of incorporation, business category, and contract signer details . A validation specialist reviews the submitted details and may contact the authorized representative for additional verification . Once validated, domains delegated to the organization become eligible for EV certificates.  
**Best for:** Organizations wanting the highest level of SSL trust indication (browser-verified identity) for customer-facing services.

---

## 🟩 Open-Source Software

Self-hosted, community-driven identity verification and proof-based systems. The open-source ecosystem for publisher verification is fragmented; these projects address identity proofs, decentralized identifiers, and domain verification at the protocol or library level.

### Keybase
**Stack:** Go / JavaScript | **License:** BSD-3-Clause (open-source client)  
Keybase provides cryptographic identity verification by linking social media accounts (Twitter, Reddit, Hacker News, GitHub), websites, and PGP keys to a single profile . Proofs are published publicly and verified by the client, not just the server — for example, a Twitter proof is checked by confirming the tweet exists at the claimed URL . Team invites can be based on these proofs, and the global Merkle tree ensures that only the Keybase username needs to be exchanged out-of-band to confirm identity . Phone and email invites use Trust On First Use (TOFU) with single-use enforcement in the sigchain . Keybase was acquired by Zoom in 2020, but the client remains open-source.  
**Best for:** Individuals and teams wanting cryptographic, proof-based identity verification across multiple platforms without relying on a centralized authority.

### DIAP (Decentralized Intelligent Agent Protocol)
**Stack:** Python / TypeScript / Rust | **License:** Open Source (per SDK)  
A protocol and multi-language SDK for decentralized identity management and agent authentication using zero-knowledge proofs. Implements W3C `did:key` (Ed25519) identifiers, real BN128 Schnorr ZK proofs, IPFS/IPNS integration, and P2P networking via iroh/libp2p . Provides key management, DID document creation, and identity registration with ZKP verification. SDKs are available for Python, TypeScript, and Rust with cross-language interoperability.  
**Best for:** Developers building decentralized identity systems or AI agent authentication where zero-knowledge proofs and W3C DIDs are required.

### domainverifier (Go)
**Stack:** Go | **License:** Open Source (per project)  
A small Go library for domain name ownership verification. It provides programmatic verification of domain control, likely via DNS TXT record checks similar to how GitHub and other platforms verify domains . With 29 stars and 3 forks, it is a lightweight building block rather than a full platform.  
**Best for:** Go developers building internal tools that need to verify domain ownership programmatically.

### OpenID Connect (OIDC) Trusted Publishing
**Stack:** Protocol / various implementations | **License:** Open Standard  
OIDC Trusted Publishing allows services (like GitHub Actions, GitLab CI) to provably identify themselves to third parties without long-lived secrets. PyPI's implementation is a reference example: it verifies OIDC tokens from GitHub/GitLab, matches claims against configured Trusted Publishers, and issues short-lived (15-minute) API tokens . PyPI checks the `repository_owner_id` claim to prevent "account resurrection attacks" where a freed username could be taken over . This pattern is increasingly adopted for package registry publishing and can be adapted for other publisher verification use cases.  
**Best for:** Package registries and platforms wanting to verify publisher identity through CI/CD providers without shared secrets.

---

## 📊 Comparison at a Glance

| Software | License | Type | Verification Method | Open-Source | Best For |
|----------|---------|------|---------------------|-------------|----------|
| **GitHub Verified Org** | Proprietary | Domain verification | DNS TXT record | ❌ | GitHub organization trust badge |
| **Postman Domain Verification** | Proprietary | Domain verification | DNS + support enablement | ❌ | Consolidating team accounts |
| **X Verified Organizations** | Proprietary | Paid organizational verification | Email/domain match + review | ❌ | X brand verification + affiliates |
| **Trustpilot** | Proprietary | Business verification | Domain, bank, ID, Google Business | ❌ | Review platform trust badge |
| **D&B D-U-N-S** | Proprietary | Business identifier | D&B portal verification | ❌ | Global B2B identity credential |
| **Sectigo EV SSL** | Proprietary | Organizational validation | Document + specialist review | ❌ | Browser-verified SSL identity |
| **Keybase** | BSD-3 (client) | Cryptographic identity proofs | Social proofs + PGP + website | ✅ (client) | Multi-platform identity linking |
| **DIAP** | Open Source | Decentralized identity + ZKP | W3C DID + zero-knowledge proofs | ✅ | Agent/DID identity systems |
| **domainverifier** | Open Source | Domain verification library | DNS TXT (likely) | ✅ | Go programmatic domain checks |
| **OIDC Trusted Publishing** | Open Standard | CI publisher identity | OIDC token claims | ✅ (implementations) | Package registry publishing |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Verified Publisher or Team Identity tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem for **organizational publisher verification** is very limited; most verification services are centralized commercial platforms. Open-source efforts tend to focus on **decentralized identity** (Keybase, DIAP) or **protocol-level publisher authentication** (OIDC Trusted Publishing) rather than direct alternatives to D-U-N-S or EV SSL.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐

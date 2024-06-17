# Understanding Certificate Chains: A Simple Guide

Certificate chains are a key part of internet security. But what are they, and how do they work? This guide will explain it all in simple terms to make the concept clearer.

# Table of Contents
  - [Why This Guide?](#why-this-guide)
  - [What is a Certificate Chain?](#what-is-a-certificate-chain)
    - [Certificate Chain Example in real-world scenario](#certificate-chain-example-in-real-world-scenario)
  - [Why Should You Understand Certificate Chains?](#why-should-you-understand-certificate-chains)
  - [Components of a Certificate Chain](#components-of-a-certificate-chain)
  - [How Certificate Chains Work](#how-certificate-chains-work)
  - [Where are These Certificates?](#where-are-these-certificates)
  - [Real World Examples of where Certificate Chains are used](#real-world-examples-of-where-certificate-chains-are-used)
  - [How to check a certificate chain](#how-to-check-a-certificate-chain)
  - [Certificate Chain Structure](#certificate-chain-structure)
  - [Creating a Certificate Chain from Scratch](#creating-a-certificate-chain-from-scratch)
    - [Step 1: Choose a Certificate Authority (CA)](#step-1-choose-a-certificate-authority-ca)
    - [Step 2: Generate a Certificate Signing Request (CSR)](#step-2-generate-a-certificate-signing-request-csr)
    - [Step 3: Submit the CSR to the CA](#step-3-submit-the-csr-to-the-ca)
    - [Step 4: Install the Certificate](#step-4-install-the-certificate)
    - [Step 5: Configure Your Server to Use the Certificate](#step-5-configure-your-server-to-use-the-certificate)
    - [Step 6: Test Your Configuration](#step-6-test-your-configuration)
    - [Step 7: Monitor and Renew Your Certificate](#step-7-monitor-and-renew-your-certificate)
  - [Managing Certificate Chains in the Cloud](#managing-certificate-chains-in-the-cloud)
    - [AWS Certificate Manager (ACM)](#aws-certificate-manager-acm)
    - [Google Cloud Certificate Authority Service (CAS)](#google-cloud-certificate-authority-service-cas)
    - [Azure Key Vault](#azure-key-vault)
  - [Conclusion](#conclusion)

## Why This Guide?

You may be thinking there are many articles out there, why I should bother with this guide?
Firstly, this article stands out for its simplicity and clarity. It aims to demystify the concept of certificate chains by providing easy-to-understand explanations and an example. Furthermore, if you are a developer or like GitHub having it in a repository would be a good idea and quick way to get this information from your command line or via your IDE code tools like Visual Studio code for example. Plus, it's a document that will stay in Github and guaranteed that won't go anywhere that can be edited by you or anyone or the community to ensure it stays updated and relevant.

## What is a Certificate Chain?

A certificate chain is a sequence of certificates, where each certificate in the chain is signed by the subsequent certificate, all the way up to a trusted root certificate. This chain of trust is fundamental to the security of SSL/TLS connections.

### Certificate Chain Example in real-world scenario

Imagine you're receiving a letter. You trust the letter because you recognize the sender's signature. But what if you don't recognize the signature? The letter might include a note from a mutual friend, saying "I vouch for this person." Now you trust the letter, because you trust your friend.

A certificate chain works in a similar way for websites:

1. **End-Entity Certificate**: This is like the letter. It's a file that a website sends to your browser.
2. **Intermediate Certificate**: This is like the note from your friend. It's another file that says "you can trust the end-entity certificate." There might be several of these.
3. **Root Certificate**: This is like recognizing a signature. It's a file that your browser already trusts. If the root certificate trusts the intermediate certificate, and the intermediate certificate trusts the end-entity certificate, then your browser trusts the website.

**Summary**: A certificate chain is a series of certificates that establish trust from a trusted root certificate to the end-entity certificate.

## Why Should You Understand Certificate Chains?

Understanding certificate chains is crucial for anyone involved in web development or IT, as they are a fundamental part of internet security. 

- **Trust**: Certificate chains establish trust on the internet. They allow your browser to confirm a website is what it claims to be, protecting you from malicious sites.
- **Encryption**: They are also key to establishing encrypted connections (HTTPS), protecting sensitive data in transit from eavesdroppers and attackers.
- **Debugging**: If you're a developer or an IT professional, understanding certificate chains can help you debug issues with SSL/TLS, such as when a website's SSL certificate isn't trusted.
- **Knowledge**: As a user, understanding certificate chains can help you make informed decisions about the security of the websites you visit.

**Summary**: Certificate chains are essential for establishing trust, enabling encryption, debugging issues, and making informed security decisions.

## Components of a Certificate Chain
As mentioned earlier in the real-world scenario, here are their components and explanations.

1. **Root Certificate**: This is a self-signed certificate that's trusted by the system. It's issued by a Certificate Authority (CA) and is stored in the system's trust store.
2. **Intermediate Certificates**: These are certificates that are issued by the root CA or another intermediate CA. They're used to sign other intermediate certificates or end-entity certificates. This creates a chain of trust from the root certificate to the end-entity certificate.
3. **End-Entity Certificate**: This is the certificate that's presented to the client (e.g., a web browser). It's signed by an intermediate CA. The client verifies this certificate by checking the signatures of all the certificates in the chain, up to the root certificate.

**Summary**: A certificate chain consists of a root certificate, intermediate certificates, and an end-entity certificate.

## How Certificate Chains Work

When a client (like a web browser) connects to a server over SSL/TLS, the server presents its end-entity certificate to the client. The client then verifies this certificate by checking its signature against the public key of the issuer's certificate. This process is repeated for each certificate in the chain, up to the root certificate.

If the client trusts the root certificate, and if all signatures in the chain are valid, then the client trusts the end-entity certificate. This means that the client trusts the identity of the server and can establish a secure connection.

**Summary**: The client verifies each certificate in the chain up to the root certificate to establish a secure connection.

## Where are These Certificates?

The location of these certificates depends on your operating system:

- **Windows**: Certificates are stored in the Certificate Store, which you can manage by running `certmgr.msc`.
- **macOS**: Certificates are stored in Keychain Access, which you can find in your Utilities folder.
- **Linux**: The location can vary, but certificates are often found in `/etc/ssl/certs`.

The end-entity and intermediate certificates are usually sent by the website you're visiting. Your browser then checks them against the root certificates it already trusts.

**Summary**: Certificates are stored in different locations depending on the operating system, and browsers check them against trusted root certificates.

## Real World Examples of where Certificate Chains are used

Here are some examples of where certificate chains are used:

- **Websites**: When you visit a website over HTTPS, your browser uses a certificate chain to verify the website's identity.
- **Email**: Email clients use certificate chains to verify the identity of email servers when sending and receiving mail over secure connections.
- **Apps**: Mobile and desktop apps use certificate chains to establish secure connections to backend servers.

**Summary**: Certificate chains are used in websites, email, and apps to establish secure connections.

## How to check a certificate chain

You can check a certificate chain using tools like `openssl`. For example, you can use the following command to check the details of a certificate:

```bash
openssl x509 -in /path/to/your/certificate.cert -text -noout
```

You can also check an online certificate chain using `openssl`. For example, you can use the following command to check the details of a certificate from a website:

```bash
echo | openssl s_client -servername hostname -connect host:port 2>/dev/null | openssl x509 -noout -text
```

Replace `hostname` with the name of the server and `host:port` with the host and port number of the server you want to check.

You can check a website's certificate chain using your web browser's developer tools or just by going to the web browser address bar pad lock icon. Here's how you can do it in Chrome using web developer tools:

1. Visit the website.
2. Open the Developer Tools (press F12).
3. Click on the "Security" tab.
4. Click on "View certificate".

This will show you the certificate chain for the website.

**Summary**: Use tools like `openssl` or web browser to check a certificate chain.

## Certificate Chain Structure
Here's a folder-like structure to represent how a certificate chain works:

```bash
Root Certificate (Trusted by the browser)
└── Intermediate Certificate 1 (Signed by Root Certificate)
    └── Intermediate Certificate 2 (Signed by Intermediate Certificate 1)
        └── End-Entity Certificate (Your Website's Certificate, signed by Intermediate Certificate 2)
```

**Summary**: A certificate chain is structured hierarchically from the root certificate to the end-entity certificate.

## Creating a Certificate Chain from Scratch

Creating a certificate chain in a real-world scenario involves several steps, including choosing a Certificate Authority (CA), generating a Certificate Signing Request (CSR), submitting the CSR to the CA, installing the issued certificate, and configuring your server to use the certificate. Here's a step-by-step guide:

### Step 1: Choose a Certificate Authority (CA)

Decide whether to use a public CA (like Let's Encrypt, DigiCert, etc.) or create your own private CA. Public CAs are trusted by most devices and browsers out of the box, while private CAs are typically used for internal purposes within an organization.

### Step 2: Generate a Certificate Signing Request (CSR)

This involves creating a private key and a CSR that includes your details like domain name, organization, country, etc. The private key should be kept secret.

```bash
# Generate a private key
openssl genpkey -algorithm RSA -out yourdomain.key

# Generate the CSR
openssl req -new -key yourdomain.key -out yourdomain.csr
```

### Step 3: Submit the CSR to the CA

The CA will validate your identity and your control over the domain you're requesting the certificate for. This process varies depending on the CA and the type of certificate you're requesting.

### Step 4: Install the Certificate

Once the CA has issued your certificate, you need to install it on your server along with any intermediate certificates provided by the CA.

### Step 5: Configure Your Server to Use the Certificate

This involves updating your server's configuration to use the new certificate and private key for SSL/TLS connections. The exact steps depend on your server software.

### Step 6: Test Your Configuration

You should test your server's SSL/TLS configuration to ensure everything is set up correctly. There are online tools available for this, such as the SSL Server Test by Qualys SSL Labs.

### Step 7: Monitor and Renew Your Certificate

SSL/TLS certificates have an expiration date and need to be renewed periodically. Many CAs offer tools or services to automate this process.

**Summary**: Creating a certificate chain involves choosing a CA, generating a CSR, submitting it, installing the certificate, configuring the server, testing, and monitoring.

## Managing Certificate Chains in the Cloud
Creating a Certificate Chain involves a lot of complicated steps, isn't it? In the cloud, the process of managing SSL/TLS certificates and certificate chains is similar, but cloud service providers often offer additional tools and services to make the process easier. Here are some examples:

### AWS Certificate Manager (ACM)

This service from Amazon Web Services (AWS) lets you easily provision, manage, and deploy public and private SSL/TLS certificates for use with AWS services and your internal connected resources. ACM handles the complexity of creating and managing public SSL/TLS certificates.

### Google Cloud Certificate Authority Service (CAS)

This is a highly available, scalable Google Cloud service that simplifies and automates the management and deployment of private Certificate Authority (CA).

### Azure Key Vault

This service from Microsoft Azure allows you to manage and control cryptographic keys and other secrets used by cloud apps and services. It can also be used to manage SSL/TLS certificates.

**Summary**: Cloud providers offer tools to simplify the management of SSL/TLS certificates and certificate chains.

## Conclusion

Certificate chains are a fundamental part of internet security. They're how your browser knows it can trust a website. So the next time you see a padlock in your address bar, you'll know there's a certificate chain working behind the scenes to keep your connection secure.

**Summary**: Certificate chains establish trust and secure connections on the internet.

## Contributing

Spotted a mistake or missing info in this guide? Don't be shy! Raise an issue or better yet, fork this repo and raise a PR. Your contributions help make this guide better for everyone.

## Sharing is Caring

You're welcome to share, clone, fork, or bookmark this content. All we ask is that you give credit where it's due :)

"# Understanding Certificate Chains: A Simple Guide" by Nicanor II Flavier, used under CC BY 4.0. To view the original material, visit https://github.com/nicanorflavier/ssl-certificate-chain-guide

## Contact

If you have any questions or suggestions, feel free to reach out. You can find my contact details on my GitHub profile https://github.com/nicanorflavier
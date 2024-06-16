
# Hosting a Static Website on AWS Using S3, Route 53, CloudFront, and a Namecheap Domain

## Introduction
This guide will walk you through the process of setting up and hosting a static website on AWS. The domain will be purchased through Namecheap, and the hosting will utilize Amazon S3, Route 53, and CloudFront services. 

## Prerequisites
1. A registered domain name (this guide uses Namecheap, but any registrar will work).
2. An AWS account.

## Step-by-Step Instructions

### Step 1: Domain Purchase
1. Purchase a domain name through Namecheap or any other domain registrar.

### Step 2: AWS Certificate Manager (ACM)
1. **Log in to AWS Management Console**.
2. **Navigate to Certificate Manager**.
3. **Request a Public Certificate**:
    - Ensure your region is set to **North Virginia** (us-east-1).
    - Click on **Request a Certificate**.
    - Enter your domain name (e.g., `example.com`) and a wildcard domain (`*.example.com`) to cover all subdomains.
    - Select **DNS Validation** and click **Next**.
    - Review and click **Confirm and Request**.
4. **Validate the Domain**:
    - Go to your domain registrar (Namecheap).
    - Navigate to **Advanced DNS Settings**.
    - Create a **CNAME** record for the DNS validation provided by AWS.
    - Wait for the status in AWS to change to **Issued**.

### Step 3: Configure Route 53
1. **Navigate to Route 53** in the AWS Management Console.
2. **Create a Hosted Zone**:
    - Click on **Create Hosted Zone**.
    - Enter your domain name (e.g., `example.com`) and click **Create**.
3. **Update Namecheap DNS Settings**:
    - Go back to Namecheap.
    - Update the **Name Servers** to the ones provided by Route 53.

### Step 4: Create S3 Buckets
1. **Navigate to S3** in the AWS Management Console.
2. **Create Two Buckets**:
    - One for the root domain (`example.com`).
    - One for the `www` subdomain (`www.example.com`).
3. **Configure Root Domain Bucket**:
    - Enable **Static Website Hosting**.
    - Set the **Index Document** to `index.html`.
    - Upload your website files to this bucket.
4. **Configure www Bucket**:
    - Enable **Static Website Hosting**.
    - Set it to **Redirect requests** to `https://example.com`.

### Step 5: Set Up CloudFront
1. **Navigate to CloudFront** in the AWS Management Console.
2. **Create a CloudFront Distribution**:
    - Set the **Origin Domain Name** to the S3 bucket for your root domain.
    - Enable **OAI (Origin Access Identity)** and update the bucket policy.
    - Redirect HTTP to HTTPS.
    - Add your domain names (`example.com` and `www.example.com`) under **Alternate Domain Names (CNAMEs)**.
    - Select the SSL certificate from ACM.
3. **Create a Second Origin**:
    - Use the S3 **Bucket Website Endpoint** for your root domain as the origin domain.

### Step 6: Update Route 53 Records
1. **Go to Route 53** in the AWS Management Console.
2. **Create Four Records**:
    - **A Record** for `example.com` pointing to the CloudFront distribution.
    - **AAAA Record** for `example.com` pointing to the CloudFront distribution (for IPv6).
    - **A Record** for `www.example.com` pointing to the CloudFront distribution.
    - **AAAA Record** for `www.example.com` pointing to the CloudFront distribution (for IPv6).

### Step 7: Verify and Test
1. **Wait for DNS Propagation** (can take up to 48 hours).
2. **Test your Website**:
    - Open a browser and navigate to `https://example.com` and `https://www.example.com`.
    - Verify that both addresses correctly display your website and that `www` redirects to the root domain.

## Conclusion
By following these steps, you will have a static website hosted on AWS, using S3 for storage, CloudFront for CDN, and Route 53 for DNS management. The domain purchased from Namecheap will be fully integrated and functional.

---

*This guide is based on a detailed walkthrough provided in a YouTube video tutorial, ensuring all steps are covered for setting up a static website on AWS with a Namecheap domain.*

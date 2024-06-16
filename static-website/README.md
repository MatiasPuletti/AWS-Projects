# AWS-Projects

# Redirect NameCheap Domain to AWS Route 53 and Configure NameServers

## Prerequisites

- AWS Account
- NameCheap Account

## Steps

### 1. AWS Console Setup

1. **Login to AWS Console:**

   - If you don’t have an account, sign up.
   - If you have an account, sign in.
   - Bookmark frequently used services for easier access.

2. **Route 53 Setup:**

   - Go to Route 53 service.
   - Click on `Hosted Zones`.
   - Click on `Create Hosted Zone`.
   - Enter your domain name.
   - Optionally, add a description.
   - Click `Create`.

3. **View Name Servers:**
   - Note the NS (Name Server) records provided by Route 53 for your domain.

### 2. Certificate Manager Setup

1. **Open Certificate Manager:**

   - Ensure you are in the North Virginia region.

2. **Request a Certificate:**

   - Click on `Request a certificate`.
   - Enter your domain name.
   - Optionally, add a wildcard domain (e.g., `*.yourdomain.com` for future subdomains).
   - Click `Request`.

3. **Validate the Certificate:**

   - Refresh the page to see the validation status.
   - Copy the CNAME record starting from the underscore `_` to your domain name.
   - In NameCheap, create a CNAME record with the copied value.

4. **Check Validation:**
   - Wait a few minutes and refresh until the certificate status shows as issued.

### 3. DNS Record Setup in Route 53

1. **Create CNAME Records:**

   - Go back to Route 53.
   - Create a new record set for your domain.
   - Choose CNAME as the record type.
   - Enter the value copied from the certificate validation.

2. **Create Redirect Records:**
   - Create another record set for `www.yourdomain.com`.
   - Select CNAME and point it to your domain (e.g., `yourdomain.com`).

### 4. Update NameCheap Name Servers

1. **Update NS Records in NameCheap:**
   - Log in to NameCheap.
   - Navigate to your domain's `Advanced DNS` settings.
   - Create NS records for each name server provided by Route 53.
   - There should be four NS records, each with the `www` prefix and the corresponding name server.

### 5. Final Steps

- Ensure all records are correctly configured in both Route 53 and NameCheap.
- Verify that your domain is properly redirected and SSL certificates are validated.

### Next Steps

- In the next part of the project, we will set up an S3 bucket for hosting HTML files and configure CloudFront distribution.

---

## Additional Resources

- [AWS Route 53 Documentation](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)
- [AWS Certificate Manager Documentation](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)
- [NameCheap DNS Settings Guide](https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-do-i-set-up-dns-records-for-my-domain)

# Static-website-Hosting-using-cloud
Static Website Hosting using S3 and CloudFront
📌 Project Overview
This project demonstrates a production-ready method for hosting a high-performance, secure static website on AWS. Instead of using standard S3 public website hosting, this architecture leverages Amazon CloudFront for global content delivery and Origin Access Control (OAC) for enhanced security. This setup ensures low latency for users worldwide and protects the origin (S3) from unauthorized access.

🏗️ Architecture Diagram
(Paste the Mermaid diagram image you generated earlier here)

🛠️ AWS Services Used
Amazon S3: Used as the storage origin for static assets (HTML, CSS, JS, images).

Amazon CloudFront: Used as the Content Delivery Network (CDN) to cache content at edge locations.

AWS IAM (OAC): Implemented Origin Access Control to restrict S3 access only to CloudFront.

Amazon Route 53 (Optional): Used for DNS management and custom domain mapping.

AWS Certificate Manager (Optional): Used to provide SSL/TLS certificates for HTTPS.

🔒 Security Implementation
The core of this project is the "Least Privilege" security model:

Private S3 Bucket: All public access to the S3 bucket is blocked. The bucket is not accessible via a URL.

Origin Access Control (OAC): A specialized AWS security principal that allows CloudFront to authenticate with S3.

S3 Bucket Policy: A JSON policy was applied to the bucket that explicitly allows only my CloudFront distribution’s ARN to perform s3:GetObject actions.

Encrypted Transit: Configured "Redirect HTTP to HTTPS" to ensure all data is encrypted.

🚀 Implementation Steps
S3 Configuration: Created a bucket with unique naming and disabled all public access. Uploaded the portfolio source code.

CDN Setup: Configured a CloudFront distribution with the S3 bucket as the origin.

OAC Deployment: Created a new Origin Access Control setting and attached the generated policy to the S3 bucket.

Error Handling: Created custom error responses (403/404) pointing to error.html to improve user experience.

Cache Optimization: Configured a default root object (index.html) to ensure the home page loads at the base URL.

📈 Performance & Cost Optimization
Performance: By using CloudFront, the Time to First Byte (TTFB) was reduced significantly as content is served from the nearest AWS Edge Location.

Cost: Leveraging the AWS Free Tier, this architecture costs nearly $0/month. S3 storage (under 5GB) and CloudFront data transfer (under 1TB) are covered, making this a highly cost-efficient professional solution.

🧠 Challenges & Learnings
Challenge: Encountered a 403 Access Denied error when first accessing the CloudFront URL.

Solution: Identified that the "Default Root Object" was not set. CloudFront didn't know which file to serve at the root level. Manually setting it to index.html resolved the issue.

Learning: Gained a deep understanding of IAM Policies and how different AWS services communicate securely through Service Principals.

🔗 Live Website
Deployment URL: https://your-unique-id.cloudfront.net

GitHub Repository: https://github.com/your-username/your-repo-name

💬 Interview Questions Covered
Why use CloudFront instead of just S3 Web Hosting? (Answer: Security, HTTPS support, and Global Latency reduction).

How does OAC differ from OAI? (Answer: OAC is the newer standard supporting more security features like SSE-KMS).

How do you update the site without waiting for the cache to expire? (Answer: By creating a CloudFront Invalidation).

🔮 Future Enhancements
[ ] CI/CD Pipeline: Automating deployments using GitHub Actions.

[ ] Security Headers: Using CloudFront Functions to add security headers like HSTS and XSS-Protection.

[ ] CloudWatch Monitoring: Setting up billing alarms and traffic monitoring.



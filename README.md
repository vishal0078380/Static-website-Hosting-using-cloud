# Static Website Hosting using S3 and CloudFront

## 📌 Project Overview
This project demonstrates a **production-ready AWS architecture** for hosting a **high-performance and secure static website**.

Instead of using standard **public S3 static website hosting**, this setup uses:
- **Amazon CloudFront** for global content delivery
- **Origin Access Control (OAC)** for secure private access to S3

This ensures:
- 🌍 Low latency worldwide
- 🔐 Strong security with zero public S3 access
- ⚡ HTTPS by default

---

## 🏗️ Architecture Diagram
<img width="1983" height="1360" alt="image" src="https://github.com/user-attachments/assets/31d1b145-2788-415c-b0e5-d4a3bafe6ef9" />


---

## 🛠️ AWS Services Used

### **Amazon S3**
- Stores static assets (HTML, CSS, JavaScript, images)
- Bucket is **private** (no public access)

### **Amazon CloudFront**
- Acts as a CDN
- Caches content at global edge locations
- Handles HTTPS and SSL termination

### **AWS IAM – Origin Access Control (OAC)**
- Allows CloudFront to securely access the private S3 bucket
- Replaces the older OAI mechanism

### **Amazon Route 53 (Optional)**
- DNS management
- Custom domain mapping

### **AWS Certificate Manager (Optional)**
- Provides SSL/TLS certificates for HTTPS

---

## 🔒 Security Implementation

This project follows the **Least Privilege Principle**:

- **Private S3 Bucket**
  - All public access is blocked
  - Bucket cannot be accessed directly via URL

- **Origin Access Control (OAC)**
  - CloudFront signs requests before accessing S3

- **S3 Bucket Policy**
  - Allows `s3:GetObject` **only** from the CloudFront distribution ARN

- **Encrypted Transit**
  - HTTP traffic is automatically redirected to HTTPS

---

## 🚀 Implementation Steps

1. **S3 Configuration**
   - Created a uniquely named bucket
   - Disabled all public access
   - Uploaded static website files

2. **CloudFront Setup**
   - Created a distribution
   - Configured S3 as the origin

3. **OAC Deployment**
   - Created an Origin Access Control
   - Attached generated bucket policy

4. **Error Handling**
   - Configured custom 403 and 404 pages (`error.html`)

5. **Cache Optimization**
   - Set `index.html` as the default root object

---

## 📈 Performance & Cost Optimization

### **Performance**
- Reduced **Time to First Byte (TTFB)**
- Content served from nearest AWS Edge Location

### **Cost**
- Runs almost **$0/month** under AWS Free Tier
- S3 (<5GB) + CloudFront (<1TB transfer)

---

## 🧠 Challenges & Learnings

### **Issue**
- Encountered `403 Access Denied` on CloudFront URL

### **Root Cause**
- Default Root Object was not configured

### **Fix**
- Set `index.html` as Default Root Object

### **Key Learning**
- Deep understanding of IAM policies and service-to-service authentication

---

## 🔗 Live Website

- **CloudFront URL**:  
  https://your-unique-id.cloudfront.net

- **GitHub Repository**:  
  https://github.com/your-username/your-repo-name

---

## 💬 Interview Questions Covered

**Why CloudFront instead of S3 Web Hosting?**  
- Better security, HTTPS support, and global low latency

**OAC vs OAI?**  
- OAC is the modern approach with improved security and flexibility

**How to update content instantly?**  
- Use **CloudFront Cache Invalidation**

---

## 🔮 Future Enhancements

- [ ] CI/CD Pipeline using GitHub Actions  
- [ ] Security headers via CloudFront Functions  
- [ ] CloudWatch monitoring & billing alarms  

---

### ⭐ This project reflects real-world AWS production practices and is resume & interview ready.

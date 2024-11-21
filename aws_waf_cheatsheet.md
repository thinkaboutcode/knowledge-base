# Overview of AWS WAF

AWS WAF (Web Application Firewall) is a cloud-based security service that protects web applications from common web exploits and vulnerabilities that could affect application availability, compromise security, or consume excessive resources. AWS WAF helps you filter and monitor HTTP/S requests according to rules you define. It is typically used to protect web applications hosted on Amazon CloudFront, Application Load Balancer (ALB), API Gateway, or AWS App Runner.

---

## Key Features of AWS WAF:
1. **Customizable Rules:** Define your own rules to allow or block specific traffic based on IP addresses, HTTP headers, URIs, query strings, and other request attributes.
2. **Predefined Managed Rules:** Use managed rule groups provided by AWS or third-party vendors, which include common protections like SQL injection and cross-site scripting (XSS).
3. **Real-time Visibility:** Monitor incoming requests and observe blocked/allowed requests in real time.
4. **Integration with Other AWS Services:** Seamlessly integrates with CloudFront, ALB, and API Gateway for easy deployment.
5. **Scalability:** Automatically scales with your application's traffic volume without manual intervention.

---

## What are OWASP Rules?

OWASP (Open Web Application Security Project) rules refer to guidelines and practices to prevent web application vulnerabilities. The OWASP Top 10 is a list of the most critical web application security risks, including:
- SQL Injection
- Cross-Site Scripting (XSS)
- Broken Authentication
- Security Misconfiguration
- Sensitive Data Exposure
- Cross-Site Request Forgery (CSRF)

AWS WAF provides a **Managed Rule Group** for OWASP Top 10, which can protect your application against these common vulnerabilities without requiring you to define complex rules.

---

## Using OWASP Rules in AWS WAF

AWS WAF offers managed rule groups based on the OWASP Top 10 through **AWS Marketplace** or as part of **AWS Managed Rules**. These are preconfigured rules that you can enable to provide protection with minimal setup.

### Steps to Use OWASP Rules in AWS WAF:

1. **Set Up AWS WAF**:
    - Open the [AWS WAF Console](https://console.aws.amazon.com/wafv2/).
    - Create a Web ACL (Access Control List) to associate with your application.

2. **Associate Your Web ACL**:
    - Link the Web ACL to your CloudFront distribution, ALB, or API Gateway.

3. **Add OWASP Managed Rule Groups**:
    - In the "Rules" section of your Web ACL, click **Add Rules** and choose **Add managed rule groups**.
    - Select the **AWS-AWSManagedRulesCommonRuleSet** or **AWS-AWSManagedRulesSQLiRuleSet**, which include OWASP protections.

4. **Customize Rules (Optional)**:
    - Exclude specific rules or rule groups if they interfere with your application.
    - For example, if your application has a legitimate pattern that resembles a SQL injection, you can disable the SQL Injection rule for specific URIs.

5. **Test Your Rules**:
    - Set rules to "Count" mode first, which logs requests that would have been blocked, without actually blocking them.
    - Review the logs in **AWS CloudWatch Logs** to ensure no false positives.

6. **Enable Full Blocking**:
    - Once testing is complete and you're satisfied with the results, switch the rules to **Block** mode.

---

## Example: Configuring OWASP Managed Rules in AWS WAF

1. **Create Web ACL**:
    - Navigate to AWS WAF Console → "Web ACLs" → **Create Web ACL**.
    - Provide a name, and select the resource type (e.g., CloudFront or ALB).

2. **Add Managed Rule Groups**:
    - Click **Add Managed Rule Groups** → Select **AWS-AWSManagedRulesCommonRuleSet**.
    - Add other relevant managed rule groups, like SQL Injection (AWS-AWSManagedRulesSQLiRuleSet) or XSS (AWS-AWSManagedRulesXSSRuleSet).

3. **Test and Monitor**:
    - Set the rule action to "Count" to test traffic patterns.
    - Monitor **CloudWatch Metrics** and Logs.

4. **Deploy with Block Mode**:
    - Switch the rule action to "Block" for production deployment.

---

## Example OWASP Rules in AWS Managed Rule Groups

| **Rule Group**                         | **Purpose**                                                                 |
|----------------------------------------|-----------------------------------------------------------------------------|
| AWS-AWSManagedRulesCommonRuleSet       | Protects against OWASP Top 10 risks like SQLi, XSS, and CSRF.               |
| AWS-AWSManagedRulesSQLiRuleSet         | Detects and blocks SQL Injection attacks.                                   |
| AWS-AWSManagedRulesXSSRuleSet          | Detects and blocks Cross-Site Scripting (XSS) attacks.                      |
| AWS-AWSManagedRulesAdminProtectionRuleSet | Protects against common admin panel exploits.                              |
| AWS-AWSManagedRulesKnownBadInputsRuleSet | Blocks requests containing bad inputs that match known malicious patterns. |

---

By leveraging AWS Managed Rule Groups, you can effectively secure your web applications against OWASP risks with minimal configuration.

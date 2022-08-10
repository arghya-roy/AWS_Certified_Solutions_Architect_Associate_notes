## AWS WAF – Web Application Firewall
- Protects your web applications from common web exploits (Layer 7)
- Layer 7 is HTTP (vs Layer 4 is TCP)
- Deploy on 
     - Application Load Balancer
     - API Gateway
     - CloudFront
- Define Web ACL (Web Access Control List):
- Rules can include: IP addresses, HTTP headers, HTTP body, or URI strings
- Protects from common attack
     - SQL injection 
     - Cross-Site Scripting (XSS)
     - OS command injection attacks
     - DDoS attacks ( layer 7 )
- Size constraints, geo-match (block countries)
- Rate-based rules (to count occurrences of events) – for DDoS protection
- AWS WAF composed of 
   - Web ACL ( Access control list )
   - Web ACL capacity unit ( WCU )
   - Rules ( custom rule / aws managed rule / marketplace rule )
   - Rules Group
- At first we have to create Web ACL, inside Web ACL we can create rule group or rule.
- The maximum capacity for a web ACL ( WCU ) is 1,500. Every rule has specific wcu value. After adding many rules the WCU will be maximum 1,500 . You can ask amazon to increate the WCU quota.

## Example of WAF Rule -
### Anonymous IP list
This group contains rules that allow you to block requests from services that allow obfuscation of viewer identity. This can include request originating from VPN, proxies, Tor nodes, and hosting providers (including AWS). This is useful if you want to filter out viewers that may be trying to hide their identity from your application. Now you can deny or allow access from those Anonymous IP list.


### AWS Shield vs AWS WAF about DDOS

- Sheild standard protect from ddos in layer 3 and 4. Shield advanced protects against layer 3, 4, 7.
- But AWS WAF protects from ddos in layer 7 only. ( additional AWS WAF protects from SQL injection attacks, Cross-site scripting attacks, OS command injection attacks also )
- WAF mainly works only on layer 7

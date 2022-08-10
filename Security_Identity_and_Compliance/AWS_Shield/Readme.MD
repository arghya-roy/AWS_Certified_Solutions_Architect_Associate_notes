## AWS Shield
- Protect against ddos attack.
### AWS Shield Standard:
- Free service that is activated for every AWS customer
- Provides protection from ddos attacks (such as SYN/UDP Floods - layer 4 transport, Reflection attacks - layrt 3 network ) on layer 3 ( network ) and layer 4 (transport) attacks.
- Dont have 24/7 access to AWS DDoS response team (DRP)
- It monitors network flow.
### AWS Shield Advanced:
- Optional DDoS mitigation service ($3,000 per month per organization)
- - It monitors network flow.
- Protect against more sophisticated and large attack on Amazon EC2, Elastic Load Balancing (ELB), Amazon CloudFront, AWS Global Accelerator, and Route 53
- 24/7 access to AWS DDoS response team (DRP)
- Protect against higher fees during usage spikes due to DDoS
- Provides protection from ddos attacks (such as SYN/UDP Floods - layer 4 transport, Reflection attacks - layrt 3 network, HTTPS flood and dns query flood - application layer 7 ) on layer 3 ( network ) and layer 4 (transport)and layer 7 ( application ) attacks.
- Include WAF in free of cost.
- need 1 year subscription commitment.

### AWS Shield vs AWS WAF about DDOS

- Sheild standard protect from ddos in layer 3 and 4. Shield advanced protects against layer 3, 4, 7.
- But AWS WAF protects from ddos in layer 7 only. ( additional AWS WAF protects from SQL injection attacks, Cross-site scripting attacks, OS command injection attacks also )
- WAF mainly works only on layer 7

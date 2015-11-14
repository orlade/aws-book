## IAM Certificates

HTTPS, SSL and TLS make the Web secure, which is an incredible feat. To secure your own app, you need to install an SSL certificate. Certificates cost between $50 and $400 per year, but you can test your setup with a free one. The terminology is complicated, but you only have to do it once a year.

The AWS documentation has a [good explanation of setting up SSL certificates][elbssl] for use with the [Elastic Load Balancer (ELB)](../ec2/elastic-load-balancers.md), which is what we'll be doing. It's quite an arcane process, so follow it very carefully step by step.

## Vendors

There are many businesses selling SSL certificates, but you should only purchase from one you trust. [Comodo][comodo] and [RapidSSL][rapidssl] both have good reputations. RapidSSL is slightly cheaper, but Comodo offers a 90-day free certificate for testing your setup.

A certificate for a single domain should cost $50-100. A wildcard certificate can be used for unlimited subdomains, but costs about four times more. Thus a wildcard certificate may be more cost effective if you plan to have more than four independent applications.

## What should I do?

Start with a [free 90-day SSL certificate from Comodo][comodo-free]. Follow the instructions of both [Comodo][comodo-free] and [AWS][elbssl].

[elbssl]: https://docs.aws.amazon.com/ElasticLoadBalancing/latest/DeveloperGuide/ssl-server-cert.html
[comodo]: https://www.comodo.com/
[comodo-free]: https://www.instantssl.com/free-ssl-certificate.html
[rapidssl]: https://www.rapidssl.com/

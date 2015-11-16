# Static Website Hosting

A **static website** does exactly one job: *serve static content*. Static content doesn't change depending on which user requested it or what arguments were provided, it is just files (like images, HTML, CSS, JavaScript, etc.).

Static websites cannot perform any server­-side logic, such as running databases or logging into
user accounts. This limitation also makes static websites extremely simple, cheap and fast. Additional functionality can still be added with third-party JavaScript libraries (such as comments with [​Disqus​][disqus] or external databases with [Firebase​][firebase]).

## Content Creation

Ultimately your website will be serving HTML documents. You probably don't want to write these by hand. Instead, you can:

* Use a WYSIWYG tool to build your site and output HTML (such as [Dreamweaver][dweaver] or [Mercury][mercury]).
* Use a static site generator which combines templating with Markdown for writing content.

Programmers (including myself) will tend to prefer the latter, so of the static site generators:

* [Jekyll][jekyll] is the most popular, with many themes and plugins. It's easy to use, and a good choice for building a blog (see also [Octopress][octo]). It's also [natively supported by GitHub Pages][pages-jekyll] (see below).
* [Wintersmith][wsmith] is similar, but based on [Node.js][node] and [Jade][jade] templates.
* [Hugo][hugo] is simpler but the design is cleaner and generation is way faster.


## Hosting with S3

S3 is great for [hosting static websites][s3docs] (see [​Example: Setting Up a Static Website Using a Custom Domain​][tute] for a detailed walkthrough). In summary:

1. Create two S3 buckets named after your domain, one with and one without the ​`www` subdomain (prefix).
1. Set the root domain bucket to forward all requests to the `www`-prefixed domain.
  * The walkthrough does this the other way around, but using `www` as the "canonical" name is [considered good practice][bare].
3. For the `www`-prefixed bucket:
  * Enable static hosting with index document set to ​ index.html
  * In bucket permissions, add a public read access policy to the bucket
  * Upload a file called ​ index.html ​ with some content to test
4. In the domain's DNS provider create a record set pointing each of the bucket's names to the respective bucket's endpoint.
  * In [AWS Route 53](../infrastructure/route53/index.md), this can be done for each bucket with an `A` Record and an `ALIAS` to the bucket's endpoint.

The S3 Web app is no good for deployment. Instead, there is a tool called [​s3_website​][s3website] which checks a destination bucket and uploads any new or changed files. [Follow the instructions in the repository][s3website] to get it up and running.


## Hosting with GitHub Pages

[GitHub Pages][pages] is a GitHub service that publishes Git repositories as static websites.

Deployment is simple: just use Git to commit and push files to a special `gh-pages` branch. GitHub will serve those same files under [a subdomain of `github.io`][subdomain].

As with S3, you can [create a `CNAME` or `ALIAS` record with your DNS provider to point a custom subdomain at your GitHub Pages site][alias]. (Note that using a `CNAME` record requires a special `CNAME` file in the repository.)

GitHub Pages works with both public and private repositories, but the content published from private repositories will be public.


## What should I do?

Unless you have a reason not to, I suggest using Jekyll because it's easy and popular, and S3 to keep everything within AWS.

1. Install [Jekyll][jekyll] and create a new project:

  ```sh
$ gem install jekyll
$ jekyll new my-awesome-site
$ cd my-awesome-site
$ jekyll serve
   ```
1. Edit your content until you're happy with how it looks locally.
1. Follow the above instructions for "Hosting with S3".
1. Install [​s3_website​][s3website].
1. Run `s3_website config` and configure it with your S3 details.
1. Push your Jekyll output to S3 with `s3_website push`.
1. Visit the website to check it out.


[disqus]: https://disqus.com/home/
[firebase]: https://www.firebase.com/
[s3docs]: https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html
[tute]: https://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html
[bare]: https://faq.nearlyfreespeech.net/section/domainnameservice/baredomain#baredomain
[dweaver]: https://www.adobe.com/au/products/dreamweaver.html
[mercury]: https://jejacks0n.github.io/mercury/
[jekyll]: https://jekyllrb.com/
[octo]: http://octopress.org/
[pages-jekyll]: https://help.github.com/articles/using-jekyll-with-pages/
[wsmith]: http://wintersmith.io/
[hugo]: http://gohugo.io/[]
[node]: https://nodejs.org/en/
[jade]: http://jade-lang.com/
[pages]:https://pages.github.com/
[alias]: https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/
[subdomain]: https://help.github.com/articles/about-custom-domains-for-github-pages-sites/#how-github-pages-sites-use-custom-domains
[s3website]: https://github.com/laurilehmijoki/s3_website

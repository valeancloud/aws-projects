<div>

# From SquareSpace to AWS: How I Fully Migrated My Business Website and Domain {#from-squarespace-to-aws-how-i-fully-migrated-my-business-website-and-domain .p-name}

</div>

::: {.section .p-summary field="subtitle"}
Recently, I decided it was time to take full control of my small
business website for Harvest Vending Co. While Squarespace was a
great...
:::

::: {.section .e-content field="body"}
::: {#eec1 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### From SquareSpace to AWS: How I Fully Migrated My Business Website and Domain {#8074 .graf .graf--h3 .graf--leading .graf--title name="8074"}

Recently, I decided it was time to take full control of my small
business website for Harvest Vending Co. While Squarespace was a great
place to start with its built-in templates and hosting, I wanted more
flexibility, better performance, and tighter integration with AWS
services. So, I migrated everything --- DNS, static site hosting, SSL,
and CDN --- over to AWS.

This post walks you through exactly how I did it, including the mistakes
I ran into and how I fixed them.

### Starting Point: Domain Registered on Squarespace {#4e80 .graf .graf--h3 .graf-after--p name="4e80"}

I originally registered the domain **harvestvendingco.com** through
Squarespace. The email, website, and basic DNS settings were managed
through their dashboard. I had Google Workspace for business email tied
to the domain too.

I wanted to move to AWS so I could:

-   [Host a static website using S3]{#ec53}
-   [Use CloudFront as a CDN]{#6558}
-   [Secure the site with HTTPS using ACM]{#7967}
-   [Manage DNS through Route 53]{#449c}

The biggest roadblock? Squarespace locks domain transfers for 60 days
after registration. So instead of transferring the domain, I updated the
nameservers to point to Route 53. This way, I could move DNS control to
AWS immediately without waiting.

### Step 1: Hosting the Static Site on S3 {#6535 .graf .graf--h3 .graf-after--p name="6535"}

I created a public S3 bucket named
[**www.harvestvendingco.com**](http://www.harvestvendingco.com){.markup--anchor
.markup--p-anchor data-href="http://www.harvestvendingco.com"
rel="noopener" target="_blank"} and enabled static website hosting. I
uploaded my custom `index.html`{.markup--code .markup--p-code}, images,
and assets.

To build the HTML site, I used **Visual Studio Code** to write and edit
the `index.html`{.markup--code .markup--p-code} file and styled it with
basic CSS. I added the content, structured the layout, and inserted
images that represented our vending machines and services. Once it
looked right locally, I zipped and uploaded the files into the S3
bucket.

<figure id="4ccb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*v7E0rz92IzEN40xp6BGU-Q.png"
class="graf-image" data-image-id="1*v7E0rz92IzEN40xp6BGU-Q.png"
data-width="2378" data-height="996" data-is-featured="true" />
</figure>

<figure id="fa0f" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*9bNH_TdOyqxA44pgMkgHFQ.png"
class="graf-image" data-image-id="1*9bNH_TdOyqxA44pgMkgHFQ.png"
data-width="2612" data-height="974" />
</figure>

I also updated the **bucket policy** to allow public read access, which
is required for web browsers to view the static site files. Without
this, you'd just get an "Access Denied" error.

Here's a simplified version of the policy I used:

``` {#4e4a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="json"}
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::www.harvestvendingco.com/*"
    }
  ]
}
```

I tested the S3 static site URL and saw my website load perfectly. It
wasn't secure yet, and didn't use my custom domain --- but that came
next.

### Step 2: Requesting an SSL Certificate in ACM {#20be .graf .graf--h3 .graf-after--p name="20be"}

CloudFront requires the SSL certificate to be in **us-east-1**, so I
made sure to switch to the N. Virginia region in AWS.

I requested a public SSL certificate for
[**www.harvestvendingco.com**](http://www.harvestvendingco.com){.markup--anchor
.markup--p-anchor data-href="http://www.harvestvendingco.com"
rel="noopener" target="_blank"} in ACM. To validate ownership, I had to
add a CNAME record to my DNS. Since DNS was still on Squarespace at the
time, I added it there. Once ACM validated the domain, the certificate
was ready.

<figure id="adcd" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*IWUj58HnN_FVMj8kXZwfSA.png"
class="graf-image" data-image-id="1*IWUj58HnN_FVMj8kXZwfSA.png"
data-width="2004" data-height="1106" />
</figure>

### Step 3: Creating a CloudFront Distribution {#8cdc .graf .graf--h3 .graf-after--figure name="8cdc"}

Next, I set up a CloudFront distribution:

-   [Origin: my S3 bucket]{#db7e}
-   [Alternate domain name (CNAME):
    [**www.harvestvendingco.com**](http://www.harvestvendingco.com){.markup--anchor
    .markup--li-anchor data-href="http://www.harvestvendingco.com"
    rel="noopener" target="_blank"}]{#4b46}
-   [Viewer protocol policy: Redirect HTTP to HTTPS]{#9c78}
-   [SSL certificate: The one I requested in ACM]{#e63b}

This gave me a CloudFront domain like
`d2rx45wl6elnp0.cloudfront.net`{.markup--code .markup--p-code}, which I
could test before switching over DNS.

<figure id="8f33" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*pCKLe4yihb7OpcycC8mhZg.png"
class="graf-image" data-image-id="1*pCKLe4yihb7OpcycC8mhZg.png"
data-width="2456" data-height="1132" />
</figure>

### Step 4: Creating a Hosted Zone in Route 53 {#4886 .graf .graf--h3 .graf-after--figure name="4886"}

While still waiting for Squarespace's 60-day lock to expire, I created a
**public hosted zone** in Route 53 for
`harvestvendingco.com`{.markup--code .markup--p-code}. AWS gave me four
name servers.

I went into Squarespace domain settings, chose **custom nameservers**,
and replaced their default with the four from Route 53. This moved DNS
control to AWS without transferring the domain.

<figure id="d8fb" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*ODBKfPL8FXzx0DqXTj5KbQ.png"
class="graf-image" data-image-id="1*ODBKfPL8FXzx0DqXTj5KbQ.png"
data-width="2070" data-height="1012" />
</figure>

### Step 5: Creating DNS Records in Route 53 {#8005 .graf .graf--h3 .graf-after--figure name="8005"}

In Route 53, I created a CNAME record:

-   [Name: `www`{.markup--code .markup--li-code}]{#f565}
-   [Type: CNAME]{#6814}
-   [Value: my CloudFront URL]{#4059}

This meant `www.harvestvendingco.com`{.markup--code .markup--p-code} now
pointed to CloudFront.

### Step 6: Testing HTTPS {#1953 .graf .graf--h3 .graf-after--p name="1953"}

At first, nothing worked. I realized the DNS changes were still
propagating. After \~15 minutes, everything clicked. When I visited
`https://www.harvestvendingco.com`{.markup--code .markup--p-code}, the
site loaded securely through CloudFront, exactly as planned.

<figure id="1c3e" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*QViCg3J2FdCgcsvobzrhcg.png"
class="graf-image" data-image-id="1*QViCg3J2FdCgcsvobzrhcg.png"
data-width="1134" data-height="90" />
</figure>

### Final Thoughts {#b3ea .graf .graf--h3 .graf-after--figure name="b3ea"}

What started as a simple idea to migrate away from Squarespace turned
into an awesome hands-on AWS project:

-   [Static site hosting with S3]{#b2b8}
-   [Global CDN with CloudFront]{#56cd}
-   [Free SSL with ACM]{#f201}
-   [Custom domain management in Route 53]{#37b0}
-   [Site coding and layout using Visual Studio Code]{#77cf}
-   [S3 bucket policy configuration for public hosting]{#4c54}

I learned a lot troubleshooting things like propagation delays, DNS
caching, and certificate validation issues. The best part? I now own the
full web stack for my business.

<figure id="1a64" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*5ME8ZPXC1GxQ-tcRz8aDRA.png"
class="graf-image" data-image-id="1*5ME8ZPXC1GxQ-tcRz8aDRA.png"
data-width="1890" data-height="1618" />
</figure>

<figure id="58ea" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*agtu5Pn-AoKA3Hagf4JnRA.png"
class="graf-image" data-image-id="1*agtu5Pn-AoKA3Hagf4JnRA.png"
data-width="1880" data-height="1420" />
</figure>

If you're thinking about doing the same, don't be afraid to jump in.
It's a rewarding way to get hands-on AWS experience and level up your
control over your brand.
:::
:::
:::
:::

By [Andrews Valean](https://medium.com/@andrewsvalean){.p-author
.h-card} on [May 12, 2025](https://medium.com/p/2bfebe332e8a).

[Canonical
link](https://medium.com/@andrewsvalean/from-squarespace-to-aws-how-i-fully-migrated-my-business-website-and-domain-2bfebe332e8a){.p-canonical}

Exported from [Medium](https://medium.com) on January 22, 2026.

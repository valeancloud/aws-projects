<div>

# Implementation of a Scalable Web Application using the services of AWS Elastic Beanstalk, DynamoDB

</div>

### *Implementation of a Scalable Web Application using the services of AWS Elastic Beanstalk, DynamoDB, CloudFront and Edge Location*
<figure id="9b89" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*vyyUmMJxKPSGow2Ns1FIsw.png"
class="graf-image" data-image-id="1*vyyUmMJxKPSGow2Ns1FIsw.png"
data-width="1920" data-height="1080" data-is-featured="true" />
</figure>

<figure id="dfb0" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*Fh-2rrUNSN2eMAFC2HaBsQ.png"
class="graf-image" data-image-id="1*Fh-2rrUNSN2eMAFC2HaBsQ.png"
data-width="1920" data-height="1080" />
</figure>

In this project based on a real-world scenario, I was responsible for
implementing an application that needs to support the high demand of a
large number of users accessing it simultaneously. This application has
been used in a large conference that had more than 10,000 people,
in-person and online, with participants from all over the world.

This event was broadcast online and in person, and 10 vouchers were
drawn for 3 Cloud certifications. At that moment, more than 10,000
people in the audience registered their e-mails to guarantee their
participation in the raffle.

Using the AWS Console, I used Elastic Beanstalk services to deploy the
web application, DynamoDB to store emails, and CloudFront to cache
static and dynamic files in an Edge Location close to the user.

Using GitBash, I logged into the instance to get the process running,
but I was encountering an error message reading, "Permissions 0644 for
'mod4-ssh-key.pem' are too open". The message typically indicates that
the permissions for the specified file are too permissive for secure SSH
key usage.

<figure id="3381" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*M21aUusWWFOriIc_xM6oiQ.png"
class="graf-image" data-image-id="1*M21aUusWWFOriIc_xM6oiQ.png"
data-width="1222" data-height="516" />
</figure>

In UNIX-like systems, file permissions are represented in octal
notation, where the leftmost digit specifies the file type and the
following three digits represent the permissions for the owner, group,
and others respectively.

In this case, "0644" means:

-   [The leading "0" indicates it's a regular file.]
-   ["6" (owner permissions) means read and write access.]
-   ["4" (group permissions) means read-only access.]
-   ["4" (other permissions) means read-only access.]

For SSH key files, it's recommended to restrict permissions to be more
restrictive because SSH keys are sensitive information. Typically, SSH
key files should have permissions of "600" or "400", which means only
the owner has read and write access, and no access for group or others.

To fix this, you can change the permissions of the file using the
`chmod`{.markup--code .markup--p-code} command in the terminal. I needed
to make sure the permissions on my private key file (usually a .pem
file) were set correctly. After using the chmod command, I was able to
resolve the issue, proceed successfully, and knock out another AWS
hands-on project.

``` {#8a89 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
chmod 400 your_key.pem
```

<figure id="d5ea" class="graf graf--figure graf-after--pre">
<img
src="https://cdn-images-1.medium.com/max/800/1*oy1KuAXXipmmmR8d1sEFtQ.png"
class="graf-image" data-image-id="1*oy1KuAXXipmmmR8d1sEFtQ.png"
data-width="1178" data-height="670" />
</figure>

<figure id="c7ed"
class="graf graf--figure graf-after--figure graf--trailing">
<img
src="https://cdn-images-1.medium.com/max/800/1*TYb8rW73g3bhDUCKsAiO1Q.png"
class="graf-image" data-image-id="1*TYb8rW73g3bhDUCKsAiO1Q.png"
data-width="1644" data-height="890" />

<div>

# Migration of a Workload running in a Corporate Data Center to AWS using the Amazon EC2 and RDS... {#migration-of-a-workload-running-in-a-corporate-data-center-to-aws-using-the-amazon-ec2-and-rds .p-name}

</div>

::: {.section .p-summary field="subtitle"}
In another project based on a real-world scenario, I acted as the Cloud
Specialist responsible for migrating a workload running in a...
:::

::: {.section .e-content field="body"}
::: {#b9e4 .section .section .section--body .section--first .section--last}
::: section-divider

------------------------------------------------------------------------
:::

::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### *Migration of a Workload running in a Corporate Data Center to AWS using the Amazon EC2 and RDS service* {#9d02 .graf .graf--h3 .graf--leading .graf--title name="9d02"}

<figure id="880f" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/1*MYrkt1lvCnZ1olMs3npi1w.png"
class="graf-image" data-image-id="1*MYrkt1lvCnZ1olMs3npi1w.png"
data-width="1920" data-height="1080" data-is-featured="true" />
</figure>

<figure id="7711" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*0Y_jNDDOvBs6UwkMYSFa2g.png"
class="graf-image" data-image-id="1*0Y_jNDDOvBs6UwkMYSFa2g.png"
data-width="1920" data-height="1080" />
</figure>

In another project based on a real-world scenario, I acted as the Cloud
Specialist responsible for migrating a workload running in a Corporate
DataCenter to AWS.\
 The application and database were migrated to AWS using the Lift &
Shift (rehost) model, moving both application and database data.

I followed the following migration steps: Planning (sizing,
prerequisites, resource naming), Execution (resource provisioning, best
practices), Go-live (validation test --- Dry-run, final
migration --- Cutover) and Post Go-live (ensure the operation of the
application and user access).

Using the AWS console, I was able to create a VPC, EC2 Instance (which
hosted my application), and connected to a MySQL Database via Amazon
RDS. In addition to the VPC generated, I created additional Subnets,
Internet Gateway, and Route Tables, using the Route Table to point to
the Internet Gateway.

Git Bash became a great friend in the process --- but, that is not to
say there were no issues. I began to encounter an issue when attempting
to connect to my DB server from my EC2 Instance. The error message,
reading, "ERROR 2003 (HY000): Can't connect to MySQL server".

After vigorous troubleshooting, I found out my issue what not setting up
the RDS DB instance properly--- I had the wrong MySQL engine version in
place and had not been connected to the newest 5.7 version mentioned
'MySQL 5.7.44'. After deleting the instance and relaunching it with the
correct information, my error message went away, and I was able to login
to MySQL via GitBash. Troubleshooting can be a stress
inducer --- especially when you are stuck on the same issue for hours on
end, only to discover that fixing the smallest mishap resolved your
issue. Nonetheless, in the moment of resolve you feel relief and a
tremendous amount of accomplishment. We have to be able to push through
issues whether they be mental, physical, spiritual, emotional, or even
professional.

<figure id="9c01" class="graf graf--figure graf-after--p">
<img
src="https://cdn-images-1.medium.com/max/800/1*R4lN6-zYn89pOmDCRUc3-Q.png"
class="graf-image" data-image-id="1*R4lN6-zYn89pOmDCRUc3-Q.png"
data-width="2418" data-height="1404" />
</figure>

<figure id="7d0b" class="graf graf--figure graf-after--figure">
<img
src="https://cdn-images-1.medium.com/max/800/1*BpUmaqIWLDr38MfK5GPKBA.png"
class="graf-image" data-image-id="1*BpUmaqIWLDr38MfK5GPKBA.png"
data-width="2418" data-height="1216" />
</figure>

<figure id="09ba"
class="graf graf--figure graf-after--figure graf--trailing">
<img
src="https://cdn-images-1.medium.com/max/800/1*BOFxR9CMNgnyum-QsVjGpw.png"
class="graf-image" data-image-id="1*BOFxR9CMNgnyum-QsVjGpw.png"
data-width="2408" data-height="1300" />
</figure>
:::
:::
:::
:::

By [Andrews Valean](https://medium.com/@andrewsvalean){.p-author
.h-card} on [March 12, 2024](https://medium.com/p/19fedb755d4d).

[Canonical
link](https://medium.com/@andrewsvalean/migration-of-a-workload-running-in-a-corporate-data-center-to-aws-using-the-amazon-ec2-and-rds-19fedb755d4d){.p-canonical}

Exported from [Medium](https://medium.com) on January 22, 2026.

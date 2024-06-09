---
layout: post
author: David
title: Making this personal website
---

### Introduction

It is actually very easy to have a personal website. If you 
just want a blog, get yourself a managed drag-and-drop designed
site on Squarespace, Wix, WordPress or something else. 
If you know a bit of frontend and Git, and you want something free, 
use GitHub Pages and an open-source template. 
Otherwise, a combination of commercial social networking platforms
is good enough to reach your target audience.

### Why have a personal website?

There is a target audience that no social networking platform can reach. 
When you post pictures on Instagram, share an update on LinkedIn, 
or publish a blog on Medium, your work goes through an algorithm 
that evaluates who will see it, and when it will appear on their feed. 
When you write for an audience who are passively being handed content, your writing 
will tend towards highlights, summaries, and digests. Only sensational content, 
or very directed content, can make an impression within 
an endlessly scrolling sea of information. 

A personal website is different. When someone enters on your personal website, 
they are looking for you and what you have to say. Yes, maybe most of those visitors 
will end up being background-checkers from HR, webscrapers for some large-language model, 
or bots looking for vulnerabilities, but perhaps some of them will be interested in 
hearing what you have to say, not just what you are obliged to write. And so, I think 
building a personal website is a chance to start a real connection.

### Why build a personal website from scratch?

Mostly for the experience. I've studied frontend, but until now I never 
really applied it to something I actually wanted to do. I know roughly how the 
HTTPS protocol works, but what good is that if I never tried to use it? I've read 
a lot of AWS documentation and learnt how to define infrastructure in Terraform, 
but isn't it all just theory until I build with it? I wanted to create something 
in my own image, not just what my capstone project advisors or product managers want.

### What is the current tech stack?

I constantly change the tech stack to explore different technology options. I'm not 
much of a UX guy and I really dislike frontend bloat, so I'm keeping the UI simple. 
I am more interested in trying out different infrastructure and hosting options, on 
AWS or otherwise. So with further iterations, my personal website will have a more 
refined architecture, but the frontend experience will remain the same.

### May 2023 to June 2023

Heroku is easily the quickest way to host a web app. In layman's terms, you 
can just upload bundles of code to the Heroku platform using their simple command 
line interface, and it will figure out how to run it as a web app. Heroku also 
handles SSL certificates and domain names, load balancing, scaling, monitoring, networking, 
all out of the box. Using Terraform to defne a Heroku configuration was almost trivial.

The tech stack is:
- Bare HTML and CSS with Jinja2 for templating
- Python Flask as the framework + Gunicorn as the webserver
- Terraform for Infrastructure-as-Code
- Heroku as a Platform-as-a-Service
- Amazon Route 53 to maintain domain names and DNS records

Here is a diagram of the system architecture:

![Heroku Diagram](/assets/img/heroku_diagram.jpeg)

### June 2023 - June 2023

The next step-up from Heroku's Platform-as-a-Service is AWS Elastic Beanstalk.
Elastic Beanstalk forces you to do much more infrastructure configuration(and to actually 
read the docs!) than Heroku, because Beanstalk acts like a Platform by orchestrating many 
AWS services under the hood. 

When you define a Elastic Beanstalk environment, you must answer questions like:
- What Amazon EC2 instance types should be used? Are they on-demand or spot instances?
- Which Amazon VPC and subnets to launch your EC2 instances? Is it a private or public VPC?
- Do you want to use an Amazon Elastic Load Balancer?
- Which Amazon VPC and subnets to launch your load balancer?
- What processes should your load balancer redirect requests to, and by what rules?
- What listeners should your load balancer define?
- What IAM Roles and Instance Profiles can the Elastic Beanstalk environment assume?
- ...autoscaling, SSL certificates, networking, update policy...

You get the idea. The tech stack is:
- Bare HTML and CSS with Jinja2 for templating</li>
- Python Flask as the framework + Gunicorn as the webserver</li>
- Terraform for Infrastructure-as-Code
- Amazon Elastic Beanstalk as a Platform-as-a-Service. It orchestrates:
    * Amazon EC2 to run workloads. An EC2 Security Group defines access control rules to the EC2 instances.
    * Amazon VPC and subnets where the Amazon EC2 instances are connected to. A network ACL to define access 
    control to the VPC, a internet gateway, and a route rable.
    * Elastic Load Balancing to balance requests across multiple EC2 instances. The security group for the load balancer.
    * Amazon Route53 maintains a domain name, and DNS records
    * Amazon Certificate Manager manages SSL certificates.
    * AWS IAM to give services permissions within AWS

Here is a diagram of the system architecture:

![Elastic Beanstalk Diagram](/assets/img/eb_diagram.jpeg)


### June 2023 - Onwards

Satisfied that I knew how to use and configure AWS Elastic Beanstalk, and concerned at how expensive running a 
load balancer is, I moved over my website to GitHub Pages, using the Jekyll static website templating engine. In a way,
becoming confident enough with AWS to no longer feel the need to prove my ability on overengineering a static blog 
website, is a sign of technical maturity.

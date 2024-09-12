> i like the "how it works" part - could we do a "How we built a context-away devops assistent in 2 months" blog-post!?

Kelly:
> We could do it from a “we were looking for something to help us with our devops/context switching issues” and the thought processes in designing it rather than the actual internal tech behind it? I’m sure we can include some of the internals but it would be more of a “we built this for us and all of our pain points that we know other DevOps engineers have” vs “how to build your own Fuse”.

---

Generate paragraphs marked with "TODO" for a blog post "Fusing Ideas: Designing Botkube Fuse to Combat Context Switching in DevOps" which talks about how we came up with Fuse.

max 12 sentences per paragraph.

# Notes


- Audience: Simple - We targeted just platform engineers / SRE / DevOps as we know them best when building Botkube 
- Based on the feedback we found Acute pain point: Context switching and multitasking
- We built Fuse in two months

- Codename: Fuse, as it's easy to remember, and comes from "fusion"

Platform Engineers often have to rapidly switch between responding to questions, issues, and outages for multiple services simultaneously. Doing ad-hoc tasks, switching tabs for multiple project docs, answering some questions to developers related to infrastructure, to help troubleshoot infra problems with developers etc.

Platform Engineers are often demotivated when doing a lot of manual stuff. Here’s a short list of tedious tasks from day-to-day work:
- Check CI alerts and get errors from CI/CD pipeline failures
- Go through all Slack mentions 
- Wait for a colleague to ask some questions about a specific domain
- Check which db is used by serviceB.
- Ask what's the difference between db sizes dev vs prod that serviceB uses.
- Do I need to worry about scaling up the db for serviceB?
- Generate tf and kube files for a new service which requires a pubsub topic and access to GCS 
- Check if a given pull request was already merged and released on production.
- Check the last failed CI jobs and their summaries
- Answer questions to developers about whether UI is already released
- Debug change for the K8s Service type: I changed it to LoadBalancer but it’s still not applied: why? I need to check GitHub repo, Helm chart, ArgoCD sync, Kubernetes resource

Also, another pain points result in context switching

- Lack of proper staffing and support: Many organizations expect Platform Engineers/DevOps/SRE practitioners to cover an extremely wide range of responsibilities ("EverythingOps") without adequate staffing, leading to burnout.
- Misalignment with development teams: Platform Engineering/DevOps/SRE teams are sometimes treated as a help desk for developers or expected to architect systems without proper support from engineering leadership
- Fuse leverages existing Botkube technology (AI assistant, Cloud infrastructure) and takes it to next level

In today's fast-paced DevOps environments, platform engineers, SREs, and DevOps teams face constant interruptions and shifting priorities. They juggle multiple services, troubleshoot infrastructure problems, and respond to requests from developers, all while ensuring system reliability. This relentless context switching can lead to inefficiency, frustration, and ultimately burnout. In response to this widespread pain point, we set out to design Botkube Fuse—a solution specifically aimed at reducing multitasking and context switching for platform engineers, allowing them to focus on more meaningful tasks. The result? A tool that fuses the capabilities of Botkube with a streamlined workflow to empower engineers to work smarter, not harder.

Botkube Fuse started with a simple observation: Platform engineers are overwhelmed. From managing CI/CD alerts to fielding questions about database scaling, these professionals are forced to pivot between various tasks and tools, rarely getting the chance to work deeply on one issue. During conversations with our community, it became clear that the endless context switching was an acute pain point. We felt this problem firsthand when working with Botkube users and realized it needed to be addressed urgently. With a two-month deadline in mind, we set out to build Fuse—a name inspired by the concept of "fusion"—to unify tasks and reduce the cognitive load of DevOps teams.

The brainstorming phase was both fast-paced and collaborative. We gathered feedback from platform engineers, SREs, and developers to map out their most tedious tasks and interruptions. Our goal was to identify the most common sources of friction: checking CI alerts, answering infrastructure questions, generating Terraform files, or investigating Kubernetes issues. By pinpointing these daily interruptions, we envisioned a tool that could handle these queries proactively and automate responses where possible. We also knew that Fuse had to integrate seamlessly with existing tools and workflows, leveraging Botkube’s AI assistant and cloud infrastructure expertise to offer a smoother experience.

The pain points were clear: platform engineers were expected to manage "everythingOps" with minimal staffing, and often without proper alignment from development teams. Engineers were demotivated by manual, repetitive work and felt like they were being treated as a help desk rather than strategic partners. Misalignment with engineering leadership added to the frustration, as these teams were tasked with system architecture while simultaneously supporting day-to-day operations. Fuse was designed with these pain points in mind—empowering engineers to combat constant interruptions, automate mundane tasks, and reclaim time for higher-impact work.


---
# BLOG POST:

# Fusing Ideas: Designing Botkube Fuse to Combat Context Switching in DevOps

## Introduction

<!-- TODO -->


In this blog post, we’ll take a look at how Botkube Fuse was built, what was the reason to build it, and which acute pain points we address.

## Acute pain point identified: Context switching and multitasking

The design process for Fuse was born out of necessity and shaped by user feedback. As we engaged with platform engineers, SREs, and DevOps practitioners in our community, it became clear that their biggest challenge was the sheer volume of tasks they had to handle simultaneously. Our team began by identifying the most common sources of frustration, such as constantly checking CI/CD alerts, troubleshooting Kubernetes issues, and answering repetitive infrastructure questions.

Context switching is one of the most significant challenges platform engineers face in their daily work. Whether it’s responding to alerts from CI pipelines, troubleshooting deployment issues, or answering developer queries, they are often pulled in multiple directions at once. This fragmented focus leads to inefficiencies and can significantly slow down productivity. In many cases, engineers spend more time switching between tasks than actually solving problems.

## Working on the solution

Once we identified the most common pain points, we began to design a new tool. As the terminal is the natural choice for DevOps or platform engineers, we decided to build a CLI tool that helps with that. While we found similar tools in the ecosystem (similar at a first glance), we had a few ideas how to build something better.

After 1 month of the development, the initial version of the tool was done.

Now, we can't forget about the hardest part: naming.

The name “Fuse” was chosen to represent the core idea of unifying and streamlining tasks for platform engineers. It stems from the concept of “fusion”, symbolizing the merging of multiple tools, tasks, and workflows into a single, cohesive solution. We wanted a name that was easy to remember and reflected the tool’s purpose of reducing fragmentation caused by context switching. Fuse brings together the enhanced power of Botkube’s AI capabilities with a simplified workflow, helping engineers focus on what matters most. The name perfectly encapsulates the tool’s mission to “fuse” everything into a seamless experience.

## So, how does Fuse work?

Botkube Fuse is a terminal tool which uses our brand-new AI assistant to answer your questions and solve your challenges during your day-to-day work. Unlike some other tools on the market (including Botkube), it's just a single CLI binary without an agent. You just simply [install Fuse](https://botkube.io/fuse) and type `fuse 'your prompt here...'`, or run `fuse` to enter interactive mode and start chatting.

Fuse uses the powerful GPT-4o model from OpenAI to get things done. We integrated a variety of tools to assist you with Kubernetes, Google Cloud Platform, GitHub, git, and local filesystem operations. It can even generate and execute Python code on your behalf!

"Whoa, that's pretty dangerous", you might say. "I don't trust the code executed by AI". Good point! That's why Fuse requires user confirmation for each potentially dangerous operation (such as filesystem write or code execution), to make sure you are in full control of what's happening on your machine.

## How does Fuse differ from other tools in the market?

While there are similar tools in the AI space, we wanted to build something different. That’s why we established two bold assumptions.

### End-to-end knowledge about your infrastructure

Firstly, we aim to integrate your data from different sources and make the Fuse AI assistant aware of connections between them. Imagine a smart assistant who understands your infrastructure: from your Terraform modules, ArgoCD app manifests in your git repository, through your GitHub Actions pipelines, Google Cloud Platform resources current state, to actual business-critical services deployed in Kubernetes. That's what we have in mind while building Fuse. Magic, eh?

[MAGIC GIF]

We introduced the `fuse init` command which currently introspects your Google Cloud Platform project, your GKE clusters and other resources, to help with your complex scenarios on the edge of Kubernetes and GCP. But that's just a glimpse of what we want to build. Stay tuned!

### Focus on actual use-cases

We want to solve real user problems. And the problems very often live on the edge of different parts of the infrastructure, hence the end-to.end infrastructure knowledge we explained in the previous paragraph.

However, even with such knowledge, we do believe that even the most powerful AI assistants out there still require some guidance. Someone needs to do the “prompt engineering” work. That’s why we introduced AI assistant guidance for different user scenarios. Currently, we focused on:
- GitHub Actions secret management
- GitHub Actions pipeline run analysis
- GKE troubleshooting with IAM permission errors
- Local environment operations and debugging

How does it work? The Fuse AI assistant categorizes your question first, and then if it’s close to our predefined scenarios, it uses our custom instruction for guidance to do the work. Of course users can still customize the behavior with customized prompts but we want to make sure it follows the right path by default.

While more scenarios will definitely ship soon, we also do believe that users should be able to write custom instructions and reuse them automatically in a given context. Expect some updates around that in the following weeks - and if you have any suggestions for improvements or new scenarios, please let us know on Slack or by getting in touch.

## Summary

<!-- TODO -->
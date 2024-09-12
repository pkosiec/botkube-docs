> i like the "how it works" part - could we do a "How we built a context-away devops assistent in 2 months" blog-post!?

Kelly:
> We could do it from a “we were looking for something to help us with our devops/context switching issues” and the thought processes in designing it rather than the actual internal tech behind it? I’m sure we can include some of the internals but it would be more of a “we built this for us and all of our pain points that we know other DevOps engineers have” vs “how to build your own Fuse”.

---

# Building Fuse 

- At Botkube, we are in contact with multiple different DevOps teams

- 

- Codename: Fuse, as it's easy to remember, and comes from "fusion"
- We built Fuse in two months


- Audience: Simple - For now we targeted just platform engineers / SRE / DevOps. However, at some point, with a suggested solution, we might target developers, managers and other team members too,with proper access rights.

- Acute pain point: Context switching and multitasking

  

- Acute pain point: Context switching and multitasking
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


Fuse leverages existing Botkube technology (AI assistant, Cloud infrastructure) and takes it to next level


# What we built differently

- there are multiple similar tools out there

- we wanted to build Fuse differently
 - Deep understanding of your infrastructure
 - Connecting multiple data sources and introspecting interdependencies
 - Focus on specific use cases, including:
   - Automated GCP and GitHub Actions Secret Management
   - Getting summary of CI/CD pipeline runs
   - Troubleshooting combined GKE Cluster and IAM Permissions outage
   - Answering environment (localhost) related questions






## How does it work?

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

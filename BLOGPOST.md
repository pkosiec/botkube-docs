# Fusing Ideas: Designing Botkube Fuse to Combat Context Switching in DevOps

## Introduction

In today’s fast-paced world, DevOps, SRE, and platform engineers constantly juggle multiple tasks—from navigating through various layers of a project while implementing new functionalities to answering developer questions and troubleshooting infrastructure issues. This constant context switching often leads to inefficiencies and burnout.

In this blog post, we’ll dive into the journey of building Botkube Fuse, a tool designed to address these challenges. We’ll explore the problems it solves, the design process, and how it can help streamline workflows for platform engineers.

## The Inspiration Behind Fuse  

The design process for Fuse was born out of necessity and shaped by user feedback. As we engaged with platform engineers, SREs, and DevOps practitioners in our community, it became clear that their biggest challenge was the sheer volume of tasks they had to handle simultaneously. Our team began by identifying the most common sources of frustration, such as switching between multiple browser tabs for project documentation, constantly checking CI/CD alerts, and answering repetitive infrastructure questions. These scenarios are just examples of a larger problem: context switching.

## Tackling the Core Pain Point: Context Switching

Context switching is one of the most significant challenges platform engineers face in their daily work. Whether it’s responding to alerts from CI pipelines, troubleshooting deployment issues, or answering developer queries, they are often pulled in multiple directions at once. This fragmented focus leads to inefficiencies and can significantly slow down productivity. In many cases, engineers spend more time switching between tasks than actually solving problems. Eventually, it might end with a burnout.

That’s not all. Context switching can also result from a lack of proper staffing and support. Many organizations expect Platform Engineers, DevOps, and SRE practitioners to cover an extremely wide range of responsibilities (“EverythingOps”) without adequate resources. Additionally, these teams are sometimes treated like a help desk for developers or are expected to architect systems without sufficient backing from engineering leadership, further worsening the problem.

![](./assets/joggling.gif)

_GIF source: [tenor.com](https://tenor.com)_

## From Idea to Reality: Crafting the Perfect Solution

Once we understood the pain point we wanted to solve, the next step was designing a solution. The terminal is the natural choice for most DevOps or platform engineers we engaged with, so we decided to use it as the foundation for our design. We opted to build a CLI tool that combines multiple different tools and knowledge sources into a single, unified experience.

Now, we can’t forget the hardest part of the design process: naming.

The name “Fuse” was chosen to represent the core idea of unifying and streamlining tasks for platform engineers. It stems from the concept of “fusion”, symbolizing the merging of multiple tools, tasks, and workflows into a single, cohesive solution. We wanted a name that was easy to remember and reflected the tool’s purpose of reducing fragmentation caused by context switching. Fuse brings together the enhanced power of Botkube’s AI capabilities with a simplified workflow, helping engineers focus on what matters most. The name perfectly encapsulates the tool’s mission to “fuse” everything into a seamless experience.

## Meet Fuse: Your New DevOps Companion

After two months of design, planning, and development, we launched the first public Fuse release.

Fuse is a terminal tool powered by our most advanced AI assistant, designed to answer your questions and tackle challenges in your day-to-day work. Unlike some other tools on the market (including Botkube), it’s just a single CLI binary without an agent. You just simply [install Fuse](https://botkube.io/fuse) and type `fuse 'your prompt here...'`, or run `fuse` to enter interactive mode and start chatting.

## Unlocking Fuse’s Power: How It Works

Fuse builds on existing Botkube technology, including our AI assistant and cloud infrastructure, and takes it to the next level.

Fuse uses the powerful GPT-4o model from OpenAI to get things done. We integrated a variety of tools to assist you with Kubernetes, Google Cloud Platform, GitHub, Git, and local filesystem operations. It can even generate and execute Python code on your behalf!

“Whoa, that’s pretty dangerous,” you might say. “I don’t trust the code executed by AI.” Good point! That’s why Fuse requires user confirmation for each potentially dangerous operation (such as filesystem writes or code execution) to ensure you are in full control of what’s happening on your machine.

## Why Fuse Stands Out

While there are similar tools in the AI space, we wanted to build something different—and better. That’s why we established two bold principles.

### A Holistic View of Your Infrastructure

Firstly, we aim to integrate your data from different sources and make the Fuse AI assistant aware of connections between them. Imagine a smart assistant who understands your infrastructure: from your Terraform modules, ArgoCD app manifests in your git repository, through your GitHub Actions pipelines, Google Cloud Platform resources current state, to actual business-critical services deployed in Kubernetes. That's what we have in mind while building Fuse. Magic, eh?

![](./assets/magic.gif)

_GIF source: [tenor.com](https://tenor.com)_

We introduced the `fuse init` command which currently introspects your Google Cloud Platform project, your GKE clusters and other resources, to help with your complex scenarios on the edge of Kubernetes and GCP. But that's just a glimpse of what we want to build. Stay tuned!

### Focused Solutions for Real Problems

We aim to solve real user problems, which often arise at the intersection of different parts of the infrastructure—hence the need for the end-to-end infrastructure knowledge we described earlier.

However, even with such knowledge, we do believe that even the most powerful AI assistants out there still require some guidance. Someone needs to do the “prompt engineering” work. That’s why we introduced AI assistant guidance for different user scenarios. Currently, we focused on:
- GitHub Actions secret management
- GitHub Actions pipeline run analysis
- GKE troubleshooting with IAM permission errors
- Local environment operations and debugging

How does it work? The Fuse AI assistant categorizes your question first, and then if it’s close to our predefined scenarios, it uses our custom instruction for guidance to do the work. Of course users can still customize the behavior with customized prompts but we want to make sure it follows the right path by default.

While more scenarios will definitely ship soon, we also do believe that users should be able to write custom instructions and reuse them automatically in a given context. Expect some updates around that in the following weeks - and if you have any suggestions for improvements or new scenarios, please let us know on Slack or by getting in touch.

## Wrapping Up

We thoroughly enjoyed the journey of building Fuse. While it was an intensive process, it was also a lot of fun!

To recap, Botkube Fuse is designed to help platform engineers, DevOps, and SREs reduce inefficiencies caused by constant context switching. By unifying multiple tools into a single, terminal-based CLI powered by AI, Fuse simplifies complex workflows and automates repetitive tasks. With features like GKE troubleshooting, GitHub Actions analysis, and more, it’s built to solve real-world challenges.

Best of all, Fuse is [free to try](https://botkube.io/fuse)—so give it a try and see how it can streamline your day-to-day work. We’d love to hear your feedback—reach out to us via [Slack](https://join.botkube.io/) or our social media channels!

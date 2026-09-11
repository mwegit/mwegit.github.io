---
title: "Self-service infrastructure, without giving up the guardrails"
date: 2026-09-11
tags: [terraform, mcp, azure, platform]
published: false
---

> **Draft.** Claude sketched this from a one-line description of `mcp-terraform`.
> Rewrite it in your own voice, check every claim against what the server actually
> does, then delete this blockquote and set `published: true`.

Platform teams get asked the same question a few hundred times a year: *can I get a
storage account / a namespace / a Postgres instance?* The honest answer is usually
yes — the work is not hard, it is just gated on someone on my team having an hour.

There are two bad ways out of that. You can hand everyone write access to the cloud
and let them provision whatever they want, which is fast right up until the first
untagged, unmonitored, publicly-routable database. Or you can keep the gate and
accept that infrastructure moves at the speed of a ticket queue.

## What I wanted instead

<!-- TODO: your actual motivation. Why MCP rather than extending the existing REST API? -->

The constraint I care about is that self-service must not mean *bypassing the
review path*. Every piece of infrastructure in our estate is described by a Terraform
module and applied through a pull request. Anything that provisions resources outside
that path creates drift, and drift is how you end up with an environment nobody can
rebuild.

So the goal was not "let developers create resources." It was **let developers
describe what they need, and have the right Terraform show up in a pull request.**

## The shape of it

`mcp-terraform` is a Model Context Protocol server. It exposes infrastructure
operations as tools an AI assistant can call, so a developer can ask for what they
need in the assistant they are already working in, and get back reviewed Terraform
rather than hand-written config.

<!-- TODO: the interesting part. Which tools does it expose? What does a call
     actually produce — a module invocation, a PR, a plan? How are provider
     credentials scoped? What stops someone asking for something they should not get? -->

## What it does not do

<!-- TODO: worth being explicit here — the limits are usually the most credible
     part of a post like this. -->

## Multi-cloud

Azure came first because that is where our platform lives, but nothing in the tool
layer is Azure-specific.

<!-- TODO: which other providers are wired up, and what actually had to change
     per-provider? -->

---

*Working on something similar, or want to argue with any of this? I am at
[ishimwemuhire@outlook.com](mailto:ishimwemuhire@outlook.com).*

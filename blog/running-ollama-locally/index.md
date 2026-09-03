---
layout: blog-post
title: "Building a Local AI Environment with Ollama"
description: "Lessons from connecting local models, Internet search, and repeatable workflows on an Apple Silicon Mac."
date: 2026-09-02
author: Rajiv Kanaujia
tags: [AI, Ollama, Developer Tools]
permalink: /blog/running-ollama-locally/
published: true
---

## Why I Built It

My recent startup work has reminded me that useful technology needs more than a successful demo. It needs a setup I understand, can maintain, and can return to without reconstructing every decision.

That thinking led me to build a local AI environment on my Apple Silicon Mac using Ollama.

I started by installing models and interacting with them through the terminal. Next, I added Open WebUI to provide a browser interface. With SearXNG, I connected Internet search so the workflow could retrieve information beyond a model’s training data.

Each component had a clear responsibility: Ollama ran the models, Open WebUI handled conversations, SearXNG retrieved search results, and Docker managed the supporting services.

## What I Learned

The more interesting lessons appeared between those components.

A browser successfully reaching a service did not automatically mean another container could reach it. Search needed the correct response format. Moving Docker configurations required preserving existing volumes so chat history and settings remained available.

I organized the configuration files into a Git-managed directory, kept secrets outside version control, and added scripts for starting, stopping, and updating the environment.

I also explored coding assistance through Continue in VS Code and enabled multiple-model conversations in Open WebUI. Comparing responses gave me a practical way to examine differences in explanations, coding suggestions, and tool use.

This work connects closely to how I approach building a startup: make progress through experimentation, then invest in repeatability and operational clarity.

Running models locally provides control over where inference happens. Internet search still introduces external connections, and model responses still need verification.

## The Complete Setup

I documented the setup in [Running Ollama Locally](https://github.com/rajivkanaujia/alphaworks/wiki/Running-Ollama-Locally), including installation, search configuration, Docker organization, model comparisons, screenshots, and scripts.

My goal is to make the path easier for someone else—and leave myself a useful reference as the tools evolve and my own requirements change.

---
title: Dune AI Prompt Engineering
description: How to craft a successful Dune AI prompt
---

# Dune AI Prompt Engineering Guide

Welcome to the Dune AI Prompt Engineering Guide! This guide is designed to help users understand how to effectively communicate with Dune AI, focusing on its powerful capabilities in parsing smart contracts and identifying project names within the blockchain analytics domain. Whether you're a developer, researcher, or enthusiast, this guide will provide you with the knowledge to leverage Dune AI's features for your projects.

## Getting Started

Before we dive into the examples, it's important to understand the basics of prompt engineering with Dune AI. Prompt engineering involves crafting questions or commands that guide the AI in performing specific tasks. A well-designed prompt results in more accurate and useful responses.

### Principles of Effective Prompting

- **Clarity**: Be clear and specific about what you're asking.
- **Context**: Provide enough context to guide the AI's response.
- **Conciseness**: Keep prompts concise to avoid overwhelming the AI.

## Capabilities Overview

Dune AI offers a range of capabilities, especially suited for blockchain analytics. Key features include:

- Parsing smart contracts addresses and identifying the relevant functions and their tables.
- Identifying and categorizing project names and mapping them to their respective contract tables and spells (expertly curated datasets)
- Identifying token symbols and injecting their contract addresses and correct contract tables.
- Injected your wallet address (when linked in profile) to provide personalized insights and analytics.

## Example Prompts

Below are examples of how you can structure your prompts to make the most out of Dune AI's capabilities.

### Parsing Smart Contracts

#### Example 1: Extracting relevant functions via contract addresses

**Prompt**: "List recent trades on 0xcf205808ed36593aa40a44f10c7f7c2f67d4a4d4 from trader 0x0b660e916537a75f8d7d3ac7dfe6c8678a8ac5fa"

**Purpose**: Given the contract address, we can find that it corresponds to the FriendtechSharesV1 contract and pick the appropriate function Trade to get the table friendtech_base.FriendtechSharesV1_evt_Trade.

![dune-ai-function-example.png](..%2F..%2Fresources%2Fimages%2Fdune-ai-function-example.png)


#### Example 2: Identifying Variables

**Prompt**: "Identify all public variables in the ABC smart contract and explain their significance."

**Purpose**: To get an overview of the variables in the ABC smart contract and understand their roles within the contract.

### Identifying Project Names

#### Example 1: Project Categorization

**Prompt**: "Categorize the following project names by their primary blockchain technology: Ethereum, Solana, Cardano."

**Purpose**: This prompt helps in understanding which projects operate on which blockchain technology, assisting in trend analysis and market segmentation.

#### Example 2: Project Insights

**Prompt**: "Provide an analysis of the project named 'DeFiKingdoms' including its blockchain base, key features, and current market position."

**Purpose**: To gather comprehensive information about the project 'DeFiKingdoms,' including its technological foundation and market performance.

## Best Practices for Prompt Engineering

- **Iterate**: Don't hesitate to refine your prompts based on the responses you get.
- **Be Specific**: The more specific your prompt, the more targeted the AI's response will be.
- **Use Examples**: When possible, provide examples within your prompt to guide the AI's understanding.

## Conclusion

Dune AI is a powerful tool for blockchain analytics, offering detailed insights into smart contracts, project names, and much more. By mastering prompt engineering, you can unlock the full potential of Dune AI for your research or development projects. Happy prompting!

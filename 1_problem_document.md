# Case Study: Affiliate Campaign Management System

## Disclaimer

This is a refined version from the original problem document to make it anonymous and protect privacy.

## Context and Terminology

- **Affiliate user**: The person in the role of the affiliate, promoting campaigns.
- **Affiliate dashboard**: A dashboard tied to a specific merchant where an affiliate user manages the campaign
  they are part of for that merchant only. If an affiliate user participates in campaigns across multiple merchants,
  they will have to manage each campaign through a separate dashboard—one for each merchant.

- **Affiliate account**: An account used by an affiliate user to sign into the affiliate dashboard. Currently,
  affiliate users may have multiple affiliate accounts, one for each campaign or merchant they are involved with.

- **Regular campaign**: A campaign created by a merchant. Affiliate users can join these campaigns via
  the merchant’s dedicated affiliate dashboard.

- **Marketplace campaign**: A public campaign that is listed on a central marketplace, where affiliate users can browse,
  discover, and join campaigns across multiple merchants.

- **Marketplace dashboard**: A unified dashboard from which affiliate users can keep track of all the marketplace
  campaigns they have joined across multiple merchants.

## Current System Overview

Merchants can create **regular campaigns** that affiliate users can join to promote their programs.
Affiliate users must create **affiliate accounts** on each merchant's dedicated dashboard (often hosted under
the merchant's subdomain), where they retrieve affiliate links, promotional codes, and manage their referral data
(e.g., commissions, earnings).

- **One campaign per merchant**: Affiliate users can only participate in one campaign per merchant.
  Merchants have the ability to move affiliate users between campaigns based on performance.

- **Multiple affiliate accounts**: Affiliate users need to create a separate account each time
  they join a campaign with a new merchant, due to the current system associating accounts with campaigns.

- **Subdomain-based dashboards**: Each merchant’s affiliate dashboard is hosted under its own subdomain
  (e.g., affiliates.company.com).

## Future Vision: Unified Affiliate Dashboard

The goal is to introduce a **unified dashboard** for affiliates to manage all the programs they are part of across
multiple merchants. This is essential for improving the affiliate user experience, especially as the system expands
to include a **marketplace** for campaigns.

### Introducing the Marketplace
- **Marketplace Campaigns**: Merchants will be able to list their campaigns on a central **marketplace**,
  making them available for affiliate users to browse and join.

- **Unified Affiliate Experience**: Affiliate users will be able to manage their marketplace campaigns
  (across multiple merchants) from a single entry point.
  
However, regular campaigns will continue to exist. For example, a merchant could create a public marketplace campaign
that any affiliate can join, while also offering exclusive, private campaigns with higher rewards for select affiliates.

## Problem Statement

You are tasked with proposing a solution for introducing what we’ll call the **Marketplace Dashboard**—
a unified dashboard for affiliate users to browse and join marketplace campaigns
and track all campaigns they are part of. Key considerations include:

1. **Coexistence of regular and marketplace campaigns**: The system needs to support both regular campaigns
   (currently accessible through individual affiliate dashboards) and marketplace campaigns
   (accessible through the new Marketplace Dashboard). The decision to either merge these
   into one unified dashboard or keep them separate is part of your task.

2. **Single Account for Affiliates**: Today, affiliate users must create a separate account for each campaign they join.
   An improved experience would allow them to manage all campaigns (both regular and marketplace) with a single account.

3. **Merchant Subdomains**: The Marketplace Dashboard will exist under a central domain (e.g., marketplace.example.com).
   However, merchants will likely want to keep their regular affiliate dashboards under their own subdomains.

## Resources and Current Setup

- **Affiliate Model**: The affiliate model handles authentication and campaign management for each affiliate user.
  It is currently scoped per campaign/merchant, meaning that an affiliate user can have multiple accounts
  (with the same email) across different merchants or campaigns. Key data, such as referrals and commissions,
  are tied directly to the affiliate model.
  
- **Routing**: Currently, affiliate dashboards are served under individual merchant subdomains,
  as specified by the merchant settings.
  This setup allows merchants to control their own affiliate dashboard, separate from other merchants.

Your solution should account for these constraints while proposing a plan to introduce
the new marketplace and the unified affiliate dashboard.
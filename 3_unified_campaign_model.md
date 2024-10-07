# Unified Campaign Model

## Problem

In addition to the existing regular campaigns (exclusive to the merchant),
introduce a new public campaign and a corresponding dashboard called the Affiliate Marketplace.

## Objectives

- Create a public and open Marketplace for affiliate programs where companies can promote their campaigns
- Maintain existing exclusive campaigns (aka Regular campaigns) and support additional private campaigns
  (hidden, invite-only)

- Support both public (marketplace) and exclusive (regular) campaign dashboards
- Provide users with a central place to manage all their campaigns (public, exclusive and private)

Now that we have a [unified user account](./2_unified_user_accounts.md), we can support one user multiple campaigns.

## Step 1: Extend `Campaign` model

### What

- Unified way to create and manage different types of Campaigns

### How

- Add type enum to existing `Campaigns` model
  - `public`: Marketplace campaigns (available to all)
  - `exclusive`: Only visible on a merchant's custom subdomain and for affiliates selected by the merchant
  - `private`: Fully hidden campaigns, only available via invite (NTH in future)
    - Additional permissions logic can control who can access and manage private campaigns
      Affiliates can only see them if invited directly
    - Merchant can invite Affiliates with specific skills to such campaigns

- Exclusive and Private campaigns won't be visible on Marketplace dashboard
- While private campaign is completely locked to merchants, no one can view them

### Achievements

- One model to rule them all
- Simplicity

## Step 2: Marketplace APIs/Pages

### What

Create dedicated APIs/pages for Marketplace dashboard

### How

- Campaign list APIs/pages for market place with default scope to public campaigns only
- Various filters (e.g., search by merchant/company, tags, topics)
  - Use [pg_search](https://github.com/Casecommons/pg_search)
    that uses Postgres full text search (tsvector)
  - Or on more extreme side, ElasticSearch could be an option too
    Would avoid ES though to keep things simpler from team learning curve and infra complexities perspectives
  - If we wait a bit longer Rails 8.1 is coming with Active Record Search out of the box

- Ensure APIs are paginated by default to handle large data volumes efficiently
- All campaign types might even be able to share the same UI code/page scoped to that specific type
  and RBAC e.g. based on subdomain and user role

- Scope API access and visibility of campaigns based on user roles and permissions (RBAC)
  (e.g. private campaigns should be accessible only by the invited affiliates)

### Achievements

- Marketplace APIs/pages are ready, and the architecture supports future extension without immediate overhead

## Step 3: Campaign management

### What

Merchants/companies need admin interface to manage their public and private campaigns centrally

### How

- Single form for merchants to create, update, archive campaigns (public/exclusive/private)
- Manage affiliates, payments, and rewards through a unified dashboard
- Enable RBAC to manage campaigns to specific roles (e.g. merchant admins)
- Allow changing campaigns from private to public and vice versa

### Achievements

- Full self-service model for merchants

## Step 4: Central affiliation managements for Affiliates

### What

Affiliates need a central place to manage all their campaigns public and private alike

### How

- Affiliates can search and apply for campaign from Marketplace
- They can now access all the campaigns they are part of from their profile centrally
- Easily jump to merchant specific dashboard from this central repository of their campaigns (polymorphic_url)
- View claim, and manage their commission pay outs and earned rewards

### Achievements

- Easy one stop UX for Affiliates

## Considerations and Next steps

### Notifications and Recommendation engine

- Based on the company, campaign and Affiliate areas of interests/skills a match making algorithm
  can be used to provide relevant suggestions to merchants and affiliates alike

- Allow affiliates to subscribe to email notification for new matches with easy apply option
- Merchants can review applications and grant access to the campaign
- Similarly merchants can invite affiliates based on their published profile,
  affiliate gets email notification, they can then accept or reject the invitation

### State machine

- Introduce state machine to manage campaign creation (if not already)
- Use states like `draft, published, archived`
- Provides higher flexibility when managing campaigns

### Future scaling

- Imagine a scenario of extreme scale and huge data turnover
- Caching, clustered deployment with egress reverse proxy like Nginx can be used and provide autoscaling

### Robust monitoring

Use tools like Sentry, UptimeRobot, Datadog or NewRelic to keep an eye on system performance.
  However, it is important to pay attention to cost and budget with these tools.

### Analytics

- Tools like Google Analytics and Hotjar can be introduced for this
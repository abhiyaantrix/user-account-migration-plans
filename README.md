# Unified user accounts and public marketplace

Detailed technical plans to separate user account data to dedicated Rails model in a live environment

There are two parts involved

**[Problem statement](./1_problem_document.md)**

**Proposed solutions**

1. Unifying user account
   1. [Option 1](./2_unified_user_accounts.md) - Using intermediate table
   2. [Option 2](./2.1_unified_user_accounts_with_upsert.md) - Using `upsert`
2. [Building Marketplace feature](./3_unified_campaign_model.md)

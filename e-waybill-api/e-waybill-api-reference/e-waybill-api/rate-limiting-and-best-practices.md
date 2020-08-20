---
description: Rate limiting & best practices all explained in this section.
---

# Rate Limiting & Best Practices

**Rate Limiting** : Currently, there is no rate limit. You are requested to apply judicial discretion while using ClearTax APIs to ensure overall level of service on our API server for all users.

**Best Practices :** 

1. Upload only 1 file at a time.
2. Space out multiple requests evenly to reduce load on our server.
3. Limit file size to 1 Mb to ensure faster processing and validation.
4. While there is practically no limitation on the number of rows or documents per file, for the purpose of optimization, we have a maximum limit of 250 line items per document in a file.


---
title: "No Country for Old Keys"
date: 2025-04-28 10:40:00 +02:00
categories: [Writeups, CIT_CTF, OSINT]
tags: [CIT_CTF, OSINT]
---

# No Country for Old Keys - Write-up

## Challenge Overview
The objective of this challenge was to find Anthony McConnolly's API key. Given the nature of the task, the first logical step was to investigate his online presence, starting with GitHub, a common platform where developers might inadvertently expose sensitive information like API keys.

## Locating Anthony McConnolly's GitHub Profile
I began by searching for Anthony McConnolly on GitHub. Fortunately, I quickly found his profile, which contained a repository for an application he had created:

![Anthony's GitHub profile](/assets/images/CIT/no_country_for_old_keys_1.png)

The repository seemed promising, as API keys are often hardcoded into application source code, especially by less experienced developers.

## Inspecting the Repository
I explored the repository to look for any visible API keys in the codebase. At first glance, the key appeared to have been removed or was not present in the latest version of the code:

![Repository code view](/assets/images/CIT/no_country_for_old_keys_3.png)

However, I knew that even if sensitive data is removed from the current version, it might still be accessible in the repository's commit history — a common oversight in GitHub repositories.

## Checking the Commit History
I navigated to the repository’s commit history to see if any previous commits might contain the API key. One commit in particular caught my attention, as its message or changes hinted at the inclusion of sensitive data:

![Commit history](/assets/images/CIT/no_country_for_old_keys_4.png)

Digging into the details of this commit, I found the API key hardcoded in the code:

![Commit with API key](/assets/images/CIT/no_country_for_old_keys_5.png)

The API key in the commit was the flag for this challenge.

## Conclusion
This challenge highlighted the importance of thoroughly reviewing a developer's GitHub activity when searching for sensitive information like API keys. While the key was removed from the latest version of the code, the commit history revealed an earlier version where it was exposed. This is a reminder to developers to avoid hardcoding sensitive data in public repositories.

**Flag**: `CIT{ap9gt04qtxcqfin9}`

## Tools Used
- Web browser: To search for Anthony McConnolly’s GitHub profile.
- GitHub: To explore the repository and its commit history.

## Tips for Similar Challenges
- Always start by searching for the target’s online presence on platforms like GitHub, GitLab, or Bitbucket.
- Check the commit history of repositories, as sensitive data might be present in earlier commits even if it’s been removed from the latest version.
- Use GitHub’s search functionality to look for keywords like `api_key`, `token`, or `secret` in the code.
- Be aware that exposing API keys in public repositories is a common security mistake — commit histories are often overlooked by developers.
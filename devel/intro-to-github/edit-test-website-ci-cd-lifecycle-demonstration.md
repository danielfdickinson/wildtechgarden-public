---
imageFeatured: /assets/images/cover/ci-cd-netlify-18-1-1024x676.png
slug: edit-test-website-ci-cd-lifecycle-demonstration
aliases:
    - /29/edit-test-website-ci-cd-lifecycle-demonstration/
    - /2020/08/29/edit-test-website-ci-cd-lifecycle-demonstration/
    - /post/edit-test-website-ci-cd-lifecycle-demonstration/
    - /edit-test-website-ci-cd-lifecycle-demonstration/
    - /docs/development/git-github-gitea/introduction-to-git-and-github/edit-test-website-ci-cd-lifecycle-demonstration/
    - /develop-design/intro-to-github/29/edit-test-website-ci-cd-lifecycle-demonstration/
    - /develop-design/intro-to-github/edit-test-website-ci-cd-lifecycle-demonstration/
    - /intro-to-github/edit-test-website-ci-cd-lifecycle/
    - /post/intro-to-github/edit-test-website-ci-cd-lifecycle/
    - /posts/intro-to-github/edit-test-website-ci-cd-lifecycle/
author: Daniel F. Dickinson
date: '2021-03-08T09:49:08+00:00'
publishDate: '2020-08-29T19:40:00+00:00'
tags:
- devel
- git
- sysadmin-devops
- web-design
- website
title: Edit-Test-Website CI/CD Lifecycle Demonstration
description: "Example of a Netlify-based website CI/CD lifecycle on GitHub"
featuredImageAlt: "Screenshot of a GitHub pull request from 2020 (light mode) with partially complete Continuous Integration checks"
---

## Tools Used

* For this demonstration we show the use of [Visual Studio Code](https://code.visualstudio.com/)
* We also use [GitHub](https://github.com)
* And [Netlify](https://www.netlify.com)

## Before Website

![screenshot of website before pushing commit](../../assets/images/ci-cd-netlify-0-1-1024x676.png) screenshot of website before pushing commit

## Creating a Commit

### Create a Branch

Not shown here, but you should create a separate branch to create a pull
request.

### Edit the Post

![screenshot of a post in Visual Studio Code with the text to be deleted highlighted](../../assets/images/ci-cd-netlify-01-1.png)
Post in Visual Studio Code with text to be deleted highlighted

### Stage Your Changes

Not shown here, but you should ‘stage’ the changes you want to commit.

### Add a Commit Message

![screenshot of adding a commit message in Visual Studio Code](../../assets/images/ci-cd-netlify-06-1.png) screenshot of adding a commit message in Visual Studio Code

### Commit

![screenshot after pressing 'Ctrl-Enter' to create the commit](../../assets/images/ci-cd-netlify-07-1.png) screenshot after pressing ‘Ctrl-Enter’ to create the commit

## Create a Pull Request

### Push the Commit to GitHub

![screenshot showing push on popup menu](../../assets/images/ci-cd-netlify-10-1-1024x676.png)
screenshot showing push on popup menu

#### If Applicable Select the GitHub ‘Remote’

For most beginners this will be ‘origin’.

![screenshot of selecting a remote](../../assets/images/ci-cd-netlify-11-1-1024x676.png) screenshot of selecting a remote

### From the Branch Create a Pull Request

#### Go to GitHub and Select Compare & Pull Request

![screenshot of creating a pull request](../../assets/images/ci-cd-netlify-13-1-1024x676.png)
screenshot of creating a pull request

#### Update the Pull Request Title (If More than One Commit)

![screenshot of setting the pull request title](../../assets/images/ci-cd-netlify-15-2.png) screenshot of setting the pull request titl

#### Actually Create the Pull Request

Screenshot is from another PR

![screenshot creating the pull request](../../assets/images/ci-cd-netlify-49-1-1024x676.png)
screenshot of creating a pull request

#### Wait for CI Checks to Complete

![screenshot of unfinished CI checks](../../assets/images/ci-cd-netlify-18-1-1024x676.png)
screenshot of unfinished CI checks

## Make sure the Continuous Integration Tests Succeeded

### Review the Test Results in GitHub

![screenshot of completed CI checks](../../assets/images/ci-cd-netlify-19-1-1024x676.png)
screenshot of completed CI checks

### Review the Preview Deploy (Netlify)

Sample preview is from a different PR

![reviewing a preview deploy on Netlify — note the URL](../../assets/images/ci-cd-netlify-54-1-1024x676.png)
reviewing a preview deploy on Netlify — note the URL

## Take the Changes Live

### Merge the Pull Request

![screenshot of merging pull request](../../assets/images/ci-cd-netlify-49-1-1024x676.png)
screenshot of merging pull request

### Verify (Once CI Tests Complete) The Site Has Been Updated

![screenshot of new post blurb on front page of live site](../../assets/images/ci-cd-netlify-24-1-1024x676.png)
screenshot of new post blurb on front page of live site

## Cleanup on GitHub

### Delete the PR Branch

![screenshot of deleting PR branch](../../assets/images/ci-cd-netlify-57-1-1024x676.png)
screenshot of deleting PR branch

## Merge the Changes Back to Your Local Repository

### Pull the Changes from GitHub

Screenshot from another PR

![screenshot of pull from remote git](../../assets/images/github-operations-35-1-1024x676.png)
screenshot of pulling from remote git

### Fetch with Prune (Cleans Copy of the GitHub Branches)

Screenshot from another PR

![screenshot of fetch with prune from remote git](../../assets/images/github-operations-25-1-1024x676.png)
screenshot of fetch with prune from remote git

## Cleanup

### Delete Your Local Copy of the PR Branch

Screenshot from another PR

![screenshot of deleting local branch](../../assets/images/github-operations-31-1-1024x676.png)
screenshot of deleting local branch

### Verify the Git History

Screenshot from another PR

![screenshot of git history](../../assets/images/github-operations-49-1-1024x676.png)
screenshot of git history

## After Website

And the final result is post is live on your website and your local repo is in
sync with GitHub.

![screenshot of new post blurb on front page of live site](../../assets/images/ci-cd-netlify-24-1-1024x676.png)
screenshot of new post blurb on front page of live site

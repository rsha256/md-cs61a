# Contributing to this Guide
First things first, thanks for taking the time to contribute and make sure that Berkeley's CS education after you can learn from your insight!

What follows is a set of guidelines for contributing to this guide, but these are in no way set in stone. Use your best judgment, and as always, feel free to propose changes to these guidelines through a pull request.

## Code of Conduct
By contributing to an intellectual resource, you're probably not going to need someone to tell you how to act. That said, if you'd feel more comfortable having one, here's the [UC Berkeley Code of Student Conduct](https://sa.berkeley.edu/sites/default/files/Code%20of%20Conduct_January%202016.pdf). Uphold this code, and use your best judgment. Report any inappropriate behavior to `vanshaj (at) berkeley (dot) edu`.

## Content Structure
Below is a rough idea of what the content structure looks like. Feel free to peruse the repository to get an idea of what it looks like in action.

### Weeks
Every week has its own directory, with the (short) directory title specifying the broad category of content to be covered that week. Within these directories, there's an `_index.md` file with the following structure:

```markdown
+++
title = "Welcome to 61A!"
weight = 1
chapter = true
pre = "<b>Week 1. </b>"
+++

# Welcome to 61A!

Let's get you setup with Python and introduce you to the very rudimentary basics of the language.
```

The idea is to keep it short and sweet, a brief "welcome to this week" message, if you will.

### Weekly Content
Each week then has relevant content stored in Markdown files as well. These look like this:

```markdown
---
title: "What is CS 61A?"
weight: 4
authors: ["Vanshaj Singhania"]
---

Now that we've established some of my incoherent thoughts about computer science, let's take a look at what this class in particular is about.

<!--more-->
```

The only thing to point out here, importantly, is the `weight`. Things are ordered within a week by weight, and weeks are ordered by (a separate) weight as well -- this is just how the theme is setup, so please follow the convention!

## How Do I Contribute?
Great questions!
### Reporting Bugs
Bugs are tracked as [GitHub issues](https://guides.github.com/features/issues/). Create an issue and describe as exactly as you can what the issue is -- does something look off? Is a variable or function call incorrect? Is there a typo?

If there's a rendering issue, please don't create an issue -- this repository is for content only, and it'd be best for all contributors if the content was kept separate from the website I host. If you *do* find such an issue, let me know in person or via email!

### Fixing Bigger Issues
If there's a code chunk or section that's completely wrong or has other glaring issues, feel free to submit a pull request using the following general template:
- **Describe the issue.** What part of the existing content was wrong or confusing? What made it confusing?
- **Explain your changes.** How did you fix the issue?
- **Make sure you added your name to the `authors` parameter.** This isn't strictly required, but if you'd like to go down in eternal glory, make sure you add your name!

### Adding More Content
I (VS) do my best to write to this guide, but if I did it on my own it would be a painfully slow process. That's why I invite you to add content as you see fit! If you feel that you can contribute helpful material, please submit a pull request using the following general template:
- **Describe your content.** What are you adding? How recently was this content introduced to 61A? How will it help students who take the class learn more?
- **Check to ensure you're not using any problems from class.** The 61A course staff tends to reuse problems, especially on homeworks and labs, so please make sure you don't use one of these as an example -- we don't want to spoil the fun!
- **Make sure you added your name to the `authors` parameter.** This isn't strictly required, but if you'd like to go down in eternal glory, make sure you add your name!

In any case, please follow the styleguides, described below.

## Styleguides
### Git Commit Messages
- Use the present tense in an imperative mood ("Fix week 1 index", not "Fixed week 1 index" or "Fixes week 1 index")
- Don't end your commit messages with a period
- Limit the first line to 80 characters, ideally less
- Freely reference issues or PRs in subsequent lines

### Markdown
- Use the templated defaults enumerated above
  - Especially note that weeks' meta sections start with `+++`, and content meta sections start with `---`
  - Also note that meta order is `title`, then `weight`, then `authors`
- When writing mathematical expressions or formulas, use [MathJax](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
- Use the following template for a note (renders in a blue box):
```markdown
{{% notice note %}}
For a history of Python, check out [Chapter 1.1.1 in *Composing Programs*](http://composingprograms.com/pages/11-getting-started.html#programming-in-python), your course textbook.
{{% /notice %}}
```
- When writing code chunks, try not to mix and match interpreter code with files
  - When writing interpreter chunks, make sure to include `>>>` to denote input
  - If defining a function in an interpreter chunk, make sure to include `...` on subsequent lines, just as the Python interpreter would:
```python
>>> def hi():
...     print('HI')
... 
>>> hi()
HI
```
- When writing interpreter chunks, omit the final blank `>>>` input line
- If you define a function/variable in a non-interpreter context, feel free to use it in an interpreter context
   - But again, create separate code chunks when doing this

That's it! Thanks for reading through this guide, and thanks in advance for helping make this place amazing. Your reward? Eternal glory when you submit something and add your name to the contributors -- printed, of course, on every page you contribute to :)
---
title: "Internship with Wikimedia"
published: true
---

It's been just a while since my internship with Wikimedia started in Outreachy and I am already learning a lot! In this blog, I will be sharing what my project is all about and a couple of things I have learned or re-learned in these days and are some common technologies that many other open-source networks use as well.

This post is going to be quite long as I will be sharing my progress as I go through the internship. Some parts of it will be useful for students looking for internship and want to familiarize with what open source encompasses, or simply people loooking to join the open source fun! I listed those in `Techs`. Feel free to only look at these topics. Others can look at the entire thing to familiarize with wikimedia in general, or more specific details about the project I will be working on.

## Techs
- IRS
- Git, GitHub and Gerrit
- Docker, Vagrant

## Contents:
1. Project Description
    - Wikimedia
    - Wikipedia
    - Abstract Wikipedia
    - Wikilambda
    - Wikidata
2. What am I working on?
3. Some initial set-up to join wikimedia
    - Wikitech, Gerrit, Phabricator Account, IRS
    - More about Git and Gerrit
    - Docker set-up
    - Mailing lists
4. Learning resources
    - Wikimedia
    - Guidelines
5. Progress

## Project Description
In short, the beginning of a huge change. We all know about Wikipedia and how it has been helping miilions of people around the world get access to free and open knowledge. And more importantly how anyone around the world can contribute to this endeavour through adding, correcting, or updating information in the wikis. But did you know Wikipedia is a project under the [Wikimedia](https://www.wikimedia.org/) foundation?

#### Wikimimedia
> The Wikimedia Foundation Inc. is the parent organization free-content projects, most notably Wikipedia, the award-winning online encyclopedia.
> The mission of the Wikimedia Foundation is to empower and engage people around the world to collect and develop educational content under a free license or in the public domain, and to disseminate it effectively and globally.

Other projects include Wikitionary, Wikibooks, Wikinews, MediaWiki (the software that runs it all), Wikidata, Wikimedia commons etc.

#### Wikipedia
Wikipedia is free and the largenst encyclopedia hosted in lots of different languages. The way it roughly works at the moment is 
- The languages have contents in them independently, updating in one language does not update the same topic in other languages. The other language may not even have that page.
- Adding content in any language requires community effort.
- There are some templates and functions that act as helpers to create wiki pages, but their usage is independent among languages. e.g functions to calculate age, distance etc. So if one page uses a function, it is not necessarily carried over to other languages. One has to copy-paste this function to use it in their language.

This is where Abstract Wikipedia comes in.

#### Abstract Wikipedia
What if we did not store information in each and every langauge separately? What if we had a notational way to store data in a 'single' place? All languages could use this data and generate wiki pages in respective languages. This can increase the richness of so-many wiki languages, maintain consistent updated information and most importantly this will pool efforts of people of all languages into one platform, making knowledge gathering and dissemination across languages a breeze.

This is the [Abstract Wikipedia](https://meta.wikimedia.org/wiki/Abstract_Wikipedia) project. Super cool! To know about it in more detail, see [this](https://arxiv.org/abs/2004.04733).
> The goal is to allow everyone to contribute and read content in Abstract Wikipedia, no matter what languages they understand, and to allow people with different languages to work on and maintain the same content.

#### Wikilambda
As I briefed above, Abstract wikipedia will require a knowledge base and a way to turn that knowledge into any natural language. The knowledge base is called Wikidata and the process to make language is through Wikilambda. 
> Wikilamdbda is a wiki of functions. For Abstract Wikipedia, we will need functions that take abstract content as the input and return natural language text as the output. Wikilambda aims at making access to functions and
writing and contributing new functions as simple as contributing to Wikipedia.

See more details in the [paper]((https://arxiv.org/abs/2004.04733)) I talked about previously. But basically Wikilambda will store information in a structural form, indicating how the various things in a sentence are related. 
For example, 'Sanfrancisco is the fourth-most populous city in California, after Los Angeles, San Diego and San Jose'. We can express it as a function:
```
Article(
    content: [
        Ranking(
            subject: San Francisco (Q62),
            rank: 4,
            object: city (Q515),
            by: population (Q1613416),
            local_constraint: California (Q99),
            after: [Los Angeles (Q65),
                    San Diego (Q16552),
                    San Jose (Q16553)]
        )
    ]
)
```
Here each name/term is denoted by a id (like Q99) and thus can be identified across languages. Now if I were to extract this information in Bangla, I would call this function and ask for a output in Bangla. Or any other language for that matter. But how can a machine know how to generate language from words and their relations? 

#### Wikidata
Did I mention that the key-values for the ids (like Q99) are stored in wikidata? Wikidata also holds information about languages (lexicographic knowlegde) to be able to render sentences in any language from the Wikilambda functions. Wikidata is already used in Wikipedia to some extent - to create infoboxes or extract certain pieces of information - but not to generate language, yet.

The way wikidata can be populated with language info is with community effort. Various communities will have to provide lexicographic knowlegde of their respective languages, ultimately creating a rich ecosystem of information flow. Notice, the amount of explicit language information required with Abstract Wikipedia will be much-much less than amount we have to build up in the current wikipedia, i.e for every topic in out language.

This is not to say that a sudden breaking change will occur when Abstarct Wikipedia comes into play. Infact, Abstract Wikipedia will join in with the existing multi-lingual wikipedia and build on it enormously and swiftly.

## What am I working on?

Phabricator [`T263678`](https://phabricator.wikimedia.org/T263678)

**Analyze community authored functions that build Wikipedia infoboxes and more**

> Finding the different community authored functions that are out there and helping to prioritize which ones would be good candidates for centralizing for Abstract Wikipedia and its centralized wiki of functions.

Tasks:
- Determine usage of community authored functions in articles and pageviews.
- Use open-source packeages to find code similarity among the functions and identify redundant ones.
- Modularize code segments, both programatically and manually.
- Publish methodology and reoports to be included as Abstract Wikiedia subage.
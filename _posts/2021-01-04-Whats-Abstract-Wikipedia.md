---
title: "What's Abstract Wikipedia?"
published: true
---

Hi, I am Aisha, Interning with Wikimedia on the Abstract Wikipedia project along with Jade (her [blog](https://dev.to/lost_enchanter/abstract-wikipedia-as-a-step-to-better-future-4lce)), who is also an Outreachy intern. It's been 5 whole weeks since the start of the internship and I have learned so much and gotten more and more excited about what our work will bring to the project and to the future of Wikipedia as a whole. Since the start of my internship, I have been eager to get more people to know about Abstract Wikipedia, share things I have learned, and write about ways to overcome struggle in certain areas of Open Source and Wikimedia. All of those plus my internship progress is blogged [here](https://tanny411.github.io/2020/12/05/Internship-With-Wikimedia/). But for this post, I just want you to get acquainted with Abstract Wikipedia and my work.

We all know about Wikipedia and how it has been helping millions of people around the world get access to free and open knowledge. And more importantly how anyone around the world can contribute to this endeavor through adding, correcting, or updating information in the wikis. But did you know Wikipedia is a project under the [Wikimedia](https://www.wikimedia.org/) foundation?

## Wikimedia

> The Wikimedia Foundation Inc. is the parent organization free-content projects, most notably Wikipedia, the award-winning online encyclopedia.
> The mission of the Wikimedia Foundation is to empower and engage people around the world to collect and develop educational content under a free license or in the public domain, and to disseminate it effectively and globally.

Other projects include Wiktionary, Wikibooks, Wikinews, MediaWiki (the software that runs it all), Wikidata, Wikimedia commons, etc.

## Wikipedia

The Wikimedia Foundation is a non-profit with the aim that `every single human being can share freely in the sum of all knowledge`. On its face, it may seem easy or something Wikipedia has already accomplished unless you start getting deeper into the project and see what's going on. Consider languages other than English, French, or some of the few common languages. Not only do these languages have drastically fewer Wikipedia articles (despite being used WIDELY as spoken and written language) but even the articles that are written may not be comprehensive or comprises of just some introductory paragraphs.

Here is a short comparison of the number of articles in a few languages. `Rank of language` is their rank by the total number of speakers of that language worldwide (source: [Wikipedia](https://en.wikipedia.org/wiki/List_of_languages_by_total_number_of_speakers))

| Wikipedia  | #Articles   | Rank of language |
| ---------- | ----------- | ---------------- |
| English    | 6.2 million | 1                |
| Chinese    | 1.2 million | 2                |
| Hindi      | 144 k       | 3                |
| Spanish    | 1.6 million | 4                |
| French     | 2.3 million | 5                |
| Arabic     | 1 million   | 6                |
| Bengali    | 101 k       | 7                |
| Russian    | 1.7 million | 8                |
| Portuguese | 1 million   | 9                |
| Indonesian | 555 k       | 10               |

I mean just look at Bengali and Hindi for a second. Despite being the 7th and 3rd most spoken language in the world, the amount of knowledge in these languages in Wikipedia is 1/60 th of English! Not to mention even the 2nd most spoken language is 1/6 th of that of English. Knowing English is a privilege not everyone has and is not even the second language in many countries. Not only are many people being deprived of knowledge in their language, but others are also deprived of so much information these people can provide.

The way it roughly works at the moment is

- The languages have contents in them independently, updating in one language does not update the same topic in other languages. The other language may not even have that page.
- Adding content in any language requires community effort.
- There are some templates and functions that act as helpers to create wiki pages, but their usage is independent among languages. e.g functions to calculate age, distance, etc. So if one page uses a function, it is not necessarily carried over to other languages. One has to copy-paste this function to use it in their language.

This is where Abstract Wikipedia comes in.

## Abstract Wikipedia

What if we did not store information in each and every language separately? What if we had a notational way to store data in a 'single' place? All languages could use this data and generate wiki pages in their respective languages. This can increase the richness of so-many wiki languages, maintain consistently updated information and most importantly this will pool efforts of people of all languages into one platform, making knowledge gathering and dissemination across languages a breeze.

This is the [Abstract Wikipedia](https://meta.wikimedia.org/wiki/Abstract_Wikipedia) project. Super cool! To know about it in more detail, see [this](https://arxiv.org/abs/2004.04733).

> The goal is to allow everyone to contribute and read content in Abstract Wikipedia, no matter what languages they understand, and to allow people with different languages to work on and maintain the same content.

## Wikifunctions

As I briefed above, Abstract Wikipedia will require a knowledge base and a way to turn that knowledge into any natural language. The knowledge base is called Wikidata and the process to make language is through Wikifunctions.

> Wikifunctions is a wiki of functions. For Abstract Wikipedia, we will need functions that take abstract content as the input and return natural language text as the output. Wikifunctions aims at making access to functions and writing and contributing new functions as simple as contributing to Wikipedia.

See more details in the [paper](https://arxiv.org/abs/2004.04733) I talked about previously. But basically, Wikifunctions will store information in a structural form, indicating how the various things in a sentence are related.
For example, 'San Francisco is the fourth-most populous city in California, after Los Angeles, San Diego, and San Jose'. We can express it as a function:

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

Here each name/term is denoted by an id (like Q99) and thus can be identified across languages. Now if I were to extract this information in Bangla, I would call this function and ask for output in Bangla. Or any other language for that matter. But how can a machine know how to generate language from words and their relations?

## Wikidata

Did I mention that the key-values for the ids (like Q99) are stored in Wikidata? Wikidata also holds information about languages (lexicographic knowledge) to be able to render sentences in any language from the Wikifunctions functions. Wikidata is already used in Wikipedia to some extent - to create infoboxes or extract certain pieces of information - but not to generate language, yet.

The way Wikidata can be populated with language info is with community effort. Various communities will have to provide lexicographic knowledge of their respective languages, ultimately creating a rich ecosystem of information flow. Notice, the amount of explicit language information required with Abstract Wikipedia will be much much less than the amount we have to build up in the current Wikipedia, i.e for every topic in our language.

This is not to say that a sudden breaking change will occur when Abstract Wikipedia comes into play. In fact, Abstract Wikipedia will join in with the existing multi-lingual Wikipedia and build on it enormously and swiftly.

## What am I working on?

**Analyze community authored functions that build Wikipedia infoboxes and more**: [Phabricator](https://phabricator.wikimedia.org/T263678) and [GitHub](https://github.com/wikimedia/abstract-wikipedia-data-science)

> Finding the different community authored functions that are out there and help prioritize which ones would be good candidates for centralizing for Abstract Wikipedia and its centralized wiki of functions.

As I've mentioned, Wikipedia uses Wikifunctions to generate information, parts of pages, or templates. My work for this internship is to take the first step to start centralizing the Wikifunctions in a language-independent manner.

- First step is to collect and store all the community authored functions across all wikis (all languages and all wiki sites, not just Wikipedia). Besides the source code of the functions, I also collected statistics about the functions using the mediawiki API and all the wiki databases, such as where are these modules (i.e functions) used. In how many languages are they used etc.
- Next step is to perform data analysis on all these data to identify which functions are most important to be centralized in Abstract Wikipedia. You can get a good sense of why that's necessary when you look at the same module in [English](https://en.wikipedia.org/wiki/Module:Yesno) and another language like [Bangla](https://bn.wikipedia.org/wiki/%E0%A6%AE%E0%A6%A1%E0%A6%BF%E0%A6%89%E0%A6%B2:Yesno). Their codes are basically the same, just some language contents differ.
- After we identify important modules, we will perform code similarity analysis and try to remove as much redundancy as possible by merging the similar codes from across languages, modularize code along the way as required.

For more information, find my work progress [here](https://www.mediawiki.org/wiki/User:Aisha_Khatun) and [here](https://tanny411.github.io/2020/12/05/Internship-With-Wikimedia/)

## Abstract Wikipedia and Deep learning NLP

There might be questions as to why we are not using modern translation models to just create Wikipedia pages? Let's just be honest with ourselves here, have you seen google translate? It's far from perfect, and more importantly, where does all the data for training all the huge language models or translation models come from? Wikipedia! and more of course.

This brings me to the next topic: Why am I so excited about our project? Glad you asked!

Ever since I got acquainted with Deep learning and NLP I've been seeing such great progress in this field with ULMFiT, BERT, GPT-2,3, etc. These models are bringing us closer and closer to machine-generated text that looks much like human language but they do require LOTS of data and LOTS of computation. The majority of these data come from Wikipedia and then some are scraped from the web. When I started using and implementing these models in Bangla (my native language) I realized the drastic difference of available Bangla text in Wikipedia and there began my concerns (besides not having that much computational power of course). Google released `multi-lingual BERT` which was trained on 100+ languages taking texts of all these languages from Wikipedia. Unfortunately, it only works well for the languages it has the most data of, English, French, etc.

Due to lack of enough community members contributing to the wikis, the number of people aware of this situation, and the barrier to entry, many languages are still under represented in Wikipedia. When I came across this project and the idea of Abstract Wikipedia my mind was blown! If we can find a way to represent knowledge without using language at all, that would open so many doors. Then Wikidata can help convert that knowledge into whatever language we want it to show us. Now the community has to contribute to building the lexicographic information of the language instead of trying to fill up more and more articles in their language.

I hope I was able to give an idea of the `what` and `how` of what I am working on and why it is so important and exciting. Next time you use Google translate or work on your NLP project, think of Wikipedia for a while. Cheers!

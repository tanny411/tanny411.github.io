---
title: "Internship with Wikimedia"
published: true
---

It's been just a while since my internship with Wikimedia started in Outreachy and I am already learning a lot! In this blog, I will be sharing what my project is all about and a couple of things I have learned or re-learned in these days and are some common technologies that many other open-source networks use as well.

This post is going to be quite long as I will be sharing my progress as I go through the internship. Some parts of it will be useful for people looking for internship and want to familiarize with what open source encompasses, or simply people looking to join the open source fun!

### General purpose content: 
Some things to know about in general as a SE. Or to join open source.
- Gerrit
- Docker
- SSH
- IRS
- Mailing lists

## Contents:
1. [Project Description](#project-description)
    - Wikimedia
    - Wikipedia
    - Abstract Wikipedia
    - Wikilambda
    - Wikidata
2. [What am I working on?](#what-am-i-working-on)
3. [Initial set-up](#initial-set-up)
    - Accounts
    - Gerrit, Docker
    - SSH
    - IRS
    - Mailing lists
4. [Onboarding and learning resources](#onboarding-and-learning-resources)
    - Wikimedia
    - On-boarding
5. [Learning Progress](#learning-progress) 
6. [Internship Progress](#internship-progress)

## Project Description
In short, the beginning of a huge change. We all know about Wikipedia and how it has been helping millions of people around the world get access to free and open knowledge. And more importantly how anyone around the world can contribute to this endeavour through adding, correcting, or updating information in the wikis. But did you know Wikipedia is a project under the [Wikimedia](https://www.wikimedia.org/) foundation?

### Wikimedia
> The Wikimedia Foundation Inc. is the parent organization free-content projects, most notably Wikipedia, the award-winning online encyclopedia.
> The mission of the Wikimedia Foundation is to empower and engage people around the world to collect and develop educational content under a free license or in the public domain, and to disseminate it effectively and globally.

Other projects include Wikitionary, Wikibooks, Wikinews, MediaWiki (the software that runs it all), Wikidata, Wikimedia commons etc.

### Wikipedia
Wikipedia is free and the largest encyclopedia hosted in lots of different languages. The way it roughly works at the moment is 
- The languages have contents in them independently, updating in one language does not update the same topic in other languages. The other language may not even have that page.
- Adding content in any language requires community effort.
- There are some templates and functions that act as helpers to create wiki pages, but their usage is independent among languages. e.g functions to calculate age, distance etc. So if one page uses a function, it is not necessarily carried over to other languages. One has to copy-paste this function to use it in their language.

This is where Abstract Wikipedia comes in.

### Abstract Wikipedia
What if we did not store information in each and every language separately? What if we had a notational way to store data in a 'single' place? All languages could use this data and generate wiki pages in respective languages. This can increase the richness of so-many wiki languages, maintain consistent updated information and most importantly this will pool efforts of people of all languages into one platform, making knowledge gathering and dissemination across languages a breeze.

This is the [Abstract Wikipedia](https://meta.wikimedia.org/wiki/Abstract_Wikipedia) project. Super cool! To know about it in more detail, see [this](https://arxiv.org/abs/2004.04733).
> The goal is to allow everyone to contribute and read content in Abstract Wikipedia, no matter what languages they understand, and to allow people with different languages to work on and maintain the same content.

### Wikilambda
As I briefed above, Abstract wikipedia will require a knowledge base and a way to turn that knowledge into any natural language. The knowledge base is called Wikidata and the process to make language is through Wikilambda. 
> Wikilambda is a wiki of functions. For Abstract Wikipedia, we will need functions that take abstract content as the input and return natural language text as the output. Wikilambda aims at making access to functions and
writing and contributing new functions as simple as contributing to Wikipedia.

See more details in the [paper]((https://arxiv.org/abs/2004.04733)) I talked about previously. But basically Wikilambda will store information in a structural form, indicating how the various things in a sentence are related. 
For example, 'San francisco is the fourth-most populous city in California, after Los Angeles, San Diego and San Jose'. We can express it as a function:
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

### Wikidata
Did I mention that the key-values for the ids (like Q99) are stored in wikidata? Wikidata also holds information about languages (lexicographic knowledge) to be able to render sentences in any language from the Wikilambda functions. Wikidata is already used in Wikipedia to some extent - to create infoboxes or extract certain pieces of information - but not to generate language, yet.

The way wikidata can be populated with language info is with community effort. Various communities will have to provide lexicographic knowledge of their respective languages, ultimately creating a rich ecosystem of information flow. Notice, the amount of explicit language information required with Abstract Wikipedia will be much-much less than amount we have to build up in the current wikipedia, i.e for every topic in out language.

This is not to say that a sudden breaking change will occur when Abstract Wikipedia comes into play. In fact, Abstract Wikipedia will join in with the existing multi-lingual wikipedia and build on it enormously and swiftly.

## What am I working on?

Phabricator [`T263678`](https://phabricator.wikimedia.org/T263678)

**Analyze community authored functions that build Wikipedia infoboxes and more**

> Finding the different community authored functions that are out there and help prioritize which ones would be good candidates for centralizing for Abstract Wikipedia and its centralized wiki of functions.

Tasks:
- Determine usage of community authored functions in articles and pageviews.
- Use open-source packages to find code similarity among the functions and identify redundant ones.
- Modularize code segments, both programmatically and manually.
- Publish methodology and reports to be included as Abstract Wikipedia sub-page.

Find me here:
- https://www.mediawiki.org/wiki/User:Aisha_Khatun
- https://meta.wikimedia.org/wiki/Abstract_Wikipedia/Updates/2020-12-09
- https://www.mediawiki.org/wiki/Outreachy/Round_21#Accepted_projects
- https://www.outreachy.org/alums

And our work here:
- https://github.com/wikimedia/abstract-wikipedia-data-science

## Initial set-up
To set up my existence in Wikimedia I had to follow a few steps. This section is not for anyone to follow but a mere report of what I have been doing. One of the best things I find in wikimedia is the organization and instructions. There are instructions for _everything_. Anything I can conceivably need to start contributing to wikimedia, they have a wiki of instructions and troubleshooting for it. This just makes life so much more easier.

### Accounts 
First is to create a bunch of accounts. This seemed a little confusing at first, but various domains on wikimedia require separate account creation and thus separate user pages. User pages are those that end in `User:your_name`. 

- Creating a user page in meta wiki is the best idea. This user page gets displayed in other domains where there isn't a user page in your name. For example if you create one in `meta.wikimedia.org`, it will show up in `en.wikipedia.org`. I did create one in mediawiki separately to post updates about the internship. My user pages are:
    - https://meta.wikimedia.org/wiki/User:Aisha_Khatun
    - https://www.mediawiki.org/wiki/User:Aisha_Khatun
    - https://en.wikipedia.org/wiki/User:Aisha_Khatun (auto)
- Also for development purposes I created a [wikitech account](https://wikitech.wikimedia.org/wiki/Special:CreateAccount), aka Wikimedia developer account or LDAP account. This account is also connected to Gerrit. It is recommended to set up 2 factor authentication here. The provided scratch codes need to be securely saved, those will be required if you loose/can't access your phone to login.
- Then I created a `phabricator account`, and connected it to both my wikimedia and wikitech accounts. Guidelines [here](https://www.mediawiki.org/wiki/Phabricator/Help#Creating_your_account). We had to set up 2 factor here as well. But phabricator does not provide any sort of scratch codes, so loosing phone is going to be a bummer. What you do is set a [committed identity](https://meta.wikimedia.org/wiki/Template:User_committed_identity) in your wiki user page so that if you get locked out of phabricator you can be recognized through your committed identity hash. [Here](https://www.mediawiki.org/wiki/Phabricator/Help/Two-factor_Authentication_Resets) are some more info.
- Login to gerrit using your wikitech username and password, and there's your account.

### Gerrit and Docker

All you need to know about git and gerrit for wikimedia is already covered in their wikis. Here's the [gerrit](https://www.mediawiki.org/wiki/Gerrit) starter. All links from this page are important, especially the [How to become a wikimedia hacker](https://www.mediawiki.org/wiki/How_to_become_a_MediaWiki_hacker) page. Follow the **[instructions](https://www.mediawiki.org/wiki/Special:MyLanguage/Gerrit/Tutorial)** to set up and use gerrit. Keep note of some of the frequently required commands like the command to push changes to Gerrit is `git review -R` or `git review <branch name>` etc. Finally set up docker and run the unit tests.

### SSH

Get to know a little more about ssh. [Here](https://www.mediawiki.org/wiki/Gerrit/Tutorial#Set_Up_SSH_Keys_in_Gerrit)'s how to create a ssh key pair and use in gerrit. But for general purpose usage, see some more. [Here](https://wikitech.wikimedia.org/wiki/Help:Toolforge/My_first_Pywikibot_tool)'s another example of creating a ssh key pair and using it in toolforge.

### IRC
[IRC](https://meta.wikimedia.org/wiki/IRC) or internet relay chat is a form of communication through pure texts and is popular among open source communities. There can be various IRC clients, either on your PC or online. You can connect to various servers and channels within those servers as you wish. To create a permanent account you will need to set up a password so no one else can use your name. Follow the [guide](https://meta.wikimedia.org/wiki/IRC/Instructions) to know more how to set it up. Note that all chat history is available as a text files. You can only see chat history on screen only after you have joined IRC.

We used the [freenode]((http://freenode.net/)) server (chat.freenode.net:6697). I used `irccloud`, a web based client to connect to various channels of this server. The web option does not remain connected on free version, so I [installed Polari](https://linuxhint.com/irc_ubuntu/), a desktop app for the same. I created a account by simply setting a password so no one can impersonate me. See instructions to use IRC [here](https://meta.wikimedia.org/wiki/IRC/Instructions) and more about it [here](https://meta.wikimedia.org/wiki/IRC). List of Wikimedia IRC channels [here](https://meta.wikimedia.org/wiki/IRC/Channels).

### Mailing lists
Wikimedia has a LOT of mailing lists. I subscribed to some of those which concern my work over there. Like abstract-wikimedia, research and wikitech. The list of all mailing lists are [here](https://lists.wikimedia.org/). Anyone can join these lists to be updated on issues of their interest. I can basically get e-mail updates and also send information to everyone in the list through it.

## Onboarding and learning resources

I have divided these materials into things about wikimedia and things to know to join wikimedia.

### About wikimedia:
- [Wikipedia @ 20](https://wikipedia20.pubpub.org/)
- [Movement Strategy](https://upload.wikimedia.org/wikipedia/commons/5/5b/Wikimedia_2030_Movement_Strategy_Recommendations_in_English.pdf)
- [Abstract Wikipedia](https://arxiv.org/abs/2004.04733)
- [WikiGnome](https://en.wikipedia.org/wiki/Wikipedia:WikiGnome). This is humorous.

### On-boarding:
- [Values](https://meta.wikimedia.org/wiki/Wikimedia_Foundation_Values)
- [Guiding Principles](https://meta.wikimedia.org/wiki/Wikimedia_Foundation_Guiding_Principles)
- [Wikimedia Engineering Architecture Principles](https://www.mediawiki.org/wiki/Wikimedia_Engineering_Architecture_Principles)
- Debugging Teams: Better Productivity through Collaboration

## Learning Progress:

### Learning and testing various components

1. **[Toolforge](https://wikitech.wikimedia.org/wiki/Portal:Toolforge)**: Created a toolforge account (logged in with wikitech account) and followed the [quickstart quide](https://wikitech.wikimedia.org/wiki/Portal:Toolforge/Quickstart). Had to go into several depths of links to create account, familiarize with how toolforge works and how to get started with it. See **[VC in toolforge](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Version_Control_in_Toolforge)** and see [Toolforge from GitHub](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Auto-update_a_tool_from_GitHub) after you have cloned your Git Repo into your tool.

    **How to work with toolforge**:
    - Main website of [toolforge](https://toolsadmin.wikimedia.org/).
    - Helpful Link: [Help:Toolfrge](https://wikitech.wikimedia.org/wiki/Help:Toolforge). [Example](https://wikitech.wikimedia.org/wiki/Help:Toolforge/My_first_Pywikibot_tool) of using toolforge
    - From terminal `ssh -i ~/.ssh/id_rsa <unix shell username>@login.toolforge.org` and `become MY_TOOL`. `exit` to get out.
    - [Licensing](https://wikitech.wikimedia.org/wiki/Help:Tool_Labs/Developing#Licensing_your_source_code) your code. [About Tools](https://wikitech.wikimedia.org/wiki/Portal:Toolforge/Tool_Accounts). These pages link from The main Toolforge wiki, I am adding them nevertheless for quick reach. It contains common commands and usages of tools. [Document your Tool](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Developing_successful_tools#Write_some_docs).
    - To transfer files to-from tools or yourself in toolforge use scp from your **local terminal**. 
        > <bd808> Bryan Davis tanny411: you can only connect with ssh/scp as your user, not as a tool user. So you would use your personal username, but could get files in/out of a tool by targeting the tool's $HOME with the location (meaning something like `scp bd808@login.toolforge.org:~tools.my_tool_name/some/file/path .`)
    - Making Tools with **[Python](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Python)**. Making venv, how to run scheduled tasks from venv. The venv does not get automatically activated in Grid job submissions. Two common workarounds are having wrapping shell scripts that activates the venv, or use absolute paths to the binaries within: `jstart -N jobname venv/bin/python3 my_script.py`
    - Using grid and python [example](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Pywikibot)

2. Learned about [Grid](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Grid), Grid usage [example](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Pywikibot).
    - Example usage `jsub [...options] python3 test.py` or `jsub script.sh`.
    - If you want to send args to the python file, it will require escaping. Better is to create a wrapper script like `script.sh`. This script can activate python env, and then call the python file with arguments easily.
    - For usage with python its best to create a venv, install pip, install all dependencies and do your work. See the example file for more.
    - Maximum of 16 active jobs simultaneously allowed per tool user. The scheduler will hold additional job submissions in the qw (queued/waiting) until an active slot is available. Maximum of 50 active and queued jobs simultaneously allowed per tool user.
    - Know more about `crontabs` see [this](https://phoenixnap.com/kb/set-up-cron-job-linux#:~:text=The%20Cron%20daemon%20is%20a,other%20commands%20to%20run%20automatically.). Basic usage:
        ```
        crontab -e
        # at the end of this file add the following to run at 8AM UTC everyday
        0 8 * * * test-script.sh
        ```
3. [Database](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Database). There are lots of ways to access the databases. From toolforge, PAWS, Quarry etc. Connect from toolforge by `sql enwiki_p` for example.
    - Tabular listing of all wikis [here](https://meta.wikimedia.org/wiki/Special:SiteMatrix).
    - [Mediawiki Database visual](https://www.mediawiki.org/w/index.php?title=Manual:Database_layout/diagram&action=render) and wikis for all tables of this [database](https://www.mediawiki.org/wiki/Category:MediaWiki_database_tables). See list of all databases by `SHOW databases;` or [here](https://quarry.wmflabs.org/query/4031). Our required one is called `mediawikiwiki_p`.
    - Some tables/data are not available in databases. See [here](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Database#Redacted_tables). Mainly `user_properties`, `interwiki` and `text` tables are not available as is.
    - How to make sql queries in mediawiki [here](https://wikitech.wikimedia.org/wiki/Help:MySQL_queries) and query [examples](https://wikitech.wikimedia.org/wiki/Help:MySQL_queries/Example_queries), More examples can be found in Quarry.
    - Run SQL from browser using [Quarry](https://quarry.wmflabs.org/).
    - We can create [user databases](https://wikitech.wikimedia.org/wiki/Help:Toolforge/Database#User_databases) too. Exmaple
        ```console
        become my_tool
        sql tool
        ## find your credential by:
        SELECT SUBSTRING_INDEX(CURRENT_USER(), '@', 1);
        CREATE DATABASE CREDENTIALUSER__DBNAME;
        ```
    - Accessing replica databases through PAWS [tutorial](https://public.paws.wmcloud.org/36582847/%2A2020%20UPDATED%2A%20Replica%20Helper%20%26%20Database%20connections%20with%20PAWS.ipynb) called `Working with Wiki replicas databases and datasets`.
    - Connecting to database from local computer. Basically set a relay port in your pc, to which if we hit, it gets it on the wiki dbs.
        ```console
        ## copy over replica.my.cnf file
        
        ## for all db connections you want, do: -L $LOCAL_PORT:$REMOTE_HOST:$REMOTE_PORT to this line
        ## different local ports (e.g. 4711, 3308 etc)

        ssh -N yourusername@login.toolforge.org -L 4711:enwiki.analytics.db.svc.eqiad.wmflabs:3306
        mysql --user=$USER_FROM_REPLICA.MY.CNF --host=127.0.0.1 --port=4711 --password enwiki_p
        ```
4. Example use of database through toolforge using python:
    ```console
    ## my terminal
    ssh -i ~/.ssh/id_rsa tanny411@login.toolforge.org

    ## toolforge terminal
    become test-tool-aisha

    ## my tools terminal
    python3 -mvenv my_venv
    source my_venv/bin/activate

    ## from venv
    pip3 install --upgrade pip
    pip install toolforge

    python3
    ## code in python3
    import toolforge
    conn = toolforge.connect('mediawikiwiki_p')
    with conn.cursor() as cur:
        cur.execute("SELECT * from user_groups LIMIT 2;")
        for x in cur:
            print(x)
    ```
    To create a user database you have to connect to `tools` database and then create database. May want to have multiple connections in your code. For our purposes we will have to collect data from API, mediawikiwiki_p and store in our user database.
5. To work interactively we can use [PAWS](https://wikitech.wikimedia.org/wiki/PAWS). It has access to the wiki databases as well.
6. Getting to know [Lua/Scribunto](https://en.wikipedia.org/wiki/Help:Lua_for_beginners) and how to use functions in wiki [here](https://www.mediawiki.org/wiki/Extension:Scribunto/Lua_reference_manual) and [here](https://en.wikipedia.org/wiki/Wikipedia:Lua).
  
## Internship Progress

Use the action API to fetch all Scribunto modules for all wiki content, in parallel, using the grid. Update these fetched data regularly. Enhance api queries with queries against the database replicas. Page contents (what we really want) is to be extracted with API as it's not available in database.
> You can maybe look at this in the other direction, though. It might be easier to do SQL queries via script to determine more reliably without API pagination the full list of modules to obtain, and then utilize the API or action=raw access to get everything you need for the actual Lua. It's also completely fine to just use the Action API for all of it!

Then we are to find the relationships between modules, data about module usage and what are the most important modules. Find and remove redundancy if possible and centralize similar codes. These are among the first steps to make wikipedia functions language independent towards the goal of Abstract Wikipedia. For example, see a function in [English](https://en.wikipedia.org/wiki/Module:Yesno) and [Bangla](https://bn.wikipedia.org/wiki/%E0%A6%AE%E0%A6%A1%E0%A6%BF%E0%A6%89%E0%A6%B2:Yesno). See for more languages from the language section of the left tab.

All Scribunto modules are in [`Modules` namespace](https://en.wikipedia.org/wiki/Special:PrefixIndex?prefix=&namespace=828).
1. First we parse all wiki links from [here](https://meta.wikimedia.org/wiki/Special:SiteMatrix). Alternatively we can get all the links from WM database replicas. Work progress [here](https://github.com/wikimedia/abstract-wikipedia-data-science/issues/1).
2. We create scripts for API calls to each of these sites and store the contents of the Scribunto models. [API docs](https://www.mediawiki.org/wiki/Special:MyLanguage/API:Main_page) and test API with [sandbox](https://www.mediawiki.org/wiki/Special:ApiSandbox#action=help). Work progress [here](https://github.com/wikimedia/abstract-wikipedia-data-science/issues/7). This includes:
    - Python script to call API and fetch contents.
    - Bash scripts to call cron jobs to run the python script daily. (Requires some testing and solving memory issues)
    - Finding a suitable way to store the content (Started with storing in csv, will move to database eventually)
3. Identify and collect relevant data for analysis of Scribunto modules. First I had to understand how Lua Modules are used in wikis and how to understand which wikis use them. Then their usage information can be collected to identify most used Modules, redundant ones etc. Work progress [here](https://github.com/wikimedia/abstract-wikipedia-data-science/issues/9). Things to know:
    - To see where a module is used, click the `what links here` on the left tab.
    - To see what pages and modules a wiki page uses, click the edit tab and scroll down. Click `Pages transcluded onto the current version of this page`. This lists modules used in this page even indirectly, for example through a template. 
    - List of modules [here](https://en.wikipedia.org/wiki/Special:PrefixIndex?prefix=&namespace=828), i.e Namespace `828`.
    - Some module pages tell us how many pages use this (transclusion) at the top (e.g. [this](https://en.wikipedia.org/wiki/Module:Adjacent_stations)). This transclusion count is done by [Ahecht bot](https://en.wikipedia.org/wiki/User:Ahechtbot/transclusioncount.py) and stored [here](https://en.wikipedia.org/wiki/Module:Transclusion_count/data). See [docs](https://en.wikipedia.org/wiki/Template:High-use/doc#Technical_details) for more details. The code of this bot can be useful as reference for our purposes.
    - Same thing can be done from API. See API docs of [listing all transclusion](https://www.mediawiki.org/wiki/API:Templates).
4. **Some learning points** when I tried to run and check huge amounts of data. I had to make very careful decisions on how to write my code. Especially in pandas, when loading csv. Let alone wiki contents (~1,8G!), only page_id and wiki link wouldn't load (15M + 18M), there's that many pages across all wikis! I had to:
    - Set columns types as int/float where necessary as loading as string was taking up too much memory.
    - I could not load two dfs together even though I would later truncate them.
    - Load in chunks. This was a issue when I wanted to compare two dfs, so in each loop, I compared each chunk to the other fully loaded df. I think this was a lucky escape, what if none of the dfs could be fully loaded into memory? Maybe will come up in future, will have to come up with a clever code.
    - I had to reuse lots of df variables, `del` dfs when done. Had to write code such that no df needed to be copied, even partially, to make any operation.
    - Also made sure I used all the `inplace` options when possible.

    Later, when I ran into issues due to bad data, I couldn't find any easy solution. I wanted to ignore bad data but pandas ignores when there is more columns than necessary, not less. Normally I would check the raw data to see whats going on and why the bad data was created in the first place. But large files! After much maneuvering with pandas docs, I ended up simply doing a `grep` looking for the piece of data that was causing the error! Sometimes I wish easier solutions ring a bell faster in my head.
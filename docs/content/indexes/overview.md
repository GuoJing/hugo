---
title: "Indexes"
date: "2013-07-01"
aliases: ["/doc/indexes/", "/extras/indexes"]
linktitle: "Overview"
groups: ["indexes"]
groups_weight: 10
---

Hugo includes support for user defined groupings of content called indexes.

Indexes can be used to organize content in a variety of ways. For example, if I
wanted to use a wordpress style organization I would create two indexes called
"categories" and "tags". Other common uses would include categories, tags, groups,
navigation, series and many more. Just think of an index as way to organize similar content.

It's important to understand what Indexes do. At it's most basic form an index
is simply a map of a key to a list of content values.

In the hugo internals this is stored as `Site.Indexes[Plural][key][]pages`.
For example all the content tagged with GoLang would be found at 
`Site.Indexes["tags"]["golang"]`.

For a
more complete example see the source of [this docs site](http://github.com/spf13/hugo/docs/).

## Defining Indexes for a site

Indexes must be defined in the site configuration, before they
can be used throughout the site. 

Here is an example configuration in YAML that specifies two indexes.
Notice the format is **singular key** : *plural value*. While 
we could use an inflection library to pluralize this, they currently
support only a few languages, so instead we've opted for user defined
pluralization.

### config.yaml

{{% highlight yaml %}}
---
indexes:
    tag: "tags"
    category: "categories"
baseurl: "http://spf13.com/"
title: "Steve Francia is spf13.com"
---
{{% /highlight %}}

## Assigning index values to content

Once an index is defined at the site level, any piece of content
can be assigned to it regardless of content type or section.

Assigning content to an index is done in the front matter.
Simply create a variable with the *plural* name of the index
and assign all keys you want this content to match against. 

**Index values are case insensitive**

### Example

{{% highlight json %}}
{
    "title": "Hugo: A fast and flexible static site generator",
    "tags": [
        "Development",
        "golang",
        "fast",
        "Blogging"
    ],
    "categories" : [
        "Development"
    ]
    "slug": "hugo",
    "project_url": "http://github.com/spf13/hugo"
}
{{% /highlight %}}


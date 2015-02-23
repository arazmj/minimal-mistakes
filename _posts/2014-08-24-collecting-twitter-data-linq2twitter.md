---
layout: post
title: Collecting Twitter Data using Linq2Twitter
date: 2014-01-24 16:27:31
comments: true
---
<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

## Overview 
I decided to use C# and LinqToTwitter library along with MongoDB. I chose C# since it’s pretty fun to have to have dynamism and imperative and function paradigms at the same time. I’m also tired of learning a new programming language.

{% highlight csharp %}

var auth = new SingleUserAuthorizer
{
    CredentialStore = new SingleUserInMemoryCredentialStore
    {
        ConsumerKey = ConfigurationManager.AppSettings["twitterConsumerKey"],
        ConsumerSecret = ConfigurationManager.AppSettings["twitterConsumerSecret"],
        AccessToken = ConfigurationManager.AppSettings["twitterAccessToken"],
        AccessTokenSecret = ConfigurationManager.AppSettings["twitterAccessTokenSecret"]
    }
};

using (var twitterCtx = new TwitterContext(auth))
{
    twitterCtx.Log = Console.Out;

    var searchResponse =
        (from search in twitterCtx.Search
         where search.Type == SearchType.Search &&
         search.Query == "\"LINQ to Twitter\"" 
         select search)
            .SingleOrDefault();

    MongoServer mongo = new MongoClient(_connectionString).GetServer();
    mongo.Connect();

    var db = mongo.GetDatabase("CiteTrack");
    var collection = db.GetCollection("Tweets");

    if (searchResponse != null && searchResponse.Statuses != null)
        foreach (var status in searchResponse.Statuses)
        {
            collection.Insert(status.ToBsonDocument());
          
            Console.WriteLine(
                "User: {0}, Tweet: {1}, Date: {2}",
                status.User.ScreenName,
                status.Text, status.CreatedAt);

        }
    
    mongo.Disconnect();

}

{% endhighlight %}


---
title:  "Serialize C# Enums with Newtonsoft.JSON"
date:   2014-09-02 08:56:00
categories: c# JSON
---
If you have Enums that you want to serialize to their string representations when converting to JSON with Newtonsoft, there is an extra step. By default Newtonsoft just serializes the integer version of the Enum. For example the class and Enum demonstrated below:

{% highlight csharp %}
class Person
{
    public string name { get; set; }
    public int age { get; set; }
    public Gender gender { get; set; }
}

enum Gender
{
    Male = 1,
    Female = 2
}
{% endhighlight %}

Will output JSON like this when serialized:

{% highlight json %}
{
    "name": "John Smith",
    "age": 25,
    "gender": 1
}
{% endhighlight %}

All you need to do to fix this is add `[JsonConverter(typeof(StringEnumConverter))]` to the property that you want to serialize to its string representation. For example:

{% highlight csharp %}
class Person
{
    public string name { get; set; }
    public int age { get; set; }
    [JsonConverter(typeof(StringEnumConverter))]
    public Gender gender { get; set; }
}
{% endhighlight %}

And then the JSON output will be:

{% highlight json %}
{
    "name": "John Smith",
    "age": 25,
    "gender": "Male"
}
{% endhighlight %}
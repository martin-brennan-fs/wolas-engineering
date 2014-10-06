---
title:  "Content-Type Header not set when uploading to S3 using the AWS SDK for Ruby"
date:   2014-10-07 09:46:00
categories: aws
---

We came across an issue when downloading files in .NET MVC that were uploaded to Amazon S3 using the Ruby AWS SDK.

{% highlight text %}
Value cannot be null or empty.
Parameter name: contentType
{% endhighlight %}

We investigated further and found that while the AWS SDK for .NET was setting Content-Type headers when uploading files to S3, the SDK for Ruby was not. The fix for this is simple; pass the Content Type in the options hash for the `write` method in the Ruby AWS SDK (see [http://docs.aws.amazon.com/AWSRubySDK/latest/AWS/S3/S3Object.html#write-instance_method](http://docs.aws.amazon.com/AWSRubySDK/latest/AWS/S3/S3Object.html#write-instance_method)).

{% highlight ruby %}
# this:
s3.buckets[bucket_name].objects[bucket_key].write(data)

# becomes this:
s3.buckets[bucket_name].objects[bucket_key].write(data, content_type: "application/pdf")
{% endhighlight %}

See the below ServerFault question and GitHub issue for confirmation:

[http://serverfault.com/questions/147061/amazon-s3-not-sending-content-type-header](http://serverfault.com/questions/147061/amazon-s3-not-sending-content-type-header)

[https://github.com/leo-project/leofs/issues/179](https://github.com/leo-project/leofs/issues/179)

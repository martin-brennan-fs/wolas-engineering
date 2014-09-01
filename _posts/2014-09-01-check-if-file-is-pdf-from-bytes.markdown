---
title:  "Check if a file is a PDF from bytes"
date:   2014-09-01 20:10:31
categories: pdf
---

An easy way to figure out whether a file is a PDF document from a byte array is to check if the first four characters of the byte array are `%PDF`. Here is an example implementation in C#:

{% highlight csharp %}
public bool CheckIfPDF(byte[] file)
{
    string firstFourBytes = System.Text.Encoding.UTF8.GetString(file, 0, 4);

    return (firstFourBytes == "%PDF");
}
{% endhighlight %}

And here it is in Ruby:

{% highlight ruby %}
def check_pdf(bytes)
    bytes.to_s[0..4].eql? "%PDF"
end
{% endhighlight %}
---
layout: post
title: "Building Services with Apache Thrift"
date: 2015-01-30 14:54:49
tags: thrift services SOA
---
So you want to build a thing. This thing is going to be awesome because you've
committed to using the right tool for the job.

When it comes to tools, specialization is more valuable than standardization.

Specialization buys you elegance, simplicity, and maintainability.

Specialization costs you extensibility, but that's okay, you're just building
this one thing. You've heard that things should do one thing well.

Except you need this other thing: availability. In order to be useful, your
awesome thing needs to be accessible, and these days that means accessible via
just about anything. The hipster you get good coffee from wants to write some
node to use your thing, but your boss needs to use your thing from the
[big ball of mud][ball-of-mud] the team wrote in Java.

When it comes to interoperability, standardization is _much_ more valuable
than specialization.

Enter the web service.

Wait! Don't stab yourself in the eye just yet. I'm not talking SOAP or CORBA,
or any of those other horrible horrible things.  I'm not even talking about
a RESTful web service. Let's get advanced here, like [Google][buffers]
advanced, but for us regular folk.

Enter [Apache Thrift][apache-thrift]. The [open-source][thrift-gh] and, in my
opinion, best way to build RPC services, with support for just about
[every relevant language][thrift-features].

Thrift lets you do your one thing well with your specialized tool, and make it
available to everyone, without worrying about extending your API to be language
or protocol agnostic.

The interface description language is simple and [well-documented][thrift-idl].

Here's a hello world example for exposing a hello world python app to a ruby
client (minus some requires and imports):

    // helloworld.thrift
    service HelloWorld {
      string sayHello(1:string msg)
    }

{% highlight ruby %}
# helloworld_client.rb

transport = Thrift::BufferedTransport.new(Thrift::Socket.new('localhost', 9090))
protocol = Thrift::BinaryProtocol.new(transport)
client = HelloWorld::Client.new(protocol)

transport.open()
response = client.sayHello('Chad')
transport.close()
{% endhighlight %}

{% highlight python %}
# PythonServer.py

class HelloWorldHandler:
  def sayHello(self, msg):
    return "Hello " + msg + "

handler = HelloWorldHandler()
processor = HelloWorld.Processor(handler)
transport = TSocket.TServerSocket(port=9090)
tfactory = TTransport.TBufferedTransportFactory()
pfactory = TBinaryProtocol.TBinaryProtocolFactory()

server = TServer.TSimpleServer(processor, transport, tfactory, pfactory)

server.serve()
{% endhighlight %}

When you use the right tool for the right job, things just go smooth.

So go ahead and build your super fast cool thing in Haskell, because with
Thrift you'll have no problem invoking it in your backgrounded Rails ActiveJob,
or even your boss's J2EE application.

[ball-of-mud]: http://laputan.org/mud
[buffers]: https://developers.google.com/protocol-buffers/
[apache-thrift]: https://thrift.apache.org
[thrift-gh]: https://github.com/apache/thrift
[thrift-features]: https://thrift.apache.org/docs/features
[thrift-idl]: https://thrift.apache.org/docs/idl

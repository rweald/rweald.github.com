---
layout: post
tite: Experiment with Goliath and EventMachine
summary: An experiment in using event driven programming an ruby fibers to tackle large file uploads.
---
After hearing lots of buzz surrounding [Goliath](https://github.com/postrank-labs/goliath) the new asynchronous web server for ruby I thought I would give it a try for a particular problem I had. As part of [COVE](https://github.com/icl/cove), an open source online video ethnography tool, we have to handle large video file uploads. The application is written in Rails which is great except when you have really long running connections. With long running connections it ties up your mongrels and reduces your ability to service request. 

  The reason for this is because Rails is an inherently I/O blocking.
When you run your application in production using
[Passenger](http://www.modrails.com/) or [Unicorn](https://github.com/blog/517-unicorn) you essentially fork worker processes which are each responsible for servicing 1 requests at a time. To prevent memory bloating if a worker takes to long to respond or consumes too much memory it is killed. Well that presents a bit of a problem when you are talking about streaming file uploads that will require an active connection be left open while the file is uploaded. This large file upload request will block one of our worker processes which present an interesting problem. Since our process is blocked it is unable to service any additional request. This will lead to serious response time issues as our worker will be tied up handling these slow requests. To solve this we could spin up more worker processes, but this in turn takes more memory and more CPU and more resources in general.There must be a simpler solution!

  It turns out there is in fact a simpler solution...[Event Driven Programming](http://en.wikipedia.org/wiki/Reactor_pattern) and the
[Reactor Pattern](http://en.wikipedia.org/wiki/Event-driven_programming). I know what you are thinking, He's talking about NodeJS. Well yes and no, NodeJS is indeed a javascript event based asyncronous web server. However, I like ruby and I want to program my web service in ruby so where does that leave me; [Eventmachine](http://rubyeventmachine.com/). EventMachine is a c++ based event-processing library with a rich ruby API that allows for event oriented programming using an event loop and callbacks. Programming a web service using EventMachine can be a little bit of a pain in the ass as your code quickly starts to look like spaghetti and that is where Goliath comes in. 

  Goliath is described as "Non-blocking, Ruby 1.9 Web Server." It supports
the full rack API and utilizes ruby 1.9.2's fibers to make readable top
down code. If you want to learn more you can check out some great
articles by [Ilya Grigorik](http://www.igvita.com/2011/03/08/goliath-non-blocking-ruby-19-web-server/). Essentially goliath gives us a great way to write code that follows a top down flow and it easy to read, but in reality it is running asynchronously using EventMachine. Now what the heck does that mean to me you ask. Well what that means is in under 30 lines of code I was able to write an asynchronous file upload server. 

And here it is:

{% gist 969981 %}


  This was just my first plunge into the world of Non-blocking evented code so I am by no means an expert. If you see that I have made a terrible mistake or just want to give me some pointers feel free to do some. 
Just remember I am still young and while my college peers were out partying I was writing this code so try and make all criticism constructive
 

  In my next post I will document the upload client that also takes
advantaged of EventMachine and fibers to compute checksums and upload
files to the web service.

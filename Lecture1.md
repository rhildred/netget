# Systematic Problem Solving

![Systematic Problem Solving](https://rhildred.github.io/netget/READMEImages/Scientific_Method.jpg "Systematic Problem Solving")

The idea of this course is to give you context for systematic problem solving with networked applications. Systematic problem solving is based on the scientific method. We use the scientific method and splitting a problem into layers to solve it.

## 3 layer architecture

Often when we develop networked applications we use some form of layered architecture.

![3 layer](https://rhildred.github.io/netget/READMEImages/Overview_of_a_three-tier_application_vectorVersion.svg "3 layer")

When something goes wrong we can use the same layered idea for troubleshooting ... and finger pointing.

<iframe width="560" height="315" src="https://www.youtube.com/embed/2PjVuTzA2lk?rel=0&amp;controls=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen title="troubleshooting"></iframe>

I feel like finger pointing is kind of "new age" troubleshooting. Sort of like just typing stuff into google and trying stuff. Facebook would agree from a technical standpoint. Facebook focuses their whole team on putting code into production. Twice a day!!! 

<iframe width="560" height="315" src="https://www.youtube.com/embed/XJb-gjhcdhg?rel=0&amp;controls=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen title="facebook devops"></iframe>

Their culture is also organized around teams working this way.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Fs15kLpqveY?rel=0&amp;controls=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen title="culture"></iframe>


# <a href="https://github.com/rhildred/netget" target="_blank">netget</a>
## gets a url using .net core

This is a project for my 2nd term INFO1380 networking class. More about networking then about .net core. This class has had a 1 semester introduction to programming in .net. I am developing this on OSX/macos during reading week. OSX because I have OSX from when a friend and I started a software company in the Waterloo Ontario Accelerator Center. All of the cool software startups ran OSX!

To get running I:

1. Installed vscode [from here](https://code.visualstudio.com/download).
1. Installed .net core [from here](https://www.microsoft.com/net/download/macos).
1. Added the C# powered by OmniSharp extension in vscode.

In vscode I:

1. Opened a new folder.
1. Opened a terminal window and ran `dotnet new console`.
1. Opened the resulting Program.cs and pressed `Ctrl-F5`.
1. Clicked `yes` on the following dialog.

![click yes](https://rhildred.github.io/netget/READMEImages/RequiredAssets.png "click yes")

The next time I pressed `Ctrl-F5` I was treated to:

![hello world!](https://rhildred.github.io/netget/READMEImages/HelloWorld.png "hello world!")

Then I replaced all of the code in Program.cs with this, my first networking code!!!!!:

```

using System;
using System.Net.Http;
using System.Threading.Tasks;

namespace helloC_
{
    class Program
    {
        private static readonly HttpClient client = new HttpClient();
        private static async Task ProcessRepositories(string sUrl)
        {
            var stringTask = client.GetStringAsync(sUrl);

            var msg = await stringTask;
            Console.Write(msg);
        }
        static void Main(string[] args)
        {
            if(args.Length > 0){
                ProcessRepositories(args[0]).Wait();
            }else{
                Console.WriteLine("usage .... " + System.AppDomain.CurrentDomain.FriendlyName + " <url>");
            }
        }
    }
}



```

Then when I pressed `Ctrl-F5` I was treated to this:

![usage .... netget <url>](https://rhildred.github.io/netget/READMEImages/usage.png "usage .... netget <url>")

Almost there! To get `args[0]` populated I had to change the debug config in `.vscode/launch.json` to add to the `args[]`.

![added http://rhildred.github.io](https://rhildred.github.io/netget/READMEImages/launch.json.png "added http://rhildred.github.io")

Finally when I pressed `Ctrl-F5` I was treated with:

![the end of the html for my home page](https://rhildred.github.io/netget/READMEImages/HtmlSuccess.png "the end of the html for my home page")

Whoa! What just happened here? Well it turned out that a lot had to go right for this to work. All of that is the true thrust of this networking course.

## Divide and conquer with layers

Have you seen a picture that looks like this before?

![dotnet layers](https://rhildred.github.io/netget/READMEImages/dotnetlayers.png "dotnet layers")

Because my application is written to the .net core layer it will run on Windows, Linux and OSX. The big breakthrough with .net core is that it opens C# programming to Linux in a new way. Linux is a network operating system (NOS) just like windows server. A network operating system runs services on behalf of many users. A network operating system usually has more memory and processing power than a client operating system like Android, IOS, Macos or Windows 10. Enterprises like Linux as a network operating system because it scales better than Windows in many ways. This matters to our (programming) people because with .net core enterprises can write C# code that scales as well as Java code.  

## Networking also uses a layered approach.

![TCP/IP Layers](https://rhildred.github.io/netget/READMEImages/TCPIPLayers.svg "TCP/IP Layers")

The line of code:

```

    var stringTask = client.GetStringAsync(sUrl);

```

sends this `GET / HTTP/1.0` request to the web server host `rhildred.github.io`. As you may have guessed from the domain name this host is part of a social network for programmers called github. You will be learning in a few weeks hot to put your own html code from last term on github. 

## Encapsulation

If you haven't learned this already encapsulation in object oriented programming is combining data and the methods and metadata that work on that data into one package. It is a good idea because consumers of the object don't need to know the internals of the object to use it. Encapsulation hides the object from the consumers of that object. The implementation can then change without the consumers being affected.

Encapsulation in networking is similar. As we go through the layers we add header code to the data from the layer above. The header code is used to do the right thing to send the data to the next layer below. The header code has addressing and state information in it for each layer.

![the first iphone](https://rhildred.github.io/netget/READMEImages/original-iphone-first-gen-review-1-800x533-c.png "the first iphone")

Part of the big leap forward with this device is that as well as SMS and digital calls it also used plain IP over the cellular network. The IP layer was then able to support a regular Safari like WebKit browsing experience and the smart phone really took off.

### Application Layer

Like that browser our application is using the http service in the application layer. In .net core the http service is provided by the HttpClient object which is created with:

```

private static readonly HttpClient client = new HttpClient();

```

We call a method on that object:

```

    var stringTask = client.GetStringAsync(sUrl);

    var msg = await stringTask;
    Console.Write(msg);


```

wait for and print the result. 

### Transport Layer

![socket in a telephone exchange](https://rhildred.github.io/netget/READMEImages/TexasRichardson_telephoneExchangeOperator.jpg "socket in a telephone exchange")

The word socket predates networking. We plug something in to a socket to complete a circuit. The transport layer creates a circuit between 2 applications. In this case our WebClient app and the web server at http://rhildred.github.io.

### Network Layer

TCP/IP started as a military project with 3 goals:

* Survive a nuclear strike
* Permit different computer systems from different Nato allies to communicate easily
* Interconnect systems even into space

The network layer realizes these goals by routing packets individually, potentially around smoking holes. The French had little gourmet packets in their ATM networks while even packets are bigger in Texas. The network layer can fragment packets to work with different systems. Finally the network layer is responsible for addressing nodes for communication. With the new IPV6 network layer 128 bit addresses we can have 340 trillion, trillion trillion addresses. Even with IPV4 networks 32 bit addresses we can have 4.3 billion nodes. 

### Link Layer

![signal transmission](https://rhildred.github.io/netget/READMEImages/tin-cans.jpg "signal transmission")

The link layer is responsible for the physical transmission of the signal. Link layer mediums in common use are twisted pair cables, coaxial cables, fiber and the radio spectrum. Fiber is superior to twisted pair because it is imune to electromagnetic interference. Like our tin can telphone example where the medium is a taut string some media can only send one signal at a time. Senders and receivers must take turns. The link layer mediates turn taking in what we call a half duplex mode. Other media like twisted pair has one pair of wires for transmission and 1 pair for receiving. In this full duplex case the sender and receiver can work simultaneously. There is also a mode of using mostly radio spectrum called simplex. This is the case that we are used to from car radios and network television.

## Using the Layers to Inform Problem Solving

![what could be wrong?](https://rhildred.github.io/netget/READMEImages/Scientific_Method.jpg "what could be wrong?")

During the break a student asked me about getting blocked on a web site. Just like the networking layers help to divide and conquer for network implementations they can also help to split up the problem space in troubleshooting.

What could it be at the application layer? How would you test?

Transport Layer?

Network Layer?

Link Layer?

It may be hard to think of something that would be blocking a web site at the Link Layer. Let's talk about a problem that I had one Thanksgiving. I got paged saying that they couldn't ping a computer. Thinking it was a basic connectivity problem of some kind. I asked if they could ping any other computers. They could. I asked them to walk up to the computer they couldn't ping and read to me what was on the screen thinking that there might be some local error message. What do you think was on the screen?


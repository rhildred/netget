# [.netget](https://github.com/rhildred/netget)
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

![click yes](READMEImages/RequiredAssets.png "click yes")

The next time I pressed `Ctrl-F5` I was treated to:

![hello world!](READMEImages/HelloWorld.png "hello world!")

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

![usage .... netget <url>](READMEImages/usage.png "usage .... netget <url>")


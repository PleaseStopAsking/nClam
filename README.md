# nClam.Net
nClam.Net is a tiny library which helps you scan files or directories using a ClamAV server.  It contains a simple API which encapsulates the communication with the ClamAV server as well as the parsing of its results.  The library is licensed under the Apache License 2.0.

## Dependencies
ClamAV Server, also known as clamd.  It is a free, open-source virus scanner.  Win32 ports can be obtained here: http://oss.netfarm.it/clamav/

## NuGet Package

    Install-Package nClam.Net

## Directions
1. Add the nuget package to your project.
2. Create a nClam.Net.ClamClient object, passing it the hostname and port of the ClamAV server.
3. Scan!

# Code Example
```csharp
using System;
using System.Linq;
using System.Threading.Tasks;
using nClam.Net;

class Program
{
    static async Task Main(string[] args)
    {
        var clam = new ClamClient("localhost", 3310);
        var scanResult = await clam.ScanFileOnServerAsync("C:\\test.txt");  //any file you would like!

        switch (scanResult.Result)
        {
            case ClamScanResults.Clean:
                Console.WriteLine("The file is clean!");
                break;
            case ClamScanResults.VirusDetected:
                Console.WriteLine("Virus Found!");
                Console.WriteLine("Virus name: {0}", scanResult.InfectedFiles.First().VirusName);
                break;
            case ClamScanResults.Error:
                Console.WriteLine("Woah an error occured! Error: {0}", scanResult.RawResult);
                break;
        }

    }
}
```

# ClamAV Setup for Windows
For directions on setting up ClamAV as a Windows Service, check out [this blog post](http://architectryan.com/2011/05/19/nclam-a-dotnet-library-to-virus-scan/).

# Test Application
For more information about how to use nClam.Net, you can look at the nClam.Net.ConsoleTest project's [Program.cs](https://github.com/PleaseStopAsking/nClam.Net/blob/master/nClam.Net.ConsoleTestC2/Program.cs).

# Contributing
I accept PRs!  We have had several contributors help maintain this library by fixing bugs, introducing async support, and moving to .NET Core.  Thank you to all the contributors!
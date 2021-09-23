# LowLevelServer

Low level ASP.NET Core example web server

An example of using the ASP.NET Core servers for a .NET web application without any of the rest of the framework (e.g. Hosting, DI, middleware etc). So you can create your own distinct opinionated framework.

# Using The Project

Mostly its an example to derive from.

src\Ben.Http contains and sets up the server; it is Kestrel by default, but any server deriving from 'IServer' will also work (e.g. HttpSys, IIS, etc)

HttpServer.cs contains the server that is newed up; currently set to various defaults/

HttpContext.cs contains the Request/Response context, but this can be changed to be whatever set of properties you want to expose; in whatever way you want to expose them. Generally you get the information from the server by asking the IFeatureCollection for them and they are in the namespace Microsoft.AspNetCore.Http.Features

HttpApplication.cs is the application that deals with processing the requests. This creates and disposes of the HttpContext setting its features; and in this example Task ProcessRequestAsync(HttpContext context) is abstract so an application can derive from this class and implement that one method; and the bolierplate of setting up the Request/Response context is handled for them.

# Building

dotnet build -c Release will build the project.

Of note a there is a samples/PlaintextJsonRaw project that then uses this server to create an application that implements the Techempower plaintext and json tests. This is a single file server that you can run from that directory with:

dotnet run -c Release

Also there is a samples/TechEmpowerGenerators project that then uses this server plus some extension methods to create an application that implements the Techempower plaintext, json and fortunes tests in a simpler manner than the Raw. This is again a single file server:

![105080682-14becc80-5a89-11eb-8864-d67c486eaea8](https://user-images.githubusercontent.com/91251540/134478347-114a7970-8d26-402b-9746-2f1793203bae.png)

You can run from that directory with:

dotnet run -c Release

And it will set up a server listening on port 8080 and responding to the paths /plaintext, /json, /db and /fortunes. You also need to pass the postgres connection string in via connection enviorment variable:
![1](https://user-images.githubusercontent.com/91251540/134478699-372c07e5-7cb0-4c13-bdd3-57f50cce253e.png)

Now you can use the above!


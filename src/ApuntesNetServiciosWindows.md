# Apuntes Net C#. Servicios windows en C#




!!!Importante!!! en los servidores IIS hay que añadir la caracteristica para WebSocket

igual hay que lanzar un comando como este si nos diera un access denies Exception

netsh http add urlacl url=http://*:8080/ user=DOMAIN\username

o un comando parecido


---
## SignalR with Self-hosted Windows Service

https://www.codeproject.com/Articles/881511/SignalR-with-Self-hosted-Windows-Service

Crear proyecto de consola

~~~
 Install-Package Microsoft.AspNet.SignalR.SelfHost 
 Install-Package TopShelf 
 Install-Package TopShelf.NLog
 Install-Package Microsoft.Owin.Cors 
~~~

En program.cs
~~~
using System;
using System.Collections.Generic;
using System.Data;
using Topshelf;

namespace SelfHostedServiceSignalRSample
{
    static class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        static void Main()
        {
            HostFactory.Run(serviceConfig =>
            {
                serviceConfig.Service<SignalRServiceChat>(serviceInstance =>
                {
                    serviceConfig.UseNLog();

                    serviceInstance.ConstructUsing(
                        () => new SignalRServiceChat());

                    serviceInstance.WhenStarted(
                        execute => execute.OnStart(null));

                    serviceInstance.WhenStopped(
                        execute => execute.OnStop());
                });

                TimeSpan delay = new TimeSpan(0, 0, 0, 60);
                serviceConfig.EnableServiceRecovery(recoveryOption =>
                {
                    recoveryOption.RestartService(delay);
                    recoveryOption.RestartService(delay);
                    recoveryOption.RestartComputer(delay, 
                       System.Reflection.Assembly.GetExecutingAssembly().GetName().Name + 
                       " computer reboot"); // All subsequent failures
                });

                serviceConfig.SetServiceName
                  (System.Reflection.Assembly.GetExecutingAssembly().GetName().Name);
                serviceConfig.SetDisplayName
                  (System.Reflection.Assembly.GetExecutingAssembly().GetName().Name);
                serviceConfig.SetDescription
                  (System.Reflection.Assembly.GetExecutingAssembly().GetName().Name + 
                   " is a simple web chat application.");

                serviceConfig.StartAutomatically();
            });
        }
    }
}
~~~
StartUp.cs
~~~
using Microsoft.Owin.Cors;
using Owin;

namespace SelfHostedServiceSignalRSample
{
    class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            app.UseCors(CorsOptions.AllowAll);
            app.MapSignalR();
        }
    }
}
    
using Microsoft.AspNet.SignalR;

namespace SelfHostedServiceSignalRSample
{
    public class MyHub : Hub
    {
        public void Send(string name, string message)
        {
            Clients.All.addMessage(name, message);
        }
    }  
}
~~~

Crear clase SignalRServiceChat
~~~
using System;
using Microsoft.Owin;
using Microsoft.Owin.Hosting;
using Topshelf.Logging;

[assembly: OwinStartup(typeof(SelfHostedServiceSignalRSample.Startup))]
namespace SelfHostedServiceSignalRSample
{
    public partial class SignalRServiceChat : IDisposable
    {
        public static readonly LogWriter Log = HostLogger.Get<SignalRServiceChat>();

        public SignalRServiceChat()
        {
        }

        public void OnStart(string[] args)
        {
            Log.InfoFormat("SignalRServiceChat: In OnStart");

            // This will *ONLY* bind to localhost, if you want to bind to all addresses
            // use http://*:8080 to bind to all addresses. 
            // See http://msdn.microsoft.com/en-us/library/system.net.httplistener.aspx 
            // for more information.
            string url = "http://localhost:8090";
            WebApp.Start(url);
        }

        public void OnStop()
        {
            Log.InfoFormat("SignalRServiceChat: In OnStop");
        }

        public void Dispose()
        {
        }
    }
}
~~~
Crear un proyecto asp.net mvc e instalar el paquete nuget siguiente:

~~~
PM> Install-Package Microsoft.AspNet.SignalR.JS
~~~


~~~
<!DOCTYPE html>
<html>
<head>
    <title>SignalR Simple Chat</title>
    <style type="text/css">
        .container {
            background-color: #99CCFF;
            border: thick solid #808080;
            padding: 20px;
            margin: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <input type="text" id="message" />
        <input type="button" id="sendmessage" value="Send" />
        <input type="hidden" id="displayname" />
        <ul id="discussion"></ul>
    </div>
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-1.6.4.min.js"></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.1.0.min.js"></script>
    <!--Reference the autogenerated SignalR hub script. -->
    <script src="http://localhost:8080/signalr/hubs"></script>
    <!--Add script to update the page and send messages.-->
    <script type="text/javascript">
        $(function () {
        //Set the hubs URL for the connection
            $.connection.hub.url = "http://localhost:8080/signalr";
            
            // Declare a proxy to reference the hub.
            var chat = $.connection.myHub;
            
            // Create a function that the hub can call to broadcast messages.
            chat.client.addMessage = function (name, message) {
                // Html encode display name and message.
                var encodedName = $('<div />').text(name).html();
                var encodedMsg = $('<div />').text(message).html();
                // Add the message to the page.
                $('#discussion').append('<li><strong>' + encodedName
                    + '</strong>:  ' + encodedMsg + '</li>');
            };
            // Get the user name and store it to prepend to messages.
            $('#displayname').val(prompt('Enter your name:', ''));
            // Set initial focus to message input box.
            $('#message').focus();
            // Start the connection.
            $.connection.hub.start().done(function () {
                $('#sendmessage').click(function () {
                    // Call the Send method on the hub.
                    chat.server.send($('#displayname').val(), $('#message').val());
                    // Clear text box and reset focus for next comment.
                    $('#message').val('').focus();
                });
            });
        });
    </script>
</body>
</html>
~~~

---

## Self-Hosting SignalR in a Windows Service *


https://weblog.west-wind.com/posts/2013/Sep/04/SelfHosting-SignalR-in-a-Windows-Service

---

## How to easily create self hosted signalr windows service using TopShelf framework

https://krishnrajrana.wordpress.com/2017/05/03/how-to-easily-create-self-hosted-signalr-windows-service-using-topshelf-framework/

---

## Tutorial: Prueba interna de SignalR

https://learn.microsoft.com/es-es/aspnet/signalr/overview/deployment/tutorial-signalr-self-host

---

## libro de jose Manuel Aguilar en ingles , pagina 123 habla de los servicios de windows y signalR

---

## Understanding SignalR From Scratch

https://www.c-sharpcorner.com/article/understanding-signalr-from-scratch/

Codigo de este articulo, paquetes nuget signalR

~~~
Microsoft.AspNet.SignalR
Microsoft.AspNet.SignalR.Client

Microsoft.AspNet.SignalR.JS


Microsoft.Owin.SelfHost
Microsoft.Owin.Cors
Microsoft.AspNet.SignalR.Core
Microsoft.AspNet.SignalR.SelfHost


~~~

## Simple SignalR Server and Client Applications Demonstrating Common Usage Scenarios


https://www.codeproject.com/Articles/5162436/Simple-SignalR-Server-and-Client-Applications-Demo

~~~
public class SimpleHub : Hub
{
//Called when a client is connected
override OnConnected()

//Called when a client is disconnected
override OnDisconnected(bool stopCalled)

//Public methods inside this region are callable from any SignalR client
#region Client Methods
//A client provides a user name for himself
void SetUserName(string userName)

//Client calls this to join a group
Task JoinGroup(string groupName)

//Client calls this to leave a group
Task LeaveGroup(string groupName)

//Clients call this to send a message to the hub
//Hub then broadcasts the message to all the connected clients
void Send(string msg)

#endregion
}
~~~

~~~
//For all the clients
Clients.All 

//For a specific client
Clients.Client(connectionId)

//For clients that are members of a group
Clients.Group(groupName)
~~~

~~~
Clients.All.addMessage(senderUserName, message);
~~~

~~~
//To add a user to a group
Groups.Add(userConectionId, groupName);

//To remove a user from a group
Groups.Remove(userConectionId, groupName);
~~~


---

## How to Push Data from Server to Client Using SignalR

https://www.codeguru.com/blog/how-to-push-data-from-server-to-client-using-signalr/

~~~
public class MyChatHub : Hub
    {
        public void BroadcastMessageToAll(string message)
        {
            Clients.All.newMessageReceived(message);
        }
 
        public void JoinAGroup(string group)
        {
            Groups.Add(Context.ConnectionId, group);
        }
 
        public void RemoveFromAGroup(string group)
        {
            Groups.Remove(Context.ConnectionId, group);
        }
 
        public void BroadcastToGroup(string message, string group)
        {
            Clients.Group(group).newMessageReceived(message);
        }
    }
~~~


~~~
[assembly: OwinStartup(typeof(MyChatApplicationServer.Startup))]
 
namespace MyChatApplicationServer
{
    public class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            app.MapSignalR();
        }
    }
}
~~~



~~~
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <script src="Scripts/jquery-1.6.4.min.js"></script>
    <script src="Scripts/jquery.signalR-2.0.1.min.js"></script>
    <script src="http://localhost:32555/signalr/hubs/" type="text/javascript"></script>
    <script type="text/javascript">
        $(function () {
            var myChatHub = $.connection.myChatHub;
            myChatHub.client.newMessageReceived = function (message) {
                $('#ulChatMessages').append('<li>' + message + '</li>');
            }
            $.connection.hub.url = "http://localhost:32555/signalr";
            $.connection.hub.start().done(function () {
                $('#btnSubmit').click(function (e) {
                    myChatHub.server.broadcastMessageToAll($('#txtEnterMessage').val(), 'Web user');
                });
            }).fail(function (error) {
                console.error(error);
            });;
           
        });
    </script>
</head>
<body>
    <div>
        <label id="lblEnterMessage">Enter Message: </label>
        <input type="text" id="txtEnterMessage" />
        <input type="submit" id="btnSubmit" value="Send Message" />
        <ul id="ulChatMessages"></ul>
    </div>
</body>
</html>
~~~

Pushing Data to a Windows Application Client

~~~
namespace WinFormClient
{
    public partial class Form1 : Form
    {
        HubConnection hubConnection;
        IHubProxy hubProxy;
        public Form1()
        {
            InitializeComponent();
            hubConnection = new HubConnection("http://localhost:32555/signalr/hubs");
            hubProxy = hubConnection.CreateHubProxy("MyChatHub");
            hubProxy.On<string>("newMessageReceived", (message) => lstMessages.Items.Add(message));
            hubConnection.Start().Wait();
        }
 
        private void btnSubmit_Click(object sender, EventArgs e)
        {
            hubProxy.Invoke("BroadcastMessageToAll", textBox1.Text, "Window App User").Wait();
        }
    }
}
~~~




---

	
## Introduction To ASP.Net SignalR Self Hosting

https://www.c-sharpcorner.com/UploadFile/4b0136/introduction-of-Asp-Net-signalr-self-hosting/

~~~
using System;
using Microsoft.AspNet.SignalR;
using Microsoft.Owin.Hosting;
using Owin;

namespace SignalRHostApp
{
    class Program
    {
        static void Main(string[] args)
        {
            string url = "http://localhost:6118";
            using (WebApp.Start<Startup>(url))
            {
                Console.WriteLine("The Server URL is: {0}", url);
                Console.ReadLine();
            }
        }
    }

    class Startup
    {
        public void Configuration(IAppBuilder MyApp)
        {
            MyApp.MapSignalR();
        }
    }

    public class ChatHub : Hub
    {
        public void LetsChat(string Cl_Name, string Cl_Message)
        {
            Clients.All.NewMessage(Cl_Name, Cl_Message);
        }
    }
}

~~~

~~~
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">

<head>
    <title>ASP.NET SignalR Chat</title>
    <style type="text/css">
        .wrapper {
            background-color: 
#99CCFF;
            border: thick solid 
#808080;
            padding: 20px;
            margin: 20px;
        }
    </style>
</head>

<body>
    <div class="container">
        <input type="text" id="TxtMessage" />
        <input type="button" id="BtnSend" value="Send" />
        <input type="hidden" id="UserName" />
        <ul id="Chats"></ul>
    </div>
    <script src="Scripts/jquery-1.6.4.min.js"></script>
    <script src="Scripts/jquery.signalR-2.0.0-rc1.min.js"></script>
    <script src="http://localhost:6118/signalr/hubs"></script>
    <script type="text/javascript">
        $(function () {
            $.connection.hub.url = "http://localhost:6118/signalr";

            var chat = $.connection.chatHub;
            chat.client.NewMessage = function (Cl_Name, Cl_Message) {
                var User = $('<div />').text(Cl_Name).html();
                var UserChat = $('<div />').text(Cl_Message).html();

                $('#Chats').append('<li><strong>' + User +
                    '</strong>: ' + UserChat + '</li>');
            };
            $('#UserName').val(prompt('Please Enter Your Name:', ''));
            $('#TxtMessage').focus();
            $.connection.hub.start().done(function () {
                $('#BtnSend').click(function () {
                    chat.server.LetsChat($('#UserName').val(), $('#TxtMessage').val());
                    $('#TxtMessage').val('').focus();
                });
            });
        });
    </script>
</body>

</html>
~~~

---
## Tutorial: SignalR Self-Host

https://github.com/dotnet/AspNetDocs/blob/main/aspnet/signalr/overview/deployment/tutorial-signalr-self-host.md

~~~
Install-Package Microsoft.AspNet.SignalR.SelfHost
~~~

~~~
Install-Package Microsoft.Owin.Cors
~~~

~~~
using System;
using Microsoft.AspNet.SignalR;
using Microsoft.Owin.Hosting;
using Owin;
using Microsoft.Owin.Cors;

namespace SignalRSelfHost
{
    class Program
    {
        static void Main(string[] args)
        {
            // This will *ONLY* bind to localhost, if you want to bind to all addresses
            // use http://*:8080 to bind to all addresses. 
            // See http://msdn.microsoft.com/library/system.net.httplistener.aspx 
            // for more information.
            string url = "http://localhost:8080";
            using (WebApp.Start(url))
            {
                Console.WriteLine("Server running on {0}", url);
                Console.ReadLine();
            }
        }
    }
    class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            app.UseCors(CorsOptions.AllowAll);
            app.MapSignalR();
        }
    }
    public class MyHub : Hub
    {
        public void Send(string name, string message)
        {
            Clients.All.addMessage(name, message);
        }
    }
}
~~~


Parte cliente html,javascript
~~~
<!DOCTYPE html>
<html>
<head>
    <title>SignalR Simple Chat</title>
    <style type="text/css">
        .container {
            background-color: #99CCFF;
            border: thick solid #808080;
            padding: 20px;
            margin: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <input type="text" id="message" />
        <input type="button" id="sendmessage" value="Send" />
        <input type="hidden" id="displayname" />
        <ul id="discussion"></ul>
    </div>
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-1.6.4.min.js"></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.1.0.min.js"></script>
    <!--Reference the autogenerated SignalR hub script. -->
    <script src="http://localhost:8080/signalr/hubs"></script>
    <!--Add script to update the page and send messages.-->
    <script type="text/javascript">
        $(function () {
        //Set the hubs URL for the connection
            $.connection.hub.url = "http://localhost:8080/signalr";
            
            // Declare a proxy to reference the hub.
            var chat = $.connection.myHub;
            
            // Create a function that the hub can call to broadcast messages.
            chat.client.addMessage = function (name, message) {
                // Html encode display name and message.
                var encodedName = $('<div />').text(name).html();
                var encodedMsg = $('<div />').text(message).html();
                // Add the message to the page.
                $('#discussion').append('<li><strong>' + encodedName
                    + '</strong>:&nbsp;&nbsp;' + encodedMsg + '</li>');
            };
            // Get the user name and store it to prepend to messages.
            $('#displayname').val(prompt('Enter your name:', ''));
            // Set initial focus to message input box.
            $('#message').focus();
            // Start the connection.
            $.connection.hub.start().done(function () {
                $('#sendmessage').click(function () {
                    // Call the Send method on the hub.
                    chat.server.send($('#displayname').val(), $('#message').val());
                    // Clear text box and reset focus for next comment.
                    $('#message').val('').focus();
                });
            });
        });
    </script>
</body>
</html>

~~~

~~~
$.connection.hub.url = "http://localhost:8080/signalr";
~~~

---

## Self Hosting With SignalR and Web API Part 1 (Self Host Server, C#)

https://www.youtube.com/watch?v=2prTfk0n9x0



Creamos una Blank solucion con dos carpeta dentro de la solucion
Folder Client
Folder Host
Tenemos que añadir un proyecto de tipo Consola en el Folder Host y lo llamados SelfHost.Server
 y dentro de este proyecto añadimos dos carpetas
 Configuration
 Controllers
 hubs

 Estas son las carpetas que tenemos que crear dentro de este proyecto
~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server
{
    class Program
    {
        static void Main(string[] args)
        {

        }
    }
}
~~~

Tenemos que añadir una clase llamada StartUp

Tenemos de descargarnos el paquete nuget Microsoft.Owin
~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
[assembly:OwinStartup(typeof(StartUp))]
namespace SelfHost.Server
{
     public partial class StartUp
     {
         public void Configuration(IAppBuilder app)
         {
             InitiateConfig(App)
         }        
     }
}

~~~

Tenemos que descargar el paquete nuget Microsoft.Owin.Cors
Tenemos que descargar el paquete nuget Microsoft ASP.NET SignalR Core Components 
Tenemos que descargar el paquete desde la consola esta vez de powershell integrada en visual Studio
Install-Package Microsoft.AspNet.WebApi.OwinSelfHost

Folder Configurations
~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
[assembly:OwinStartup(typeof(StartUp))]
namespace SelfHost.Server
{
     public partial class StartUp
     {
         public void InitiateConfig(IAppBuilder app){
             httpConfiguration config = new httpConfiguration();
             RouteConfig.ResgisterRoute(config);
             app.UseCors(CorsOptions.AllowAll);
             app.Map("/signalr", map =>{
                 HubConfiguration hcf = new HubConfiguration();
                 map.RunSignalR();
             });
             app.UseWebApi(config);
         }
     }
}


~~~

Tenemos que descargar el paquete nuget Microsoft ASP.Net Web Api 2.2 Core Libraries

Añadir en el FolderConfiguractions RouteConfig.cs
~~~

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server
{
     public partial class RouteConfig
     {
         public static void RegisterRoute(httpConfiguration route){
             route.Routes.MapHttpRoute(
                name:"DefaultApi",
                routeTemplate:"api/{controller}/{id}",
                defaults: new {id=RouteParameter.Optional}
             ); 
         }
     }
}


~~~
Tenemos que añadir en la carpeta controller una nueva clase ProductController
~~~

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server.Controllers
{
     public partial class ProductController : ApiController
     {
        public IEnumerable<String> Get()
        {
            return new string[]{"value1","value2","value3","value4"}
        }
     }
}

~~~


---

## Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 2


https://www.youtube.com/watch?v=VXty3TbWZpQ

En la carpeta Hubs añadir NoficationHub.cs
~~~

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server.Hubs
{
     public partial class NoficationHub : Hub
     {
         public void ServerTime(){
             do 
             {
                  clients.All.displayTime($"{DateTime.UtcNow:F}");
                  Thread.Sleep(TimeSpan.FromSeconds(1));
             }while(true);
         }       
     }
}

~~~

~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server
{
    class Program
    {
       
        static void Main(string[] args)
        {
            string url="http://localhost:5050";
            using(WebApp.Start<StartUp>(url))
            {
               Console.WriteLine($"Services started at: {DateTime.UtcNow:D} at Url:{url}");
               Console.ReadLine();

            }
        }
    }
}
~~~
Ahora vamos a añadir en la carpeta client un proyecto de tipo console llamado SelfHost.ConsoleClient


Tenemos que descargar un paquete nuget system.net.http.formatting.extension
program.cs
~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server
{
    class Program
    {
        static string[] GetFromServer()
        {
            HttpClient client = new HttpClient();
            HttpResponseMessage response = client.GetAsync("http://localhost:5050/api/product").Result;
            
            var result = response.Content.ReadAsAsync<string[]>().Result;
            
            if (response.isSuccessStatusCode)
            {
                result;
            }
            
            return null
        }

        static void Main(string[] args)
        {
            Console.WriteLine("press enter to continue ++++");
            Console.ReadLine();
            GetFromServer().ToList().ForEach(p => {
                 Console.WriteLine($"{p}");
            });
              
            
        }
    }
}


~~~

---
## Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 3


https://www.youtube.com/watch?v=f-COVqUL8NI


Hay que descargarse el paquete nuget Microsoft ASP.NET SignalR.NET Client

~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server
{
    class Program
    {
        static string[] GetFromServer()
        {
            HttpClient client = new HttpClient();
            HttpResponseMessage response = client.GetAsync("http://localhost:5050/api/product").Result;
            
            var result = response.Content.ReadAsAsync<string[]>().Result;
            
                   if (response.isSuccessStatusCode)
            {
                result;
            }
            
            return null;
        }
        
        static void RunSignalR()
        {
            string url="http://localhost:5050";
            
            HubConnection connection = new HubConnection();

            var proxy = connection.CreateHubProxy("notificationHub"); 
            try
            {
                connection.Start().Wait();
                proxy.On<string>("DisplayTime" , time =>{
                    Console.Clear();
                    Console.WriteLine($"");
                
                });
                proxy.Invoke("ServerTime");
            }
            catch (Exception e)
            {

            }

        }
          
        
        
        static void Main(string[] args)
        {
            Console.WriteLine("press enter to continue ++++");
            Console.ReadLine();
            GetFromServer().ToList().ForEach(p => {
                 Console.WriteLine($"{p}");
            });
              
            Console.WriteLine("press enter for signalr services");
            RunSignalR();
            Console.ReadLine();

        }
    }
}

~~~

En el noficationHub.cs ponemos lo siguiente:
~~~

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SelfHost.Server.Hubs
{
     public partial class NoficationHub : Hub
     {
         public void ServerTime(){
             do 
             {
                  Console.WriteLine($"Connection ID {Context.ConnectionId} time called: {DateTime.UtcNow:G}");
                  clients.All.displayTime($"{DateTime.UtcNow:F}");
                  Thread.Sleep(TimeSpan.FromSeconds(1));
             }while(true);
         }       
     }
}

~~~


---

## Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 4

https://www.youtube.com/watch?v=x_kjIvhVZh0

---


## C# - How to Create a Windows Service - Part 1/3

https://www.youtube.com/watch?v=uM9o8GsO_u4

Por el minuto 5 empieza a hablar de como poner en modo debug el servicio y que hacer
para poder levantarlo en el modo debug, hay que escribir un codigo como este para que cuando
entre en modo debug podamos levantar el servicio y depurarlo


En el fichero Program.cs
~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.ServiceProcess;
using System.Text;

namespace WindowsService1
{
    static void Main()
    {
        
 #if debug
       Service1 myService = new Service1();
       myService.OnDebug();
       System.Threading.Sleep(System.Threading.Timeout.Infinite);
 #else       
        
        ServiceBase[] ServicesToRun;
        ServicesToRun new ServiceBase[];
        {
            new Service1();
        };
        ServiceBase.Run(ServicesToRun);
 #endif       
        
    }



}

~~~

En el fichero Service1.cs
~~~
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Linq;
using System.ServiceProcess;ç
using System.Text;

namespace WindowsService1
{
    public Service1()
    {
       InitializeComponent();  
    }
    
    public void OnDebug()
    {
        OnStart(null);
    }
    
    protected override void OnStart(string[] args)
    {
        
    }

    protected override void OnStop()
    {
         
    }
}

~~~

---

## Hosting SignalR under SSL/https

https://weblog.west-wind.com/posts/2013/Sep/23/Hosting-SignalR-under-SSLhttps





---

## Painless .NET Windows Service Creation with Topshelf

http://dontcodetired.com/blog/post/Painless-NET-Windows-Service-Creation-with-Topshelf

---

## Migrating SignalR from ASP.NET Web API 2 to Self Hosted Server (Part 3)

https://dotjord.wordpress.com/2018/05/29/migrating-signalr-from-asp-net-web-api-2-to-self-hosted-server-part-3/

---

	
## Running a Windows Service in Debug Mode

https://www.c-sharpcorner.com/UploadFile/akkiraju/running-a-windows-service-in-debug-mode/

Service.cs
~~~
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Linq;
using System.ServiceProcess;ç
using System.Text;

namespace WindowsService1
{
    public partial service1: ServiceBase
    {
        private static System.Timers.Timer _aTimer;

        public Service1()
        {
            _aTimer = new System.Timers.Timer(30000);
           _aTimer.Enabled = true;
           _aTimer.Elapsed += new System.Timers.ElapsedEventHandler(_aTimer_Elapsed);
           
            InitializeComponent();  
        }
        
        public void Start()
        {
            _aTimer.Start();
        }
        public void Stop()
        {
            _aTimer.Stop();
        }
        
        protected override void OnStart(string[] args)
        {
            this.Start();
        }

        protected override void OnStop()
        {
            this.Stop();
        }
    }
}
~~~
Hacemos una serie de cambios en el program.cs

~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.ServiceProcess;
using System.Text;
using System.Threading;namespace TestService
{
    static class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        static void Main()
        {


#if DEBUG
            //If the mode is in debugging
            //create a new service instance
            Service1 myService = new Service1();
            //call the start method - this will start the Timer.
            myService.Start();
            //Set the Thread to sleep
            Thread.Sleep(60000);
            //Call the Stop method-this will stop the Timer.
            myService.Stop();
#else
            //The following is the default code - You may fine tune
            //the code to create one instance of the service on the top
            //and use the instance variable in both debug and release mode
            ServiceBase[] ServicesToRun;
            ServicesToRun = new ServiceBase[] 
                          { 
                                   new Service1() 
                          };
            ServiceBase.Run(ServicesToRun);
#endif
        }
    }
}

~~~

---

## Self Hosted signalR in windows service; Minimum permissions for base url = http://*:1111

https://stackoverflow.com/questions/23428886/self-hosted-signalr-in-windows-service-minimum-permissions-for-base-url-http

~~~
netsh http add urlacl url=http://*:1111/ user=DOMAIN\user
~~~


---
Krishnraj Rana

My notes and tips about the programming concepts

### How to easily create self hosted signalr windows service using TopShelf framework

https://krishnrajrana.wordpress.com/2017/05/03/how-to-easily-create-self-hosted-signalr-windows-service-using-topshelf-framework/






Registrar la url con la ip
~~~
netsh http add urlacl url=http://192.168.151.87:18275/ user=EveryOne
~~~
para desregistrar
~~~
netsh http delete urlacl url=http://192.168.151.87:18275/
~~~




---









































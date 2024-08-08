# Apuntes Net C#. Servicios windows en C# y SignalR
- [Apuntes Net C#. Servicios windows en C# y SignalR](#apuntes-net-c-servicios-windows-en-c-y-signalr)
    - [Notas](#notas)
  - [Introduccion SignalR - Basico](#introduccion-signalr---basico)
    - [Understanding SignalR From Scratch](#understanding-signalr-from-scratch)
    - [How to Push Data from Server to Client Using SignalR](#how-to-push-data-from-server-to-client-using-signalr)
    - [Tutorial: **Prueba** interna de SignalR](#tutorial-prueba-interna-de-signalr)
    - [SignalR Console app example](#signalr-console-app-example)
    - [ASP.NET SignalR Hubs API Guide - Server (C#)](#aspnet-signalr-hubs-api-guide---server-c)
    - [ASP.NET SignalR Hubs API Guide - .NET Client (C#)](#aspnet-signalr-hubs-api-guide---net-client-c)
  - [Como hacer debug en servicio de windows](#como-hacer-debug-en-servicio-de-windows)
    - [C# - How to Create a Windows Service - Part 1/3](#c---how-to-create-a-windows-service---part-13)
    - [Running a Windows Service in Debug Mode](#running-a-windows-service-in-debug-mode)
  - [SelfHosted](#selfhosted)
    - [Self-Hosting SignalR in a Windows Service (importante)](#self-hosting-signalr-in-a-windows-service-importante)
    - [SignalR Self Hosting in a Windows Service](#signalr-self-hosting-in-a-windows-service)
    - [Using SignalR 2 Broadcasting and Notifications with a Self-Hosted Windows Service](#using-signalr-2-broadcasting-and-notifications-with-a-self-hosted-windows-service)
    - [libro de jose Manuel Aguilar en ingles , pagina 123 habla de los servicios de windows y signalR](#libro-de-jose-manuel-aguilar-en-ingles--pagina-123-habla-de-los-servicios-de-windows-y-signalr)
    - [Simple SignalR Server and Client Applications Demonstrating Common Usage Scenarios](#simple-signalr-server-and-client-applications-demonstrating-common-usage-scenarios)
    - [Introduction To ASP.Net SignalR Self Hosting](#introduction-to-aspnet-signalr-self-hosting)
    - [Tutorial: SignalR Self-Host](#tutorial-signalr-self-host)
    - [Self Hosting With SignalR and Web API Part 1 (Self Host Server, C#)](#self-hosting-with-signalr-and-web-api-part-1-self-host-server-c)
    - [Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 2](#self-hosting-signalr-and-web-api-self-host-server-c--visual-studio-2019--part-2)
    - [Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 3](#self-hosting-signalr-and-web-api-self-host-server-c--visual-studio-2019--part-3)
    - [Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 4](#self-hosting-signalr-and-web-api-self-host-server-c--visual-studio-2019--part-4)
    - [Hosting SignalR under SSL/https](#hosting-signalr-under-sslhttps)
    - [Migrating SignalR from ASP.NET Web API 2 to Self Hosted Server (Part 3)](#migrating-signalr-from-aspnet-web-api-2-to-self-hosted-server-part-3)
    - [Self Hosted signalR in windows service; Minimum permissions for base url = http://\*:1111](#self-hosted-signalr-in-windows-service-minimum-permissions-for-base-url--http1111)
  - [Libreria TopShelf para crear servicios windows](#libreria-topshelf-para-crear-servicios-windows)
    - [SignalR with Self-hosted Windows Service (TopShelf)](#signalr-with-self-hosted-windows-service-topshelf)
    - [Painless .NET Windows Service Creation with Topshelf](#painless-net-windows-service-creation-with-topshelf)
    - [How to easily create self hosted signalr windows service using TopShelf framework](#how-to-easily-create-self-hosted-signalr-windows-service-using-topshelf-framework)
  - [Injeccion de dependencias (IoC)](#injeccion-de-dependencias-ioc)
    - [Dependency Inject with SignalR \& Castle Windsor](#dependency-inject-with-signalr--castle-windsor)
    - [Using Unity for Dependency Injection with SignalR](#using-unity-for-dependency-injection-with-signalr)
    - [SignalR with an IoC container](#signalr-with-an-ioc-container)
    - [Using SignalR with Unity](#using-signalr-with-unity)
    - [Dependency Injection in SignalR](#dependency-injection-in-signalr)



---
### Notas
!!!Importante!!! en los servidores IIS hay que añadir la caracteristica para WebSocket

igual hay que lanzar un comando como este si nos diera un access denies Exception
~~~
netsh http add urlacl url=http://*:8080/ user=DOMAIN\username
~~~
o un comando parecido

---
## Introduccion SignalR - Basico


### Understanding SignalR From Scratch

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
---


### How to Push Data from Server to Client Using SignalR

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

### Tutorial: **Prueba** interna de SignalR

https://learn.microsoft.com/es-es/aspnet/signalr/overview/deployment/tutorial-signalr-self-host

---


### SignalR Console app example

https://stackoverflow.com/questions/11140164/signalr-console-app-example

Hay que agregar los siguientes paquetes nugets para los proyectos de consola
~~~
Install-Package SignalR.Hosting.Self -Version 0.5.2 (version antigua)

Install-Package Microsoft.AspNet.SignalR.SelfHost -Version 2.2.1

Install-Package Microsoft.AspNet.SignalR.Client (version antigua)

Install-Package Microsoft.AspNet.SignalR.Client -Version 2.2.1


~~~

El paquete Microsoft.AspNet.SignalR.Client contiene soporte para WinRT,Silverlight,WPF,Console applicacion,para net 4.0 y net 4.5

El paquete llamado Microsoft.AspNet.SignalR es distinto, no contiene este soporte


Tenemo el detalle de esto en el siguinte articulo:
ASP.NET SignalR Hubs API Guide - .NET Client (C#)

https://learn.microsoft.com/en-us/aspnet/signalr/overview/guide-to-the-api/hubs-api-guide-net-client


Aqui tenemos el codigo de ejemplo del articulo de levantar un servidor y un cliente en modo consola


Server console app

~~~
using System;
using SignalR.Hubs;

namespace SignalR.Hosting.Self.Samples {
    class Program {
        static void Main(string[] args) {
            string url = "http://127.0.0.1:8088/";
            var server = new Server(url);

            // Map the default hub url (/signalr)
            server.MapHubs();

            // Start the server
            server.Start();

            Console.WriteLine("Server running on {0}", url);

            // Keep going until somebody hits 'x'
            while (true) {
                ConsoleKeyInfo ki = Console.ReadKey(true);
                if (ki.Key == ConsoleKey.X) {
                    break;
                }
            }
        }

        [HubName("CustomHub")]
        public class MyHub : Hub {
            public string Send(string message) {
                return message;
            }

            public void DoSomething(string param) {
                Clients.addMessage(param);
            }
        }
    }
}
~~~

Client console app

~~~
using System;
using SignalR.Client.Hubs;

namespace SignalRConsoleApp {
    internal class Program {
        private static void Main(string[] args) {
            //Set connection
            var connection = new HubConnection("http://127.0.0.1:8088/");
            //Make proxy to hub based on hub name on server
            var myHub = connection.CreateHubProxy("CustomHub");
            //Start connection

            connection.Start().ContinueWith(task => {
                if (task.IsFaulted) {
                    Console.WriteLine("There was an error opening the connection:{0}",
                                      task.Exception.GetBaseException());
                } else {
                    Console.WriteLine("Connected");
                }

            }).Wait();

            myHub.Invoke<string>("Send", "HELLO World ").ContinueWith(task => {
                if (task.IsFaulted) {
                    Console.WriteLine("There was an error calling send: {0}",
                                      task.Exception.GetBaseException());
                } else {
                    Console.WriteLine(task.Result);
                }
            });

            myHub.On<string>("addMessage", param => {
                Console.WriteLine(param);
            });

            myHub.Invoke<string>("DoSomething", "I'm doing something!!!").Wait();


            Console.Read();
            connection.Stop();
        }
    }
}
~~~





---

### ASP.NET SignalR Hubs API Guide - Server (C#)

https://learn.microsoft.com/en-us/aspnet/signalr/overview/guide-to-the-api/hubs-api-guide-server

---

### ASP.NET SignalR Hubs API Guide - .NET Client (C#)

https://learn.microsoft.com/en-us/aspnet/signalr/overview/guide-to-the-api/hubs-api-guide-net-client

---
Working with Groups in SignalR

https://learn.microsoft.com/en-us/aspnet/signalr/overview/guide-to-the-api/working-with-groups

---

## Como hacer debug en servicio de windows


### C# - How to Create a Windows Service - Part 1/3

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
	
### Running a Windows Service in Debug Mode

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






## SelfHosted

---

### Self-Hosting SignalR in a Windows Service (importante)


https://weblog.west-wind.com/posts/2013/Sep/04/SelfHosting-SignalR-in-a-Windows-Service


~~~
public class SignalRStartup
{
    public static IAppBuilder App = null;

    public void Configuration(IAppBuilder app)
    {
        var hubConfiguration = new HubConfiguration { 
            EnableCrossDomain = true,
            EnableDetailedErrors = true
        };
                                                                                   
        app.MapHubs(hubConfiguration);                        
    }        
}
~~~

para signalR 2.0 la configuracion seria asi:
~~~
public class SignalRStartup
{
    public static IAppBuilder App = null;

    public void Configuration(IAppBuilder app)
    {
        var hubConfiguration = new HubConfiguration { 
            EnableCrossDomain = true,
            EnableDetailedErrors = true
        };
                                                                                   
        app.MapHubs(hubConfiguration);                        
    }        
}

~~~

~~~
SignalR = WebApp.Start<SignalRStartup>("http://*:8080/");
~~~



~~~
public class MPQueueService : ServiceBase
{
    MPWorkflowQueueController Controller { get; set; }
    IDisposable SignalR { get; set; }

    public void Start()
    {
        Controller = new MPWorkflowQueueController(App.AdminConfiguration.ConnectionString);

        var config = QueueMessageManagerConfiguration.Current;
        Controller.QueueName = config.QueueName;
        Controller.WaitInterval = config.WaitInterval;
        Controller.ThreadCount = config.ControllerThreads;

        SignalR = WebApp.Start<SignalRStartup>(App.AdminConfiguration.MonitorHostUrl);

        // Spin up the queue
        Controller.StartProcessingAsync();

        LogManager.Current.LogInfo(String.Format("QueueManager Controller Started with {0} threads.",
                                        Controller.ThreadCount));

        // Allow access to a global instance of this controller and service
        // So we can access it from the stateless SignalR hub
        Globals.Controller = Controller;
        Globals.WindowsService = this;
    }

    public new void Stop()
    {
        LogManager.Current.LogInfo("QueueManager Controller Stopped.");

        Controller.StopProcessing();
        Controller.Dispose();
        SignalR.Dispose();

        Thread.Sleep(1500);
    }


    /// <summary>
    /// Set things in motion so your service can do its work.
    /// </summary>
    protected override void OnStart(string[] args)
    {
        Start();
    }

    /// <summary>
    /// Stop this service.
    /// </summary>
    protected override void OnStop()
    {
        Stop();
    }

    protected override void Dispose(bool disposing)
    {
        base.Dispose(disposing);

        if (SignalR != null)
        {
            SignalR.Dispose();
            SignalR = null;
        }
    }
}
~~~


~~~
public static class Globals
{
    public static MPWorkflowQueueController Controller;
    public static MPQueueService WindowsService;
}
~~~

Estableciendo configuracion del servicio windows
~~~
[STAThread]
static void Main(string[] args)
{            
    string arg0 = string.Empty;
    if (args.Length > 0)
        arg0 = (args[0] ?? string.Empty).ToLower();

    if (arg0 == "-service" ) 
    {
        RunService();
        return;
    }
    if (arg0 == "-fakeservice")
    {
        FakeRunService();
        return;
    }

}

static void RunService()
{                                        
    var ServicesToRun = new ServiceBase[] { new MPQueueService() };
    LogManager.Current.LogInfo("Queue Service started as a Windows Service.");            
    ServiceBase.Run(ServicesToRun);
}

static void FakeRunService()
{            
    var service = new MPQueueService();
    service.Start();

    LogManager.Current.LogInfo("Queue Service started as FakeService for debugging.");            

    // never ends but waits
    Console.ReadLine();
}
~~~


~~~
public class QueueMonitorServiceHub : Hub
{    
    /// <summary>
    /// Writes a message to the client that displays on the status bar
    /// </summary>
    public void StatusMessage(string message, bool allClients = false)
    {
        if (allClients)
            Clients.All.statusMessage(message);
        else
            Clients.Caller.statusMessage(message);
    }

    /// <summary>
    /// Starts the service
    /// </summary>
    public void StartService()
    {
        // unpause the QueueController to start processing again
        Globals.Controller.Paused = false;

        Clients.All.startServiceCallback(true);
        Clients.All.writeMessage("Queue starting with " + 
                                 Globals.Controller.ThreadCount.ToString() + 
                                 " threads.",
                                 "Info", DateTime.Now.ToString("HH:mm:ss"));                        
    }

    public void StopService()
    {
        // Pause - we can't stop service because that'll exit the server            
        Globals.Controller.Paused = true;
            
        Clients.All.stopServiceCallback(true);

        Clients.All.writeMessage("Queue has been stopped.","Info",
                                 DateTime.Now.ToString("HH:mm:ss"));
    }

    …

    /// <summary>
    /// Context instance to access client connections to broadcast to
    /// </summary>
    public static IHubContext HubContext
    {
        get
        {
            if (_context == null)
                _context = GlobalHost.ConnectionManager.GetHubContext<QueueMonitorServiceHub>();

            return _context;
        }
    }
    static IHubContext _context = null;


    /// <summary>
    /// Writes out message to all connected SignalR clients
    /// </summary>
    /// <param name="message"></param>
    public static void WriteMessage(string message, string id = null, 
                                    string icon = "Info", DateTime? time = null)
    {
        if (id == null)
            id = string.Empty;

        // if no id is passed write the message in the ID area
        // and show no message
        if (string.IsNullOrEmpty(id))
        {
            id = message;
            message = string.Empty;
        }

        if (time == null)
            time = DateTime.UtcNow;

        // Write out message to SignalR clients  
        HubContext.Clients.All.writeMessage(message,
            icon,
            time.Value.ToString("HH:mm:ss"),
            id, 
            string.Empty);
    }
        

    /// <summary>
    /// Writes out a message to all SignalR clients
    /// </summary>
    /// <param name="queueItem"></param>
    /// <param name="elapsed"></param>
    /// <param name="waiting"></param>
    public static void WriteMessage(QueueMessageItem queueItem, 
                                    int elapsed = 0, int waiting = -1, 
                                     DateTime? time = null)
    {
        string elapsedString = string.Empty;
        if (elapsed > 0)
            elapsedString = (Convert.ToDecimal(elapsed) / 1000).ToString("N2");

        var msg = HtmlUtils.DisplayMemo(queueItem.Message);

        if (time == null)
            time = DateTime.UtcNow;

        // Write out message to SignalR clients            
        HubContext.Clients.All.writeMessage(msg,
                queueItem.Status,
                time.Value.ToString("HH:mm:ss"),
                queueItem.Id,
                elapsedString,
                waiting);
    }      
}
~~~


Implementacion del Hub:
~~~
public class QueueMonitorServiceHub : Hub
{    
    /// <summary>
    /// Writes a message to the client that displays on the status bar
    /// </summary>
    public void StatusMessage(string message, bool allClients = false)
    {
        if (allClients)
            Clients.All.statusMessage(message);
        else
            Clients.Caller.statusMessage(message);
    }

    /// <summary>
    /// Starts the service
    /// </summary>
    public void StartService()
    {
        // unpause the QueueController to start processing again
        Globals.Controller.Paused = false;

        Clients.All.startServiceCallback(true);
        Clients.All.writeMessage("Queue starting with " + 
                                 Globals.Controller.ThreadCount.ToString() + 
                                 " threads.",
                                 "Info", DateTime.Now.ToString("HH:mm:ss"));                        
    }

    public void StopService()
    {
        // Pause - we can't stop service because that'll exit the server            
        Globals.Controller.Paused = true;
            
        Clients.All.stopServiceCallback(true);

        Clients.All.writeMessage("Queue has been stopped.","Info",
                                 DateTime.Now.ToString("HH:mm:ss"));
    }

    …

    /// <summary>
    /// Context instance to access client connections to broadcast to
    /// </summary>
    public static IHubContext HubContext
    {
        get
        {
            if (_context == null)
                _context = GlobalHost.ConnectionManager.GetHubContext<QueueMonitorServiceHub>();

            return _context;
        }
    }
    static IHubContext _context = null;


    /// <summary>
    /// Writes out message to all connected SignalR clients
    /// </summary>
    /// <param name="message"></param>
    public static void WriteMessage(string message, string id = null, 
                                    string icon = "Info", DateTime? time = null)
    {
        if (id == null)
            id = string.Empty;

        // if no id is passed write the message in the ID area
        // and show no message
        if (string.IsNullOrEmpty(id))
        {
            id = message;
            message = string.Empty;
        }

        if (time == null)
            time = DateTime.UtcNow;

        // Write out message to SignalR clients  
        HubContext.Clients.All.writeMessage(message,
            icon,
            time.Value.ToString("HH:mm:ss"),
            id, 
            string.Empty);
    }
        

    /// <summary>
    /// Writes out a message to all SignalR clients
    /// </summary>
    /// <param name="queueItem"></param>
    /// <param name="elapsed"></param>
    /// <param name="waiting"></param>
    public static void WriteMessage(QueueMessageItem queueItem, 
                                    int elapsed = 0, int waiting = -1, 
                                     DateTime? time = null)
    {
        string elapsedString = string.Empty;
        if (elapsed > 0)
            elapsedString = (Convert.ToDecimal(elapsed) / 1000).ToString("N2");

        var msg = HtmlUtils.DisplayMemo(queueItem.Message);

        if (time == null)
            time = DateTime.UtcNow;

        // Write out message to SignalR clients            
        HubContext.Clients.All.writeMessage(msg,
                queueItem.Status,
                time.Value.ToString("HH:mm:ss"),
                queueItem.Id,
                elapsedString,
                waiting);
    }      
}

~~~


---

### SignalR Self Hosting in a Windows Service

https://damienbod.com/2014/06/03/signalr-self-hosting-template-for-a-windows-service/

Codigo del proyecto en GitHub:

https://github.com/damienbod/SignalRWSelfHostingWindowsServiceTemplate


~~~
using System.Threading;
using System.Threading.Tasks;
using Microsoft.AspNet.SignalR;
using Microsoft.Owin;
using Microsoft.Owin.Cors;
using Microsoft.Owin.Hosting;
using Owin;
using SignalREngine;
 
[assembly: OwinStartup(typeof(Startup))]
 
namespace SignalREngine
{
    public class Startup
    {
        static CancellationTokenSource _cancellationTokenSource = new CancellationTokenSource();
 
        // Your startup logic
        public static void StartServer()
        {
            var cancellationTokenSource = new CancellationTokenSource();
            Task.Factory.StartNew(RunSignalRServer, TaskCreationOptions.LongRunning
                                  , cancellationTokenSource.Token);  
        }
 
        private static void RunSignalRServer(object task)
        {
            string url = "http://localhost:8089";
            WebApp.Start(url);
        }
 
        public static void StopServer()
        {
            _cancellationTokenSource.Cancel();
        }
 
        // This code configures Web API. The Startup class is specified as a type
        // parameter in the WebApp.Start method.
        public void Configuration(IAppBuilder app)
        {
            app.Map("/signalr", map =>
            {
                map.UseCors(CorsOptions.AllowAll);
                var hubConfiguration = new HubConfiguration
                {
                };
 
                hubConfiguration.EnableDetailedErrors = true;
                map.RunSignalR(hubConfiguration);
            });
        }
    }
}
~~~

~~~
using System;
using System.ServiceProcess;
using SignalREngine;
 
namespace SignalREngineServiceWindowsService
{
    static class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        static void Main(string[] args)
        {
            // Importante borrar o poner #if DEBUG aqui:  Remove this if you want to test as a console application and add an arg
            ServiceBase.Run(new SignalREngineServiceWindowsService());
 
            if (args != null)
            {
                try
                {
                    Startup.StartServer();
                    Console.ReadKey();
                }
                finally
                {
                    Startup.StopServer();
                }
            }
        }
    }
}
~~~

Em el servicio de windows las llamadas Start/Stop (SignalREngineServiceWindowsService)
~~~
protected override void OnStart(string[] args)
{
  Startup.StartServer();
  base.OnStart(args);
}
 
protected override void OnStop()
{
  Startup.StopServer();
  base.OnStop();
}
~~~

---

### Using SignalR 2 Broadcasting and Notifications with a Self-Hosted Windows Service

https://www.codeproject.com/Articles/892634/Using-SignalR-Broadcasting-and-Notifications-with

~~~
PM> Install-Package Microsoft.AspNet.SignalR.SelfHost
PM> Install-Package ServiceProcess.Helpers
PM> Install-Package Microsoft.Owin.Cors

~~~


~~~
using ServiceProcess.Helpers;
using System;
using System.Collections.Generic;
using System.Data;
using System.ServiceProcess;

namespace SignalRBroadcastServiceSample
{
    static class Program
    {
        private static readonly List<ServiceBase> _servicesToRun = new List<ServiceBase>();

        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        static void Main()
        {
            _servicesToRun.Add(CurrencyExchangeService.Instance);

            if (Environment.UserInteractive)
            {
                _servicesToRun.ToArray().LoadServices();
            }
            else
            {
                ServiceBase.Run(_servicesToRun.ToArray());
            }
        }
    }
}
~~~



~~~
using System;
using System.Threading.Tasks;
using Microsoft.Owin;
using Owin;

[assembly: OwinStartup(typeof(SignalRBroadcastServiceSample.Startup))]

namespace SignalRBroadcastServiceSample
{
    public class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            // Add configuration code or hub wire up here if needed
            app.MapSignalR();
        }
    }
}
~~~

Si quieres establecer una configuracion mas personalizada:
~~~
var hubConnection = new HubConnection("http://contoso.com/mycustomurl", useDefaultUrl: false);
~~~

En el cliente o desde el cliente, C# o js, tenemos que acceder a esta url
~~~
var hubConnection = new HubConnection("http://contoso.com/mycustomurl", useDefaultUrl: false);
~~~

Pasos para añadir codigo SignalR al servicio:

Añadir Currency.cs
~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SignalrDomain
{
    public class Currency
    {
        private decimal _usdValue;
        public string CurrencySign { get; set; }
        public decimal Open { get; private set; }
        public decimal Low { get; private set; }
        public decimal High { get; private set; }
        public decimal LastChange { get; private set; }

        public decimal RateChange
        {
            get
            {
                return USDValue - Open;
            }
        }

        public double PercentChange
        {
            get
            {
                return (double)Math.Round(RateChange / USDValue, 4);
            }
        }

        public decimal USDValue
        {
            get
            {
                return _usdValue;
            }
            set
            {
                if (_usdValue == value)
                {
                    return;
                }

                LastChange = value - _usdValue;
                _usdValue = value;

                if (Open == 0)
                {
                    Open = _usdValue;
                }
                if (_usdValue < Low || Low == 0)
                {
                    Low = _usdValue;
                }
                if (_usdValue > High)
                {
                    High = _usdValue;
                }
            }
        }
    }
}
~~~

Objeto Hub:


Clase CurrencyExchangeHub.cs
~~~
[HubName("PascalCaseMyChatHub")]
~~~

~~~
using Microsoft.AspNet.SignalR;
using Microsoft.AspNet.SignalR.Hubs;
using Microsoft.Owin;
using SignalrDomain;
using System;
using System.Collections.Generic;
using System.Linq;

namespace SignalRBroadcastServiceSample
{
    public class CurrencyExchangeHub : Hub
    {
        private readonly CurrencyExchangeService _currencyExchangeHub;

        public CurrencyExchangeHub() :
            this(CurrencyExchangeService.Instance)
        {

        }

        public CurrencyExchangeHub(CurrencyExchangeService currencyExchange)
        {
            _currencyExchangeHub = currencyExchange;
        }

        public IEnumerable<Currency> GetAllCurrencies()
        {
            return _currencyExchangeHub.GetAllCurrencies();
        }

        public string GetMarketState()
        {
            return _currencyExchangeHub.MarketState.ToString();
        }

        public bool OpenMarket()
        {
            _currencyExchangeHub.OpenMarket();
            return true;
        }

        public bool CloseMarket()
        {
            _currencyExchangeHub.CloseMarket();
            return true;
        }

        public bool Reset()
        {
            _currencyExchangeHub.Reset();
            return true;
        }
    }
}
~~~

Añadir a la clase CurrencyExchangeService.cs

~~~
public async IEnumerable<Currency> GetAllCurrencies()
{
    IEnumerable<Currency> currencies = new IEnumerable<Currency>();
    Task loadCurrenciesTask = Task.Factory.StartNew(() => LoadCurrencies(currencies));
    await loadCurrenciesTask;

    return currencies;
}

private static void LoadCurrencies(IEnumerable<Currency> currencies)
{
   currencies = _currencyExchangeHub.GetAllCurrencies();
}
~~~


~~~
using Microsoft.AspNet.SignalR;
using Microsoft.AspNet.SignalR.Hubs;
using Microsoft.Owin.Hosting;
using SignalrDomain;
using System;
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.ServiceProcess;
using System.Threading;

namespace SignalRBroadcastServiceSample
{
    public partial class CurrencyExchangeService : ServiceBase
    {
        private Thread mainThread;
        private bool isRunning = true;
        private Random random = new Random();

        protected override void OnStart(string[] args)
        {
            WebApp.Start("http://localhost:8083"); // Must be 
            	//@"http://+:8083" if you want to connect from other computers
            LoadDefaultCurrencies();

            // Start main thread
            mainThread = new Thread(new ParameterizedThreadStart(this.RunService));
            mainThread.Start(DateTime.MaxValue);
        }

        protected override void OnStop()
        {
            mainThread.Join();
        }

        public void RunService(object timeToComplete)
        {
            DateTime dtTimeToComplete = timeToComplete != null ? 
            	Convert.ToDateTime(timeToComplete) : DateTime.MaxValue;

            while (isRunning && DateTime.UtcNow < dtTimeToComplete)
            {
                Thread.Sleep(15000);
                NotifyAllClients();
            }
        }

        // This line is necessary to perform the broadcasting to all clients
        private void NotifyAllClients()
        {
            Currency currency = new Currency();
            currency.CurrencySign = "CAD";
            currency.USDValue = random.Next();
            BroadcastCurrencyRate(currency);
            Clients.All.NotifyChange(currency);
        }

        #region "SignalR code"

        // Singleton instance
        private readonly static Lazy<CurrencyExchangeService> 
        	_instance = new Lazy<CurrencyExchangeService>(
            () => new CurrencyExchangeService
            (GlobalHost.ConnectionManager.GetHubContext<CurrencyExchangeHub>().Clients));

        private readonly object _marketStateLock = new object();
        private readonly object _updateCurrencyRatesLock = new object();

        private readonly ConcurrentDictionary<string, 
        	Currency> _currencies = new ConcurrentDictionary<string, Currency>();

        // Currency can go up or down by a percentage of this factor on each change
        private readonly double _rangePercent = 0.002;

        private readonly TimeSpan _updateInterval = TimeSpan.FromMilliseconds(250);

        public TimeSpan UpdateInterval
        {
            get { return _updateInterval; }
        } 

        private readonly Random _updateOrNotRandom = new Random();

        private Timer _timer;
        private volatile bool _updatingCurrencyRates;
        private volatile MarketState _marketState;

        public CurrencyExchangeService(IHubConnectionContext<dynamic> clients)
        {
            InitializeComponent();

            Clients = clients;
        }

        public static CurrencyExchangeService Instance
        {
            get
            {
                return _instance.Value;
            }
        }

        private IHubConnectionContext<dynamic> Clients
        {
            get;
            set;
        }

        public MarketState MarketState
        {
            get { return _marketState; }
            private set { _marketState = value; }
        }

        public IEnumerable<Currency> GetAllCurrencies()
        {
            return _currencies.Values;
        }

        public bool OpenMarket()
        {
            bool returnCode = false;

            lock (_marketStateLock)
            {
                if (MarketState != MarketState.Open)
                {
                    _timer = new Timer(UpdateCurrencyRates, null, _updateInterval, _updateInterval);

                    MarketState = MarketState.Open;

                    BroadcastMarketStateChange(MarketState.Open);
                }
            }
            returnCode = true;

            return returnCode;
        }

        public bool CloseMarket()
        {
            bool returnCode = false;

            lock (_marketStateLock)
            {
                if (MarketState == MarketState.Open)
                {
                    if (_timer != null)
                    {
                        _timer.Dispose();
                    }

                    MarketState = MarketState.Closed;

                    BroadcastMarketStateChange(MarketState.Closed);
                }
            }
            returnCode = true;

            return returnCode;
        }

        public bool Reset()
        {
            bool returnCode = false;

            lock (_marketStateLock)
            {
                if (MarketState != MarketState.Closed)
                {
                    throw new InvalidOperationException
                    	("Market must be closed before it can be reset.");
                }
                
                LoadDefaultCurrencies();
                BroadcastMarketReset();
            }
            returnCode = true;

            return returnCode;
        }

        private void LoadDefaultCurrencies()
        {
            _currencies.Clear();

            var currencies = new List<Currency>
            {
                new Currency { CurrencySign = "USD", USDValue = 1.00m },
                new Currency { CurrencySign = "CAD", USDValue = 0.85m },
                new Currency { CurrencySign = "EUR", USDValue = 1.25m }
            };

            currencies.ForEach(currency => _currencies.TryAdd(currency.CurrencySign, currency));
        }

        private void UpdateCurrencyRates(object state)
        {
            // This function must be re-entrant as it's running as a timer interval handler
            lock (_updateCurrencyRatesLock)
            {
                if (!_updatingCurrencyRates)
                {
                    _updatingCurrencyRates = true;

                    foreach (var currency in _currencies.Values)
                    {
                        if (TryUpdateCurrencyRate(currency))
                        {
                            BroadcastCurrencyRate(currency);
                        }
                    }

                    _updatingCurrencyRates = false;
                }
            }
        }

        private bool TryUpdateCurrencyRate(Currency currency)
        {
            // Randomly choose whether to update this currency or not
            var r = _updateOrNotRandom.NextDouble();
            if (r > 0.1)
            {
                return false;
            }

            // Update the currency price by a random factor of the range percent
            var random = new Random((int)Math.Floor(currency.USDValue));
            var percentChange = random.NextDouble() * _rangePercent;
            var pos = random.NextDouble() > 0.51;
            var change = Math.Round(currency.USDValue * (decimal)percentChange, 2);
            change = pos ? change : -change;

            currency.USDValue += change;
            return true;
        }

        private void BroadcastMarketStateChange(MarketState marketState)
        {
            switch (marketState)
            {
                case MarketState.Open:
                    Clients.All.marketOpened();
                    break;
                case MarketState.Closed:
                    Clients.All.marketClosed();
                    break;
                default:
                    break;
            }
        }

        private void BroadcastMarketReset()
        {
            Clients.All.marketReset();
        }

        private void BroadcastCurrencyRate(Currency currency)
        {
            Clients.All.updateCurrencyRate(currency);
        }
    }

    public enum MarketState
    {
        Closed,
        Open
    }

    #endregion
}
~~~

Vamos a crear el apartado cliente que en este caso va a ser un proyecto cliente pero que lanza test unitarios para comprobar el servicio, tenemos que añadirle la libreria de cliente para C#.

~~~
PM> Install-Package Microsoft.AspNet.SignalR.SelfHost
PM> Install-Package  Microsoft.AspNet.SignalR.Client
~~~


~~~
using System;
using System.ServiceProcess;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using SignalRBroadcastServiceSample;

namespace UnitTests
{
    [TestClass]
    public class TestCurrencyExchangeService
    {
        #region Additional test attributes
        // 
        //You can use the following additional attributes as you write your 
        //tests:
        //Use ClassInitialize to run code before running the first test in the
        //class
        [ClassInitialize()]
        public static void MyClassInitialize(TestContext testContext)
        {
        }

        //Use ClassCleanup to run code after all tests in a class have run
        [ClassCleanup()]
        public static void MyClassCleanup()
        {
        }

        //Use TestInitialize to run code before running each test
        [TestInitialize()]
        public void MyTestInitialize()
        {

        }

        //Use TestCleanup to run code after each test has run
        [TestCleanup()]
        public void MyTestCleanup()
        {

        }

        #endregion

        [TestMethod]
        public void TestClientGetMarketStateFromHub()
        {
            // Make sure to call WebApp.Start:
            PrivateObject privateObject = new PrivateObject(_service);
            privateObject.Invoke("OnStart", new object[] { null });

            // Create client proxy and call hub method
            using (HubConnection hub = new HubConnection(String.Format("http://{0}:8084", "localhost")))
            {
                IHubProxy proxy = hub.CreateHubProxy("CurrencyExchangeHub");
                hub.Start().Wait();

                var state = proxy.Invoke<string>("GetMarketState").Result;
                Assert.IsNotNull(state);
                Assert.IsTrue(state.Length > 0);
            }
        }

        [TestMethod]
        public void TestClientGetAllCurrenciesFromHub()
        {
            // Make sure to call WebApp.Start:
            PrivateObject privateObject = new PrivateObject(_service);
            privateObject.Invoke("OnStart", new object[] { null });

            // Create client proxy and call hub method
            using (HubConnection hub = new HubConnection(String.Format("http://{0}:8084", "localhost")))
            {
                IHubProxy proxy = hub.CreateHubProxy("CurrencyExchangeHub");
                hub.Start().Wait();

                var currencies = proxy.Invoke<ienumerable<currency>>("GetAllCurrencies").Result;
                Assert.IsNotNull(currencies);
                Assert.IsTrue(currencies.ToString().Length > 0);
            }
        }

        [TestMethod]
        public void TestClientOpenCloseMarketFromHub()
        {
            // Make sure to call WebApp.Start:
            PrivateObject privateObject = new PrivateObject(_service);
            privateObject.Invoke("OnStart", new object[] { null });

            // Create client proxy and call hub method
            using (HubConnection hub = new HubConnection(String.Format("http://{0}:8084", "localhost")))
            {
                IHubProxy proxy = hub.CreateHubProxy("CurrencyExchangeHub");
                hub.Start().Wait();

                var state = proxy.Invoke<bool>("OpenMarket").Result;
                Assert.IsNotNull(state);
                Assert.IsTrue(state == true);

                state = proxy.Invoke<bool>("CloseMarket").Result;
                Assert.IsNotNull(state);
                Assert.IsTrue(state == true);
            }
        }

        [TestMethod]
        public void TestGetMarketStateFromHub()
        {
            CurrencyExchangeHub hub = new CurrencyExchangeHub(CurrencyExchangeService.Instance);
            var state = hub.GetMarketState();
            Assert.IsNotNull(state);
        }

        [TestMethod]
        public void TestOpenCloseMarket()
        {
            var currencies = CurrencyExchangeService.Instance.GetAllCurrencies();
            Assert.IsNotNull(currencies);
            bool expected = true;
            bool actual = CurrencyExchangeService.Instance.OpenMarket();
            Assert.AreEqual(expected, actual);
            actual = CurrencyExchangeService.Instance.OpenMarket();
            Assert.AreEqual(expected, actual);
        }

        [TestMethod]
        public void TestOpenCloseMarketFromHub()
        {
            var hub = new CurrencyExchangeHub(CurrencyExchangeService.Instance);
            var currencies = hub.GetAllCurrencies();
            Assert.IsNotNull(currencies);
            bool expected = true;
            bool actual = hub.OpenMarket();
            Assert.AreEqual(expected, actual);
            actual = hub.OpenMarket();
            Assert.AreEqual(expected, actual);
        }
    }
}</bool></bool></ienumerable<currency></string>
~~~

Vamos a añadir un proyecto de consola para conectar un cliente C# para signalR

~~~
PM> Install-Package  Microsoft.AspNet.SignalR.Client
~~~


Creamos una clase ComunicationHandler
~~~
using Microsoft.AspNet.SignalR.Client;
using SignalrDomain;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Client
{
    public static class CommunicationHandler
    {
        public static string ExecuteMethod(string method, string args, string serverUri, string hubName)
        {
            var hubConnection = new HubConnection("http://localhost:8083");
            IHubProxy currencyExchangeHubProxy = hubConnection.CreateHubProxy("CurrencyExchangeHub");

            // This line is necessary to subscribe for broadcasting messages
            currencyExchangeHubProxy.On<Currency>("NotifyChange", HandleNotify);

            // Start the connection
            hubConnection.Start().Wait();

            var result = currencyExchangeHubProxy.Invoke<string>(method).Result;

            return result;
        }

        private static void HandleNotify(Currency currency)
        {
            Console.WriteLine("Currency " + currency.CurrencySign + ", Rate = " + currency.USDValue);
        }
    }
}
~~~

En program.cs

~~~
using System;
using System.Diagnostics;
using System.Net;

namespace Client
{
    class Program
    {
        static void Main(string[] args)
        {
            var state = CommunicationHandler.ExecuteMethod("GetMarketState", 
            	"", IPAddress.Any.ToString(), "CurrencyExchangeHub");
            Console.WriteLine("Market State is " + state);

            if (state == "Closed")
            {
                var returnCode = CommunicationHandler.ExecuteMethod
                	("OpenMarket", "", IPAddress.Any.ToString(), "CurrencyExchangeHub");
                Debug.Assert(returnCode == "True");
                Console.WriteLine("Market State is Open");
            }

            Console.ReadLine();
        }
    }
}
~~~


---
### libro de jose Manuel Aguilar en ingles , pagina 123 habla de los servicios de windows y signalR


---
### Simple SignalR Server and Client Applications Demonstrating Common Usage Scenarios


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


	
### Introduction To ASP.Net SignalR Self Hosting

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
### Tutorial: SignalR Self-Host

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

### Self Hosting With SignalR and Web API Part 1 (Self Host Server, C#)

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

### Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 2


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
### Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 3


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

### Self Hosting SignalR and Web API (Self Host Server, C#) | Visual Studio 2019 | Part 4

https://www.youtube.com/watch?v=x_kjIvhVZh0

---

### Hosting SignalR under SSL/https

https://weblog.west-wind.com/posts/2013/Sep/23/Hosting-SignalR-under-SSLhttps





---


### Migrating SignalR from ASP.NET Web API 2 to Self Hosted Server (Part 3)

https://dotjord.wordpress.com/2018/05/29/migrating-signalr-from-asp-net-web-api-2-to-self-hosted-server-part-3/

---



### Self Hosted signalR in windows service; Minimum permissions for base url = http://*:1111

https://stackoverflow.com/questions/23428886/self-hosted-signalr-in-windows-service-minimum-permissions-for-base-url-http

~~~
netsh http add urlacl url=http://*:1111/ user=DOMAIN\user
~~~


---

## Libreria TopShelf para crear servicios windows


### SignalR with Self-hosted Windows Service (TopShelf)

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

### Painless .NET Windows Service Creation with Topshelf

http://dontcodetired.com/blog/post/Painless-NET-Windows-Service-Creation-with-Topshelf

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



## Injeccion de dependencias (IoC)

### Dependency Inject with SignalR & Castle Windsor

https://themarabeseblog.wordpress.com/2016/02/07/dependency-inject-with-signalr-castle-windsor/

Tenemos que añadir aparte de los paquetes nugets para signalR otro paquete mas:

~~~
signalR.Castle.Windsor 
~~~

tenemos que tener en el archivo cs donde difinimos el hub
~~~
[HubName("randomNumberHub")]  
   public class RandomNumberHub : Hub  
   {  
     private readonly ILogger _log;  
     public IRandomNumberGenerator Generator { get; set; }  
     public RandomNumberHub(ILogger logger)   
     {  
       _writer = writer;  
     }  
     public void GetRandomNumber()  
     {  
       _logger.Log("Get Random Number Called");
       Clients.All.updateRandomNumber(Generator.Random());  
     }  
   }  
~~~

un fichero .cs para poner esto
~~~
  public class SignalRDependencyResolver : DefaultDependencyResolver  
   {  
     private readonly IWindsorContainer _container;  
     public SignalRDependencyResolver(IWindsorContainer container)  
     {  
       if (container == null)  
       {  
         throw new ArgumentNullException(nameof(container));  
       }  
       _container = container;  
     }  
     public override object GetService(Type serviceType)  
     {  
       return _container.Kernel.HasComponent(serviceType) ? _container.Resolve(serviceType) : base.GetService(serviceType);  
     }  
     public override IEnumerable<object> GetServices(Type serviceType)  
     {  
       return _container.Kernel.HasComponent(serviceType) ? _container.ResolveAll(serviceType).Cast<object>() : base.GetServices(serviceType);  
     }  
   }  
~~~
Luego o bien desde el mismo startup o bien en un fichero aparte .cs, debemos poner esto:

~~~
 private static HubConfiguration CreateHubConfiguration()  
     {  
       var signalrDependency = new SignalRDependencyResolver(_container);  
       var configuration = new HubConfiguration { Resolver = signalrDependency };  
       return configuration;  
     }  

~~~

Luego en el startup tenemos que poner lo siguiente:

~~~
 app.MapSignalR(CreateHubConfiguration());  
~~~


---




### Using Unity for Dependency Injection with SignalR

https://consultwithgriff.com/using-unity-for-dependency-injection-with-signalr/


~~~
public class MyHub : Hub
{
   public MyHub(ISomeInterface interface)
   {
      // handle constructor injection here
   }
}
~~~


~~~
 public static void Initialise() // this isn't my misspelling, it's in the Unity.MVC NuGet package.
        {
            var container = BuildUnityContainer();

            var unityDependencyResolver = new UnityDependencyResolver(container);

            // used for MVC
            DependencyResolver.SetResolver(unityDependencyResolver);
            // used for WebAPI
            GlobalConfiguration.Configuration.DependencyResolver = new Unity.WebApi.UnityDependencyResolver(container);
            // used for SignalR
            GlobalHost.DependencyResolver = new SignalRUnityDependencyResolver(container);
        }

        private static IUnityContainer BuildUnityContainer()
        {
            var container = new UnityContainer();

            // register all your dependencies here.
            container.RegisterType<ISomeInterface, SomeInterface>();

            return container;
        }
~~~

~~~
public class SignalRUnityDependencyResolver : DefaultDependencyResolver
    {
        private IUnityContainer _container;

        public SignalRUnityDependencyResolver(IUnityContainer container)
        {
            _container = container;
        }

        public override object GetService(Type serviceType)
        {
            if (_container.IsRegistered(serviceType)) return _container.Resolve(serviceType);
            else return base.GetService(serviceType);
        }

        public override IEnumerable<object> GetServices(Type serviceType)
        {
            if (_container.IsRegistered(serviceType)) return _container.ResolveAll(serviceType);
            else return base.GetServices(serviceType);
        }

    }
~~~


Esto viene del trozo de codigo mas arriba, en el metodo Initialise() y BuildUnitiContainer() que le hemos añadido en este metodo ultimo, unas lineas mas de codigo para añadir el registro del hub de signalR:

~~~
private static IUnityContainer BuildUnityContainer()
        {
            var container = new UnityContainer();

            container.RegisterType<ISomeInterface, SomeInterface>();
            //esto es lo nuevo que se ha añadido
            container.RegisterType<MyHub>(new InjectionFactory(CreateMyHub));

            return container;
        }

        private static object CreateMyHub(IUnityContainer p)
        {
            var myHub= new MyHub(p.Resolve<ISomeInterface>());

            return myHub;
        }
~~~

---
### SignalR with an IoC container

https://cockneycoder.wordpress.com/2013/10/19/signalr-with-an-ioc-container/

Dicen en el articulo que este enfoque es mas sencillo, habra que probarlo
Aplican un enfoque con IHubActivator


~~~
  /// <summary>
    /// Uses Unity to create Hubs - and ONLY Hubs.
    /// </summary>

    // Register with GlobalHost.DependencyResolver.Register(typeof(IHubActivator), () => unityHubActivator);
    public class UnityHubActivator : IHubActivator
    {
        private readonly IUnityContainer container;

        public UnityHubActivator(IUnityContainer container)
        {
            this.container = container;
        }

        public IHub Create(HubDescriptor descriptor)
        {
            return (IHub)container.Resolve(descriptor.HubType);
        }
    }

    public class ExampleHub : Hub
    {
        private readonly IMyService myService;
        private readonly ILogger logger; 

        public ExampleHub(IMyService myService, ILogger logger)
        {
               this.myService = myService;
               this.logger = logger;
        }

        // Blah blah....
    }
~~~

---
### Using SignalR with Unity

https://damienbod.com/2013/11/05/using-signalr-with-unity/

codigo en Gihub : [Codigo:](https://github.com/damienbod/SignalRHostWithUnity)

Hay que instalar los siguientes paquetes nugets:

~~~
paquete nuget llamado <strong>Unity</strong> 'The Unity Application Block...'

paquete nuget llamado Microsoft ASP.NET SignalR Self Host
~~~

~~~
using System;
using Microsoft.AspNet.SignalR.Hubs;
using Microsoft.Practices.Unity;
 
namespace SignalRHostWithUnity.Unity
{
    public class UnityHubActivator : IHubActivator
    {
        private readonly IUnityContainer _container;
 
        public UnityHubActivator(IUnityContainer container)
        {
            _container = container;
        }
 
        public IHub Create(HubDescriptor descriptor)
        {
            if (descriptor == null)
            {
                throw new ArgumentNullException("descriptor");
            }
 
            if (descriptor.HubType == null)
            {
                return null;
            }
 
            object hub = _container.Resolve(descriptor.HubType) ?? Activator.CreateInstance(descriptor.HubType);
            return hub as IHub;
        }
    }
}


~~~

~~~
using System;
using Microsoft.AspNet.SignalR.Hubs;
using Microsoft.Practices.Unity;
using SignalRHostWithUnity.DataAccess;
 
namespace SignalRHostWithUnity.Unity
{
    public class UnityConfiguration
    {
        #region Unity Container
        private static Lazy<IUnityContainer> container = new Lazy<IUnityContainer>(() =>
        {
            var container = new UnityContainer();
            RegisterTypes(container);
            return container;
        });
 
        public static IUnityContainer GetConfiguredContainer()
        {
            return container.Value;
        }
        #endregion
 
        public static void RegisterTypes(IUnityContainer container)
        {
            container.RegisterType<MyHub, MyHub>(new ContainerControlledLifetimeManager());
            container.RegisterType<IHubActivator, UnityHubActivator>(new ContainerControlledLifetimeManager());
            container.RegisterType<IRepositoryUnityTestClass, RepositoryUnityTestClass>();
             
        }
    }
}
~~~

~~~
public class MyHub : Hub
    {
        private readonly IRepositoryUnityTestClass _repositoryUnityTestClass;
 
        public MyHub(IRepositoryUnityTestClass repositoryUnityTestClass)
        {
            _repositoryUnityTestClass = repositoryUnityTestClass;
        }
 
        public void AddMessage(string name, string message)
        {
            Console.WriteLine("Hub AddMessage {0} {1}\n", name, _repositoryUnityTestClass.SayHello() + message);
            Clients.All.addMessage(name, _repositoryUnityTestClass.SayHello() + message);
        }
~~~


~~~
using System;
using Microsoft.AspNet.SignalR;
using Microsoft.AspNet.SignalR.Hubs;
using Microsoft.Owin;
using Microsoft.Owin.Hosting;
using SignalRHostWithUnity.Dto;
using SignalRHostWithUnity.Unity;
 
namespace SignalRHostWithUnity
{
    class Program
    {
        private static  IHubContext _hubContext;
 
        static void Main(string[] args)
        {
            GlobalHost.DependencyResolver.Register(typeof(IHubActivator), () => new UnityHubActivator(UnityConfiguration.GetConfiguredContainer()));
 
            string url = "http://localhost:8089";
                     
            using (WebApp.Start(url))
            {
                _hubContext = GlobalHost.ConnectionManager.GetHubContext<MyHub>();
 
                Console.WriteLine("Server running on {0}", url);
                 
                while (true)
                {
                    string key = Console.ReadLine();
                    if (key.ToUpper() == "W")
                    {
                        _hubContext.Clients.All.addMessage("server", "ServerMessage");
                        Console.WriteLine("Server Sending addMessage\n");
                    }
                    if (key.ToUpper() == "E")
                    {
                        _hubContext.Clients.All.heartbeat();
                        Console.WriteLine("Server Sending heartbeat\n");
                    }
                    if (key.ToUpper() == "R")
                    {
                        var helloModel = new HelloModel {Age = 37, Molly = "pushed direct from Server "};
                        _hubContext.Clients.All.sendHelloObject(helloModel);
                        Console.WriteLine("Server Sending sendHelloObject\n");
                    }
                    if (key.ToUpper() == "C")
                    {
                        break;
                    }
                }
 
                Console.ReadLine();
            }
        }
    }
}
~~~




---
### Dependency Injection in SignalR

https://learn.microsoft.com/en-us/aspnet/signalr/overview/advanced/dependency-injection



---







































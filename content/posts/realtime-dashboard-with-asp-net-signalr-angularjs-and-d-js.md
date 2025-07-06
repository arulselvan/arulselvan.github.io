---
author: arul
category:
  - software-development
cover:
  alt: demo_screen-1024x5551212
  image: /wp-content/uploads/2014/10/demo_screen-1024x5551212-1.png
date: "2014-10-15T08:24:51+00:00"
guid: http://arul.pw/?p=199
tag:
  - angularjs
  - d3js
  - realtime-dashboard
  - signalr
title: RealTime Dashboard with ASP.NET Signalr, AngularJS and D3JS
url: /realtime-dashboard-asp-net-signalr-angularjs-d3js/

---
**About Signalr :**

Asp.NET SignalR is a library for ASP.NET developers to push the content from server to connected clients and vise versa.

Reference Link: [http://signalr.net/](http://signalr.net/ "SignalR") ,  [http://www.asp.net/signalr](http://www.asp.net/signalr/overview/signalr-20/getting-started-with-signalr-20/introduction-to-signalr "SignalR Introduction")/

**About AngularJS :**

AngularJS is an opensource web application client side framework, maintained by Google and community.

Reference Link: [https://angularjs.org/](https://angularjs.org/ "AngularJS") **About D3js :**

D3.js is a javascript library for manipulating document based on data. It helps in bringing data to visualization using HTML,SVG and CSS.

Reference Link: [http://d3js.org/](http://d3js.org/ "D3 Link")

Okay We can start now. In this article we are going to see how to build real-time dashboard application using above technologies, for sample I took scenario of available waiting calls in the call centre  (contact center) on each department. so this sample real time dashboard will be benefit for contact center manager and supervisor to monitor how many customers are waiting in the queue to get the agent transfer.

**Server Side Implementation:**

SignalR is an abstraction over some of the transports (WebSoket,Server Sent Event ,Forever Frame,Ajax long polling ). It will also support  fallback. For example if we take WebSocket transpor,it should meet some of the system requirement from both server and client end.

Server end: Windows Server 2012 or Windows 8

Client  end: Html5 supported browser(IE 10+, chrome,etc..)

If any one of the requirement gets failed, obviously websocket will not work. Here  Signalr will do magic, automatically it will look for alternative supported transport.(Forever or Ajax). So developer don't want to worry  about anything.

To Learn more about SignalR please visit following link [http://www.asp.net/signalr/](http://www.asp.net/signalr/). In below we are going to see only how these technologies makes our Job easy to build real time solution.

**The Server side Hub:**

This will push content to clients.

```default
public class RealTimeQueueHub : Hub
{

}
```

 **Client Side Hub connection with (angularJS) :**

Reference file require in HTML page.

```default
<script src="Scripts/jquery-1.6.4.min.js"></script>
<script src="Scripts/angular.min.js"></script>
<script src="Scripts/jquery.signalR-2.1.0.min.js"></script>
<script src="/signalr/hubs"></script>
```

We having  our client connection inside angular JS service because Service are singleton and easy to take control for callback.

```default
var myApp=angular.module('myApp', []);

myApp.service('queueService', function ($rootScope) {

        var hub = $.connection.realTimeQueueHub;

        hub.client.receiveRealTimeData = function (data) {

            //broadcast the received data  to all the subscribed controller.

            $rootScope.$emit("acceptData", data);
        };

        $.connection.hub.start();  // start the signalr connection

});
```

Controller will  receive the data from service then pass to $scope variable  to update the user interface.

```default
myApp.controller('Ctrl',['$scope','$rootScope','queueService',function Ctrl($scope,$rootScope,queueService) {

		$scope.loading=true;

		$rootScope.$on("acceptData",function(e,message){

				$scope.$apply(function(){
						$scope.myData= message;
				});

				$scope.loading=false;
		});

}]);
```

angular JS is two way binding, once the data updated in the controller, view automatically re-rendered based on updated values.

```default
<div ng-app="myApp" ng-controller="Ctrl">
	<bars-chart chart-data="myData" title='Queue RealTime Dashboard' > </bars-chart>
</div>
```

Inside view we have custom directive to  draw simple bar chat based on myData value. This custom directive we build with the help of D3.JS .

```default
//custom directive to create the bar chart with help of D3.js
myApp.directive('barsChart', function ($parse) {

    var directiveDefinitionObject = {

        restrict: 'E',
        replace: true,
        scope: { data: '=chartData', title: '@' },
        template: '<div class="chart"><h3 class="chartTitle">{{title}}<h3></div>',
        link: function (scope, element, attrs, ctrl) {

            scope.$watchCollection('data', function (newVal, oldVal) {

                if (!newVal)
                    return;

                var chart = d3.select('.chart');
                chart.selectAll('div').remove().transition().ease("elastic");

                chart.selectAll('div')
					.data(newVal).enter().append("div").transition().ease("elastic")
					.style("width", function (d) { return (d.value) + "%" })
					.style("background-color", function (d) {

					    //This background style will help to segregate bar based on some threshold value

					    if (d.value > 30 && d.value <= 60)
					        return "#D4A835";
					    else if (d.value > 60)
					        return "#E0272A";
					    else
					        return "#2F9756";

					})
				 .text(function (d) { return d.label + "  (" + d.value + ")"; });

            });

        }
    };
    return directiveDefinitionObject;
});

```

Now again we can go to server end. We have to pull the real time data from  database or some back end system with some specified interval  then push the data to all our subscribed client.

Really running scheduled background work in asp.net I will not suggest, Even this example we used official recommended approach  IReggisteredObject with the ASP.NET runtime and hook it up at application start.

For more robust solution even we can host the signalR explicit windows service.

```default
 public class BackgroundProcess : IRegisteredObject
    {
        private Timer _timer;
        private IHubContext _hub;

        public BackgroundProcess()
        {
            HostingEnvironment.RegisterObject(this);

            _hub = GlobalHost.ConnectionManager.GetHubContext<RealTimeQueueHub>();

            _timer = new Timer(OnTimerElapsed, null,
                TimeSpan.FromSeconds(1), TimeSpan.FromSeconds(5));
        }

        private void OnTimerElapsed(object sender)
        {
            // Here we can do our logic to get the data from API / Database .
            // This example just I am taking random value and pushing to all connected clients.

            var rnd = new Random();

            var updatedValues = new List<RealTimeData>{
                    new RealTimeData("CreditCard",rnd.Next(1,100)),
                    new RealTimeData("Banking",rnd.Next(1,100)),
                    new RealTimeData("Loan",rnd.Next(1,100)),
                    new RealTimeData("Other Service",rnd.Next(1,100)),

            };

            _hub.Clients.All.ReceiveRealTimeData(updatedValues);
        }
        public void Stop(bool immediate)
        {
            _timer.Dispose();
            HostingEnvironment.UnregisterObject(this);
        }
    }
```

In Application\_Start method simply we can start our background thread.

```default
 public class WebApiApplication : System.Web.HttpApplication
    {
        protected void Application_Start()
        {
            AreaRegistration.RegisterAllAreas();
            GlobalConfiguration.Configure(WebApiConfig.Register);
            RouteConfig.RegisterRoutes(RouteTable.Routes);
            BundleConfig.RegisterBundles(BundleTable.Bundles);

            //starting our background thread process
            new BackgroundProcess();
        }
    }
```

Here we are simply pushing the data to all the connected clients, But real time we can do lot more,  maintain active client, identifying particular user and  pushing to only logged in clients, etc...

Snapshot :

[![demo_screen](/wp-content/uploads/2014/10/demo_screen-1024x555.png)](/wp-content/uploads/2014/10/demo_screen.png)

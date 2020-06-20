AngularJs
-------------

Continuous integration with Angular Node.js

Course: Continuous integration with Angular Node.js
Course: Building Angular and Node.js Apps with the MEAN Stack, 2014
https://app.pluralsight.com/library/courses/building-angularjs-nodejs-apps-mean/table-of-contents 
// serving index.html
app.get('/', function(req, res) {
    res.sendfile(__dirname + '/index.html');
});



How node.js send index.html
Jade: html templating
Heroku.com: app host 
Mongolab: online mongo
Bluebird: promise async
Codeship: deploy, email notification
	Npm install -g mocha
	Mocha
	$ Git add -a
	$ git commit -a “test”
	$ git push

Karma: test in browser
Karma-mocha, karma-chi, karma-cli
Phantomjs, karma-phantomjs-launcher

Nodemailer
http://masashi-k.blogspot.com/2013/06/sending-mail-with-gmail-using-xoauth2.html 

Deploy to Heroku (updated 1/29/2017)
Getting started: https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction 
best practice: https://devcenter.heroku.com/articles/node-best-practices
https://devcenter.heroku.com/articles/git 
Use port in server: process.env.PORT
Install Heroku toolbelt
Cd your app/web where it has .git (if not, $ git init)
$ cd ~/lottery/web
$ heroku login	(w@g, m*)
$ heroku git:remote -a houlottery
$ git add .
$ git commit -am "make it better"
$ git push heroku master
$ heroku logs –t
$ heroku restart
$ heroku ps:scale web=0 --app houlottery // stop the app

Post: http://houlottery.herokuapp.com/updateCron 
Heroku force free app after 30 min inactivity! Ping service every 30 min:
http://kaffeine.herokuapp.com/
https://uptimerobot.com/dashboard#mainDashboard 

gmail Oath2
full instructions:
https://medium.com/@pandeysoni/nodemailer-service-in-node-js-using-smtp-and-xoauth2-7c638a39a37e#.xbe42hmvo

create app to get client ID and secret:
https://console.cloud.google.com/apis/credentials?pli=1&project=lottoscheduler

get access token and refresh token:
https://developers.google.com/oauthplayground

emailjs
https://www.npmjs.com/package/emailjs
xom.houston@outlook.com, lottery2017, 1/27/1980

crawler scraper
cheerio for static dom
phantomjs, phantomjs-node for dynamic content
	Npm install phantom
http://code.tutsplus.com/tutorials/screen-scraping-with-nodejs--net-25560 
Angular
Course: Angular Application Development, 2015
https://app.pluralsight.com/library/courses/angular-application-development/table-of-contents 

github.com/simpulton/notorious
github.com/simpulton/angularjs-testing-quick-start
bit.ly/ng-app-workshop

files structure
organize files by feature/function
	html and js files are put in the same folder
app
index.html – main.js
boards
common (shared across features)
		model
		services
login
main
notes
assets
	css
	font
	imges
vendor
	angular-gridster.min.js
	angular-ui-router.min.js
	angularfire.js

route
Karma (unit testing), Protractor (E2E testing)

View

Controller
Ng-controller = “MainCtrl as main” results in
	$scope.main = new MainCtrl();
A controller should never know about the view it controls.

Services
Provide common functionality across your entire application
Essentially the model in the MVW.
Keep your controllers skinny so that your models can be fat.
	userPreferenceService.js, updateService.js

factory just return object with properties
service has a constructor, so it has “this”

directive
convert camel style to snake style in html
link: 
ng-click=”main.setCurrentItem(item); ctrl.incrementCount();”

state
allow named views, states, nested view, 
$state.go()

Angular Patterns: Clean Code
TCE notes:
1.	folder structure by feature/module: app.tceFax, app.tceUpload, app.core, app.common
2.	wrap all in IIFE; 
3.	interface: declare properties/return value first in file; 
4.	Avengers as av; vm = this; 
5.	in route, resolve: { container: function(){} }

Introduction
Webstorm 2016.2: http://jetbrains.tencent.click/ 
	git clone Github.com/johnpapa/ng-demos
	Modular, cc-bmean
1.	Install nodejs
2.	> npm install –g bower gulp karma-cli nodemon
3.	> Cd modular
4.	> npm install
5.	> gulp serve-dev

Edit configuration: set up “run app”
Set up mongo in webstorm: ^shift A

Separation of Concerns (SoC)
Controller is for view
A component has one roll, one per file, singular purpose

Inject and invoke module startup code
App.run([‘appStart’, function(appStart) {
	appStart.start();
}]);

Organizing Your App
Organize by type (small app), by feature (big app)

LIFT principle
L: locating our code is easy (structure/naming)
I: identify code at a glance
F: flat structure as long as we can (3-4 files per folder)
T: try to stay DRY (no repeating)

Expose properties and services in the biginning
 

/app/avengers
/app/blocks
	/exception
	/logger
	/router
/app/common (common functions: createSearchThrottle, debouncedThrottle, isNumber, logger, textContains)
/app/core (dataService: getAvengerCast, getAvengerCount, getAvengers, ready)
/app/dashboard
/app/layout (templates with directive)
/app/widgets (sidebar, spinner, close, header, minimize)

preload data in app.js with ui-router
http://stackoverflow.com/questions/22209107/angularjs-ui-router-preload-http-data-before-app-loads

naming
angular
	.module(‘app.avengers’)
	.controller(‘Avengers’, [‘common’, ‘dataservice’, Avengers]);
Function Avengers(common, dataservice) {}
PascalCase for controller, camelCase for others

Modules
//setter
Var app = angular.module(‘app’, []);
//getter
Var app = angular.module(‘app’);

Angular.module(‘app’, [
	‘app.core’,
	‘app.widgets’,
	‘app.dashboard’,
	‘app.avengers’,
	‘app.layout’
]);

Angular.module(‘app.core’, [
	‘ngAnimate’,
	‘ngRoute’,
	‘ngSanitize’,
	‘blocks.exception’,
	‘blocks.logger’,
	‘blocks.router’,
	‘ngplus’
]);


Dependencies strategy

Widgets (directive) are lazy loaded: app still runs without loading it in app.js


Readable Code and AngularJS
Chaining up
Angular.module(‘app’)
	.controller(‘Avengers’, Avengers);
Avengers.$inject = [‘$location’, ‘$scope’, …];
/* @ngInject */  //ngAnnotate, no need for above then
Function Avengers($location, $scope) {
}

Immediately invoked function express (IIFE)
(function(){
	Angular
		.module(‘app’)
		.controller(‘Avengers’, Avengers);
})();

Use named functions

Controller Patterns
Controller always create a new instance, essentially a constructor

<div ng-controller=”Avengers as av”>
<input ng-model=”av.name”/>
<span>{{av.name}}</span>
var vm = this;

$scope.$watch(function(){ 
return vm.title; },  // this.title does not work here
	Function(newVal, oldVal) {
		Console.log(newVal + ‘---‘ + oldVal);
	});

Defined it in the route to dynamically change controllers
	Controller: ‘Avengers’,
	ControlerAs: ‘vm’

Ng-route: resolve: {} has to use together with controllerAs in route
Put this in the routeHelperConfiguer, not in app.run() which is hard to test

Annotations and Code Analysis via Gulp Task Automation
Grunt vs gulp
	Npm init
	Npm install gulp –save-dev
	Npm install gulp-ng-annotate gulp-jshint –save-dev

	Gulp –gulpfile gulpfile.js annotate
	Gulp –gulpfile gulpfile.js jshint
	Gulp –gulpfile gulpfile.js watch


Exception Handling
Decorator

$http.get(‘/api/maa404’)
	.then(getAvengers)
	.catch(exception.catcher(‘XHR failed for getAvengers’));

	Catch(function(message) {
		Exception.catcher(‘XHR error’)(message);
		$location.url(‘/’); // redirect to homepage
	}

Style guide: https://github.com/johnpapa/angular-styleguide

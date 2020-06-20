Node.js
-------------

All about Node.js From the Ground Up and More
2015.02
Open node console, then REPL

Var testStream = Fs.createReadStream(‘./test.txt’).pipe(res);
testStream.on(‘error’, function(){
	
});

NodeJS implements commons interface for importing modules:
Module.exports = {
	addFn: function(a, b) {
		return a + b;
	},
	subtractFn: function(a, b) {
		return a – b;
	}
}

Qr-image: yet another QR code generator

MongoDB
Table -> collection; row -> document
	High performance read/write
	Highly & easily scalable (sharding)
	Schemaless
	Json style, easy to work with NodeJS

Create folder c:\mongo\data\db
	In mongo installation path:
	Copy con mongod.cfg
Logpath=c:\mongo\log
Dbpath=c:\mongo\data\db
install mongod as a service
	Mongod.exe –config “C:\mongoPath\mongod.cfg” –install
	Net start mongodb // start mongo as a windows service
	Mongod // open mongo shell
	Show dbs
	User mailingList
	Show collection
	Db.users.insert({“name”: “John”, “email”: “test@gmail.com”})
	Db.users.find().pretty()
	Db.users.update({“name”: “John”}, {$set: {“phone”: 1234567}}, {upsert: true})
	Db.users.remove({“name”: “Json”})
	Db.dropDatabase()


ChatCAT project
https://github.com/Frosty92/ChatCat 
Modules: Express, passport, MongoLab, socket.io, heroku 
Hogan-express: html template engine, similar to Jade
Var app = require(‘express’)();
App.set(‘view’, path.join(__dirname, ‘views’));
App.engine(‘html’, require(‘hogan-express’));
App.set(‘view engine’, ‘html’);
App.use(express.static(path.join(__dirname, ‘public’)));
//App.route(‘/’).get(function(req, res, next) {
//	Res.render(‘index’, {});	// /views/index.html
//}

require(‘./routes/routes.js’)(express, app);

// put all routes in routes.js
Module.exports = function(express, app) {
	var router = express.Router();
	router.get(‘/’, function(req, res, next) {
		Res.render(‘index’, {title: ‘Welcome to ChatCAT’});
	});

	App.use(‘/’, router);
}

Session
var cookieParser = require(‘cookie-parser’);
var session  = require(‘express-session’);
App.use(cookieParser());
App.use(session({secret: ‘catcanfly’, saveUninitialized:true, resave:true}));

Router.get(‘/setColor’, function(req, res, next) {
	Req.session.favColor = ‘Red’;
	Res.send(‘Setting favorite color!’);
}

Router.get(‘/getColor’, function(req, res, next) {
	Res.send(‘Favorite color: ‘ + (req.session.favColor === undefined? ‘Not found’ : req.session.favColor);
}

Var env = process.env.NODE_ENV || ‘development’;
	Set NODE_ENV=production // in Windows 
In production, need mongodb to save sessions.
Folder /config	
/config.js
	Module.exports = require(‘./’ + (process.env.NODE_ENV || ‘development’) + ‘.json’);
		/production.json
		Development.json

Var ConnectMongo = require(‘connect-mongo’)(session);

// production: store sessions in mongodb
App.use(session({
	Secret: config.sessionSecret,
	Store: new ConnectMongo({
		//url: config.dbURL,	// mongoLab DB url
		Mongoose_connection:mongoose.connection[0], // use the existing mongo connection 
		stringify: true
		})
}));

// mongoose
Mongoose = require(‘mongoose’).connect(config.dbURL);
var userSchema = mongoose.Schema({
	Username: String, password: String, fullname: String});
var Person = mongoose.model(‘users’, userSchema);
var John = new Person({username: ‘john’, password: ‘john@test’, fullname: ‘John Test’});
John.save(function(){
	Console.log(‘John is save in mongoDB’);
})

//Login via facebook: developers.facebook.com
// Passport


Node.js MEAN stack
Course: Play by Play: Building a Node Web API with Sam Artioli and John Papa
Course: Introduction to MEAN JS 
http://bootstrapzero.com/bootstrap-template/solid
code generation from MEAN.js
	npm install -g generator-meanjs
	Yo meanjs:angular-module widget
	Yo meanjs:angular-route myroute
	Yo meanjs:angular-view foo
	Yo meanjs:curd-module need
Nodemailer (own gmail), Sendgrid (cloud email service) to send email

 
 
https://github.com/samartioli/node-play-by-play
$ npm init -y // create the default package.json
$ npm install express –save
$ npm install -g nodemon // auto update js/html to server
	Nodemon is platform specific
$ npm install –save lodash
$ npm install –save body-parser
$ npm install –save mongoose
$ npm install -g forever // runs as daemon
$ forever dog_server.js
$ forever list
$ forever restart dog_server.js
$ npm install –save request // make http request
$ npm install –save async
$ npm install –save blocked

Redis: key-value in-memory caching


Test: mocha, expect, should, supertest
Debug: devtool

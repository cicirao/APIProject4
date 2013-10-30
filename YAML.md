#Better Know a Format -- YAML


##YAML: YAML Ain't Markup Language

YAML is a human friendly data serialization standard for all programming languages.

##History

Since 2001, YAML has three editions till today:
>  [YAML 1.2 (3rd Edition)](http://www.yaml.org/spec/1.2/spec.html)

>  [YAML 1.1 (2rd Edition)](http://yaml.org/spec/1.1/)

>  [YAML 1.0 (1rd Edition)](http://yaml.org/spec/1.0/)	

YAML is superset of JSON.

YAML's initial direction was set by the data serialization and markup language discussions among SML-DEV members. Later on it directly incorporated experience from Brian Ingerson's Perl module Data::Denter. 

YAML’s core type system is based on the requirements of agile languages such as Perl, Python, and Ruby. YAML directly supports both collections (mappings, sequences) and scalars. Support for these common types enables programmers to use their language’s native data structures for YAML manipulation, instead of requiring a special document object model (DOM).

## Example & Usage

Cashers often use it to store the receipt information.

		---
		receipt:     Oz-Ware Purchase Invoice
		date:        2012-08-06
		customer:
		    given:   Dorothy
		    family:  Gale

		items:
		    - part_no:   A4786
		      descrip:   Water Bucket (Filled)
		      price:     1.47
		      quantity:  4

		...

Google app engine use YAML to write configuration file. To almost all the script languages, YAML is a great way to write configuration files, especially in Ruby.
				
		# 
		# Config file example 
		# 

		node_a: 
		conntimeout: 300 
		 external: 
		 iface: eth0 
		 port: 556 
		 internal: 
		 iface: eth0 
		port: 778 
		 broadcast: 
		 client: 1000 
		 server: 2000 
		node_b: 
		 0: 
		 ip: 10.0.0.1 
		 name: b1 
		 1: 
		 ip: 10.0.0.2 
		 name: b2 

## YAML in Action on the Internet

A Go App Engine application can be configured by a file named app.yaml that specifies how URL paths correspond to request handlers and static files. It also contains information about the application code, such as the application ID and the latest version identifier.

know more about it: [https://developers.google.com/appengine/docs/go/config/appconfig](https://developers.google.com/appengine/docs/go/config/appconfig)

## Parsed 

We can used the module "[js-yaml](https://github.com/nodeca/js-yaml)" to help.

### In the Browser 

		<script>
		var doc = jsyaml.load('greeting: hello\nname: world');
		$( document ).ready(function() {
		  $('p').html(doc.greeting);
		});
		</script>

But in the browser, it could only parse YAML as string, not the '.yml' or '.yaml' file.

## Node.js

The module is designed for Node.js.
This example will parse a small configuration file in YAML.

In your configuration file:

		---
		username: admin
		password: guest
		days:
		- mon
		- tue
		- wed
		- thu
		- fri

In node.js, the module "js-module" automatically registers handlers for '.yml' and '.yaml' files. It's easy to only use "require" to load them.

		// Include our 'js-yaml' module.
		var yaml = require("js-yaml");

		// Import the 'config.yaml' file in the current directory
		// store it in the config variable
		var config = require('./config.yaml');
		// display on the console
		console.log(config);

If succeed, you will see the javascript object on the console.

		{ username: 'admin',
		  password: 'guest',
		  days: [ 'mon', 'tue', 'wed', 'thu', 'fri' ] }

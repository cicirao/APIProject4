#Better Know a Format -- YAML


##YAML: YAML Ain't Markup Language

YAML is a human friendly data serialization standard for all programming languages.

YAML is superset of JSON.

Since 2001, YAML has three editions till today:
>  [YAML 1.2 (3rd Edition)](http://www.yaml.org/spec/1.2/spec.html)

>  [YAML 1.1 (2rd Edition)](http://yaml.org/spec/1.1/)

>  [YAML 1.0 (1rd Edition)](http://yaml.org/spec/1.0/)	

##Origins

YAML's initial direction was set by the data serialization and markup language discussions among SML-DEV members. Later on it directly incorporated experience from Brian Ingerson's Perl module Data::Denter. Since then YAML has matured through ideas and support from its user community.

YAML integrates and builds upon concepts described by C, Java, Perl, Python, Ruby, RFC0822 (MAIL), RFC1866 (HTML), RFC2045 (MIME), RFC2396 (URI), XML, SAX, SOAP, and JSON.

The syntax of YAML was motivated by Internet Mail (RFC0822) and remains partially compatible with that standard. Further, borrowing from MIME (RFC2045), YAML’s top-level production is a stream of independent documents, ideal for message-based distributed processing systems.

YAML’s indentation-based scoping is similar to Python’s (without the ambiguities caused by tabs). Indented blocks facilitate easy inspection of the data’s structure. YAML’s literal style leverages this by enabling formatted text to be cleanly mixed within an indented structure without troublesome escaping. YAML also allows the use of traditional indicator-based scoping similar to JSON’s and Perl’s. Such flow content can be freely nested inside indented blocks.

YAML’s double-quoted style uses familiar C-style escape sequences. This enables ASCII encoding of non-printable or 8-bit (ISO 8859-1) characters such as “\x3B”. Non-printable 16-bit Unicode and 32-bit (ISO/IEC 10646) characters are supported with escape sequences such as “\u003B” and “\U0000003B”.

Motivated by HTML’s end-of-line normalization, YAML’s line folding employs an intuitive method of handling line breaks. A single line break is folded into a single space, while empty lines are interpreted as line break characters. This technique allows for paragraphs to be word-wrapped without affecting the canonical form of the scalar content.

YAML’s core type system is based on the requirements of agile languages such as Perl, Python, and Ruby. YAML directly supports both collections (mappings, sequences) and scalars. Support for these common types enables programmers to use their language’s native data structures for YAML manipulation, instead of requiring a special document object model (DOM).

Like XML’s SOAP, YAML supports serializing a graph of native data structures through an aliasing mechanism. Also like SOAP, YAML provides for application-defined types. This allows YAML to represent rich data structures required for modern distributed computing. YAML provides globally unique type names using a namespace mechanism inspired by Java’s DNS-based package naming convention and XML’s URI-based namespaces. In addition, YAML allows for private types specific to a single application.

YAML was designed to support incremental interfaces that include both input (“getNextEvent()”) and output (“sendNextEvent()”) one-pass interfaces. Together, these enable YAML to support the processing of large documents (e.g. transaction logs) or continuous streams (e.g. feeds from a production machine).



## Example & Usage

The way YAML organize data depends on space, indentation, line feeds, etc, which makes it easy to use.

Cashers often use it to store the receipt information.

Below is a example of YAML. It's a receipt.

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

		    - part_no:   E1628
		      descrip:   High Heeled "Ruby" Slippers
		      size:      8
		      price:     100.27
		      quantity:  1

		bill-to:  &id001
		    street: |
		            123 Tornado Alley
		            Suite 16
		    city:   East Centerville
		    state:  KS

		ship-to:  *id001

		specialDelivery:  >
		    Follow the Yellow Brick
		    Road to the Emerald City.
		    Pay no attention to the
		    man behind the curtain.
		...


The grammar is quite easy: 

This sample document defines an associative array with 7 top level keys: one of the keys, "items", contains a 2 element array (or "list"), each element of which is itself an associative array with differing keys. Relational data and redundancy removal are displayed: the "ship-to" associative array content is copied from the "bill-to" associative array's content as indicated by the anchor ( & ) and reference ( * ) labels. Optional blank lines can be added for readability. Multiple documents can exist in a single file/stream and are separated by "---". An optional "..." can be used at the end of a file (know more: [reference card](http://www.yaml.org/refcard.html))

Also, to almost all the script languages, YAML is a great way to write configuration files. It's parsed faster than XML, especially in Ruby.
				
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

The following is an example of an app.yaml file for a Go application:

		application: myapp
		version: 1
		runtime: go
		api_version: go1

		handlers:
		- url: /stylesheets
		  static_dir: stylesheets

		- url: /(.*\.(gif|png|jpg))
		  static_files: static/\1
		  upload: static/(.*\.(gif|png|jpg))

		- url: /.*
		  script: _go_app

know more about it: [https://developers.google.com/appengine/docs/go/config/appconfig](https://developers.google.com/appengine/docs/go/config/appconfig)



## Parsed 

Here I used the module "js-yaml" to help.

### In the Browser 

		<!DOCTYPE html>
		<html>
		<head>
			<meta charset="utf-8">
			<title>YAML</title>
		</head>
		<body>
			<p>Not loaded yet..</p>
		<script src="http://ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
		<script src="http://nodeca.github.io/js-yaml/js/js-yaml.js"></script>
		<script>
		var doc = jsyaml.load('greeting: hello\nname: world');
		$( document ).ready(function() {
		  $('p').html(doc.greeting);
		});
		</script>
		</body>
		</html>

If succeed, you will see "hello" in the browser.
But in the browser, it could only parse YAML as string, not the '.yml' or '.yaml' file.

## Node.js

The module is designed for Node.js.
This example will parse a small configuration file in YAML.

Make sure "js-yaml" is included in your dependencies.

		{
			"name": "YAML",
			"version": "0.0.1",
			"description": "Parse YAML with Node.js",
			"dependencies": {
				"js-yaml": "2.1.3"
			}
		}

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

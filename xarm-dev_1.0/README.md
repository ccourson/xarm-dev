Create folders for project

	mkdir myapp_1.0
	mkdir myapp_1.0/DEBIAN

Create and edit control

	nano myapp_1.0/DEBIAN/control
		Package: myapp
		Version: 1.0
		Maintainer: Chris Courson <chris@chrisbot.com>
		Architecture: all
		Description: A description that can span multiple lines. Each additional
		 line should start with a space.

Files are included in a folder structure as they will be applied on the target system.

	mkdir -p myapp_1.0/usr/bin

Create the example app

	nano myapp_1.0/usr/bin/myapp
		#!/usr/bin/env bash
		echo "This text came from a custom application!"

Set owner of project folder to root

	sudo chown -R root:root myapp_1.0/
	
Set permission of /usr/bin folder

	sudo chmod -R 755 myapp_1.0/usr
	
Set permission on CONTROL file

	sudo chmod 644 myapp_1.0/DEBIAN/control

Create package

	dpkg-deb --build myapp_1.0

Install package

	dpkg -i myapp_1.0.deb
	
Other commands

	dpkg --list
	apt --purge remove myapp


Config scripts - <app_name>/DEBIAN/config

	#!/bin/sh
	 
	# Exit on error
	set -e
	 
	# Source debconf library.
	. /usr/share/debconf/confmodule
	 
	# Ask questions
	db_input low packagename/question1 || true
	db_input low packagename/question2 || true
	 
	# Show interface
	db_go || true
	
	# Fetching configuration from debconf
	db_get packagename/question1
	ANSWER1=$RET
	 
	db_get packagename/question2
	ANSWER2=$RET


Templates - <app_name>/DEBIAN/templates

	Template: packagename/question1
	Type: [select,multiselect,string,boolean,note,text,password]
	Default: [an optional default value]
	Description: Blah blah blah?
	 
	Template: packagename/question2
	....
	
	From <https://www.leaseweb.com/labs/2013/06/creating-custom-debian-packages/> 
	
	

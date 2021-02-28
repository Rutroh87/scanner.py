#!/bin/python

import sys
import socket
from datetime import datetime 

#define our target 
if len(sys.argv) == 2:
	target = socket.gethostbyname(sys.argv[1]) #Translate hostname to IPv4
else: 
	print("invaild amount of arguements.") 
	print("Syntax: python3 scanner.py <ip>")

#Add a pretty banner 
print("." * 50)
print("scanning target " +target)
print("time started: "+str(datetime.now()))

try: 
	for port in range(50,81): 
		s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
		socket.setdefaulttimeout(1)
		result = s.connect_ex((target,port)) #returns an error indicator 
		if result == 0:
			print("Port{} is open".format(port))
		s.close()
			
		
except KeyboardInterrupt: 
	print("\nExiting program.")
	sys.exit()
	
except socket.gaierror:
	print("Hostname could not be resolved.")
	sys.exit()
	
except socket.error:
	print("Couldn't connect to server.")
	sys.exit()

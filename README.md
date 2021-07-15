# link-ros-with-web-pag
get servo angles from http requests and publish to/joint_states topic

#include <Servo.h>

Servo myservo; 

String header;

String valueString = String(5);

int pos1 = 0;

int pos2 = 0;

 if(header.indexOf("GET /?value=")>=0) {
              pos1 = header.indexOf('=');
              pos2 = header.indexOf('&');
              valueString = header.substring(pos1+1, pos2);
               myservo.write(valueString.toInt());
              Serial.println(valueString); 
            }      
            
First, we include the Servo library, and create a servo object called myservo.

#include <Servo.h>

Servo myservo; 

// Variable to store the HTTP request

String header;

// Decode HTTP GET value
Then, create a couple of variables that will be used to extract the slider position from the HTTP request.

String valueString = String(5);

int pos1 = 0;
int pos2 = 0;

The following part of the code retrieves the slider value from the HTTP request.

//GET /?value=180& HTTP/1.1
            if(header.indexOf("GET /?value=")>=0) {
              pos1 = header.indexOf('=');
              pos2 = header.indexOf('&');
              valueString = header.substring(pos1+1, pos2);
	      
  When you move the slider, you make an HTTP request on the following URL, that contains the slider position between the = and & signs.
  
  The slider position value is saved in the valueString variable.
  
Then,set the servo to that specific position using myservo.write() with the valueString variable as an argument. The valueString variable is a string, so we need to use the toInt() method to convert it into an integer number – the data type accepted by the write() method.

 myservo.write(valueString.toInt());
              Serial.println(valueString); 
            }      


# location
36. Lecture: -
 

When the user clicks on the save button the form should be submitted. 
And on the server side: -
The spring container will take all the fields (like., id, code, name type) that come in the request.  It will convert into an object and we can retrieve that object inside our controller using a concept called ModelAttribute in spring. 
Explanation: - User entered all the fields id, code, name, and Type and submit ‘save’ button. Then 
(Spring container will take the (user) client request (this request contains id, code, name, and type) and convert into an object. 
That object retrieves (captured that request) inside of the controller. How do we retrieve it?
The concept is called ModelAttribute in spring.  (Here, Location is object) Take the object (Location) and save it the database.   
How do save it? 
We must have all these (here, following JPA) Bean, Service and Repository layers to save object, update object, get object, get all objects, and delete object in database.)


---  Go to createLocation.jsp page 
 
    So, <form action=”saveLoc” This is URI that we will be mapping to the controller method. 
 method =”post”>  because we are submitting a form and all its data will go through a POST method we are creating a location. 

Go back to the controller -> 
Write a one request mapping for “saveLoc” for POST method. 
 




This method returning jsp page. Ie., createLocation.jsp 
 
createLocation.jsp
 


 
@RequesgtMapping is the annotation. This @RequestMapping capture the request from frontend or UI. (“/”) -> it means called URI
URI = (“/”)
Here, what URI is placing ?  
 <form action=”saveLoc” This is URI.

  This method. saveLoction() has to perform the save Location object.  How to do ?
We have one concept of ModelAttribute in spring. This @ModelAttribute annotation will do this one. 
  When you are passing @ModelAttribute(“location”)
By default, spring will create a model object and set all the fields of Location class or entity (id, code, name, and type) that come into the request. That request exposes it out as a bean with following name. 
It will use class name Location. But first letter will be lower case. 
So, this is bean that Spring container will handover and we are taking it and we are asking it set that as a parameter, Location location.

 
So, we got model object and so,  the request will mapped to the model object and we got it in our controller method. 
( @ModelAttribute(“location”) in the braces the first letter must be small like “location”. Which object are you passing to database? Location object. )

The next step is to simply invoke the repository or the service.save. 
 
 
You can find above line   service.saveLocation(location); -> Why do we go service. saveLocation(location)?
Directly why do write -> repository. save(location)? 
Ans: - Directly we can save the object into database through repository layer. But here, we are not doing. The reason behind is that decoupling. Spring will recommend you that follow decoupling. It means that 
When you are following the process: Like:
First Entity Layer -> Controller -> public interface -> class ServiceImpl -> Interface Repository
Had Better to follow: When you follow this way. Wherever you want to improvise particular class or layer you can do it in easy way. 


Steps 1
 
Note: - Location is entity for database object. 
Step 2
 
 
Note: - Controller will capture client or user request and process to save the java object into the database.  LocationService (I)autowired with reference of service. This service reference is pointing 
LocationService.
Step 3
 
Note: - So, LocationService interface has many methods declared among that 
SaveLocation (Location location);







Step 4:
 
Note: - All non-implemented methods in LocationService to be imported in LocationServiceImpl class.
Here, we are implementing for those methods. 
Step 5
 
Note: - 1. JpaReposiotory is an interface of Jpa. This interface already has all methods (save (), findbyId (), delete () and so on) by default. 
2. By default all those methods are extended to our customized interface i.e.., LocationRepository.  
Next: -

 Whenever you create an object (Location) into the database. Then, send a success message back to the web browser.  We will send the id of the object that was just created or that was just created back to the user.  

Go to -> Controller class 
 
  
Above line meaning is that just save the location object into the database. But we need to make it confirm whether the object is created or not.  How can make it confirm?
Ans: - Two things. 
1. Return type (assign type) of the method (service. saveLocation(location).
2. The id of the object (Location -> id, code, name, and type) that was just created or that was just created and back to the user. By a message. 

1.	 
Explanation: - service. saveLocation(location): - location is what type Location type. So, 
you must assign the location object into Location type only. 
2.	 

Explanation: - The   + id will get it in back end only. 
But how can I get it this message to the UI or front end.
Ans: - The spring will allow us to do that using a concept called ModelMap. 
(1)	To handle the request, it is ModelAttribute.
(2)	To handle the response, it is ModelMap. 
 
	 
 

Notes: - ModelMap is passing as an argument and using this ModelMap object (ModelMap modelMap). 
Call the addAttribute () method and pass the msg as argument.

Next --- 
This ModelMap   can be accessed by jsp using spring expression language. 
 
 

Next
 
 
 
The first part of the View All requirement is to add.  View All button clicking on which the request will be sent to our controller and inside the controller we need to handle the incoming request. 

Go to -> createLocation.jsp

Use a link display. This is relative displayLocation. 
Add the hyperlink.     
This is View All so add that text there the user clicks on this, this relative URI will be used. 
The request will be sent to the server and on the server side in the location controller. 
We need to handle this new request. So, add a controller method. 
 
Next step you need to retrieve all the locations? How can you do it?
 
How do send Locations to UI?
ModelMap modelMap -> It handles response from server or database to UI. 
 
How do retrieve all the locations?  
First set it into the modelMap so that in the jsp we will be able to access these locations from server or database. So, we are sending back response (Location) to UI. 


 

Step 1: - 
Next -> When user click on this link on UI- it comes to controller -> Below Method () displayLocation ()
Step 2: - Comes to the server
  
Step 3: - 
And retrieve the locations.
 
Step 4: - 
 
modelMap will send the locations to UI. 
And send them back to jsp
 
Next -: -
Now, we are going to generate the jsp page for “displayLocations”
 
After setting up jsp page then.
 
It means that User can under stand what is that,
Inside we are creating html table. 
 

Table heading is called <tr>

Next 
 
Example: - 
 
 
Add one more <tr>
This <tr> we are going to generate it dynamically using JSTL. You can use a java for loop by using JSP script lets but that’s not recommended. 
So, we will be using JSTL and iterate through the list that comes back and display everything. 



We will do that in two steps.
1.	Add maven dependency 
2.	Tag lib in the jsp page.

Go to -> pom.xml 
1. Add jstl dependency:
then add JSTL jar.
 
2.Tag lib in the jsp page.
 


Then we are creating simple dynamic way.
 
You can use the express language ($) and Show dynamically Location objects in displayLocation.jsp 
Below loop will display on UI page whatever the location objects in DB 
 

Now  you can  see the result :
 
Next -> One more important piece left in the flow. 
Add Record
 
  When use clicks on the Add Record link on the view all page it should be directed to the createLocation page so that. It can create more locations, so that the flow will continue. 
Go to ->  
 
This url -> showCreate will direct to controller class
 
Then again it is directing to createLocation.jsp page for adding the location. 
 




Delete the location:
 
 Delete link to our displayLocation.jsp.  When this link is clicked it should pass the Id of that row dynamically to our controller. 
Let’s handle that piece or that flow. 
Go to -> displayLocation.jsp  we will add a new column. 
 
 
Here,  we need to pass the id dynamically.  That is the tricky piece. 
 
 
 
 
It means that we pass the id dynamically. This is UI side.
Then come to Controller side.
We can create a new method delete in controller class
 
This URL is declared in displayLocation.jsp page like 
 
Then come back to controller -> 
 
T
The parameter should be mapped from the request parameter. 
Here, parameter is mapped from UI to backend.
From jsp  
To backend  
So, that we can write (@RequestParam (“id”) int id)
So, here, request parameter is from browser client click the location must delete. Example: - 
NY location has to delete. Then NY corresponding Id has passed from front end to UI and server or backend like controller class with parameter. So, this is called request parameter. 


 
This tells spring that it should retrieve this parameter from the URL parameters and the name of the parameter is id because we used id and we are retrieving it.   We are asking spring to retrieve it. 
Then next 
 
Full method below. 

When try to delete it 
 
The result would be below

 
Even you can observe on browser side,
 
It means that Id was deleted. You can observe on browser side id=1 was deleted. 
If you see the url ->  
This url goes to the controller, then spring will bind that id into this id here. We are invoking, we are setting that id onto a new location object that we are creating. We are invoking deleteLocation by passing in that location. 
 

When click on id=1 on the Delete Button -> It has to go the controller 
 


Next : editLocation.jsp  (Update)
Edit link, we should handle that in the controller and we should display a new page called editLocation.jsp
 
Go to -> displayLocation.jsp page
Update button is also very similar of delete button. 
 
“showUpdate”  this is uri. 
 
Go to controller class-
New method is update method. 
this method is not update location simply display update page. So, it is similar of 
 
Then create updateShow method
 
This editLocation.jps has the information of the   
 

When the user clicks the edit button. So, the id comes in. So, in our controller, you can retrieve the id very similar to deleteLocation. 
Whenever you are going to edit particular location then click edit button and go back to the 
displayLocation.jsp and url and come to controller and map the request and return editLocation.jsp page. Because we are editing the location. The editing location and creating the location both are same format.
Editing:
Edit -> editLocation.jsp -> database. 
Adding:
Add record -> createLocation.jsp -> database
 


Then go to editLocation.jsp page ->
 

and add jstl tag because dynamically displays. 
 
It is already there is createLocation.jsp page copy and paste over the editLocation.jsp page. 





36. Lecture: -
 

When the user clicks on the save button the form should be submitted. 
And on the server side: -
The spring container will take all the fields (like., id, code, name type) that come in the request.  It will convert into an object and we can retrieve that object inside our controller using a concept called ModelAttribute in spring. 
Explanation: - User entered all the fields id, code, name, and Type and submit ‘save’ button. Then 
(Spring container will take the (user) client request (this request contains id, code, name, and type) and convert into an object. 
That object retrieves (captured that request) inside of the controller. How do we retrieve it?
The concept is called ModelAttribute in spring.  (Here, Location is object) Take the object (Location) and save it the database.   
How do save it? 
We must have all these (here, following JPA) Bean, Service and Repository layers to save object, update object, get object, get all objects, and delete object in database.)


---  Go to createLocation.jsp page 
 
    So, <form action=”saveLoc” This is URI that we will be mapping to the controller method. 
 method =”post”>  because we are submitting a form and all its data will go through a POST method we are creating a location. 

Go back to the controller -> 
Write a one request mapping for “saveLoc” for POST method. 
 




This method returning jsp page. Ie., createLocation.jsp 
 
createLocation.jsp
 


 
@RequesgtMapping is the annotation. This @RequestMapping capture the request from frontend or UI. (“/”) -> it means called URI
URI = (“/”)
Here, what URI is placing ?  
 <form action=”saveLoc” This is URI.

  This method. saveLoction() has to perform the save Location object.  How to do ?
We have one concept of ModelAttribute in spring. This @ModelAttribute annotation will do this one. 
  When you are passing @ModelAttribute(“location”)
By default, spring will create a model object and set all the fields of Location class or entity (id, code, name, and type) that come into the request. That request exposes it out as a bean with following name. 
It will use class name Location. But first letter will be lower case. 
So, this is bean that Spring container will handover and we are taking it and we are asking it set that as a parameter, Location location.

 
So, we got model object and so,  the request will mapped to the model object and we got it in our controller method. 
( @ModelAttribute(“location”) in the braces the first letter must be small like “location”. Which object are you passing to database? Location object. )

The next step is to simply invoke the repository or the service.save. 
 
 
You can find above line   service.saveLocation(location); -> Why do we go service. saveLocation(location)?
Directly why do write -> repository. save(location)? 
Ans: - Directly we can save the object into database through repository layer. But here, we are not doing. The reason behind is that decoupling. Spring will recommend you that follow decoupling. It means that 
When you are following the process: Like:
First Entity Layer -> Controller -> public interface -> class ServiceImpl -> Interface Repository
Had Better to follow: When you follow this way. Wherever you want to improvise particular class or layer you can do it in easy way. 


Steps 1
 
Note: - Location is entity for database object. 
Step 2
 
 
Note: - Controller will capture client or user request and process to save the java object into the database.  LocationService (I)autowired with reference of service. This service reference is pointing 
LocationService.
Step 3
 
Note: - So, LocationService interface has many methods declared among that 
SaveLocation (Location location);







Step 4:
 
Note: - All non-implemented methods in LocationService to be imported in LocationServiceImpl class.
Here, we are implementing for those methods. 
Step 5
 
Note: - 1. JpaReposiotory is an interface of Jpa. This interface already has all methods (save (), findbyId (), delete () and so on) by default. 
2. By default all those methods are extended to our customized interface i.e.., LocationRepository.  
Next: -

 Whenever you create an object (Location) into the database. Then, send a success message back to the web browser.  We will send the id of the object that was just created or that was just created back to the user.  

Go to -> Controller class 
 
  
Above line meaning is that just save the location object into the database. But we need to make it confirm whether the object is created or not.  How can make it confirm?
Ans: - Two things. 
1. Return type (assign type) of the method (service. saveLocation(location).
2. The id of the object (Location -> id, code, name, and type) that was just created or that was just created and back to the user. By a message. 

1.	 
Explanation: - service. saveLocation(location): - location is what type Location type. So, 
you must assign the location object into Location type only. 
2.	 

Explanation: - The   + id will get it in back end only. 
But how can I get it this message to the UI or front end.
Ans: - The spring will allow us to do that using a concept called ModelMap. 
(1)	To handle the request, it is ModelAttribute.
(2)	To handle the response, it is ModelMap. 
 
	 
 

Notes: - ModelMap is passing as an argument and using this ModelMap object (ModelMap modelMap). 
Call the addAttribute () method and pass the msg as argument.

Next --- 
This ModelMap   can be accessed by jsp using spring expression language. 
 
 

Next
 
 
 
The first part of the View All requirement is to add.  View All button clicking on which the request will be sent to our controller and inside the controller we need to handle the incoming request. 

Go to -> createLocation.jsp

Use a link display. This is relative displayLocation. 
Add the hyperlink.     
This is View All so add that text there the user clicks on this, this relative URI will be used. 
The request will be sent to the server and on the server side in the location controller. 
We need to handle this new request. So, add a controller method. 
 
Next step you need to retrieve all the locations? How can you do it?
 
How do send Locations to UI?
ModelMap modelMap -> It handles response from server or database to UI. 
 
How do retrieve all the locations?  
First set it into the modelMap so that in the jsp we will be able to access these locations from server or database. So, we are sending back response (Location) to UI. 


 

Step 1: - 
Next -> When user click on this link on UI- it comes to controller -> Below Method () displayLocation ()
Step 2: - Comes to the server
  
Step 3: - 
And retrieve the locations.
 
Step 4: - 
 
modelMap will send the locations to UI. 
And send them back to jsp
 
Next -: -
Now, we are going to generate the jsp page for “displayLocations”
 
After setting up jsp page then.
 
It means that User can under stand what is that,
Inside we are creating html table. 
 

Table heading is called <tr>

Next 
 
Example: - 
 
 
Add one more <tr>
This <tr> we are going to generate it dynamically using JSTL. You can use a java for loop by using JSP script lets but that’s not recommended. 
So, we will be using JSTL and iterate through the list that comes back and display everything. 



We will do that in two steps.
1.	Add maven dependency 
2.	Tag lib in the jsp page.

Go to -> pom.xml 
1. Add jstl dependency:
then add JSTL jar.
 
2.Tag lib in the jsp page.
 


Then we are creating simple dynamic way.
 
You can use the express language ($) and Show dynamically Location objects in displayLocation.jsp 
Below loop will display on UI page whatever the location objects in DB 
 

Now  you can  see the result :
 
Next -> One more important piece left in the flow. 
Add Record
 
  When use clicks on the Add Record link on the view all page it should be directed to the createLocation page so that. It can create more locations, so that the flow will continue. 
Go to ->  
 
This url -> showCreate will direct to controller class
 
Then again it is directing to createLocation.jsp page for adding the location. 
 




Delete the location:
 
 Delete link to our displayLocation.jsp.  When this link is clicked it should pass the Id of that row dynamically to our controller. 
Let’s handle that piece or that flow. 
Go to -> displayLocation.jsp  we will add a new column. 
 
 
Here,  we need to pass the id dynamically.  That is the tricky piece. 
 
 
 
 
It means that we pass the id dynamically. This is UI side.
Then come to Controller side.
We can create a new method delete in controller class
 
This URL is declared in displayLocation.jsp page like 
 
Then come back to controller -> 
 
T
The parameter should be mapped from the request parameter. 
Here, parameter is mapped from UI to backend.
From jsp  
To backend  
So, that we can write (@RequestParam (“id”) int id)
So, here, request parameter is from browser client click the location must delete. Example: - 
NY location has to delete. Then NY corresponding Id has passed from front end to UI and server or backend like controller class with parameter. So, this is called request parameter. 


 
This tells spring that it should retrieve this parameter from the URL parameters and the name of the parameter is id because we used id and we are retrieving it.   We are asking spring to retrieve it. 
Then next 
 
Full method below. 

When try to delete it 
 
The result would be below

 
Even you can observe on browser side,
 
It means that Id was deleted. You can observe on browser side id=1 was deleted. 
If you see the url ->  
This url goes to the controller, then spring will bind that id into this id here. We are invoking, we are setting that id onto a new location object that we are creating. We are invoking deleteLocation by passing in that location. 
 

When click on id=1 on the Delete Button -> It has to go the controller 
 


Next : editLocation.jsp  (Update)
Edit link, we should handle that in the controller and we should display a new page called editLocation.jsp
 
Go to -> displayLocation.jsp page
Update button is also very similar of delete button. 
 
“showUpdate”  this is uri. 
 
Go to controller class-
New method is update method. 
this method is not update location simply display update page. So, it is similar of 
 
Then create updateShow method
 
This editLocation.jps has the information of the   
 

When the user clicks the edit button. So, the id comes in. So, in our controller, you can retrieve the id very similar to deleteLocation. 
Whenever you are going to edit particular location then click edit button and go back to the 
displayLocation.jsp and url and come to controller and map the request and return editLocation.jsp page. Because we are editing the location. The editing location and creating the location both are same format.
Editing:
Edit -> editLocation.jsp -> database. 
Adding:
Add record -> createLocation.jsp -> database
 


Then go to editLocation.jsp page ->
 

and add jstl tag because dynamically displays. 
 
It is already there is createLocation.jsp page copy and paste over the editLocation.jsp page. 





36. Lecture: -
 

When the user clicks on the save button the form should be submitted. 
And on the server side: -
The spring container will take all the fields (like., id, code, name type) that come in the request.  It will convert into an object and we can retrieve that object inside our controller using a concept called ModelAttribute in spring. 
Explanation: - User entered all the fields id, code, name, and Type and submit ‘save’ button. Then 
(Spring container will take the (user) client request (this request contains id, code, name, and type) and convert into an object. 
That object retrieves (captured that request) inside of the controller. How do we retrieve it?
The concept is called ModelAttribute in spring.  (Here, Location is object) Take the object (Location) and save it the database.   
How do save it? 
We must have all these (here, following JPA) Bean, Service and Repository layers to save object, update object, get object, get all objects, and delete object in database.)


---  Go to createLocation.jsp page 
 
    So, <form action=”saveLoc” This is URI that we will be mapping to the controller method. 
 method =”post”>  because we are submitting a form and all its data will go through a POST method we are creating a location. 

Go back to the controller -> 
Write a one request mapping for “saveLoc” for POST method. 
 




This method returning jsp page. Ie., createLocation.jsp 
 
createLocation.jsp
 


 
@RequesgtMapping is the annotation. This @RequestMapping capture the request from frontend or UI. (“/”) -> it means called URI
URI = (“/”)
Here, what URI is placing ?  
 <form action=”saveLoc” This is URI.

  This method. saveLoction() has to perform the save Location object.  How to do ?
We have one concept of ModelAttribute in spring. This @ModelAttribute annotation will do this one. 
  When you are passing @ModelAttribute(“location”)
By default, spring will create a model object and set all the fields of Location class or entity (id, code, name, and type) that come into the request. That request exposes it out as a bean with following name. 
It will use class name Location. But first letter will be lower case. 
So, this is bean that Spring container will handover and we are taking it and we are asking it set that as a parameter, Location location.

 
So, we got model object and so,  the request will mapped to the model object and we got it in our controller method. 
( @ModelAttribute(“location”) in the braces the first letter must be small like “location”. Which object are you passing to database? Location object. )

The next step is to simply invoke the repository or the service.save. 
 
 
You can find above line   service.saveLocation(location); -> Why do we go service. saveLocation(location)?
Directly why do write -> repository. save(location)? 
Ans: - Directly we can save the object into database through repository layer. But here, we are not doing. The reason behind is that decoupling. Spring will recommend you that follow decoupling. It means that 
When you are following the process: Like:
First Entity Layer -> Controller -> public interface -> class ServiceImpl -> Interface Repository
Had Better to follow: When you follow this way. Wherever you want to improvise particular class or layer you can do it in easy way. 


Steps 1
 
Note: - Location is entity for database object. 
Step 2
 
 
Note: - Controller will capture client or user request and process to save the java object into the database.  LocationService (I)autowired with reference of service. This service reference is pointing 
LocationService.
Step 3
 
Note: - So, LocationService interface has many methods declared among that 
SaveLocation (Location location);







Step 4:
 
Note: - All non-implemented methods in LocationService to be imported in LocationServiceImpl class.
Here, we are implementing for those methods. 
Step 5
 
Note: - 1. JpaReposiotory is an interface of Jpa. This interface already has all methods (save (), findbyId (), delete () and so on) by default. 
2. By default all those methods are extended to our customized interface i.e.., LocationRepository.  
Next: -

 Whenever you create an object (Location) into the database. Then, send a success message back to the web browser.  We will send the id of the object that was just created or that was just created back to the user.  

Go to -> Controller class 
 
  
Above line meaning is that just save the location object into the database. But we need to make it confirm whether the object is created or not.  How can make it confirm?
Ans: - Two things. 
1. Return type (assign type) of the method (service. saveLocation(location).
2. The id of the object (Location -> id, code, name, and type) that was just created or that was just created and back to the user. By a message. 

1.	 
Explanation: - service. saveLocation(location): - location is what type Location type. So, 
you must assign the location object into Location type only. 
2.	 

Explanation: - The   + id will get it in back end only. 
But how can I get it this message to the UI or front end.
Ans: - The spring will allow us to do that using a concept called ModelMap. 
(1)	To handle the request, it is ModelAttribute.
(2)	To handle the response, it is ModelMap. 
 
	 
 

Notes: - ModelMap is passing as an argument and using this ModelMap object (ModelMap modelMap). 
Call the addAttribute () method and pass the msg as argument.

Next --- 
This ModelMap   can be accessed by jsp using spring expression language. 
 
 

Next
 
 
 
The first part of the View All requirement is to add.  View All button clicking on which the request will be sent to our controller and inside the controller we need to handle the incoming request. 

Go to -> createLocation.jsp

Use a link display. This is relative displayLocation. 
Add the hyperlink.     
This is View All so add that text there the user clicks on this, this relative URI will be used. 
The request will be sent to the server and on the server side in the location controller. 
We need to handle this new request. So, add a controller method. 
 
Next step you need to retrieve all the locations? How can you do it?
 
How do send Locations to UI?
ModelMap modelMap -> It handles response from server or database to UI. 
 
How do retrieve all the locations?  
First set it into the modelMap so that in the jsp we will be able to access these locations from server or database. So, we are sending back response (Location) to UI. 


 

Step 1: - 
Next -> When user click on this link on UI- it comes to controller -> Below Method () displayLocation ()
Step 2: - Comes to the server
  
Step 3: - 
And retrieve the locations.
 
Step 4: - 
 
modelMap will send the locations to UI. 
And send them back to jsp
 
Next -: -
Now, we are going to generate the jsp page for “displayLocations”
 
After setting up jsp page then.
 
It means that User can under stand what is that,
Inside we are creating html table. 
 

Table heading is called <tr>

Next 
 
Example: - 
 
 
Add one more <tr>
This <tr> we are going to generate it dynamically using JSTL. You can use a java for loop by using JSP script lets but that’s not recommended. 
So, we will be using JSTL and iterate through the list that comes back and display everything. 



We will do that in two steps.
1.	Add maven dependency 
2.	Tag lib in the jsp page.

Go to -> pom.xml 
1. Add jstl dependency:
then add JSTL jar.
 
2.Tag lib in the jsp page.
 


Then we are creating simple dynamic way.
 
You can use the express language ($) and Show dynamically Location objects in displayLocation.jsp 
Below loop will display on UI page whatever the location objects in DB 
 

Now  you can  see the result :
 
Next -> One more important piece left in the flow. 
Add Record
 
  When use clicks on the Add Record link on the view all page it should be directed to the createLocation page so that. It can create more locations, so that the flow will continue. 
Go to ->  
 
This url -> showCreate will direct to controller class
 
Then again it is directing to createLocation.jsp page for adding the location. 
 




Delete the location:
 
 Delete link to our displayLocation.jsp.  When this link is clicked it should pass the Id of that row dynamically to our controller. 
Let’s handle that piece or that flow. 
Go to -> displayLocation.jsp  we will add a new column. 
 
 
Here,  we need to pass the id dynamically.  That is the tricky piece. 
 
 
 
 
It means that we pass the id dynamically. This is UI side.
Then come to Controller side.
We can create a new method delete in controller class
 
This URL is declared in displayLocation.jsp page like 
 
Then come back to controller -> 
 
T
The parameter should be mapped from the request parameter. 
Here, parameter is mapped from UI to backend.
From jsp  
To backend  
So, that we can write (@RequestParam (“id”) int id)
So, here, request parameter is from browser client click the location must delete. Example: - 
NY location has to delete. Then NY corresponding Id has passed from front end to UI and server or backend like controller class with parameter. So, this is called request parameter. 


 
This tells spring that it should retrieve this parameter from the URL parameters and the name of the parameter is id because we used id and we are retrieving it.   We are asking spring to retrieve it. 
Then next 
 
Full method below. 

When try to delete it 
 
The result would be below

 
Even you can observe on browser side,
 
It means that Id was deleted. You can observe on browser side id=1 was deleted. 
If you see the url ->  
This url goes to the controller, then spring will bind that id into this id here. We are invoking, we are setting that id onto a new location object that we are creating. We are invoking deleteLocation by passing in that location. 
 

When click on id=1 on the Delete Button -> It has to go the controller 
 


Next : editLocation.jsp  (Update)
Edit link, we should handle that in the controller and we should display a new page called editLocation.jsp
 
Go to -> displayLocation.jsp page
Update button is also very similar of delete button. 
 
“showUpdate”  this is uri. 
 
Go to controller class-
New method is update method. 
this method is not update location simply display update page. So, it is similar of 
 
Then create updateShow method
 
This editLocation.jps has the information of the   
 

When the user clicks the edit button. So, the id comes in. So, in our controller, you can retrieve the id very similar to deleteLocation. 
Whenever you are going to edit particular location then click edit button and go back to the 
displayLocation.jsp and url and come to controller and map the request and return editLocation.jsp page. Because we are editing the location. The editing location and creating the location both are same format.
Editing:
Edit -> editLocation.jsp -> database. 
Adding:
Add record -> createLocation.jsp -> database
 


Then go to editLocation.jsp page ->
 

and add jstl tag because dynamically displays. 
 
It is already there is createLocation.jsp page copy and paste over the editLocation.jsp page. 





36. Lecture: -
 

When the user clicks on the save button the form should be submitted. 
And on the server side: -
The spring container will take all the fields (like., id, code, name type) that come in the request.  It will convert into an object and we can retrieve that object inside our controller using a concept called ModelAttribute in spring. 
Explanation: - User entered all the fields id, code, name, and Type and submit ‘save’ button. Then 
(Spring container will take the (user) client request (this request contains id, code, name, and type) and convert into an object. 
That object retrieves (captured that request) inside of the controller. How do we retrieve it?
The concept is called ModelAttribute in spring.  (Here, Location is object) Take the object (Location) and save it the database.   
How do save it? 
We must have all these (here, following JPA) Bean, Service and Repository layers to save object, update object, get object, get all objects, and delete object in database.)


---  Go to createLocation.jsp page 
 
    So, <form action=”saveLoc” This is URI that we will be mapping to the controller method. 
 method =”post”>  because we are submitting a form and all its data will go through a POST method we are creating a location. 

Go back to the controller -> 
Write a one request mapping for “saveLoc” for POST method. 
 




This method returning jsp page. Ie., createLocation.jsp 
 
createLocation.jsp
 


 
@RequesgtMapping is the annotation. This @RequestMapping capture the request from frontend or UI. (“/”) -> it means called URI
URI = (“/”)
Here, what URI is placing ?  
 <form action=”saveLoc” This is URI.

  This method. saveLoction() has to perform the save Location object.  How to do ?
We have one concept of ModelAttribute in spring. This @ModelAttribute annotation will do this one. 
  When you are passing @ModelAttribute(“location”)
By default, spring will create a model object and set all the fields of Location class or entity (id, code, name, and type) that come into the request. That request exposes it out as a bean with following name. 
It will use class name Location. But first letter will be lower case. 
So, this is bean that Spring container will handover and we are taking it and we are asking it set that as a parameter, Location location.

 
So, we got model object and so,  the request will mapped to the model object and we got it in our controller method. 
( @ModelAttribute(“location”) in the braces the first letter must be small like “location”. Which object are you passing to database? Location object. )

The next step is to simply invoke the repository or the service.save. 
 
 
You can find above line   service.saveLocation(location); -> Why do we go service. saveLocation(location)?
Directly why do write -> repository. save(location)? 
Ans: - Directly we can save the object into database through repository layer. But here, we are not doing. The reason behind is that decoupling. Spring will recommend you that follow decoupling. It means that 
When you are following the process: Like:
First Entity Layer -> Controller -> public interface -> class ServiceImpl -> Interface Repository
Had Better to follow: When you follow this way. Wherever you want to improvise particular class or layer you can do it in easy way. 


Steps 1
 
Note: - Location is entity for database object. 
Step 2
 
 
Note: - Controller will capture client or user request and process to save the java object into the database.  LocationService (I)autowired with reference of service. This service reference is pointing 
LocationService.
Step 3
 
Note: - So, LocationService interface has many methods declared among that 
SaveLocation (Location location);







Step 4:
 
Note: - All non-implemented methods in LocationService to be imported in LocationServiceImpl class.
Here, we are implementing for those methods. 
Step 5
 
Note: - 1. JpaReposiotory is an interface of Jpa. This interface already has all methods (save (), findbyId (), delete () and so on) by default. 
2. By default all those methods are extended to our customized interface i.e.., LocationRepository.  
Next: -

 Whenever you create an object (Location) into the database. Then, send a success message back to the web browser.  We will send the id of the object that was just created or that was just created back to the user.  

Go to -> Controller class 
 
  
Above line meaning is that just save the location object into the database. But we need to make it confirm whether the object is created or not.  How can make it confirm?
Ans: - Two things. 
1. Return type (assign type) of the method (service. saveLocation(location).
2. The id of the object (Location -> id, code, name, and type) that was just created or that was just created and back to the user. By a message. 

1.	 
Explanation: - service. saveLocation(location): - location is what type Location type. So, 
you must assign the location object into Location type only. 
2.	 

Explanation: - The   + id will get it in back end only. 
But how can I get it this message to the UI or front end.
Ans: - The spring will allow us to do that using a concept called ModelMap. 
(1)	To handle the request, it is ModelAttribute.
(2)	To handle the response, it is ModelMap. 
 
	 
 

Notes: - ModelMap is passing as an argument and using this ModelMap object (ModelMap modelMap). 
Call the addAttribute () method and pass the msg as argument.

Next --- 
This ModelMap   can be accessed by jsp using spring expression language. 
 
 

Next
 
 
 
The first part of the View All requirement is to add.  View All button clicking on which the request will be sent to our controller and inside the controller we need to handle the incoming request. 

Go to -> createLocation.jsp

Use a link display. This is relative displayLocation. 
Add the hyperlink.     
This is View All so add that text there the user clicks on this, this relative URI will be used. 
The request will be sent to the server and on the server side in the location controller. 
We need to handle this new request. So, add a controller method. 
 
Next step you need to retrieve all the locations? How can you do it?
 
How do send Locations to UI?
ModelMap modelMap -> It handles response from server or database to UI. 
 
How do retrieve all the locations?  
First set it into the modelMap so that in the jsp we will be able to access these locations from server or database. So, we are sending back response (Location) to UI. 


 

Step 1: - 
Next -> When user click on this link on UI- it comes to controller -> Below Method () displayLocation ()
Step 2: - Comes to the server
  
Step 3: - 
And retrieve the locations.
 
Step 4: - 
 
modelMap will send the locations to UI. 
And send them back to jsp
 
Next -: -
Now, we are going to generate the jsp page for “displayLocations”
 
After setting up jsp page then.
 
It means that User can under stand what is that,
Inside we are creating html table. 
 

Table heading is called <tr>

Next 
 
Example: - 
 
 
Add one more <tr>
This <tr> we are going to generate it dynamically using JSTL. You can use a java for loop by using JSP script lets but that’s not recommended. 
So, we will be using JSTL and iterate through the list that comes back and display everything. 



We will do that in two steps.
1.	Add maven dependency 
2.	Tag lib in the jsp page.

Go to -> pom.xml 
1. Add jstl dependency:
then add JSTL jar.
 
2.Tag lib in the jsp page.
 


Then we are creating simple dynamic way.
 
You can use the express language ($) and Show dynamically Location objects in displayLocation.jsp 
Below loop will display on UI page whatever the location objects in DB 
 

Now  you can  see the result :
 
Next -> One more important piece left in the flow. 
Add Record
 
  When use clicks on the Add Record link on the view all page it should be directed to the createLocation page so that. It can create more locations, so that the flow will continue. 
Go to ->  
 
This url -> showCreate will direct to controller class
 
Then again it is directing to createLocation.jsp page for adding the location. 
 




Delete the location:
 
 Delete link to our displayLocation.jsp.  When this link is clicked it should pass the Id of that row dynamically to our controller. 
Let’s handle that piece or that flow. 
Go to -> displayLocation.jsp  we will add a new column. 
 
 
Here,  we need to pass the id dynamically.  That is the tricky piece. 
 
 
 
 
It means that we pass the id dynamically. This is UI side.
Then come to Controller side.
We can create a new method delete in controller class
 
This URL is declared in displayLocation.jsp page like 
 
Then come back to controller -> 
 
T
The parameter should be mapped from the request parameter. 
Here, parameter is mapped from UI to backend.
From jsp  
To backend  
So, that we can write (@RequestParam (“id”) int id)
So, here, request parameter is from browser client click the location must delete. Example: - 
NY location has to delete. Then NY corresponding Id has passed from front end to UI and server or backend like controller class with parameter. So, this is called request parameter. 


 
This tells spring that it should retrieve this parameter from the URL parameters and the name of the parameter is id because we used id and we are retrieving it.   We are asking spring to retrieve it. 
Then next 
 
Full method below. 

When try to delete it 
 
The result would be below

 
Even you can observe on browser side,
 
It means that Id was deleted. You can observe on browser side id=1 was deleted. 
If you see the url ->  
This url goes to the controller, then spring will bind that id into this id here. We are invoking, we are setting that id onto a new location object that we are creating. We are invoking deleteLocation by passing in that location. 
 

When click on id=1 on the Delete Button -> It has to go the controller 
 


Next : editLocation.jsp  (Update)
Edit link, we should handle that in the controller and we should display a new page called editLocation.jsp
 
Go to -> displayLocation.jsp page
Update button is also very similar of delete button. 
 
“showUpdate”  this is uri. 
 
Go to controller class-
New method is update method. 
this method is not update location simply display update page. So, it is similar of 
 
Then create updateShow method
 
This editLocation.jps has the information of the   
 

When the user clicks the edit button. So, the id comes in. So, in our controller, you can retrieve the id very similar to deleteLocation. 
Whenever you are going to edit particular location then click edit button and go back to the 
displayLocation.jsp and url and come to controller and map the request and return editLocation.jsp page. Because we are editing the location. The editing location and creating the location both are same format.
Editing:
Edit -> editLocation.jsp -> database. 
Adding:
Add record -> createLocation.jsp -> database
 


Then go to editLocation.jsp page ->
 

and add jstl tag because dynamically displays. 
 
It is already there is createLocation.jsp page copy and paste over the editLocation.jsp page. 






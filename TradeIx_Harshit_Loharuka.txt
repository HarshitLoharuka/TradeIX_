import requests
from urllib.request import urlopen
from requests.auth import HTTPDigestAuth
import json
import jsonpath

##Task 1 to add new entry to employee table

#creating class to add new set of data using POST command
class Employee_create:
    name = ""
    salary = ""
    age = ""
    image = ""
    id1 = ""
    
    #Declaring function to create record
    def createRecord(self,name,salary,age,image):
        #Hitting url use to create data in API
        create_url = "http://dummy.restapiexample.com/api/v1/create"
        #converting my data into JSON format
        data_json = json.dumps({"name":name,"salary":salary,"age":age,"image":image})
        headers = {'Content-type': 'application/json'}
        #Reccording Response after hitting end point URL with input data
        response_create = requests.post(create_url, data=data_json, headers=headers)
        #Recording new ID which got genertaed
        id1 = jsonpath.jsonpath(response_create.json(),'id') 
        #Verifying whetehr data got sucessfully created or not
        assert response_create.status_code ==200, "Invalid Insert Request"
       
        #Returning the output values
        return name,salary,age,image,id1     
		
# Recording the input parameters in different variables
input_name = "Harshit"
input_age = "25"
input_salary = "45000"
input_image = "image"

#Calling the Employee class and creating it's object
out_create = Employee_create()

#Recording the output which got returned by Employee class
name,salary,age,image,id1 = out_create.createRecord(input_name,input_salary,input_age,input_image)

#Printing the output
print("employee_name: "+name)
print("employee_age: "+age)
print("employee_salary: "+salary)
print("profile_image: "+image)

#--------------------------------------------------------------------------------------------------------------------------------


##Task 2 to verify the data got sucessfully updated using GET command

#creating class to add new set of data using POST command
class Employee_verify:
    temp_id = ""
    def verifyRecord(self,ver_id):
        #Hitting url use to fetch data in API for ID which got created in Task 1
        get_url = "http://dummy.restapiexample.com/api/v1/employee/" + ver_id
        # Recording the response using GET command
        response_verify = requests.get(get_url)
        #Loading the output data in a variable to access all data from dictionary
        json_response = json.loads(response_verify.text)
        #Temposrarily storing name, salary, age in a local variable
        n = json_response.get('employee_name')
        s = json_response.get('employee_salary')
        a = json_response.get('employee_age')
        
        #Using assertion to verify data got sucessfully updated
        assert n == input_name, 'Incorrect Name'
        assert s == input_salary, 'Incorrect Salary'
        assert a == input_age, 'Incorrect Age'
        
        #Printing Response Code
        print(response_verify.status_code)

#Recording ID which need to be verified
id_verify = id1[0]

#Calling the Employee class and creating it's object
out_verify = Employee_verify()

#Calling the function using object and passing id which need to be verified
out_verify.verifyRecord(id_verify)

#--------------------------------------------------------------------------------------------------------------------------------


##Task 3 to update employee salary with new data using PUT

#Creating class to Update employee salary
class Employee_update:
    name = input_name
    new_salary = ""
    age = input_age
    image = input_image
    
    #Creating updateRecord function for updating the data
    def updateSalary(self,new_salary):
        #Hitting update URL with id which got generated above while creating
        update_url = "http://dummy.restapiexample.com/api/v1/update/" + id1[0]
        #Converting my new data into JSON format
        data_json = json.dumps({"name":name,"salary":new_salary,"age":age,"image":image})
        headers = {'Content-type': 'application/json'}
        #Recording the response using new data by PUT command
        response_update = requests.put(update_url, data=data_json, headers=headers)
        #Verifying whether data got updated or not
        assert response_update.status_code ==200, "Invalid Update Request"
        
        #Printing Response Code
        print(response_update.status_code)
        
        #Returning new set of data
        return name,new_salary,age,image
		
#Storing new salary in a variable
new_salary = "3450"

#Creating object for the class Update_salary
new_out = Employee_update()

#Storing new sets of data in multiple variables
name,n_salary,age,image = new_out.updateSalary(new_salary)

#Printing the output with updated data
print("employee_name: "+name)
print("employee_age: "+age)
print("employee_salary: "+n_salary)
print("profile_image: "+image)

#--------------------------------------------------------------------------------------------------------------------------------

##Task 4 to delet the data which got generated using DELETE

#Creating class to Delete employee salary
class Employee_delete:
    temp_id = ""
    
    def DeleteRecord(self,ver_id):
        #Hitting delete URL with id which got generated above while creating
        delete_url = "http://dummy.restapiexample.com/api/v1/delete/" + ver_id
        
        #Recording the response by delete command
        response_del = requests.delete(delete_url)
        
        #Verifying whether data got deleted or not
        assert response_del.status_code ==200, "Invalid Delete Request"
        
        #Printing Response Code
        print(response_del.status_code)
		
#Recording ID which need to be verified
id_verify = id1[0]

#Calling the Employee class and creating it's object
out_delete = Employee_delete()

#Calling the function using object and passing id which need to be verified
out_delete.DeleteRecord(id_verify)
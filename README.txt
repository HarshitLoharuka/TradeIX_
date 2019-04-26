API Used: http://dummy.restapiexample.com/

1. Create and return a new Employee with:
a. Employee_name
b. Employee_age
c. Employee_salary
d. Profile_image (dummy url can be used)

Solution:

Created Employee_create with function createRecord

Input Parameters: Employee_Name, Employee_Salary, Employee_Age, Employee_Image
Output: Employee_Name, Employee_Salary, Employee_Age, Employee_Image, Employee_ID


2. Verify the employee was created with the correct data.

Solution:

Created Employee_verify with function verifyRecord

Input Parameters: Employee_ID
Output: NA (Data is getting verified inside class using assertion).


3. Update this employee’s salary, verify update and return record.

Solution:

Created Employee_update with function updateSalary

Input Parameters: Employee_Salary
Output: Employee_Name, Employee_Salary, Employee_Age, Employee_Image

4. Delete the employee and demonstrate employee now deleted.

Solution:

Created Employee_delete with function DeleteRecord

Input Parameters: Employee_ID
Output: NA (Data is getting deleted inside class).
# TestNGDetails
This repository contains codes for TestNG practice of Selenium tutorial
TestNG - a testing framework, building block similar to jUnit
used in Unittesting by Developers. Easy and User Friendly.
Execute Test cases in a batch. 
Group test cases and run in a batch. 
Reports
Data Driven tests. 

Installation of TestNG. .............................
Window -> Market Place -> or
testng.org/doc/download.html
Window -> Preferences - check if you have testNG
Help -> Install New SOftware -> Paste the URL - Add 
Select and Next
Accept License -> Finish
----------------------------------------------------------
File - New Project Framework -> Sample Class - new class 
Annotations - Dont Check Public static void main 
Create a Package for testngFiles

package testngFiles;

package testngProject;

import org.testng.annotations.AfterMethod;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class Annotations {
	
	@BeforeMethod
	public void UserID()
	{
		System.out.println("User ID Generated");
	}
	@BeforeTest
	public void Cookies()
	{
		System.out.println("Delete Them All Before");
	}
	@AfterTest
	public void Cookiesclose()
	{
		System.out.println("Delete Cookies After");
		//close out browsers
	}
	@AfterMethod
	public void LogoutUserID()
	{
		System.out.println("User ID Logged Out");
	}
	@Test
	public void OpeningBrowser(){
	System.out.println("test");
	}
	
	@Test
	public void BookFlights() {
		System.out.println("Clicking to book");
	}
	
	
	
}
----------------------------------------------------------
package testngProject;

import org.testng.annotations.AfterSuite;
import org.testng.annotations.BeforeSuite;

public class Annotation2 {

	@BeforeSuite
	public void installsoftware()
	{
		//This executes First before class
		System.out.println("Before Suite");
	}
	@AfterSuite
	public void uninstallsoftware()
	{
		System.out.println("After Suite");
	}
}
----------------------------------------------------------
package testngProject;

import org.testng.annotations.Test;

public class DependencyAnnotation {
	
	@Test
	public void OpeningBrowser(){
	System.out.println("test");
	}
	
	@Test(dependsOnMethods={"OpeningBrowser"},alwaysRun=true)
	public void BookFlights() {
		System.out.println("Clicking to book");
	}
	@Test(timeOut =5000)
	public void timeRel()
	{
		System.out.println("New Case");
	}
	
	@Test(enabled=false)// to exclde from execution
	public void payment()
	{
		//This Opens the Browser
		System.out.println("Payment Perform");
	}
}
------------------------------------------------------------
Working with XML Files 
---------------------------------------------------------
<?xml version="1.0" encoding="UTF-8"?>
<suite name ="Auto Test">
	<test name = "First Test Case">
	<Classes>
		<class name="testngProject.Annotation2"/>
		<class name="testngProject.Annotations"/>
	</Classes>
	</test>
</suite>
................................................
<?xml version="1.0" encoding="UTF-8"?>
<suite name ="Auto Test">
	<test name = "First Test Case">
	<packages>
		<package name="testngProject"/>
	</packages>
	</test>
</suite>
.....................................................
<?xml version="1.0" encoding="UTF-8"?>
<suite name ="Auto Test">
	<test name = "First Test Case">
	<packages>
		<package name="test.*"/>
	</packages>
	</test>
</suite>

========================================================
Priority in Test Case Execution

@Test (groups={"Priority1"}) //attribute assigned as Priority1

@Test (groups={"Priority2"})

create XML File accordingly - write before the class
<groups>
	<run>
	<include name ="Priority1"/>
	</run>
</groups>
========================================================
Data Driven Test cases

	@DataProvider
	public Object[][] getData()
	{
		//i - number of times test case runs
		//j - number of parameters for one go
		
		Object[][] data=new Object[3][3];
		data[0][0]="abc";
		data[0][1]="xyz";
		data[0][2]="2983";
		data[1][0]="abca";
		data[1][1]="xyzz";
		data[1][2]="2984";
		data[2][0]="abcd";
		data[2][1]="xyzd";
		data[2][2]="2982";
		return data;
	}

	@Test(dataProvider="getData")
	public void UserID2(String username, String Password, String id )
	{
		System.out.println("Tested");
		System.out.println(username);
		System.out.println(Password);
		System.out.println(id);
	}
------------------------------------------------------------
Parameterization : 

#######on xml file add before Classes : 
<parameter name ="adminUserid" value ="abcd"/>

#########on java file#############
@Parameters({"adminUserid"})
public void BookFlight(String Userid)
{
System.out.pringln(Userid);
}

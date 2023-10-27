# Manisha-sRepo-PF


I have implemented Page object model framework where I have created BasePO, BaseTest, Dashboard test classes to create tests.
Also, I have added Utilities folders which contains constants, DriverManager, JavaHelpers, SeleniumHelpers, WaitHelper classes to manage our tests smoothly.
Test Class:
This will contain all the test which we have for dashboard along with log file so any non-technical person can also understand.
It can contain number of test cases.
BaseTest & BasePO:
BaseTest will contain annotation methods of selenium like BeforeMethod, AfterMethod for the test so we can perform certain action before or after test execution.
BasePO will contain WebDriver class object & SeleniumHelpers class object for the methods which we manipulate in class for better used.

DashboardPO:
Basically, PO means Page Object, which mean dashboard will contains all the elements which we see on dashboard page UI in form of locators.
So, I have used mostly XPaths and created methods for perform a particular action in dashboard page.

Utilities Folder:
 
It contains below classes:
Constants Class:
It contains all the hard coded text which are used in project.
DriverManager Class:
This class will return driver for specific browser which we want for now I have set it up for chrome browser.
Also, this contains teardown method which close the chrome browser.
SeleniumHelpers:
This will contain all the method which we used to interact with web browser like EnterText, GetText, click on button, TakeScreenshot, navigate to page, JavaScriptClick etc.,
WaitHelpers:
It will contain explicit wait methods which we used while interacting with web element for dynamic wait to avoid unnecessary failures.
Scenario 1: Check the total displayed number of results for category Villas with a price range of less than 30,000 AED / yearly

Steps:
1.	Navigate to URL.
Using this method selenium.navigateToPage(“URL”); URL launch Into the chrome browser
2.	Select the Property 'Villa'.
Using this method selenium.javascriptClickOn(propertyTypeDropDown); Automation software click on the property type dropdown element

Using this method selenium.javascriptClickOn(propertyTypeDropDown); automation software click on the propertytype(Villa) element


3.	Select the maximum price 30,000.
Using this method selenium.javascriptClickOn(priceDropdown); Automation software click on the price dropdown element
Using this method selenium.enterText(priceInput, priceRange, true);
automation software enter the pricerange(30000) in the price input element

4.	Click on the search button.
Using this method selenium.click(searchButton);
Automation software click on the search button element

5.	Get the property count.
Using this method String count = selenium.getText(searchResultCount); 
Automation software get the value of the count element 
String[] abc = count.split(" "); return abc[0];
Above logic define that only numeric value is return from the string 
For Ex: Value is ‘4 Property’ then it returns 4


6.	Get all the property card values.
Using this method int cnt = driver.findElements(By.xpath("//ul[@aria-label='Properties']/li")).size(); Automation software get the the element size (Total Property which display in UI)

Assertions:
1.	Verify that the displayed number of results matches the property count.
Its verify the Step 5 and Step 6 value if value is different then its give the error
2.	Verify that all property values are less than or equal to 30,000 AED / yearly.
List<WebElement> priceList = driver.findElements(By.xpath("//ul[@aria-label='Properties']/li//p[@data-testid='property-card-price']"));
List<String> price3 = priceList.stream()
        .map(WebElement::getText)
        .map(price -> price.replaceAll("[^0-9]", ""))
        .filter(price -> Integer.parseInt(price) <= 30000)
        .collect(Collectors.toList());

return (priceList.size() == price3.size());

Above method store the all property value which is less than 30000, and verify that total property list and total stored size is same or not
If size is different then it gives the error


Scenario 2: Check the property price, description, location, size of the commercial office property

Steps:
1.	Navigate to URL.
Using this method selenium.navigateToPage(“URL”); URL launch Into the chrome browser

2.	Click on the "Show commercial properties" checkbox and click on the search icon.
selenium.click(showCommercialPropertyCheckBox);

Automation software click on the show commercial property element
Using this method selenium.click(searchButton);
Automation software click on the search button element

3.	Click on the "Office" category.
selenium.click(selectOfficesOption);
Automation software click on the office element

4.	Get the search result count.

Using this method String count = selenium.getText(searchResultCount); 
Automation software get the value of the count element 
String[] abc = count.split(" "); return abc[0];
Above logic define that only numeric value is return from the string 
For Ex: Value is ‘4 Property’ then it return 4

Assertions:
1.	Verify that the displayed number of results matches the property card list.
Its verify the Step 4  value and total number of card value if value is different than its give the error


2.	Verify that the first property has a description, location, price, and space area present.
Assert.assertTrue(dashboard.isCardDescriptionPresent(), "Card Price is not present");
Assert.assertTrue(dashboard.isCardSpaceAreaPresent(), "Card Size is not present");
Assert.assertTrue(dashboard.isCardPricePresent(), "Card Price is not present");
Assert.assertTrue(dashboard.isCardLocationPresent(), "Card Location is not present");

First assertion method dashboard.isCardDescriptionPresent( ) is return the value true or false if the value is false then give the error "Card Price is not present" 


Scenario 3: Search the property by location

Steps:
1.	Navigate to URL.
Using this method selenium.navigateToPage(“URL”); URL launch Into the chrome browser

2.	Search for the property 'Bahrain Bay' and select from the list.
selenium.click(searchPropertyInput);
selenium.enterText(searchPropertyInput, location, false);

Automation software firstly click on the search property element and then enter the location('Bahrain Bay') value
3.	Click on the search button.
Using this method selenium.click(searchButton);
Automation software click on the search button element

4.	Click on the first property card.
Using this method selenium.javascriptClickOn(firstPropertyCard);
Automation Software click on the first property card


Assertions:
1.	Verify that the "Available from" date is not empty for the first property card.
Using this method Assert.assertNotNull(dashboard.GetAvailableFromPropertyValue(), "available From Date is empty!");
Automation software verify the dashboard.GetAvailableFromPropertyValue(), method it returns the property value 
If value is empty then it gives the error "available From Date is empty!");



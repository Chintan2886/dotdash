// depending on the IDE/environment you use, your project files can reside here.

package Test;

import java.util.concurrent.TimeUnit;
import org.junit.*;
import static org.junit.Assert.*;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.Select;


public class dotdash {
  private WebDriver driver;
  private String baseUrl;
  private StringBuffer verificationErrors = new StringBuffer();

  
  @Before
  public void setUp() throws Exception {
	System.setProperty("webdriver.chrome.driver", "/Users/chintan-mac/Documents/Selenium/workspace/QA Automation/chromedriver");//"<PATH TO LOCATION>\\chromedriver.exe"); 
	driver = new ChromeDriver();
    baseUrl = "http://localhost/dotdash-project/index.php";
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
    driver.manage().window().maximize();
  }

  @Test
  public void testAssetLibrayforRegression() throws Exception {
    driver.get(baseUrl);
    
    //Creation of Category
    //Enter Category text
    driver.findElement(By.xpath("//input[@name='categorydata']")).sendKeys("Category Test");
    //Select from Color drop down
    new Select(driver.findElement(By.xpath("//select[@name='colour']"))).selectByVisibleText("Green");
    //Click on add button
  	driver.findElement(By.xpath("//input[@value='Add category']")).click();
  	
  	
  	
    // Creation and verifying of ToDo line item 
    //Enter ToDo line item
  	driver.findElement(By.xpath("//input[@name='data']")).sendKeys("TODO line item Test5");
    //Select from Color drop down
    new Select(driver.findElement(By.xpath("//select[@name='category']"))).selectByVisibleText("Category Test");
    //Select from Date drop down
    new Select(driver.findElement(By.xpath("//select[@name='due_day']"))).selectByVisibleText("2");
    new Select(driver.findElement(By.xpath("//select[@name='due_month']"))).selectByVisibleText("Mar");
    new Select(driver.findElement(By.xpath("//select[@name='due_year']"))).selectByVisibleText("2019");
    //Click on add button
  	driver.findElement(By.xpath("//input[@value='Add']")).click();
  	// Thread.sleep(3000);
  	
  	//Verifying of ToDo line item created
  	boolean ToDoListCreationStatus = driver.findElement(By.xpath("//div[@id='todos-content' and contains(.,'TODO line item Test5')]")).isDisplayed();
  	if (ToDoListCreationStatus == true)
  	{
  		System.out.println("ToDo line item Created successfully");
  	}
  	else
  	{
  		System.out.println("Unable to found newly created ToDo line item");	
  	}
    
  	
  	// Verifying Complete button functionality 
  	driver.findElement(By.xpath("//input[@type='checkbox']")).click();
  	driver.findElement(By.xpath("//input[@value='Complete']")).click();
    Thread.sleep(1000);
 
    
    // Verifying Remove button functionality 				
    driver.findElement(By.xpath("//input[@type='checkbox']")).click();
    driver.findElement(By.xpath("//input[@value='Remove']")).click();
    Thread.sleep(1000);
    
    // Verifying Toggle all check box
    driver.findElement(By.xpath("//input[@value='on']")).click();
    
  //Close browser
    driver.close();
  
  }

  @After
  public void tearDown() throws Exception {
    driver.quit();
    String verificationErrorString = verificationErrors.toString();
    if (!"".equals(verificationErrorString)) {
      fail(verificationErrorString);
    }
  }

}

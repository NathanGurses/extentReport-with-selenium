# extentReport with selenium.
It provides rich HTML reports that can be customized to get a graphical representation of each test step.
You can easily track test cases run in a single test suite.
Integration with multiple frameworks TestNG and JUnit become easy.
It helps you determine the time it takes to run the test.
You can add important screenshots, tags, devices, or other relevant information to create a descriptive report that you can fully control.

import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.ExtentTest;
import com.aventstack.extentreports.reporter.ExtentHtmlReporter;
import deneme.utilities.TestBase;
import io.github.bonigarcia.wdm.WebDriverManager;
import org.junit.Assert;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

import java.text.SimpleDateFormat;
import java.time.Duration;
import java.util.Date;

public class ExtentReports extends TestBase {

    protected ExtentReports extentReports;
    protected ExtentHtmlReporter extentHtmlReporter;
    protected ExtentTest extentTest;
    @Test
    public void extentReportsTest(){

//        REPORT PATH
        String currentTime = new SimpleDateFormat("yyyyMMddhhmmss").format(new Date());
        String path = System.getProperty("user.dir")+"/test-output/reports/"+currentTime+"html_report.html";
//        creating HTML report in the path
        extentHtmlReporter = new ExtentHtmlReporter(path);

//        creating extent reports object for generating the Entire reports with configuration
        extentReports =new ExtentReports();

        extentReports.setSystemInfo("Test Environment", "regression");
        extentReports.setSystemInfo("Application", "******");
        extentReports.setSystemInfo("Browser", "Chrome");
        extentReports.setSystemInfo("Team", "Eagles");
        extentReports.setSystemInfo("SQA", "MURAT GURSES");

//        adding more custom info
        extentHtmlReporter.config().setReportName("***** home page");
        extentHtmlReporter.config().setDocumentTitle("****** extent reports");
//        ******************

//        DONE WITH CONFIGURATION
        extentReports.attachReporter(extentHtmlReporter);

//        REPORT IS DONE. NOW CREATING EXTENT TEST TO LOG INFO IN THE TEST CASE
//        Creating extent test
        extentTest = extentReports.createTest("My Extent Reporter", "Regression Test Report");

//        DONE WITH REPORT SET UP. FROM NOW ON USE extentTest object to log information.

        extentTest.pass("PASS");
        extentTest.info("INFO");
        extentTest.fail("FAIL");
        extentTest.skip("SKIP");
        extentTest.warning("WARNING");


        extentTest.pass("Going to the application URL");
        driver.get("https://*******.com");

        extentTest.pass("Searching QA");
        driver.findElement(By.xpath("//*****[@*****='*****']")).sendKeys("QA"+ Keys.ENTER);
        
        Note; i do not recommended copy xpah for find element 
        extentTest.pass("Verify URL has QA keyword");
        Assert.assertTrue(driver.getCurrentUrl().contains("QA"));

        extentTest.pass("Closing the browser");
        driver.quit();



//        Generating
        extentReports.flush();

    }
}

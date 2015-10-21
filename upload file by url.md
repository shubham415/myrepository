# myrepository
repository for rtmedia

import java.util.regex.Pattern;
import java.util.concurrent.TimeUnit;
import org.junit.*;
import static org.junit.Assert.*;
import static org.hamcrest.CoreMatchers.*;
import org.openqa.selenium.*;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.Select;

public class UrlUpload {
  private WebDriver driver;
  private String baseUrl;
  private boolean acceptNextAlert = true;
  private StringBuffer verificationErrors = new StringBuffer();

  @Before
  public void setUp() throws Exception {
    driver = new FirefoxDriver();
    baseUrl = "google.com";
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
  }

  @Test
  public void testUrlUpload() throws Exception {
    driver.get("http://demo.rtcamp.com/rtmedia/members/shubham-pal/");
    assertEquals("shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.cssSelector("div.bp-login-widget-user-link > a[title=\"shubham pal\"]")).click();
    assertEquals("shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("user-media")).click();
    assertEquals("shubham pal | Media | Profile | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("rtm_show_upload_ui")).click();
    driver.findElement(By.cssSelector("button.bulk-edit-cancel")).click();
    driver.findElement(By.cssSelector("li.rtm-url-import-tab")).click();
    driver.findElement(By.id("rtmedia_url_upload_input")).clear();
    driver.findElement(By.id("rtmedia_url_upload_input")).sendKeys("http://i.forbesimg.com/media/lists/companies/apple_416x416.jpg");
    driver.findElement(By.cssSelector("input.start-media-upload")).click();
  }

  @After
  public void tearDown() throws Exception {
    driver.quit();
    String verificationErrorString = verificationErrors.toString();
    if (!"".equals(verificationErrorString)) {
      fail(verificationErrorString);
    }
  }

  private boolean isElementPresent(By by) {
    try {
      driver.findElement(by);
      return true;
    } catch (NoSuchElementException e) {
      return false;
    }
  }

  private boolean isAlertPresent() {
    try {
      driver.switchTo().alert();
      return true;
    } catch (NoAlertPresentException e) {
      return false;
    }
  }

  private String closeAlertAndGetItsText() {
    try {
      Alert alert = driver.switchTo().alert();
      String alertText = alert.getText();
      if (acceptNextAlert) {
        alert.accept();
      } else {
        alert.dismiss();
      }
      return alertText;
    } finally {
      acceptNextAlert = true;
    }
  }
}

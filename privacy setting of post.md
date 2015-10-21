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

public class PrivacySetting {
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
  public void testPrivacySetting() throws Exception {
    driver.get("http://demo.rtcamp.com/rtmedia/");
    assertEquals("rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("rtmedia-add-media-button-post-update")).click();
    driver.findElement(By.id("html5_1a25lmh6j23n1t93st8utbat83")).click();
    driver.findElement(By.id("html5_1a25lmh6j23n1t93st8utbat83")).clear();
    driver.findElement(By.id("html5_1a25lmh6j23n1t93st8utbat83")).sendKeys("");
    new Select(driver.findElement(By.id("rtSelectPrivacy"))).selectByVisibleText("Private");
    driver.findElement(By.id("whats-new")).clear();
    driver.findElement(By.id("whats-new")).sendKeys("hiiii");
    driver.findElement(By.id("aw-whats-new-submit")).click();
    driver.findElement(By.cssSelector("#wp-admin-bar-logout > a.ab-item")).click();
    assertEquals("rtMedia Demo Site", driver.getTitle());
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

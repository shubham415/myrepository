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

public class UpdateProfile {
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
  public void testUpdateProfile() throws Exception {
    driver.get("http://demo.rtcamp.com/rtmedia/members/shubham-pal/profile/edit/group/1/");
    assertEquals("Edit | Profile | shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.linkText("shubham pal")).click();
    assertEquals("shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("user-xprofile")).click();
    assertEquals("Profile | shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("change-avatar")).click();
    assertEquals("Change Profile Photo | Profile | shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("bp-browse-button")).click();
    driver.findElement(By.id("html5_1a25lsnmaugv1li71jm71skt1cu75")).clear();
    driver.findElement(By.id("html5_1a25lsnmaugv1li71jm71skt1cu75")).sendKeys("");
    driver.findElement(By.linkText("Crop Image")).click();
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

# myrepository
repository for rtmedia
package com.example.tests;

import java.util.regex.Pattern;
import java.util.concurrent.TimeUnit;
import org.junit.*;
import static org.junit.Assert.*;
import static org.hamcrest.CoreMatchers.*;
import org.openqa.selenium.*;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.Select;

public class UploadDifferentMedia {
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
  public void testUploadDifferentMedia() throws Exception {
    driver.get("http://demo.rtcamp.com/rtmedia/members/shubham-pal/profile/change-avatar/");
    assertEquals("Change Profile Photo | Profile | shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.linkText("shubham pal")).click();
    assertEquals("shubham pal | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("user-media")).click();
    assertEquals("shubham pal | Media | Profile | rtMedia Demo Site", driver.getTitle());
    driver.findElement(By.id("rtm_show_upload_ui")).click();
    driver.findElement(By.cssSelector("button.bulk-edit-cancel")).click();
    driver.findElement(By.id("rtMedia-upload-button")).click();
    driver.findElement(By.id("html5_1a25m2a8sian1at310n25s4l6s3")).clear();
    driver.findElement(By.id("html5_1a25m2a8sian1at310n25s4l6s3")).sendKeys("");
    new Select(driver.findElement(By.id("rtSelectPrivacy"))).selectByVisibleText("Logged in Users");
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

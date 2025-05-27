# testuse1
<build>
        <plugins>
            <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-resources-plugin</artifactId>
                    <version>3.2.0</version>
                <executions>
                    <execution>
                        <phase>prepare-package</phase>
                        <goals>
                            <goal>copy-resources</goal>
                        </goals>
                        <configuration>
                            <outputDirectory>${project.basedir}/docs</outputDirectory>  <!--- deploy to /docs folder -->
                            <resources>
                            <resource>
                                <directory>src/main/resources</directory>
                                <includes>
                                    <include>**/*</include>  <!---Copy all files in src/main/resources -->
                                </includes>
                            </resource>
                            </resources>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
         </plugins>
 </build>


<distributionManagement>
        <repository>
            <id>local-repo</id>
            <url>file:///C:\Users\gopik\OneDrive\Desktop\prg2test</url>
        </repository>
    </distributionManagement>

    <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.2.0</version>
                <configuration>
                    <archive>
                        <manifestEntries>
                            <Main-Class>org.example.Main </Main-Class>
                        </manifestEntries>
                    </archive>
                </configuration>
 </plugin>


 <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-site-plugin</artifactId>
                    <version>3.12.1</version>
 </plugin>

package org.test;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;
import org.testng.annotations.AfterTest;

import static org.testng.Assert.assertTrue;

public class WebPageTest{
    private static WebDriver driver;

    @BeforeTest
    public void openBrowser() throws InterruptedException{
        driver = new ChromeDriver();
        driver.manage().window().maximize();
        Thread.sleep(2000);
        driver.get(" https://gopi-5.github.io/Experiment2/");
    }

    @Test
    public void titleValidationTest(){
        String actualTitle = driver.getTitle();
        System.out.println("Page Title: " + actualTitle);
        String expectedTitle = "My Portfolio";
        Assert.assertEquals(actualTitle, expectedTitle, "Page title doesn't match!");
        Assert.assertTrue(actualTitle.contains("Portfolio"), "Title should contain 'Portfolio'");
    }

    @AfterTest
    public void closeBrowser() throws InterruptedException {
        Thread.sleep(2000);
        driver.quit();
    }
}

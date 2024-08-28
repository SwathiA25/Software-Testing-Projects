package Assignments;

import java.io.IOException;
import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import DataDrivenTesting.ExcelUtils;

public class Assignment7 {

	public static void main(String[] args) throws IOException, InterruptedException {
		
		WebDriver driver=new ChromeDriver();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
		driver.get("https://www.cit.com/cit-bank/resources/calculators/certificate-of-deposit-calculator");
		driver.manage().window().maximize();
		
		String filepath=System.getProperty("user.dir")+"\\testdata\\caldata.xlsx";
		
		int rows=ExcelUtils.getRowCount(filepath, "Sheet1");

		for(int r=1;r<=rows;r++)
		{
			//read data from excel
			String amt=ExcelUtils.getCellData(filepath, "Sheet1", r,0);
			String len=ExcelUtils.getCellData(filepath, "Sheet1", r,1);
			String roi=ExcelUtils.getCellData(filepath, "Sheet1", r,2);
			String comp=ExcelUtils.getCellData(filepath, "Sheet1", r,3);
			String exp_total=ExcelUtils.getCellData(filepath, "Sheet1", r,4);
			
			//pass the above value into the application
			WebElement amtele = driver.findElement(By.xpath("//input[@id='mat-input-0']"));
			amtele.clear();
			amtele.sendKeys(amt);
			
			WebElement lenele = driver.findElement(By.xpath("//input[@id='mat-input-1']"));
			lenele.clear();
			lenele.sendKeys(len);
			
			WebElement roiele = driver.findElement(By.xpath("//input[@id='mat-input-2']"));
			roiele.clear();
			roiele.sendKeys(roi);
			
			driver.findElement(By.xpath("//div[@class='mat-form-field-infix ng-tns-c102-3']")).click();
			//cmpele.click();
			Thread.sleep(2000);
			driver.findElement(By.xpath("//span[@class='mat-option-text'][normalize-space()='"+comp+"']")).click();
			
			
			driver.findElement(By.xpath("//button[@type='submit']//div[@class='mdc-button__ripple']")).click();
			
			//validation
			String act_total = driver.findElement(By.xpath("//span[@id='displayTotalValue']")).getText();
			//System.out.println(exp_total+" "+act_total);
			if(exp_total.equals(act_total))
			{
				System.out.println("Test Passed");
				ExcelUtils.setCellData(filepath, "Sheet1", r, 6, "Passed");
				ExcelUtils.fillGreenColor(filepath, "Sheet1", r, 6);
			}
			else
			{
				System.out.println("Test Failed");
				ExcelUtils.setCellData(filepath, "Sheet1", r, 6, "Failed");
				ExcelUtils.fillRedColor(filepath, "Sheet1", r, 6);
			}
			Thread.sleep(3000);
		}
		driver.quit();
	}

}

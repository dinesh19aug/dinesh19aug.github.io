---
title: Read / Write Excel file in Java using Apache POI
author: Dinesh
type: post
date: 2014-04-18T16:27:58+00:00
url: /2014/04/18/apache-poi-tutorial-reading-writing-excel-files-java/
featured_image: /wp-content/uploads/2014/04/creating-a-chainable-select-for-spreadsheets-with-apache-POI.jpg
dsq_thread_id:
  - 5441656492
  - 5441656492
categories:
  - Tech Notes

---
About a year or two ago I was working with finance team where they wanted to pull the credit card transactions for all the customer using various combinations. Ex &#8211;

&#8211; Get the credit card txns for today or certain date.

&#8211; Get the txns for customer who used Mastercard or Visa.

However they wanted this application to generate a Excel file and save it on their local machine so that they could prepare reports for our CEO. I used a Apache POI project to create jar files. This tutorial will walk you through the process of reading and writing excel sheet. So let&#8217;s see &#8211; How to read and write excel files in Java?

<span style="color: #ff0000;"><strong>Brief History on Apache POI</strong></span>

Apache POI is a powerful Java library to work with different Microsoft Office file formats such as Excel, Power point, Visio, MS Word etc. The name POI was originally an acronym for **Poor Obfuscation Implementation**, referring humorously to the file formats that seemed deliberately obfuscated, but poorly, since they were successfully reverse-engineered.  In short, you can read / write MS Excel files using Java. In addition, you can read/write MS Word and MS PowerPoint files using Java. Apache POI is your Java Excel solution .

Apache POI can be used to create both old ( 2003-2008) and new( 2010 &#8211; newer) format. I think the newer jar file to create XLSX document is out of BETA phase now. Back when I used this POI it was still in Beta format.

So let&#8217;s see what does it entails to read /write Excel files in Java.

I am will be using Maven and IntelliJ to create my project, however you are welcome to use <a href="https://www.eclipse.org/downloads/" target="_blank">Eclipse </a>or <a title="netbeans" href="https://netbeans.org/" target="_blank">Netbeans</a>.

**Apache POI dependencies**

There are two different maven dependencies one for creating an older version of excel &#8211; XLS format and other for creating new version of Excel &#8211; XLSX format. I am listing both the dependencies here.

> <dependencies>
  
> <!&#8211; For Excel 2007 &#8211;>
  
> <dependency>
  
> <groupId>org.apache.poi</groupId>
  
> <artifactId>poi</artifactId>
  
> <version>3.9</version>
  
> </dependency>
  
> <dependency>
  
> <groupId>org.apache.poi</groupId>
  
> <artifactId>poi-ooxml</artifactId>
  
> <version>3.9</version>
  
> </dependency>
  
> </dependencies>

Create a new module in IntelliJ.

<img class="alignnone size-full wp-image-709" src="http://javahabit.com/wp-content/uploads/2014/04/img_535146b33cf4f1.png" alt="" />

Add the dependency in your pom.xml

<img class="alignnone size-full wp-image-710" src="http://www.javahabit.com/wp-content/uploads/2014/04/img_535146cc7b62e.png" alt="" />

**PAUSE & THINK: KEY POI CLASSES**

Before we go ahead here&#8217;s quick primer on 3  key classes in POI.

  1. HSSF &#8211; Java implementation of the Excel ’97(-2007) file format. e.g. <a style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;" title="HSSFWorkbook" href="http://poi.apache.org/apidocs/org/apache/poi/hssf/usermodel/HSSFWorkbook.html" target="_blank" rel="external nofollow">HSSFWorkbook</a>, <a style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;" title="HSSFSheet" href="http://poi.apache.org/apidocs/org/apache/poi/hssf/usermodel/HSSFSheet.html" target="_blank" rel="external nofollow">HSSFSheet</a>.
  2. XSSF &#8211;  Java implementation of the Excel 2007 OOXML (.xlsx) file format. e.g. <a style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;" title="XSSFWorkbook" href="http://poi.apache.org/apidocs/org/apache/poi/xssf/usermodel/XSSFWorkbook.html" target="_blank" rel="external nofollow">XSSFWorkbook</a>, <a style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;" title="XSSFSheet" href="http://poi.apache.org/apidocs/org/apache/poi/xssf/usermodel/XSSFSheet.html" target="_blank" rel="external nofollow">XSSFSheet</a>.
  3. SXSSF &#8211; Used when very large spreadsheets have to be produced, and heap space is limited. e.g. <a style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;" title="SXSSFWorkbook" href="http://poi.apache.org/apidocs/org/apache/poi/xssf/streaming/SXSSFWorkbook.html" target="_blank" rel="external nofollow">SXSSFWorkbook</a>, <a style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;" title="SXSSFSheet" href="http://poi.apache.org/apidocs/org/apache/poi/xssf/streaming/SXSSFSheet.html" target="_blank" rel="external nofollow">SXSSFSheet</a>.

<span style="font-size: 16px;">There are other wide range of classes as well which can be used to manipulate the Excel sheet. Ex &#8211; </span><span style="font-size: 16px;"> </span><a style="font-size: 16px;" title="BuiltinFormats" href="http://poi.apache.org/apidocs/org/apache/poi/ss/usermodel/BuiltinFormats.html" target="_blank" rel="external nofollow">BuiltinFormats</a><span style="font-size: 16px;">, <a title="ConditionalFormattingRule" href="http://poi.apache.org/apidocs/org/apache/poi/ss/usermodel/ConditionalFormattingRule.html" target="_blank" rel="external nofollow">ConditionalFormattingRule</a>,</span><a style="font-size: 16px;" title="ComparisonOperator" href="http://poi.apache.org/apidocs/org/apache/poi/ss/usermodel/ComparisonOperator.html" target="_blank" rel="external nofollow">ComparisonOperator</a><span style="font-size: 16px;">,<a title="CellStyle" href="http://poi.apache.org/apidocs/org/apache/poi/ss/usermodel/CellStyle.html" target="_blank" rel="external nofollow">CellStyle</a>, </span><a style="font-size: 16px;" title="FontFormatting" href="http://poi.apache.org/apidocs/org/apache/poi/ss/usermodel/FontFormatting.html" target="_blank" rel="external nofollow">FontFormatting</a><span style="font-size: 16px;">, </span><a style="font-size: 16px;" title="IndexedColors" href="http://poi.apache.org/apidocs/org/apache/poi/ss/usermodel/IndexedColors.html" target="_blank" rel="external nofollow">IndexedColors</a><span style="font-size: 16px;">, </span><a style="font-size: 16px;" title="PatternFormatting" href="http://poi.apache.org/apidocs/org/apache/poi/hssf/record/cf/PatternFormatting.html" target="_blank" rel="external nofollow">PatternFormatting</a><span style="font-size: 16px;">, </span><a style="font-size: 16px;" title="SheetConditionalFormatting" href="http://poi.apache.org/apidocs/org/apache/poi/ss/usermodel/SheetConditionalFormatting.html" target="_blank" rel="external nofollow">SheetConditionalFormatting</a>. These used for formatting the sheet and formula evaluation.<span style="font-size: 16px;"><br /> </span>

**HOW TO CREATE A NEW EXCEL SHEET**

This involves the following steps.

<img class="alignnone size-full wp-image-711" src="http://www.javahabit.com/wp-content/uploads/2014/04/img_53514874f1362.png" alt="" />

So go ahead and create a new file called NewExcel.java

<pre>package com.dinesh;
import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;
import java.util.TreeMap;

/**
 * Created by darora on 4/18/14.
 */
public class NewExcel {
    public static void main(String[] args) {
        //Create a new Workbook
        XSSFWorkbook workbook = new XSSFWorkbook();

        //Create a blank sheet
        XSSFSheet sheet = workbook.createSheet("Student data");

        //Create the data for the excel sheet
        Map&lt;string, object[]=""&gt; data = new TreeMap&lt;string, object[]=""&gt;();
        data.put("1", new Object[] {"ID", "FIRSTNAME", "LASTNAME"});
        data.put("2", new Object[] {1, "Randy", "Maven"});
        data.put("3", new Object[] {2, "Raymond", "Smith"});
        data.put("4", new Object[] {3, "Dinesh", "Arora"});
        data.put("5", new Object[] {4, "Barbra", "Klien"});

        //Iterate over data and write it to the sheet
        Set keyset = data.keySet();
        int rownum = 0;
        for (String key : keyset)
        {
            Row row = sheet.createRow(rownum++);
            Object [] objArr = data.get(key);
            int cellnum = 0;
            for (Object obj : objArr)
            {
                Cell cell = row.createCell(cellnum++);
                if(obj instanceof String)
                    cell.setCellValue((String)obj);
                else if(obj instanceof Integer)
                    cell.setCellValue((Integer)obj);
            }
        }
        //Save the excel sheet
        try{
            FileOutputStream out = new FileOutputStream(new File("c:\Dinesh\javahabitExcelDemo.xlsx"));
            workbook.write(out);
            out.close();
            System.out.println("javahabitExcelDemo.xlsx Successfully created");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}</pre>

**OUTPUT**

<img class="alignnone size-full wp-image-723" src="http://www.javahabit.com/wp-content/uploads/2014/04/img_53514e60ec9eb.png" alt="" />

&nbsp;

**HOW TO READ A NEW EXCEL SHEET**

So now that we have written an excel sheet. let&#8217;s try to read it back.

The steps involved are

<img class="alignnone size-full wp-image-724" src="http://www.javahabit.com/wp-content/uploads/2014/04/img_53514eb219cb7.png" alt="" />

&nbsp;

<pre>package com.dinesh;

import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Iterator;

/**
 * Created by darora on 4/18/14.
 */
public class ReadExcel {
    //Create Workbook instance from excel sheet
    public static void main(String[] args) {
        try {
            //Get the Excel File
            FileInputStream file = new FileInputStream(new File("c:\Dinesh\javahabitExcelDemo.xlsx"));
            XSSFWorkbook workbook = new XSSFWorkbook(file);

            //Get the Desired sheet
            XSSFSheet sheet = workbook.getSheetAt(0);

            //Increment over rows
            for (Row row : sheet) {
                //Iterate and get the cells from the row
                Iterator cellIterator = row.cellIterator();
                // Loop till you read all the data
                while (cellIterator.hasNext()) {
                    Cell cell = cellIterator.next();

                    switch (cell.getCellType()) {
                        case Cell.CELL_TYPE_NUMERIC:
                            System.out.print(cell.getNumericCellValue() + "t");
                            break;
                        case Cell.CELL_TYPE_STRING:
                            System.out.print(cell.getStringCellValue() + "t");
                            break;
                    }
                }
                System.out.println("");
            }
            file.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}</pre>

**OUTPUT**

<img class="alignnone size-full wp-image-725" src="http://www.javahabit.com/wp-content/uploads/2014/04/img_53514ff0c1a46.png" alt="" />

&nbsp;

### **Using formulas in excel sheet**

When working on excel sheets, we sometimes have to create cells which use formulas to calculate their values.  Apache POI has supports methods for adding formula to cells and evaluating the already present formula in the cells. Neat!!

So Let&#8217;s see an example on setting a formula cells in the excel sheet.

In this code we will try to calculate the Simple interest. Formula &#8211; Principal \* Interest \* Time.

&nbsp;

<pre>package com.dinesh;

import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

/**
 * Created by darora on 4/18/14.
 */
public class CalculateFormula {
    public static void main(String[] args)
    {
        //Create the workbook
        XSSFWorkbook workbook = new XSSFWorkbook();
        //Create the sheet
        XSSFSheet sheet = workbook.createSheet("Calculate Simple Interest");
        //Create Wor Headers
        Row header = sheet.createRow(0);
        header.createCell(0).setCellValue("Principal");
        header.createCell(1).setCellValue("Interest");
        header.createCell(2).setCellValue("Time");
        header.createCell(3).setCellValue("OUTPUT (P * r * t)");

        //Create the Rows
        Row dataRow = sheet.createRow(1);
        dataRow.createCell(0).setCellValue(1000d);
        dataRow.createCell(1).setCellValue(12.00);
        dataRow.createCell(2).setCellValue(6d);
        dataRow.createCell(3).setCellFormula("A2*B2*C2");

        //Save the File
        try {
            FileOutputStream out =  new FileOutputStream(new File("c:\Dinesh\javahabitformulaDemo.xlsx"));
            workbook.write(out);
            out.close();
            System.out.println("Excel File with formla is created!");

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}</pre>

**OUTPUT**

<img class="alignnone size-full wp-image-726" src="http://www.javahabit.com/wp-content/uploads/2014/04/img_5351516d00b65.png" alt="" />

&nbsp;

So experiment your way with this jar file and do post your comments and suggestions on topics you had like to see in my future posts.

&nbsp;

~ Ciao

&#8211;
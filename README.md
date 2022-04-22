# SessionTrackingManagementApp
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Session tracking management </title>
</head>
<body>
<h1><center>Session tracking management</center></h1>
<center>
<form action="s1url" method="get" style="color:red;">
<table>
<tr><td> Name</td>
<td><input type="text" name="pname"></td>
</tr>

<tr><td>Age</td>
<td><input type="text" name="page"></td>
</tr>
<tr><td>MaritalStates</td>
<td><input type="checkbox" values="married" name='ms'></td>
</tr>
<tr>
<td><input type="submit" values="continue"></td>
</tr>
</table>
</form>
</center>


</body>
</html>
package com.nt.Servlet;
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
public class Servlet1 extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
	//create variable 
		PrintWriter pw=null;
		String name=null;
		String age=null;
		String mgstates=null;
		//General seting 
		pw=res.getWriter();
		res.setContentType("text/html");
		//read data from form component 
		name=req.getParameter("pname");
		age=req.getParameter("page");
		mgstates=req.getParameter("ms");
		if(mgstates==null)
			mgstates="single";
		//Generate second form Dynamically here 
		if(mgstates.equals("married")) {
			pw.println("<form action='s2url' method='post' >");
			pw.println("<b>Spouse Name <input type='text' name='st1'><br>");
			pw.println("<b>NO of children <input type='text' name='st2'><br>");
			pw.println("<b><input type='submit'  values='submit'>");
			pw.println("</form >");
		}//end if block
		else {
			pw.println("<form action='s2url' method='post' >");
			pw.println("<b>when do you want to marry <input type='text' name='st1'><br>");
			pw.println("<b>why do you want to marry <input type='text' name='st2'><br>");
			pw.println("<b><input type='submit'  values='submit'>");
			pw.println("</form >");
		}//end else block
		//close stream 
		pw.close();
	}//end of the method 
	public  void doPost(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
		// TODO Auto-generated method stub
		doGet(req, res);
	}//end of the method 

}//end of the class
package com.nt.Servlet;
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
public class Servlet2 extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
	//create variable 
		PrintWriter pw=null;
		//General setign 
		pw=res.getWriter();
		res.setContentType("text/html");
		//read first And second data 
		pw.println("<br>First Form data  is ");
		pw.println("<br>Name is"+((ServletRequest) res).getParameter("pname"));
		pw.println("<br>Age is"+((ServletRequest) res).getParameter("page"));
		pw.println("<br>Marital States is"+((ServletRequest) res).getParameter("ms"));
		//second form data 
		pw.println("<br> Second from data  is "+((ServletRequest) res).getParameter("st1"));
		pw.println("<br>  "+((ServletRequest) res).getParameter("st2"));
		//close stream 
		pw.close();
	}//end of the method
	public void doPost(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
		// TODO Auto-generated method stub
		doGet(req, res);
	}//end of the method 
}//end of the class

  
  
  <?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>SessionTrackingManagement</display-name>
  <welcome-file-list>
    <welcome-file>Detail.html</welcome-file>
  </welcome-file-list>
  <servlet>
  <servlet-name>ABC</servlet-name>
  <servlet-class>com.nt.Servlet.Servlet1</servlet-class>
  </servlet>
  <servlet-mapping>
<servlet-name>ABC</servlet-name>
<url-pattern>/s1url</url-pattern>
</servlet-mapping>

<servlet>
  <servlet-name>XYZ</servlet-name>
  <servlet-class>com.nt.Servlet.Servlet2</servlet-class>
  </servlet>
  <servlet-mapping>
<servlet-name>XYZ</servlet-name>
<url-pattern>/s2url</url-pattern>
</servlet-mapping>
  
</web-app>

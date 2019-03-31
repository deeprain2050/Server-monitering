# Server-monitering
It can moniter 2 servers in one web app.
<%@ page import="java.sql.*" %>
<HTML>
<HEAD>
<TITLE>comptel-mediation &copy</TITLE>

</HEAD>
<BODY>

<%
Connection connection1 = null;
String pass="Passw0rd";
String sql= "select network,monitering,maintainance from om";
try
{
Class.forName("oracle.jdbc.driver.OracleDriver");
connection1 = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:rizu","SYSTEM",pass);
Statement statement = connection1.createStatement();
ResultSet resultSet = statement.executeQuery(sql);
%>
<table align="left" border="0" cellspacing="3" width="350" bgcolor="#FFFF99">
<tr bgcolor="#FFCC33"><th align=center>---BSCS---</th></tr>
<tr><td align=center><table border="0" cellspacing="3" width=150 >
<%

while (resultSet.next())
{
String x = resultSet.getString("network");
String z = resultSet.getString("monitering");
String y = resultSet.getString("maintainance");

out.print("<tr bgcolor=\"#CCCCCC\"><th bgcolor=\"#FFCC33\" align=left>"+x+"</th><td bgcolor=\"#66CC00\">"+z+"</td><td bgcolor=\"#66CC00\">"+y+"</td></tr>");
}

}

catch(Exception exception)
{
out.println("Exception : " + exception.getMessage() + "");
}

finally
{
if(connection1 != null)
{
try
{
connection1.close();
}
catch (Exception ignored)
{
// ignore
}

}
}


%>

<%
Connection connection2 = null;
try
{
Class.forName("oracle.jdbc.driver.OracleDriver");
connection2 = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:rizu","SYSTEM",pass);
Statement statement = connection2.createStatement();
ResultSet resultSet = statement.executeQuery("select network,monitering,maintainance from om");
%>
<table align="left" border="0" cellspacing="3" width="350" bgcolor="#FFFF99">
<tr bgcolor="#FFCC33"><th align=center>---OM---</th></tr>
<tr><td align=center><table border="0" cellspacing="3" width=150 >
<%

while (resultSet.next())
{
String x = resultSet.getString("network");
String z = resultSet.getString("monitering");
String y = resultSet.getString("maintainance");

out.print("<tr bgcolor=\"#CCCCCC\"><th bgcolor=\"#FFCC33\" align=left>"+x+"</th><td bgcolor=\"#66CC00\">"+z+"</td><td bgcolor=\"#66CC00\">"+y+"</td></tr>");
}

}

catch(Exception exception)
{
out.println("Exception : " + exception.getMessage() + "");
}

finally
{
if(connection2 != null)
{
try
{
connection2.close();
}
catch (Exception ignored)
{
// ignore
}

}
}


%>


</BODY>
</HTML>

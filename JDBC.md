
```


package com.trivium.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

import com.trivium.bean.Employee;

public class EmployeeDAOImpl implements EmployeeDAO {

	Connection connection = null;
	PreparedStatement statement = null;

	void init() {
		try {
            // Loading Driver class
			getClass().forName("com.mysql.cj.jdbc.Driver");

		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

    // Creating the connection object
		try {
			connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/triviumdb", "root", "12345");
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

	@Override
	public boolean addEmployee(Employee emp) {

		init();
		int result = 0;
		
		try {
            // Creating a new connection statement
			statement = connection.prepareStatement("insert into Employee values(?,?,?);");

			statement.setInt(1, emp.getEno());
			statement.setString(2, emp.getName());
			statement.setFloat(3, emp.getBp());

    // executing the statement with query
			result = statement.executeUpdate();

			return result > 0 ? true : false;

		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

		return false;
	}

	@Override
	public boolean updateEmployee(int eno,String name,float bp) {
		init();
		try {
			statement = connection.prepareStatement("update Employee set name = ? , bp = ? where eno = ?");
			statement.setString(1, name);
			statement.setFloat(2, bp);
			statement.setInt(3, eno);
			
			int result = statement.executeUpdate();

			return result > 0 ? true : false;
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		return false;
	}

}



```
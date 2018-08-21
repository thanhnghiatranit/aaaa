package fs.dao;

import java.sql.Connection;
import java.sql.Date;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;

import fs.common.JDBC_Connection;

public class MSTCUSTOMER_DAO {

	public ArrayList<MSTCUSTOMER> getListCustomer() {
		Connection conn = JDBC_Connection.getConnection();
		String sql = "SELECT * FROM MSTCUSTOMER";
		ArrayList list = new ArrayList();
		try {
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			ResultSet rs = ps.executeQuery();
			while (rs.next()) {
				MSTCUSTOMER mstcustomer = new MSTCUSTOMER() {
				};
				mstcustomer.setS_customerID(rs.getString("CUSTOMER_ID"));
				mstcustomer.setS_customerName(rs.getString("CUSTOMER_NAME"));
				mstcustomer.setS_sex(rs.getString("SEX"));
				mstcustomer.setS_birthday(rs.getDate("BIRTHDAY"));
				mstcustomer.setS_address(rs.getString("ADDRESS"));
				list.add(mstcustomer);
			}
			conn.close();
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return list;
	}

	public ArrayList<MSTCUSTOMER> getListCustomerByID(String id) {
		Connection conn = JDBC_Connection.getConnection();
		String sql = "SELECT * FROM MSTCUSTOMER WHERE CUSTOMER_ID = ?";
		ArrayList list = new ArrayList();
		try {
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			//
			ps.setString(1, id);
			ResultSet rs = ps.executeQuery();
			while (rs.next()) {
				MSTCUSTOMER mstcustomer = new MSTCUSTOMER() {
				};
				mstcustomer.setS_customerID(rs.getString("CUSTOMER_ID"));
				mstcustomer.setS_customerName(rs.getString("CUSTOMER_NAME"));
				mstcustomer.setS_sex(rs.getString("SEX"));
				mstcustomer.setS_birthday(rs.getDate("BIRTHDAY"));
				mstcustomer.setS_address(rs.getString("ADDRESS"));
				mstcustomer.setS_email(rs.getString("EMAIL"));
				mstcustomer.setD_deleteYMD(rs.getDate("DELETE_YMD"));
				mstcustomer.setD_insertYMD(rs.getDate("INSERT_YMD"));
				mstcustomer.setD_updateYMD(rs.getDate("UPDATE_YMD"));
				list.add(mstcustomer);
			}
			conn.close();
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return list;
	}

	public boolean DeleteByID(String id) {
		try {
			Connection conn = JDBC_Connection.getConnection();
			String sql = "DELETE FROM MSTCUSTOMER WHERE CUSTOMER_ID = ?";
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			ps.setString(1, id);
			if (ps.executeUpdate() != 0)
				return true;
			else
				return false;

		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			return false;
		}
	}

	public boolean CreateNew(MSTCUSTOMER cus) {
		try {
			Connection conn = JDBC_Connection.getConnection();
			//String sql = "INSERT INTO MSTCUSTOMER(CUSTOMER_NAME, SEX, ADDRESS, BIRTHDAY, EMAIL, UPDATE_YMD, INSERT_YMD, DELETE_YMD) VALUES(?,?,?,?,?,?,?,?)";
			String sql = "INSERT INTO MSTCUSTOMER(CUSTOMER_NAME, SEX, ADDRESS) VALUES(?,?,?)";
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			
			ps.setString(1, cus.getS_customerName());
			ps.setString(2, cus.getS_sex());
			ps.setString(3, cus.getS_address());
			/*ps.setDate(4, cus.getS_birthday());
			ps.setString(5, cus.getS_email());
			ps.setDate(6, cus.getD_updateYMD());
			ps.setDate(7, cus.getD_insertYMD());
			ps.setDate(8, cus.getD_deleteYMD());*/
			
			if (ps.executeUpdate() != 0)
				return true;
			else
				return false;

		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			return false;
		}
	}
	
	//phan trang
	//Pages number 1->4 or 5->8 ..
	public ArrayList<MSTCUSTOMER> GetCustomerPT(int start, int sl) {
		Connection conn = JDBC_Connection.getConnection();
	    ArrayList<MSTCUSTOMER> list = new ArrayList();
	    String sql = "SELECT * FROM MSTCUSTOMER ORDER BY CUSTOMER_ID OFFSET ? ROWS FETCH NEXT ? ROWS ONLY";
	    try {
	        PreparedStatement ps = conn.prepareStatement(sql);
	        ps.setInt(1, start);
	        ps.setInt(2, sl);
	        ResultSet rs = ps.executeQuery();
	        while (rs.next()) {
				MSTCUSTOMER mstcustomer = new MSTCUSTOMER() {
				};
				mstcustomer.setS_customerID(rs.getString("CUSTOMER_ID"));
				mstcustomer.setS_customerName(rs.getString("CUSTOMER_NAME"));
				mstcustomer.setS_sex(rs.getString("SEX"));
				mstcustomer.setS_birthday(rs.getDate("BIRTHDAY"));
				mstcustomer.setS_address(rs.getString("ADDRESS"));
				list.add(mstcustomer);
			}
			conn.close();
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return list;
	    
		
	}
	
	
	public int getCount() {
		Connection conn = JDBC_Connection.getConnection();
	    ArrayList<MSTCUSTOMER> list = new ArrayList();
	    String sql = "SELECT count(CUSTOMER_ID) FROM MSTCUSTOMER";
	    int count = 0;
	    try {
	        PreparedStatement stmt = conn.prepareStatement(sql);
	        ResultSet rs = stmt.executeQuery();
	        while (rs.next()) {
	            count = rs.getInt(1);
	        }
	    } catch (SQLException e) {
	        e.printStackTrace();
	    }
	    return count;
	}
	
	
	//test

	public static void main(String[] args) {
		MSTCUSTOMER_DAO dao = new MSTCUSTOMER_DAO();

		// if (dao.DeleteByID("1"))
		// System.out.println("ok");
		// else
		// System.out.println("not ok");

		/*MSTCUSTOMER cus = new MSTCUSTOMER();
		// CUSTOMER_NAME, SEX, ADDRESS, BIRHDAY, EMAIL, UPDATEYMD, INSERTYMD, DELETEYMD
		cus.setS_customerName("bi");
		cus.setS_sex("male");
		cus.setS_address("quan9");
		cus.setS_birthday(new Date(2008, 11, 11));
		cus.setS_email("mail");
		cus.setD_updateYMD(new Date(2008, 11, 11));
		cus.setD_insertYMD(new Date(2008, 11, 11));
		cus.setD_deleteYMD(new Date(2008, 11, 11));

		if (dao.CreateNew(cus))
			System.out.println("ok");
		else
			System.out.println("not ok");*/
		
		/*for (MSTCUSTOMER cus : dao.GetCustomerPT(1, 2)) {
			System.out.println(cus.toString());
		}*/
		
	}
	
}

package fs.action;

import java.io.IOException;
import java.util.ArrayList;
import java.sql.Date;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import fs.dao.MSTCUSTOMER;
import fs.dao.MSTCUSTOMER_DAO;

/**
 * Servlet implementation class CustomerAction
 */
@WebServlet("/CustomerAction")
public class CustomerAction extends HttpServlet {
	private static final long serialVersionUID = 1L;

	/**
	 * @see HttpServlet#HttpServlet()
	 */
	public CustomerAction() {
		super();
		// TODO Auto-generated constructor stub
	}

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// TODO Auto-generated method stub
		MSTCUSTOMER_DAO dao = new MSTCUSTOMER_DAO();
		String action = request.getParameter("action");
		if (action.equals("delete")) {
			//// tra ve  id da chon o checkbox 22022,22023
			String strList = request.getParameter("listDelete"); 
			//tra ve mang id
			String[]listId = strList.split(","); // [22022,22023]
			for (String id : listId) {
				dao.DeleteByID(id);
			}
			response.sendRedirect("jsp/T002.jsp");
		}
		if(action.equals("create")) {
			MSTCUSTOMER mstcustomer = new MSTCUSTOMER();
			String s_customerName = request.getParameter("CUSTOMER_NAME");
			String sex = request.getParameter("SEX");
			String address = request.getParameter("ADDRESS");

			String birthday=request.getParameter("BIRTHDAY");
//			String email = request.getParameter("EMAIL");
//			Date UPDATE_YMD = new Date(request.getParameter("UPDATE_YMD"));
//			Date INSERT_YMD = new Date(request.getParameter("INSERT_YMD"));
//			Date DELETE_YMD = new Date(request.getParameter("DELETE_YMD"));
			mstcustomer.setS_customerName(s_customerName);
			mstcustomer.setS_sex(sex);
			mstcustomer.setS_address(address);
//			mstcustomer.setS_birthday(birthday);
			System.out.println(mstcustomer.toString());
			if(dao.CreateNew(mstcustomer)) {
				System.out.println("OKkkkkkkkkkk");
			}
			response.sendRedirect("jsp/T002.jsp");
			System.out.println("Zo");
		}
		if(action.equals("update")) {

				
		}
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// TODO Auto-generated method stub
		doGet(request, response);
	}

}

package fs.action;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import fs.common.Constants;
import fs.dao.MSTUSER_DAO;

/**
 * Servlet implementation class LoginServlet
 */
//@WebServlet("/LoginServlet")
public class LoginServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	/**
	 * @see HttpServlet#HttpServlet()
	 */
	public LoginServlet() {

	}

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		RequestDispatcher myRD = null;
		// Hien thi man hinh Login
		//dispatcher: khong co dinh duong dan
		myRD = request.getRequestDispatcher(Constants.T001_LOGIN);

		myRD.forward(request, response);

	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		
		String action = request.getParameter("action");
		if (action.equals("login")) {
			// tao session
			HttpSession session = request.getSession();
			PrintWriter out = response.getWriter();
			String username = request.getParameter("txtUserID");
			String password = request.getParameter("txtPassword");
			// xac thuc id va pass
			if (MSTUSER_DAO.validate(username, password)) {
				session.setAttribute("txtUserID", username);
//				RequestDispatcher rd = request.getRequestDispatcher("/jsp/T002.jsp");
//				rd.forward(request, response);
				response.sendRedirect("jsp/T002.jsp");
			} else {
//				RequestDispatcher rd = request.getRequestDispatcher("/jsp/T001.jsp");
//				rd.forward(request, response);
				response.sendRedirect("jsp/T001.jsp");
			}
			out.close();
		}
		if (action.equals("logout")) {
			HttpSession session = request.getSession();
			PrintWriter out = response.getWriter();
//			request.getRequestDispatcher(Constants.T001_LOGIN).include(request, response);
			response.sendRedirect("jsp/T001.jsp");
			session.invalidate();
			out.close();
		}
	}

}

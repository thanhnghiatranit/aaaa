T002

<%@page import="java.util.List"%>
<%@page import="fs.dao.MSTCUSTOMER"%>
<%@page import="fs.dao.MSTCUSTOMER_DAO"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Insert title here</title>
		<script type="text/javascript" src="../js/error.js"></script>
</head>
<body>
	<div class="container">
		<h2 style="color: red;">Training</h2>
		<form class="form-group" action="../T001" method="post" name="myform">
			<div class="form-group">
				<div class="col-sm-3">
					Welcome:<%=session.getAttribute("txtUserID")%>
				</div>
				<input name="action" value="logout" hidden> <input type="submit"
					value="Logout"><br> <input
					class="form-control input-sm"
					style="background: blue; margin-bottom: 20px"></input>
			</div>
		</form>

		<form class="form-group" action="" method="post">
			<div class="form-group" style="background: #ffff33">
				<div class="col-sm-5">
					<label id="llbCustomername">Customer name:</label> <input
						id="txtCustomerName"> <label>Sex </label> <select
						id="llbSex">
						<option></option>
						<option>Male</option>
						<option>Female</option>
					</select>
				</div>
				<div class="col-sm-5">
					<label>Birthday:</label> <input id="txtBirthdayForm">~<input
						id="txtBirthdayTo">
				</div>
				<div class="col-sm-offset-11">
					<button id="btnSearch" type="button" class="btn"
						onclick="searchName()">Search</button>
				</div>
			</div>
			<!-- <div class="form-group">
				<div class="row-sm-12">
					<div class="col-sm-3">
						<button name="btnFirst" type="button" class="btn"><</button>
						<button name="btnPrevious" type="button" class="btn"><<</button>
						Previous
					</div>

					<div class="col-sm-offset-9">
						Next
						<button name="btnNext" type="button" class="btn">>></button>
						<button name="btnLast" type="button" class="btn">></button>

					</div>

				</div>
			</div> -->

			<!-- Phân trang -->
			<%
				int first = 0, last = 0, pages = 1;

				if (request.getParameter("pages") != null) {
					pages = (int) Integer.parseInt(request.getParameter("pages"));
				}
				//Lấy tổng CUS
				int total = new MSTCUSTOMER_DAO().getCount();

				if (total <= 4) {
					first = 0;
					last = total;
				} else {
					first = (pages - 1) * 2;
					last = 4;
				}
			%>





			<table id="myTable" class="display">
				<thead>
					<tr>
						<th><input type="checkbox" name="Check_All" value="Check All"
							onclick="toggle(this);"></th>	
						<th>Customer ID</th>
						<th>Customer Name</th>
						<th>Sex</th>
						<th>Birthday</th>
						<th>Address</th>
					</tr>
				</thead>
				<tbody>
					<%
						//Lấy ra danh sách sản phẩm
						List<MSTCUSTOMER> list = new MSTCUSTOMER_DAO().GetCustomerPT(first, last);
						for (MSTCUSTOMER customerlist : list) {
					%>
					<tr>
						
					
						<td><input type="checkbox"
							id="<%=customerlist.getS_customerID()%>"
							value="<%=customerlist.getS_customerID()%>"
							onclick="
							checkedFunction(this)" name="check_list"
							class="styled"></td>


						<td><a
							href="T003.jsp?action=view&idCustomer=<%=customerlist.getS_customerID()%>"><%=(customerlist.getS_customerID() != null ? customerlist.getS_customerID() : "")%></a></td>
						<td><%=(customerlist.getS_customerName() != null ? customerlist.getS_customerName() : "")%></td>
						<td><%=(customerlist.getS_sex() != null ? customerlist.getS_sex() : "")%></td>
						<td><%=(customerlist.getS_birthday() != null ? customerlist.getS_birthday() : "")%></td>
						<td><%=(customerlist.getS_address() != null ? customerlist.getS_address() : "")%></td>
					</tr>
				</tbody>
				<%
					}
				%>
			</table>

			<!-- Phan trang -->
			<ul class="start">
				<%
					//Button Previous
					int back = 0;
					if (pages == 0 || pages == 1) {
						back = 1;//Luon la page 1
					} else {
						back = pages - 1;//Neu pages tu 2 tro len thi back tru 1
					}
				%>
				<li><a href="T002.jsp?pages=<%=back%>"><i></i></a></li>
				<%
					//Button Number pages
					int loop = 0, num = 0;
					if ((total / 2) % 2 == 0) {
						num = total / 4;
					} else {
						num = (total + 1) / 2;
					}
					//Nếu total lẻ thêm 1
					if (total % 2 != 0) {
						loop = (total / 2) + 1;

					} else {
						//Nếu total chẵn nhỏ hơn fullpage và # fullPage thì thêm 1
						if (total < (num * 2) + 2 && total != num * 2) {
							loop = (total / 2) + 1;
						} else {
							//Nếu bằng fullPage thì không thêm
							loop = (total / 2);
						}
					}
					//Lap so pages
					for (int i = 1; i <= loop; i++) {
				%>
				<%
					if (pages == i) {
				%>

				<li><span><a href="T002.jsp?pages=<%=i%>"><%=i%></a></span></li>
				<%
					} else {
				%>
				<li class="arrow"><a href="T002.jsp?pages=<%=i%>"><%=i%></a></li>

				<%
					}
					}
				%>
				<%
					//Button Next
					int next = 0;
					//Nếu total lẻ
					if (total % 2 != 0) {
						if (pages == (total / 2) + 1) {
							next = pages;//Khong next
						} else {
							next = pages + 1;//Co next
						}
					} else {
						//Nếu total chẵn nhỏ hơn fullpage
						//Và không fullPage thì thêm 1
						if (total < (num * 2) + 2 && total != num * 2) {
							if (pages == (total / 2) + 1) {
								next = pages;//Khong next
							} else {
								next = pages + 1;//Co next
							}
						} else {
							//Nếu fullPage đến trang cuối dừng
							//Chưa tới trang cuối thì được next
							if (pages == (total / 2)) {
								next = pages;//Khong next
							} else {
								next = pages + 1;//Co next
							}
						}
					}
				%>
				<li><a href="T002.jsp?pages=<%=next%>"><i class="next"></i></a></li>
			</ul>
	</div>

	<br>
	</form>
	</div>


	<form action="../CustomerAction" method="post">
		<input hidden name="listDelete" id="customerId"> <input name="action"
			hidden value="delete">
		<button name="btnDelete" class="btn" type="submit">Delete</button>
	</form>

	<form action="T003.jsp" method="post">
		<input name="action" hidden value="addnew">
		<button class="btn" type="submit">Add new</button>
	</form>
<!-- checkid -->
	<script type="text/javascript">
		function checkedFunction(arg) {
			var x = document.getElementById("customerId");
			if (arg.checked == true) {
				x.value = x.value + ",";
				x.value = x.value + arg.id;
			}
			if (arg.checked == false) {
				x.value = x.value.replace("," + arg.id, "");
			}
		}
	</script>
	
</body>
</html>

# Spring-checkbox<%@page import="com.sun.xml.internal.txw2.Document"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ page isELIgnored="false"%>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="spring" uri="http://www.springframework.org/tags"%>


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet"
	href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">
<script
	src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"
	type="text/javascript"></script>
<script
	src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js"
	type="text/javascript"></script>
<script
	src="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js"
	type="text/javascript"></script>
<script type="text/javascript"
	src="https://code.jquery.com/jquery-3.3.1.js"></script>

<script type="text/javascript"
	src="https://cdn.datatables.net/1.10.19/js/jquery.dataTables.min.js"></script>
<script type="text/javascript"
	src="https://cdn.datatables.net/1.10.19/js/dataTables.bootstrap4.min.js"></script>

</head>
<script type="text/javascript">
	$(document).ready(function() {
		$('.dtVerticalScroll').DataTable({
			"scrollY" : "50vh",
			"scrollCollapse" : true,
			"info":false
		});
		$('.dataTables_length').addClass('bs-select');
	});
</script>

<script>
function copyFunction() {
    if (confirm("Do you really want to copy the selected item?")) {
        
    } else {
        
    }
    document.getElementById("copy").innerHTML;
}
</script>
<!-- <script>
function deleteFunction() {
    if (confirm("Do you really want to delete the selected item?")) {
        
    } else {
    }
    document.getElementById("delete").innerHTML;
} 
</script> -->
<style>
.bgcolor{
	background-color:#A0CFEC;
}
.btn{
	background-color:#77BFC7;
}
</style> 
<body>
	<form:form method="POST" modelAttribute="ucm" action="" id="catForm" name="ucm">

		<div class="container">
		
		
			<h2 class="text-center"><u>List Of Categories</u></h2><br>
			<table style="width:100%;border:0px;" cellpadding="0" cellspacing="0" summary="">
<tbody><tr><td class="uwrJustFormat"><div class="uwrTb"><table cellpadding="0" cellspacing="0" border="0" height="20px;" width="100%">
					<tr>
			 			<td width="87%" valign="middle">

						</td>
						
							
								<!--  <td width="10%" align="right">Show all&nbsp;&nbsp;</td> -->
								<td width="3%" align="right"> 
						  		 <input type="checkBox" id="checkBox" name="checkBox" class="cuiCheckBox" value="true" onclick="checkBox()"><label class="cuiCheckBoxOption"></label> 
						  		<!--  <button type="button"  id="code"  class="cuiCheckBox" name="checkBox" value="1" onclick="checkBox();">Show All</button>  -->
						  		<!--  <button type="button" class="btn"  name="checkBox">Show All</button> -->
						  		 
						  	</td>
					  	
						
					</tr>					
					</table></div></td><td class="uwrJustFormat" style="text-align:right;"></td></tr></tbody></table>
			<table  class="dtVerticalScroll table  table-hover table-striped table-bordered table-sm" style="background-color:#F0F8FF">
				<thead class="bgcolor">
					<tr>
						<th class="th-sm">Category<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">CUG<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Active<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">No.Of Events<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Select<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				 <tbody>
				
					<c:forEach items="${categories}" var="categ" varStatus="status">
					
						<tr>
                                         		<td class="titelClass"> ${categ.titel}</td>
                                         		<td>${categ.hasClosedUserGroup}</td>
                                         		<td class="activeState">${categ.activeState}</td>
                                         		<td>${categ.anzEvents}</td>
                                         		 <td>${categ.idrow}</td> 
                                               <td><form:radiobutton path="idrow" value="${categ.idrow}"  />
                                                </td> 
					</c:forEach>
				</tbody> 
			</table><br>
			<div class="container-fluid">
			<div class="row">
			<div class="col text-center">
			<button type="button" class="btn" data-toggle="modal" data-target="#editModal" onclick="editBox();">Edit</button>
			<button type="button" class="btn" onclick="copyFunction()">Copy</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#DeleteModal">Delete</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#perModal" name="categPermButton">Permission</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#uplModal">Upload</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#regModal" name="regButton">Registration</button>
			<button type="button" class="btn btn-show-value" data-toggle="modal" data-target="#urlModal"  >URL</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#newModal">New</button>
			</div>
			</div>
		</div>
		
		
 	
	
	 <script>
		$('#checkBox').click(function() {
  /*   var checked = $(this).is(':checked'); */
    var checked = $(this).val();
alert(checked);
    $.ajax({
    	/* dataType : 'text', */
        url: 'showAllCateg',
        data: { checked : checked },
        success: function(data) {
        	alert(checked);
            alert('it worked');
            alert(JSON.stringify(data));
        },
        error: function() {
            alert('it broke');
        },
        complete: function() {
            alert('it completed');
        }
    });
    
    
    
    $
	.post({
		url : 'showAllCateg',
	 data : $('form[name=ucm]')
				.serialize(),  
				/* data: JSON.stringify({ selectedItems: $('#event').data('ListBox').dataItems() }), */		
		success : function(res) {
			alert(JSON.stringify(res));
		}

	})
	
	

	
    
});
	
		</script>  
	
	
	
	
		
		<!--   <script>
		 function checkBox(){
		/* var x= document.getElementById('code');
		var y="";
		 if(x.checked){
	          y = x.innerHTML;
	          alert(y);
		 } */
		 if ( $('#code').is(':checked') ) { 

		        // execute AJAX request here
			 $('#checkBox').change(function() {
				    var checked = $(this).is(':checked');

				    $.ajax({
				    	dataType : 'text',
				        url: 'showAllCateg',
				      /*   data: { checked : checked }, */
				        data : $('form[name=ucm]')
						.serialize(),
				        success: function(data) {
				            alert('it worked');
				        },
				        error: function() {
				            alert('it broke');
				        },
				        complete: function() {
				            alert('it completed');
				        }
				    });
				});

		    }
		 }	
		</script>  --> 
		
		<!-- 
		<script>
		$(document).ready(function(){
			$('#checkBox').change(function(){
				var selectedValue= $(this).val();
				$ajax.({
					url:"showAllCateg",
					method:"POST",
					data:{selectedValue:selectedValue},
					success:function(data){
						alert('it worked');
						
					},
					error: function() {
			            alert('it broke');
			        }
				});
			});
			
		});
			
			
		</script>
		 -->
		
		
		
		
		
		<!-- Edit Modal -->
  <div class="modal fade" id="editModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Category Properties</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
         <form action="/action_page.php">
    <div class="form-group">
      <label for="name">Name Of Category:</label>
      <form:input path="titel" cssClass="form-control"/>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio1">Activation State:
       <%--  <form:radiobutton path="idrow"  class="form-check-input" id="radio1" name="optradio" value="yes" />On --%>
       <input type='radio' name='optradio' value='yes' />On
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio2">
       <!--  <input type="radio" class="form-check-input" id="radio2" name="optradio">Off -->
       <form:radiobutton path="idrow" class="form-check-input" id="radio2"  value="${categ.idrow}" />Off
      </label>
    </div><br><br>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio3">Visible In The List:
        <form:radiobutton path="code"  class="form-check-input" id="radio3" name="optradio1" value="${categ.code}" />Visible
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio4">
        <form:radiobutton path="code"  class="form-check-input" id="radio4" name="optradio1" value="${categ.code}"/>Not Visible
      </label>
    </div><br><br>
    <div class="form-group">
      <label for="name">Registration:</label>
      <img src="<c:url value="/static/de.gif"/>" >
      <img src="<c:url value="/static/en.gif" />" >				 				
      <img src="<c:url value="/static/fr.gif" /> " >
      <img src="<c:url value="/static/it.gif" /> " >
    </div>
  </form>
        </div>
        <div class="modal-footer">
          <button type="submit" class="btn"  onclick='this.form.action="save/";'>Save</button>
        </div>
      </div>
    </div>
  </div>

  <script>
  function editBox(){
	  
	  var radio = document.getElementsByName('idrow');
	  var titel=document.getElementsByClassName('titelClass');
	  var active= document.getElementsByClassName('activeState');
	  var rBox="";
	  var inputBox="";
	 
	  for(var i = 0; i < radio.length; i++){
	      if(radio[i].checked){
	          inputBox = titel[i].innerHTML;
	          rBox= active[i].innerHTML;
	       
	      }
	  }
	  document.getElementById("titel").value=inputBox;
	  document.getElementById("titel").autofocus="autofocus";

	  if(rBox=="yes"){
		  document.getElementById("idrow").value=rBox;
		  alert(idrow);
	  }
	  $(function() {
		    var $radios = $('input:radio[name=optradio]');
		    if($radios.is(':checked') === false) {
		        $radios.filter('[value=yes]').prop('checked', true);
		        alert(radios);
		    }
		});
  } 
  </script>
  <script type="text/javascript">
  
  </script>
  
  <!-- Copy Button-->
  <p id="copy"></p>
  <!-- Copy Button -->
  
  <!-- Delete Button-->
  <!-- <p id="delete"></p> -->
  
  <div class="modal fade" id="DeleteModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        <!-- Modal Header -->
        <div class="modal-header">
          <h4 class="modal-title">Category Delete</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        <!-- Modal body -->
        <div class="modal-body">
         Are you sure you want to delete?
        </div>
        
        <!-- Modal footer -->
        <div class="modal-footer">
          <button type="submit" class="btn"  onclick='this.form.action="cd/";'>OK</button>
        </div>
        
      </div>
    </div>
  </div>
  
  <!-- Delete Button -->
  
  <!-- Permission Modal -->
  <div class="modal fade" id="perModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Category Permission</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
         <div class="container-fluid">
		<div class="row">
		<div class="col text-center">
			<h5 class="text-center">Category Managers</h5><br>
			<table id="dtVerticalScroll1" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<th class="th-sm">GPN<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Select<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					
				</tbody>
			</table></div></div></div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal" onclick="deleteFunction()">Delete</button>
          <button type="button" class="btn" data-dismiss="modal" data-toggle="modal" data-target="#pernewModal">New</button>
        </div>
      </div>
    </div>
  </div>
  
  <div class="modal fade" id="pernewModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
       
        <div class="modal-header">
          <h4 class="modal-title">User Search</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        
        <div class="modal-body">
          <div class="form-group">
      <label for="name">Last Name:</label>
      <input type="text" class="form-control" id="lname" name="name">
    </div>
    <div class="form-group">
      <label for="name">First Name:</label>
      <input type="text" class="form-control" id="fname" name="name">
    </div>
    <div class="form-group">
      <label for="name">GPN:</label>
      <input type="text" class="form-control" id="gpn" name="gpn">
    </div>
        </div>
        
        
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Search</button>
          <button type="button" class="btn" data-dismiss="modal">Reset</button>
        </div>
        
      </div>
    </div>
  </div>
  <!-- Permission Modal -->
  
   <!-- Upload Modal -->
   
    <div class="modal fade" id="uplModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">List Of Categories</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
          <div class="container">
 
  <ul class="nav nav-pills" role="tablist">
    <li class="nav-item">
      <a class="nav-link active" data-toggle="pill" href="#user">User Group</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" data-toggle="pill" href="#ban">Banner</a>
    </li>
  </ul>

  
  <div class="tab-content">
    <div id="user" class="container tab-pane active"><br>
      <h5>Upload Closed User Group</h5>
      <div class="container mt-3">
  <form action="/action_page.php">
    File Name:
    <div class="custom-file mb-3">
      <input type="file" class="custom-file-input" id="filename" name="filename">
      <label class="custom-file-label" for="filename">Choose file</label>
    </div>  
    <div class="mt-3">
      <button type="submit" class="btn">Upload</button>
    </div><br>
    <div class="row">
    <div class="col-4">
            Level:
            <select class="custom-select" id="level">
                <option value=""></option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div>
        <div class="col-4">
            Feedback:
            <select class="custom-select" id="feedback">
                <option value=""></option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div></div><br>
        <h6 class="text-center">Closed User Group List</h6>
        <table id="dtVerticalScroll" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<th class="th-sm">GPN<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Email<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Location<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Level<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Feedback<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Language<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					<c:forEach items="${areas}" var="area" varStatus="status">
						<tr>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
						</tr>
					</c:forEach>
				</tbody>
			</table>
  </form>
</div>
    </div>
    <div id="ban" class="container tab-pane fade"><br>
      <h5>Upload Banner</h5>
      <div class="container mt-3">
  <form action="/action_page.php">
    File Name:
    <div class="custom-file mb-3">
      <input type="file" class="custom-file-input" id="file" name="filename">
      <label class="custom-file-label" for="file">Choose file</label>
    </div>
    <div class="row">
    <div class="col-4">
            Language:
            <select class="custom-select" id="lang">
                <option value=""></option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div></div>  
    <div class="mt-3">
      <button type="submit" class="btn">Upload</button>
      <button type="submit" class="btn">Default Banner</button>
    </div><br><br>
        <h6 class="text-center">Banner List</h6>
        <table id="dtVerticalScroll" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<th class="th-sm">File Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Language<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Level<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					<c:forEach items="${areas}" var="area" varStatus="status">
						<tr>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
						</tr>
					</c:forEach>
				</tbody>
			</table>
  </form>
</div>
    </div>
  </div>
</div>
           
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Show</button>
          <button type="button" class="btn" data-dismiss="modal">Excel Export</button>
          <button type="button" class="btn" data-dismiss="modal">Delete</button>
          <button type="button" class="btn" data-dismiss="modal">Delete List</button>
        </div>
        
      </div>
    </div>
  </div></div>
    <!-- Upload Modal -->
    
     <!-- Registration Modal -->
    <div class="modal fade" id="regModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Registration</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        
        <div class="modal-body">
        <div class="container ">
         <h5>Search</h5>
          <div class="row">
           <div class="col-11">
           Event:
            <select class="custom-select" name="event" id="event" >
              <%--  <form:option value="ALL"></form:option> --%>
            </select>
           </div>
           </div>
           <div class="row">
           <div class="col-6">
            <div class="form-group">
      <label for="name">Name:</label>
      <input type="text" class="form-control" id="name" name="name" >
       </div>
       </div>
              <div class="form-group">
      <label for="name">GPN:</label>
      <input type="text" class="form-control" id="name" name="name">
       </div>
       </div>
       <div class="row">
           <div class="col-6">
            Filter State:
            <select class="custom-select" id="fil">
                <option value="">ALL</option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div>
         <button type="submit" class="btn btn-info" name="userSearch" >Search</button>
        </div><br>
        <h6 class="text-center">Registrations</h6>
        
       <%--  <div class="modal-body">
							
        <table id="dtVerticalScroll" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<!-- <th class="th-sm">Event<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th> -->
						<th class="th-sm">GPN<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Status<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Phone<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Mail<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Date<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					<c:forEach items="${categories}" var="cate" varStatus="status">
						<tr>
							<td>${categ.titel}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
						</tr>
					</c:forEach>
				</tbody>
			</table>
        </div> --%>
        
        
        <div class="modal-body">
							
							<table id="dtVerticalScroll3" style="display: none;"
								class="table  table-hover table-striped table-bordered table-sm">
								<thead class="thead-light">
									<tr>
										<th class="th-sm">GPN <i
											class="fa fa-sort float-right" aria-hidden="true"></i>
										</th>
										<th class="th-sm">NAME <i class="fa fa-sort float-right"
											aria-hidden="true"></i>
										</th>
										<th class="th-sm">STATUS<i
											class="fa fa-sort float-right" aria-hidden="true"></i>
										</th>
										<th class="th-sm">PHONE<i
											class="fa fa-sort float-right" aria-hidden="true"></i>
										</th>
										<th class="th-sm">MAIL<i
											class="fa fa-sort float-right" aria-hidden="true"></i>
										</th>
										<th class="th-sm">DATE<i
											class="fa fa-sort float-right" aria-hidden="true"></i>
										</th>
									</tr>
								</thead>


							</table>
						</div>
        
        
        
        
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Excel Export</button>
        </div>
        
        </div>
      </div>
    </div>
  </div>
  </div>
 <!--  <script>
  function RegisterSearchBox(){
	  
	  var eventList = document.getElementsByClassName('custom-select');
	  /* var titel=document.getElementsByClassName('titelClass');
	  var active= document.getElementsByClassName('activeState');
	  var rBox="";*/
	  var inputBox=""; 
	alert( eventList.length);
	  
	  for(var i = 0; i < eventList.length; i++){
	      if(eventList[i].selectedIndex){
	    	   inputBox = $('#event').find('option:selected').text(); 
	          alert(inputBox);
	          
	          
	       
	      }
	    
	  } 
	  
	  
	  
  } 
  </script> -->
  
  
  
  
<!--   <script type="text/javascript">
		$(function() {
			/*  Submit form using Ajax */
			$("button[name='userSearch']")
					.click(
							function(e) {

								//Prevent default submission of form
								e.preventDefault();

								//Remove all errors
								$('input').next().remove();
								
								 

								$
										.post({
											url : 'EventRegistrationDetail',
										 data : $('form[name=ucm]')
													.serialize(),  
													/* data: JSON.stringify({ selectedItems: $('#event').data('ListBox').dataItems() }), */		
											success : function(res) {
												
												inputBox = $('#event').find('option:selected').text(); 
												alert(inputBox);
												 var x= inputBox;
												alert(x); 
												alert(JSON.stringify(res));
											}

										})
							});

		});
	</script> -->
  
  
  
  	<script type="text/javascript">
		$(function() {
			/*  Submit form using Ajax */
			$("button[name='userSearch']")
					.click(
							function(e) {

								//Prevent default submission of form
								e.preventDefault();

								//Remove all errors
								$('input').next().remove();

								$
										.post({
											url : 'EventRegistrationDetail',
											data : $('form[name=ucm]')
													.serialize(),
											success : function(res) {
												
												if (true) {
													//Set response
													
													inputBox = $('#event').find('option:selected').text(); 
												/* alert(inputBox);
												 var x= inputBox;
												alert(x); 
												alert(JSON.stringify(res)); */

													var object = JSON
															.stringify(res);
													var dummy = $(
															'#dtVerticalScroll3')
															.DataTable();
													dummy.clear().draw();
													dummy.destroy();
													document
															.getElementById("dtVerticalScroll3").style.display = "table";
													var table = $(
															'#dtVerticalScroll3')
															.DataTable(
																	{
																		"paging" : false,
																		"ordering" : false,
																		"info" : false,
																		aaSorting : []
																	});
alert(res[0].status);
if(res[0].status ==3)
	{
													for (var i = 0; i < res.length; i++) {
														
														table.row
																.add(
																		[
																				(res[i].gpn),
																				(res[i].fullName),
																				('booked'),
																				(res[i].phone),
																				(res[i].mail),
																				(res[i].recCreatedate)
																				//var date = moment(x).format("YYYY-MM-DD");
																				

																		])
																.draw();

													}
	}
												} else {
													//Set error messages need to check later
													$
															.each(
																	res.errorMessages,
																	function(
																			key,
																			value) {
																		$(
																				'input[name='
																						+ key
																						+ ']')
																				.after(
																						'<span class="error">'
																								+ value
																								+ '</span>');
																	});
												}
											}

										})
							});

		});
	</script>
  
  <!--  Registration Modal -->
  
  <!-- URL Modal -->
  
  
	
	<script  type="text/javascript">
   $(document).ready(function(){
	   $(".btn-show-value").click(function(){
		   var radioValue= $("input[name='idrow']:checked").val();
		   var radioValue_e= $("input[name='idrow']:checked").val();
		   var radioValue_f= $("input[name='idrow']:checked").val();
		   var radioValue_i= $("input[name='idrow']:checked").val();
		   var currLoc= window.location.origin;
		   
		  
		  
		   
	   
	   if(radioValue){
		  
		   document.getElementById("radio-value_d").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue+"&lang=d";
		   
			   document.getElementById("radio-value_e").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue_e+"&lang=e";
		   
			   document.getElementById("radio-value_f").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue_f+"&lang=f";
		   
			   document.getElementById("radio-value_i").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue_i+"&lang=i";
		   
		   
	   }
	   
   
   });
	   });
   
		  </script> 
		  
	  
   
  
  <div class="modal fade" id="urlModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        <!-- Modal Header -->
        <div class="modal-header">
          <h4 class="modal-title">URL</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        <!-- Modal body -->
        
        <div class="modal-body">
        
        <script language="JavaScript">	
		function preview(lang){
		  var id = radioValue;
		  window.open("/RegisterLoginFormAction.do?idrow=" + id + "&lang=" + lang, "fenster", "height=850, width=900, status=1, location=no, scrollbars=1");
		}
	</script>
        
           <table border="0" cellpadding='0' cellspacing='0' width="100%"> 
           <tr>
           <td width="50" height="30">
           <a href="javascript:preview('d');" style="text-decoration: none">
			    <img src="<c:url value="/static/de.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400">
			<script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_d" size="80" readonly></p>
          </td>
          </tr>
          <tr>
			<td height="30">
			  <a href="javascript:preview('e');" style="text-decoration: none">
			    <img src="<c:url value="/static/en.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_e" size="80" readonly></p>
          </td></tr>
         <tr>
			<td height="30">
			  <a href="javascript:preview('f');" style="text-decoration: none">
			    <img src="<c:url value="/static/fr.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_f" size="80" readonly></p>
          </td></tr><tr>
			<td height="30">
			  <a href="javascript:preview('i');" style="text-decoration: none">
			    <img src="<c:url value="/static/it.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_i" size="80" readonly></p>
          </td></tr>
           <tr> 
			<td colspan="3" align="left">
				<img src="<c:url value="/static/info_mouseover.gif" />"  border="0" style="vertical-align: top">&nbsp;
				Click on the flag in order to register a user.
			</td>
		</tr>
	</table> 
           
		<%-- <tr>
			<td width="50" height="30">
			  <a href="javascript:preview('d');" style="text-decoration: none">
			    <img src='static/de.gif' border="0" width="25" height="16" style="vertical-align: bottom">
			  </a>
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script><input name="url_de" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_de%>" size="100"  /></td>
		</tr>
		<tr>
			<td height="30">
			  <a href="javascript:preview('e');" style="text-decoration: none">
			    <img src='static/en.gif' border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td>&nbsp;</td>
			<td><input name="url_en" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_en%>" size="100"></td>
		</tr>
		<tr>
			<td height="30">
				<a href="javascript:preview('f');" style="text-decoration: none">
				  <img src='static/fr.gif' border="0" width="25" height="16" style="vertical-align: bottom">
				</a> 			
			</td>
		  <td>&nbsp;</td>
			<td><input name="url_fr" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_fr%>" size="100"></td>
		</tr>
		<tr>
			<td height="30">
				<a href="javascript:preview('i');" style="text-decoration: none">
				  <img src='static//it.gif' border="0" width="25" height="16" style="vertical-align: bottom">
				</a>			
			</td>
			<td>&nbsp;</td>
			<td><input name="url_it" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_it%>" size="100"></td>
		</tr>
		<tr>
			<td colspan="3" height="10"></td>
		</tr> --%>
		<!-- <tr> 
			<td colspan="3" align="left">
				<img src='static/info_mouseover.gif' border="0" style="vertical-align: top">&nbsp;
				Click on the flag in order to register a user.

			</td>
		</tr>
	</table> -->
        </div>

        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Close</button>
        </div>
        
      </div>
    </div>
  </div>
  <!-- URL Modal -->
  
  <!-- New Modal -->
  <div class="modal fade" id="newModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Category Properties</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
         <form action="/action_page.php">
    <div class="form-group">
      <label for="name">Name Of Category:</label>
      <input type="text" class="form-control" id="name" name="name">
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio1">Activation State:
        <input type="radio" class="form-check-input" id="radio1" name="optradio" checked>On
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio2">
        <input type="radio" class="form-check-input" id="radio2" name="optradio">Off
      </label>
    </div><br><br>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio3">Visible In The List:
        <input type="radio" class="form-check-input" id="radio3" name="optradio1" checked>Visible
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio4">
        <input type="radio" class="form-check-input" id="radio4" name="optradio1">Not Visible
      </label>
    </div><br>
  </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Save</button>
        </div>
      </div>
    </div>
  </div>
  <!-- New Modal -->
  </div>
	</form:form>
</body>



<script type="text/javascript">
		var count = 0;
		$(function() {
			/*  Submit form using Ajax */
			$("button[name='categPermButton']")
					.click(
							function(e) {
alert("hi");
								//Prevent default submission of form
								e.preventDefault();

								//Remove all errors
								$('input').next().remove();

								$
										.post({
											url : 'permissions',
											data : $('form[name=ucm]')
													.serialize(),
											success : function(res) {

								alert(JSON.stringify(res));
											}
										})
							});

		});
	</script>
	
	<script type="text/javascript">
		var count = 0;
		$(function() {
			/*  Submit form using Ajax */
			$("button[name='regButton']")
					.click(
							function(e) {

								//Prevent default submission of form
								e.preventDefault();

								//Remove all errors
									$("#event").empty()

								$
										.post({
											url : 'registration',
											data : $('form[name=ucm]')
													.serialize(),
													success: function(res){
														alert(res.length);
														var dataLen = res.length;
														$('#event').append('<option value="">ALL</option>'); 
														for (i=0; i<dataLen; i++) {
															
															$('#event').append('<option value="' + res[i].event + '">' + res[i].event + '</option>'); 
														
														}
														alert(JSON.stringify(res));
													var x=	res[0].eventidrow;
													
														
													}
													    })
													});
										});
						

		
	</script>
	
	
	
	 <!-- <script type="text/javascript">
		$('#checkBox').click(function() {
			
			/*  Submit form using Ajax */
			$("button[name='checkBox']")
					.click(
							function(e) {

								//Prevent default submission of form
								e.preventDefault();

								//count comes from above script where data is getting fetched
								
									//Remove all errors
									

									$
											.post({
												url : 'showAllCateg',
												data : $('form[name=ucm]')
														.serialize(),
												success : function(res) {
													alert("errora");
													alert(JSON.stringify(res));
													window.location.reload(true);
												},
												error : function() {
													alert("errora");
													
												}

											})
								
							});

		});
	</script>  -->
	 
</html>

<!DOCTYPE html>
<html>
<head>
    <link href='~/Content/bootstrap.min.css' rel='stylesheet' />
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
        integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
     <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>    
</head>
    <body ng-app='myApp' ng-controller='myCtrl'>


                <!-- Button trigger modal -->
        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
          Add
        </button>

        <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
          <div class="modal-dialog" role="document">
            <div class="modal-content">
              <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
              <div class="modal-body">
                
                    <form class="ng-pristine ng-valid">
                        <!-- <ul>
                            <li>ID:<input type='text' class='form-control' ng-model='id'  /></li>
                        </ul> -->
                        <ul>
                            <li>city code:<input type='number' class='form-control' id="code" ng-model='code'  /></li>
                        </ul>
                        <ul>
                            <li>name:<input type='text' class='form-control' id="name" ng-model='name'  /></li>
                        </ul>
                        <ul>
                            <li>course:<input type='text' class='form-control' id="course" ng-model='course'  /></li>
                        </ul>
                        <ul>
                            <li>contact:<input type='number' class='form-control' id="contact" ng-model='contact'  /></li>
                        </ul>
                        <ul>
                            <li>city:<input type='text' class='form-control' id="city" ng-model='city'  /></li>
                        </ul>
                        <ul>
                            <li>state:<input type='text' class='form-control' id="state" ng-model='state' /></li>
                        </ul>
                        <ul>
                            <li>country:<input type='text' class='form-control' id="country" ng-model='country'  /></li>
                        </ul>
                                
                    </form>
                      
              </div>
              <div class="modal-footer">
                <button type="button" class="btn btn-secondary" ng-click="clearData()" data-dismiss="modal" >Close</button>
                <button type="button" ng-click="submitEvent()" class="btn btn-primary" >Save changes</button>
              </div>
            </div>
          </div>
        </div>


      <div class="form-outline">
        Search: <input type="search" id="search" ng-model="query"  class="form-control"
            mdbInput />
    </div>


<table class="table table-boardered" id="myTable">
        <tr>
            <th ng-click="sortTable('id')">id</th>
            <th ng-click="sortData('code')">code</th>
            <th ng-click="sortTable('3')">name</th>
            <th ng-click="sortData('course')">course</th>
            <th ng-click="sortTable('contact')">contact</th>
            <th ng-click="sortData('city')">city</th>
            <th ng-click="sortTable('state')">state</th>
            <th ng-click="sortTable('country')">country</th>
            <th>Edit</th>
            <th>Delete</th>
        </tr>
        <tr ng-repeat="data in postsArr | filter:query">
            <td>{{ data.id }}</td>
            <td>{{ data.code }}</td>
            <td>{{ data.name }}</td>
            <td>{{ data.course }}</td>
            <td>{{ data.contact}}</td>
            <td>{{ data.city }}</td>
            <td>{{ data.state }}</td>
            <td>{{ data.country }}</td>
            <td><button ng-click="editEvent(data.id)" data-toggle="modal"
                data-target="#exampleModal">edit</button></td>
            <td><button ng-click="deleteEvent(data.id)">Delete</button></td>
        </tr>
    </table>




    <!-- pagination -->
    <div class="pagination-warp hidepagination">
            <nav aria-lable="...">
              <div id="mytable" class="ng-binding">To Records: {{data}}</div>  
                <ul class="pagination justify-content-center">
                  <li class="page-item" ng-class="{disabled:currentpage == 1}">
                    <a class="page-link" ng-click="Appprevpage()">previous</a>
                  </li>
                  <li class="page-item" ng-repeat="n in Appprevpage(1,totalpages) ng-class="{'active' : currentPage == n}" ng-click="AppsetPage()">
                    <span class="page-link" ng-if="currentPage == n" ng-bind="n">1</span>
                    <a class="page-link" ng-if="currentPage ! =n" href ng-bind="n">1</a>
                  </li>
                  <li class="page-item" ng-class="{disabled: currentPage == totalpages}">
                    <a class="page-link" href ng-click="AppnextPage()">Next</a>
                  </li>
                </ul>
              
            </nav>
          </div>





<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope,$http) {
    $scope.id = "";
    $scope.code = "";
    $scope.name = "";
    $scope.course = "";
    $scope.contact = "";
    $scope.city = "";
    $scope.state = "";
    $scope.country = "";

 $scope.validation = function () {
                var isValid = true;
                if (!$scope.code) {
                    document.getElementById('code').style.border = "0.2px solid red";
                    isValid = false;
                }
                if ($scope.position) {
                    document.getElementById('code').style.border = "";

                }
                if (!$scope.name) {
                    document.getElementById('name').style.border = "0.2px solid red"
                    isValid = false;
                }
                if ($scope.name) {
                    document.getElementById('name').style.border = "";
                }
                if (!$scope.course) {
                    document.getElementById('course').style.border = "0.2px solid red"
                    isValid = false;
                }
                if ($scope.course) {
                    document.getElementById('course').style.border = "";
                }
                if (!$scope.contact) {
                    document.getElementById('contact').style.border = "0.2px solid red"
                    isValid = false;
                }
                if ($scope.contact) {
                    document.getElementById('contact').style.border = "";
                }
                return isValid;
            }
            $scope.clearData =function(){
                $scope.id = "";
                $scope.code = "";
                $scope.name = "";
                $scope.course = "";
                $scope.contact = "";
                $scope.city = "";
                $scope.state = "";
                $scope.country = "";

            }
            $scope.editFlag = false;
            $scope.submitEvent = function () {
                if (!$scope.validation()) {
                    return false;
                }


                if ($scope.editFlag == false) {
                    $scope.event=false;
                    console.log("ADD");
                    obj = {
                        id: $scope.postsArr.length+1,
                        code: $scope.code,
                        name: $scope.name,
                        course: $scope.course,
                        contact: $scope.contact,
                        city: $scope.city,
                        state: $scope.state,
                        country: $scope.country
                    }
                    $scope.postsArr.push(obj);
                    $scope.id = "";
                    $scope.code = "";
                    $scope.name = "";
                    $scope.course = "";
                    $scope.contact = "";
                    $scope.city = "";
                    $scope.state = "";
                    $scope.country = "";
                } else {

                    console.log("EDIT");
                    for (let data of $scope.postsArr) {
                        if (data.id === $scope.editFlagId) {
                            data.id = $scope.id;
                            data.code = $scope.code;
                            data.name = $scope.name;
                            data.course = $scope.course;
                            data.contact = $scope.contact;
                            data.city = $scope.city;
                            data.state = $scope.state;
                            data.country = $scope.country;
                            break;
                        }
                    }
                    $scope.editFlag = false;
                    $scope.editFlagId = "";
                    $scope.id = "";
                    $scope.code = "";
                    $scope.name = "";
                    $scope.course = "";
                    $scope.contact = "";
                    $scope.city = "";
                    $scope.state = "";
                    $scope.country = "";

                }

            }

             $scope.editFlag = false;

            $scope.editEvent = function (id) {

                console.log("data",id)
                for (let data of $scope.postsArr) {
                    if (data.id === id) {
                        $scope.editFlag = true;
                        $scope.editFlagId = data.id;
                        $scope.id = data.id;
                        $scope.code = data.code;
                        $scope.name = data.name;
                        $scope.course = data.course;
                        $scope.contact = data.contact;
                        $scope.city = data.city;
                        $scope.state = data.state;
                        $scope.country = data.country;
                        break;
                    }
                }
            }
            $scope.deleteEvent = function (id) {
                $scope.postsArr = $scope.postsArr.filter(data => data.id !== id);
            }
            $scope.postsArr = [];
            $scope.getData = function () {
                $http.get("student.json")
                    .then((resp) => {
                        console.log(resp);
                        $scope.postsArr = resp.data;
                        console.log($scope.postsArr)
                    })
                    .catch()
            }
            $scope.getData();

            $scope.editFlag = false;


            

             $scope.sortTable = function (n) {


                const getCellValue = (tr, idx) => tr.children[idx].innerText || tr.children[idx].textContent;

                const comparer = (idx, asc) => (a, b) => ((v1, v2) => 
                    v1 !== '' && v2 !== '' && !isNaN(v1) && !isNaN(v2) ? v1 - v2 : v1.toString().localeCompare(v2)
                    )(getCellValue(asc ? a : b, idx), getCellValue(asc ? b : a, idx));

                // do the work...
                document.querySelectorAll('th').forEach(th => th.addEventListener('click', (() => {
                    const table = th.closest('table');
                    Array.from(table.querySelectorAll('tr:nth-child(n+2)'))
                        .sort(comparer(Array.from(th.parentNode.children).indexOf(th), this.asc = !this.asc))
                        .forEach(tr => table.appendChild(tr) );
                })));}




    $scope.postsArr =[];
    $scope.getData = function () {
                
        $http.get("student.json")
            .then((resp) => {
                console.log(resp.data);
                
                console.log("data");
                $scope.postsArr = resp.data;
                console.log($scope.postsArr)
            })
                    
    }
    $scope.getData();
});



</script>
</body>
</html>

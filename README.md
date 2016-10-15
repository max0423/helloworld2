

<div id="dashboard-main" ng-controller="AccessSettingsCtrl">
	<!-- top section -->
	<div id="dashboard-top">
		<span class="left-cell">
			<h4>Access Settings</h4>
		</span>
		<span class="right-cell" style="width: 300px">
			<a href="javascript:void(0)" class="green-btn" id="addUserBtn" ng-click="addUser()">Add User</a>
			<!-- <a ng-controller="ExportCtrl" href="javascript:void(0)" class="green-btn" id="exportBtn" ng-click="export()">Export</a> -->
		</span>
	</div>
	<!-- bottom section: grid layout -->
	<md-grid-list md-cols-xs="1" md-cols-sm="2" md-cols-md="3" md-cols-gt-md="3" md-row-height-gt-md="1:1" md-row-height="1:1" md-gutter="12px" md-gutter-gt-sm="8px" class="gridListdemoBasicUsage">
		<!-- left side - module -->
		<md-grid-tile class="white md-whiteframe-z5" md-rowspan="1" md-colspan="3" md-colspan-sm="2">
			<md-content flex layout="column" layout-fill>
				<table st-table="displayedCollection" st-safe-src="userList" class="table table-striped" summary="List of system users">
					<thead>
						<tr>
							<th class="userSearch" >
							    <label for="userSearch" hidden>User Search</label>
								<input id="userSearch" st-search="fullname" st-delay="0" placeholder="Search Users By Name" class="input-sm form-control" type="search"/>
							</th>	
                            <th class="businessUnitSearch" >
                                <label for="businessUnitSearch" hidden>BU Search</label>
                                <input id="businessUnitSearch" style="border:none; width:150px; margin-left:30px" ng-model="businessUnitSearch" st-delay="0" placeholder="Search Users By BU" class="input-sm form-control" type="search" />
                            </th>						
						<tr>
						<tr>
							<th id="fullName" st-sort-default="true" st-sort="getters.fullName" ng-click="">User Name</th>
							<th id="isActive" st-sort="getters.active" ng-click="">Active</th>
							<th id="bu" st-sort="getters.bu" ng-click="">Business Unit</th>
							<th id="reviews" st-sort="getters.reviews" ng-click="">Review(s)</th>
							<th id="role" st-sort="getters.role" ng-click="">Role(s)</th>
							<th id="email" st-sort="getters.email" ng-click="">Email</th>
							<th id="action" >Action</th>
						</tr>
					</thead>
					<tbody>
						<tr ng-repeat="s in displayedCollection | filter:{fullName: searchName, bu: businessUnitSearch}">
							<td header="fullName"><img class="bluepages-image" src="http://images.w3ibm.mybluemix.net/image/{{s.email}}.jpg?s=30"/> {{s.fullname}}</td>
							<td header="isActive">{{ s.isUser!="Yes" ? "No" : "Yes" }}</td>
							<td header="bu">{{s.bu}}<span ng-if="s.bu==''">Not Assigned</span></td>
							<td header="reviews">{{ getReviewsAsString(s) }}</td>
							<td header="role">{{ getRolesAsString(s) }}</td>
							<td header="email">{{s.email}}</td>
							<td header="action">
								<a href="javascript:void(0)" ng-click="editUser(s)">Edit</a> | <a href="javascript:void(0)" ng-click="deleteUser(s)">Delete</a>
							</td>
						</tr>
					</tbody><tfoot>
						<tr>
							<td colspan="7" class="text-center" ng-hide="(searchName)">
								<div st-pagination="" st-items-by-page="8" st-displayed-pages="7"></div>
							</td>
						</tr>
					</tfoot>
				</table>
				<md-progress-circular layout="row" md-diameter="200px" md-mode="indeterminate" ng-show="showProgress" layout-align="center center" style="margin-left: 35%;" aria-valuenow="1" aria-labelledby="progressBar"></md-progress-circular>
			</md-content>
		</md-grid-tile>
	</md-grid-list>
</div>

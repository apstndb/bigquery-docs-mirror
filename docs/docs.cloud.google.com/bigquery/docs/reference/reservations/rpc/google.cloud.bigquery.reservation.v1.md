## Index

  - `  ReservationService  ` (interface)
  - `  Assignment  ` (message)
  - `  Assignment.JobType  ` (enum)
  - `  Assignment.State  ` (enum)
  - `  BiReservation  ` (message)
  - `  CapacityCommitment  ` (message)
  - `  CapacityCommitment.CommitmentPlan  ` (enum)
  - `  CapacityCommitment.State  ` (enum)
  - `  CreateAssignmentRequest  ` (message)
  - `  CreateCapacityCommitmentRequest  ` (message)
  - `  CreateReservationGroupRequest  ` (message)
  - `  CreateReservationRequest  ` (message)
  - `  DeleteAssignmentRequest  ` (message)
  - `  DeleteCapacityCommitmentRequest  ` (message)
  - `  DeleteReservationGroupRequest  ` (message)
  - `  DeleteReservationRequest  ` (message)
  - `  Edition  ` (enum)
  - `  FailoverMode  ` (enum)
  - `  FailoverReservationRequest  ` (message)
  - `  GetBiReservationRequest  ` (message)
  - `  GetCapacityCommitmentRequest  ` (message)
  - `  GetReservationGroupRequest  ` (message)
  - `  GetReservationRequest  ` (message)
  - `  ListAssignmentsRequest  ` (message)
  - `  ListAssignmentsResponse  ` (message)
  - `  ListCapacityCommitmentsRequest  ` (message)
  - `  ListCapacityCommitmentsResponse  ` (message)
  - `  ListReservationGroupsRequest  ` (message)
  - `  ListReservationGroupsResponse  ` (message)
  - `  ListReservationsRequest  ` (message)
  - `  ListReservationsResponse  ` (message)
  - `  MergeCapacityCommitmentsRequest  ` (message)
  - `  MoveAssignmentRequest  ` (message)
  - `  Reservation  ` (message)
  - `  Reservation.Autoscale  ` (message)
  - `  Reservation.ReplicationStatus  ` (message)
  - `  Reservation.ScalingMode  ` (enum)
  - `  ReservationGroup  ` (message)
  - `  SearchAllAssignmentsRequest  ` (message)
  - `  SearchAllAssignmentsResponse  ` (message)
  - `  SearchAssignmentsRequest  ` (message)
  - `  SearchAssignmentsResponse  ` (message)
  - `  SplitCapacityCommitmentRequest  ` (message)
  - `  SplitCapacityCommitmentResponse  ` (message)
  - `  TableReference  ` (message)
  - `  UpdateAssignmentRequest  ` (message)
  - `  UpdateBiReservationRequest  ` (message)
  - `  UpdateCapacityCommitmentRequest  ` (message)
  - `  UpdateReservationRequest  ` (message)

## ReservationService

This API allows users to manage their BigQuery reservations.

A reservation provides computational resource guarantees, in the form of [slots](https://cloud.google.com/bigquery/docs/slots) , to users. A slot is a unit of computational power in BigQuery, and serves as the basic unit of parallelism. In a scan of a multi-partitioned table, a single slot operates on a single partition of the table. A reservation resource exists as a child resource of the admin project and location, e.g.: `  projects/myproject/locations/US/reservations/reservationName  ` .

A capacity commitment is a way to purchase compute capacity for BigQuery jobs (in the form of slots) with some committed period of usage. A capacity commitment resource exists as a child resource of the admin project and location, e.g.: `  projects/myproject/locations/US/capacityCommitments/id  ` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateAssignment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateAssignment(                         CreateAssignmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              Assignment            </code> )</p>
<p>Creates an assignment object which allows the given project to submit jobs of a certain type using slots from the specified reservation.</p>
<p>Currently a resource (project, folder, organization) can only have one assignment per each (job_type, location) combination, and that reservation will be used for all jobs of the matching type.</p>
<p>Different assignments can be created on different levels of the projects, folders or organization hierarchy. During query execution, the assignment is looked up at the project, folder and organization levels in that order. The first assignment found is applied to the query.</p>
<p>When creating assignments, it does not matter if other assignments exist at higher levels.</p>
<p>Example:</p>
<ul>
<li>The organization <code dir="ltr" translate="no">            organizationA           </code> contains two projects, <code dir="ltr" translate="no">            project1           </code> and <code dir="ltr" translate="no">            project2           </code> .</li>
<li>Assignments for all three entities ( <code dir="ltr" translate="no">            organizationA           </code> , <code dir="ltr" translate="no">            project1           </code> , and <code dir="ltr" translate="no">            project2           </code> ) could all be created and mapped to the same or different reservations.</li>
</ul>
<p>"None" assignments represent an absence of the assignment. Projects assigned to None use on-demand pricing. To create a "None" assignment, use "none" as a reservation_id in the parent. Example parent: <code dir="ltr" translate="no">           projects/myproject/locations/US/reservations/none          </code> .</p>
<p>Returns <code dir="ltr" translate="no">           google.rpc.Code.PERMISSION_DENIED          </code> if user does not have 'bigquery.admin' permissions on the project using the reservation and the project that owns this reservation.</p>
<p>Returns <code dir="ltr" translate="no">           google.rpc.Code.INVALID_ARGUMENT          </code> when location of the assignment does not match location of the reservation.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateCapacityCommitment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateCapacityCommitment(                         CreateCapacityCommitmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              CapacityCommitment            </code> )</p>
<p>Creates a new capacity commitment resource.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateReservation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateReservation(                         CreateReservationRequest            </code> ) returns ( <code dir="ltr" translate="no">              Reservation            </code> )</p>
<p>Creates a new reservation resource.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateReservationGroup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateReservationGroup(                         CreateReservationGroupRequest            </code> ) returns ( <code dir="ltr" translate="no">              ReservationGroup            </code> )</p>
<p>Creates a new reservation group.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteAssignment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteAssignment(                         DeleteAssignmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes a assignment. No expansion will happen.</p>
<p>Example:</p>
<ul>
<li>Organization <code dir="ltr" translate="no">            organizationA           </code> contains two projects, <code dir="ltr" translate="no">            project1           </code> and <code dir="ltr" translate="no">            project2           </code> .</li>
<li>Reservation <code dir="ltr" translate="no">            res1           </code> exists and was created previously.</li>
<li>CreateAssignment was used previously to define the following associations between entities and reservations: <code dir="ltr" translate="no">            &lt;organizationA, res1&gt;           </code> and <code dir="ltr" translate="no">            &lt;project1, res1&gt;           </code></li>
</ul>
<p>In this example, deletion of the <code dir="ltr" translate="no">           &lt;organizationA, res1&gt;          </code> assignment won't affect the other assignment <code dir="ltr" translate="no">           &lt;project1, res1&gt;          </code> . After said deletion, queries from <code dir="ltr" translate="no">           project1          </code> will still use <code dir="ltr" translate="no">           res1          </code> while queries from <code dir="ltr" translate="no">           project2          </code> will switch to use on-demand mode.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteCapacityCommitment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteCapacityCommitment(                         DeleteCapacityCommitmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes a capacity commitment. Attempting to delete capacity commitment before its commitment_end_time will fail with the error code <code dir="ltr" translate="no">           google.rpc.Code.FAILED_PRECONDITION          </code> .</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteReservation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteReservation(                         DeleteReservationRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes a reservation. Returns <code dir="ltr" translate="no">           google.rpc.Code.FAILED_PRECONDITION          </code> when reservation has assignments.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteReservationGroup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteReservationGroup(                         DeleteReservationGroupRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes a reservation. Returns <code dir="ltr" translate="no">           google.rpc.Code.FAILED_PRECONDITION          </code> when reservation has assignments.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>FailoverReservation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc FailoverReservation(                         FailoverReservationRequest            </code> ) returns ( <code dir="ltr" translate="no">              Reservation            </code> )</p>
<p>Fail over a reservation to the secondary location. The operation should be done in the current secondary location, which will be promoted to the new primary location for the reservation. Attempting to failover a reservation in the current primary location will fail with the error code <code dir="ltr" translate="no">           google.rpc.Code.FAILED_PRECONDITION          </code> .</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetBiReservation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetBiReservation(                         GetBiReservationRequest            </code> ) returns ( <code dir="ltr" translate="no">              BiReservation            </code> )</p>
<p>Retrieves a BI reservation.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetCapacityCommitment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetCapacityCommitment(                         GetCapacityCommitmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              CapacityCommitment            </code> )</p>
<p>Returns information about the capacity commitment.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetIamPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetIamPolicy(                         GetIamPolicyRequest            </code> ) returns ( <code dir="ltr" translate="no">              Policy            </code> )</p>
<p>Gets the access control policy for a resource. May return:</p>
<ul>
<li>A <code dir="ltr" translate="no">            NOT_FOUND           </code> error if the resource doesn't exist or you don't have the permission to view it.</li>
<li>An empty policy if the resource exists but doesn't have a set policy.</li>
</ul>
<p>Supported resources are: - Reservations - ReservationAssignments</p>
<p>To call this method, you must have the following Google IAM permissions:</p>
<ul>
<li><code dir="ltr" translate="no">            bigqueryreservation.reservations.getIamPolicy           </code> to get policies on reservations.</li>
</ul>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetReservation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetReservation(                         GetReservationRequest            </code> ) returns ( <code dir="ltr" translate="no">              Reservation            </code> )</p>
<p>Returns information about the reservation.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetReservationGroup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetReservationGroup(                         GetReservationGroupRequest            </code> ) returns ( <code dir="ltr" translate="no">              ReservationGroup            </code> )</p>
<p>Returns information about the reservation group.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListAssignments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListAssignments(                         ListAssignmentsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListAssignmentsResponse            </code> )</p>
<p>Lists assignments.</p>
<p>Only explicitly created assignments will be returned.</p>
<p>Example:</p>
<ul>
<li>Organization <code dir="ltr" translate="no">            organizationA           </code> contains two projects, <code dir="ltr" translate="no">            project1           </code> and <code dir="ltr" translate="no">            project2           </code> .</li>
<li>Reservation <code dir="ltr" translate="no">            res1           </code> exists and was created previously.</li>
<li>CreateAssignment was used previously to define the following associations between entities and reservations: <code dir="ltr" translate="no">            &lt;organizationA, res1&gt;           </code> and <code dir="ltr" translate="no">            &lt;project1, res1&gt;           </code></li>
</ul>
<p>In this example, ListAssignments will just return the above two assignments for reservation <code dir="ltr" translate="no">           res1          </code> , and no expansion/merge will happen.</p>
<p>The wildcard "-" can be used for reservations in the request. In that case all assignments belongs to the specified project and location will be listed.</p>
<p><strong>Note</strong> "-" cannot be used for projects nor locations.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListCapacityCommitments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListCapacityCommitments(                         ListCapacityCommitmentsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListCapacityCommitmentsResponse            </code> )</p>
<p>Lists all the capacity commitments for the admin project.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListReservationGroups</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListReservationGroups(                         ListReservationGroupsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListReservationGroupsResponse            </code> )</p>
<p>Lists all the reservation groups for the project in the specified location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListReservations</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListReservations(                         ListReservationsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListReservationsResponse            </code> )</p>
<p>Lists all the reservations for the project in the specified location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>MergeCapacityCommitments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc MergeCapacityCommitments(                         MergeCapacityCommitmentsRequest            </code> ) returns ( <code dir="ltr" translate="no">              CapacityCommitment            </code> )</p>
<p>Merges capacity commitments of the same plan into a single commitment.</p>
<p>The resulting capacity commitment has the greater commitment_end_time out of the to-be-merged capacity commitments.</p>
<p>Attempting to merge capacity commitments of different plan will fail with the error code <code dir="ltr" translate="no">           google.rpc.Code.FAILED_PRECONDITION          </code> .</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>MoveAssignment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc MoveAssignment(                         MoveAssignmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              Assignment            </code> )</p>
<p>Moves an assignment under a new reservation.</p>
<p>This differs from removing an existing assignment and recreating a new one by providing a transactional change that ensures an assignee always has an associated reservation.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SearchAllAssignments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc SearchAllAssignments(                         SearchAllAssignmentsRequest            </code> ) returns ( <code dir="ltr" translate="no">              SearchAllAssignmentsResponse            </code> )</p>
<p>Looks up assignments for a specified resource for a particular region. If the request is about a project:</p>
<ol>
<li>Assignments created on the project will be returned if they exist.</li>
<li>Otherwise assignments created on the closest ancestor will be returned.</li>
<li>Assignments for different JobTypes will all be returned.</li>
</ol>
<p>The same logic applies if the request is about a folder.</p>
<p>If the request is about an organization, then assignments created on the organization will be returned (organization doesn't have ancestors).</p>
<p>Comparing to ListAssignments, there are some behavior differences:</p>
<ol>
<li>permission on the assignee will be verified in this API.</li>
<li>Hierarchy lookup (project-&gt;folder-&gt;organization) happens in this API.</li>
<li>Parent here is <code dir="ltr" translate="no">            projects/*/locations/*           </code> , instead of <code dir="ltr" translate="no">            projects/*/locations/*reservations/*           </code> .</li>
</ol>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SearchAssignments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>This item is deprecated!</p>
<p><code dir="ltr" translate="no">           rpc SearchAssignments(                         SearchAssignmentsRequest            </code> ) returns ( <code dir="ltr" translate="no">              SearchAssignmentsResponse            </code> )</p>
<p>Deprecated: Looks up assignments for a specified resource for a particular region. If the request is about a project:</p>
<ol>
<li>Assignments created on the project will be returned if they exist.</li>
<li>Otherwise assignments created on the closest ancestor will be returned.</li>
<li>Assignments for different JobTypes will all be returned.</li>
</ol>
<p>The same logic applies if the request is about a folder.</p>
<p>If the request is about an organization, then assignments created on the organization will be returned (organization doesn't have ancestors).</p>
<p>Comparing to ListAssignments, there are some behavior differences:</p>
<ol>
<li>permission on the assignee will be verified in this API.</li>
<li>Hierarchy lookup (project-&gt;folder-&gt;organization) happens in this API.</li>
<li>Parent here is <code dir="ltr" translate="no">            projects/*/locations/*           </code> , instead of <code dir="ltr" translate="no">            projects/*/locations/*reservations/*           </code> .</li>
</ol>
<p><strong>Note</strong> "-" cannot be used for projects nor locations.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SetIamPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc SetIamPolicy(                         SetIamPolicyRequest            </code> ) returns ( <code dir="ltr" translate="no">              Policy            </code> )</p>
<p>Sets an access control policy for a resource. Replaces any existing policy.</p>
<p>Supported resources are: - Reservations</p>
<p>To call this method, you must have the following Google IAM permissions:</p>
<ul>
<li><code dir="ltr" translate="no">            bigqueryreservation.reservations.setIamPolicy           </code> to set policies on reservations.</li>
</ul>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SplitCapacityCommitment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc SplitCapacityCommitment(                         SplitCapacityCommitmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              SplitCapacityCommitmentResponse            </code> )</p>
<p>Splits capacity commitment to two commitments of the same plan and <code dir="ltr" translate="no">           commitment_end_time          </code> .</p>
<p>A common use case is to enable downgrading commitments.</p>
<p>For example, in order to downgrade from 10000 slots to 8000, you might split a 10000 capacity commitment into commitments of 2000 and 8000. Then, you delete the first one after the commitment end time passes.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>TestIamPermissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc TestIamPermissions(                         TestIamPermissionsRequest            </code> ) returns ( <code dir="ltr" translate="no">              TestIamPermissionsResponse            </code> )</p>
<p>Gets your permissions on a resource. Returns an empty set of permissions if the resource doesn't exist.</p>
<p>Supported resources are: - Reservations</p>
<p>No Google IAM permissions are required to call this method.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateAssignment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UpdateAssignment(                         UpdateAssignmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              Assignment            </code> )</p>
<p>Updates an existing assignment.</p>
<p>Only the <code dir="ltr" translate="no">           priority          </code> field can be updated.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateBiReservation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UpdateBiReservation(                         UpdateBiReservationRequest            </code> ) returns ( <code dir="ltr" translate="no">              BiReservation            </code> )</p>
<p>Updates a BI reservation.</p>
<p>Only fields specified in the <code dir="ltr" translate="no">           field_mask          </code> are updated.</p>
<p>A singleton BI reservation always exists with default size 0. In order to reserve BI capacity it needs to be updated to an amount greater than 0. In order to release BI capacity reservation size must be set to 0.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateCapacityCommitment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UpdateCapacityCommitment(                         UpdateCapacityCommitmentRequest            </code> ) returns ( <code dir="ltr" translate="no">              CapacityCommitment            </code> )</p>
<p>Updates an existing capacity commitment.</p>
<p>Only <code dir="ltr" translate="no">           plan          </code> and <code dir="ltr" translate="no">           renewal_plan          </code> fields can be updated.</p>
<p>Plan can only be changed to a plan of a longer commitment period. Attempting to change to a plan with shorter commitment period will fail with the error code <code dir="ltr" translate="no">           google.rpc.Code.FAILED_PRECONDITION          </code> .</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateReservation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UpdateReservation(                         UpdateReservationRequest            </code> ) returns ( <code dir="ltr" translate="no">              Reservation            </code> )</p>
<p>Updates an existing reservation resource.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## Assignment

An assignment allows a project to submit jobs of a certain type using slots from the specified reservation.

Fields

`  name  `

`  string  `

Output only. Name of the resource. E.g.: `  projects/myproject/locations/US/reservations/team1-prod/assignments/123  ` . The assignment\_id must only contain lower case alphanumeric characters or dashes and the max length is 64 characters.

`  assignee  `

`  string  `

Optional. The resource which will use the reservation. E.g. `  projects/myproject  ` , `  folders/123  ` , or `  organizations/456  ` .

`  job_type  `

`  JobType  `

Optional. Which type of jobs will use the reservation.

`  state  `

`  State  `

Output only. State of the assignment.

## JobType

Types of job, which could be specified when using the reservation.

Enums

`  JOB_TYPE_UNSPECIFIED  `

Invalid type. Requests with this value will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

`  PIPELINE  `

Pipeline (load/export) jobs from the project will use the reservation.

`  QUERY  `

Query jobs from the project will use the reservation.

`  ML_EXTERNAL  `

BigQuery ML jobs that use services external to BigQuery for model training. These jobs will not utilize idle slots from other reservations.

`  BACKGROUND  `

Background jobs that BigQuery runs for the customers in the background.

`  CONTINUOUS  `

Continuous SQL jobs will use this reservation. Reservations with continuous assignments cannot be mixed with non-continuous assignments.

`  BACKGROUND_CHANGE_DATA_CAPTURE  `

Finer granularity background jobs for capturing changes in a source database and streaming them into BigQuery. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists).

`  BACKGROUND_COLUMN_METADATA_INDEX  `

Finer granularity background jobs for refreshing cached metadata for BigQuery tables. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists).

`  BACKGROUND_SEARCH_INDEX_REFRESH  `

Finer granularity background jobs for refreshing search indexes upon BigQuery table columns. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists).

## State

Assignment will remain in PENDING state if no active capacity commitment is present. It will become ACTIVE when some capacity commitment becomes active.

Enums

`  STATE_UNSPECIFIED  `

Invalid state value.

`  PENDING  `

Queries from assignee will be executed as on-demand, if related assignment is pending.

`  ACTIVE  `

Assignment is ready.

## BiReservation

Represents a BI Reservation.

Fields

`  name  `

`  string  `

Identifier. The resource name of the singleton BI reservation. Reservation names have the form `  projects/{project_id}/locations/{location_id}/biReservation  ` .

`  update_time  `

`  Timestamp  `

Output only. The last update timestamp of a reservation.

`  size  `

`  int64  `

Optional. Size of a reservation, in bytes.

`  preferred_tables[]  `

`  TableReference  `

Optional. Preferred tables to use BI capacity for.

## CapacityCommitment

Capacity commitment is a way to purchase compute capacity for BigQuery jobs (in the form of slots) with some committed period of usage. Annual commitments renew by default. Commitments can be removed after their commitment end time passes.

In order to remove annual commitment, its plan needs to be changed to monthly or flex first.

A capacity commitment resource exists as a child resource of the admin project.

Fields

`  name  `

`  string  `

Output only. The resource name of the capacity commitment, e.g., `  projects/myproject/locations/US/capacityCommitments/123  ` The commitment\_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.

`  slot_count  `

`  int64  `

Optional. Number of slots in this commitment.

`  plan  `

`  CommitmentPlan  `

Optional. Capacity commitment commitment plan.

`  state  `

`  State  `

Output only. State of the commitment.

`  commitment_start_time  `

`  Timestamp  `

Output only. The start of the current commitment period. It is applicable only for ACTIVE capacity commitments. Note after the commitment is renewed, commitment\_start\_time won't be changed. It refers to the start time of the original commitment.

`  commitment_end_time  `

`  Timestamp  `

Output only. The end of the current commitment period. It is applicable only for ACTIVE capacity commitments. Note after renewal, commitment\_end\_time is the time the renewed commitment expires. So itwould be at a time after commitment\_start\_time + committed period, because we don't change commitment\_start\_time ,

`  failure_status  `

`  Status  `

Output only. For FAILED commitment plan, provides the reason of failure.

`  renewal_plan  `

`  CommitmentPlan  `

Optional. The plan this capacity commitment is converted to after commitment\_end\_time passes. Once the plan is changed, committed period is extended according to commitment plan. Only applicable for ANNUAL and TRIAL commitments.

`  edition  `

`  Edition  `

Optional. Edition of the capacity commitment.

`  is_flat_rate  `

`  bool  `

Output only. If true, the commitment is a flat-rate commitment, otherwise, it's an edition commitment.

## CommitmentPlan

Commitment plan defines the current committed period. Capacity commitment cannot be deleted during it's committed period.

Enums

`  COMMITMENT_PLAN_UNSPECIFIED  `

Invalid plan value. Requests with this value will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

`  FLEX  `

Flex commitments have committed period of 1 minute after becoming ACTIVE. After that, they are not in a committed period anymore and can be removed any time.

`  FLEX_FLAT_RATE  `

Same as FLEX, should only be used if flat-rate commitments are still available.

This item is deprecated\!

`  TRIAL  `

Trial commitments have a committed period of 182 days after becoming ACTIVE. After that, they are converted to a new commitment based on the `  renewal_plan  ` . Default `  renewal_plan  ` for Trial commitment is Flex so that it can be deleted right after committed period ends.

This item is deprecated\!

`  MONTHLY  `

Monthly commitments have a committed period of 30 days after becoming ACTIVE. After that, they are not in a committed period anymore and can be removed any time.

`  MONTHLY_FLAT_RATE  `

Same as MONTHLY, should only be used if flat-rate commitments are still available.

This item is deprecated\!

`  ANNUAL  `

Annual commitments have a committed period of 365 days after becoming ACTIVE. After that they are converted to a new commitment based on the renewal\_plan.

`  ANNUAL_FLAT_RATE  `

Same as ANNUAL, should only be used if flat-rate commitments are still available.

This item is deprecated\!

`  THREE_YEAR  `

3-year commitments have a committed period of 1095(3 \* 365) days after becoming ACTIVE. After that they are converted to a new commitment based on the renewal\_plan.

`  NONE  `

Should only be used for `  renewal_plan  ` and is only meaningful if edition is specified to values other than EDITION\_UNSPECIFIED. Otherwise CreateCapacityCommitmentRequest or UpdateCapacityCommitmentRequest will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` . If the renewal\_plan is NONE, capacity commitment will be removed at the end of its commitment period.

## State

Capacity commitment can either become ACTIVE right away or transition from PENDING to ACTIVE or FAILED.

Enums

`  STATE_UNSPECIFIED  `

Invalid state value.

`  PENDING  `

Capacity commitment is pending provisioning. Pending capacity commitment does not contribute to the project's slot\_capacity.

`  ACTIVE  `

Once slots are provisioned, capacity commitment becomes active. slot\_count is added to the project's slot\_capacity.

`  FAILED  `

Capacity commitment is failed to be activated by the backend.

## CreateAssignmentRequest

The request for `  ReservationService.CreateAssignment  ` . Note: "bigquery.reservationAssignments.create" permission is required on the related assignee.

Fields

`  parent  `

`  string  `

Required. The parent resource name of the assignment E.g. `  projects/myproject/locations/US/reservations/team1-prod  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservationAssignments.create  `

`  assignment  `

`  Assignment  `

Assignment resource to create.

`  assignment_id  `

`  string  `

The optional assignment ID. Assignment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. Max length is 64 characters.

## CreateCapacityCommitmentRequest

The request for `  ReservationService.CreateCapacityCommitment  ` .

Fields

`  parent  `

`  string  `

Required. Resource name of the parent reservation. E.g., `  projects/myproject/locations/US  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.capacityCommitments.create  `

`  capacity_commitment  `

`  CapacityCommitment  `

Content of the capacity commitment to create.

`  enforce_single_admin_project_per_org  `

`  bool  `

If true, fail the request if another project in the organization has a capacity commitment.

`  capacity_commitment_id  `

`  string  `

The optional capacity commitment ID. Capacity commitment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. The first and last character cannot be a dash. Max length is 64 characters. NOTE: this ID won't be kept if the capacity commitment is split or merged.

## CreateReservationGroupRequest

The request for `  ReservationService.CreateReservationGroup  ` .

Fields

`  parent  `

`  string  `

Required. Project, location. E.g., `  projects/myproject/locations/US  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservationGroups.create  `

`  reservation_group_id  `

`  string  `

Required. The reservation group ID. It must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.

`  reservation_group  `

`  ReservationGroup  `

Required. New Reservation Group to create.

## CreateReservationRequest

The request for `  ReservationService.CreateReservation  ` .

Fields

`  parent  `

`  string  `

Required. Project, location. E.g., `  projects/myproject/locations/US  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservations.create  `

`  reservation_id  `

`  string  `

The reservation ID. It must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.

`  reservation  `

`  Reservation  `

Definition of the new reservation to create.

## DeleteAssignmentRequest

The request for `  ReservationService.DeleteAssignment  ` . Note: "bigquery.reservationAssignments.delete" permission is required on the related assignee.

Fields

`  name  `

`  string  `

Required. Name of the resource, e.g. `  projects/myproject/locations/US/reservations/team1-prod/assignments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservationAssignments.delete  `

## DeleteCapacityCommitmentRequest

The request for `  ReservationService.DeleteCapacityCommitment  ` .

Fields

`  name  `

`  string  `

Required. Resource name of the capacity commitment to delete. E.g., `  projects/myproject/locations/US/capacityCommitments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.capacityCommitments.delete  `

`  force  `

`  bool  `

Can be used to force delete commitments even if assignments exist. Deleting commitments with assignments may cause queries to fail if they no longer have access to slots.

## DeleteReservationGroupRequest

The request for `  ReservationService.DeleteReservationGroup  ` .

Fields

`  name  `

`  string  `

Required. Resource name of the reservation group to retrieve. E.g., `  projects/myproject/locations/US/reservationGroups/team1-prod  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservationGroups.delete  `

## DeleteReservationRequest

The request for `  ReservationService.DeleteReservation  ` .

Fields

`  name  `

`  string  `

Required. Resource name of the reservation to retrieve. E.g., `  projects/myproject/locations/US/reservations/team1-prod  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservations.delete  `

## Edition

The type of editions. Different features and behaviors are provided to different editions Capacity commitments and reservations are linked to editions.

Enums

`  EDITION_UNSPECIFIED  `

Default value, which will be treated as ENTERPRISE.

`  STANDARD  `

Standard edition.

`  ENTERPRISE  `

Enterprise edition.

`  ENTERPRISE_PLUS  `

Enterprise Plus edition.

## FailoverMode

The failover mode when a user initiates a failover on a reservation determines how writes that are pending replication are handled after the failover is initiated.

Enums

`  FAILOVER_MODE_UNSPECIFIED  `

Invalid value.

`  SOFT  `

When customers initiate a soft failover, BigQuery will wait until all committed writes are replicated to the secondary. This mode requires both regions to be available for the failover to succeed and prevents data loss.

`  HARD  `

When customers initiate a hard failover, BigQuery will not wait until all committed writes are replicated to the secondary. There can be data loss for hard failover.

## FailoverReservationRequest

The request for ReservationService.FailoverReservation.

Fields

`  name  `

`  string  `

Required. Resource name of the reservation to failover. E.g., `  projects/myproject/locations/US/reservations/team1-prod  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservations.update  `

`  failover_mode  `

`  FailoverMode  `

Optional. A parameter that determines how writes that are pending replication are handled after a failover is initiated. If not specified, HARD failover mode is used by default.

## GetBiReservationRequest

A request to get a singleton BI reservation.

Fields

`  name  `

`  string  `

Required. Name of the requested reservation, for example: `  projects/{project_id}/locations/{location_id}/biReservation  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.bireservations.get  `

## GetCapacityCommitmentRequest

The request for `  ReservationService.GetCapacityCommitment  ` .

Fields

`  name  `

`  string  `

Required. Resource name of the capacity commitment to retrieve. E.g., `  projects/myproject/locations/US/capacityCommitments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.capacityCommitments.get  `

## GetReservationGroupRequest

The request for `  ReservationService.GetReservationGroup  ` .

Fields

`  name  `

`  string  `

Required. Resource name of the reservation group to retrieve. E.g., `  projects/myproject/locations/US/reservationGroups/team1-prod  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservationGroups.get  `

## GetReservationRequest

The request for `  ReservationService.GetReservation  ` .

Fields

`  name  `

`  string  `

Required. Resource name of the reservation to retrieve. E.g., `  projects/myproject/locations/US/reservations/team1-prod  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservations.get  `

## ListAssignmentsRequest

The request for `  ReservationService.ListAssignments  ` .

Fields

`  parent  `

`  string  `

Required. The parent resource name e.g.:

`  projects/myproject/locations/US/reservations/team1-prod  `

Or:

`  projects/myproject/locations/US/reservations/-  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservationAssignments.list  `

`  page_size  `

`  int32  `

The maximum number of items to return per page.

`  page_token  `

`  string  `

The next\_page\_token value returned from a previous List request, if any.

## ListAssignmentsResponse

The response for `  ReservationService.ListAssignments  ` .

Fields

`  assignments[]  `

`  Assignment  `

List of assignments visible to the user.

`  next_page_token  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

## ListCapacityCommitmentsRequest

The request for `  ReservationService.ListCapacityCommitments  ` .

Fields

`  parent  `

`  string  `

Required. Resource name of the parent reservation. E.g., `  projects/myproject/locations/US  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.capacityCommitments.list  `

`  page_size  `

`  int32  `

The maximum number of items to return.

`  page_token  `

`  string  `

The next\_page\_token value returned from a previous List request, if any.

## ListCapacityCommitmentsResponse

The response for `  ReservationService.ListCapacityCommitments  ` .

Fields

`  capacity_commitments[]  `

`  CapacityCommitment  `

List of capacity commitments visible to the user.

`  next_page_token  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

## ListReservationGroupsRequest

The request for `  ReservationService.ListReservationGroups  ` .

Fields

`  parent  `

`  string  `

Required. The parent resource name containing project and location, e.g.: `  projects/myproject/locations/US  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservationGroups.list  `

`  page_size  `

`  int32  `

The maximum number of items to return per page.

`  page_token  `

`  string  `

The next\_page\_token value returned from a previous List request, if any.

## ListReservationGroupsResponse

The response for `  ReservationService.ListReservationGroups  ` .

Fields

`  reservation_groups[]  `

`  ReservationGroup  `

List of reservations visible to the user.

`  next_page_token  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

## ListReservationsRequest

The request for `  ReservationService.ListReservations  ` .

Fields

`  parent  `

`  string  `

Required. The parent resource name containing project and location, e.g.: `  projects/myproject/locations/US  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservations.list  `

`  page_size  `

`  int32  `

The maximum number of items to return per page.

`  page_token  `

`  string  `

The next\_page\_token value returned from a previous List request, if any.

## ListReservationsResponse

The response for `  ReservationService.ListReservations  ` .

Fields

`  reservations[]  `

`  Reservation  `

List of reservations visible to the user.

`  next_page_token  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

## MergeCapacityCommitmentsRequest

The request for `  ReservationService.MergeCapacityCommitments  ` .

Fields

`  parent  `

`  string  `

Parent resource that identifies admin project and location e.g., `  projects/myproject/locations/us  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.capacityCommitments.update  `

`  capacity_commitment_ids[]  `

`  string  `

Ids of capacity commitments to merge. These capacity commitments must exist under admin project and location specified in the parent. ID is the last portion of capacity commitment name e.g., 'abc' for projects/myproject/locations/US/capacityCommitments/abc

`  capacity_commitment_id  `

`  string  `

Optional. The optional resulting capacity commitment ID. Capacity commitment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. The first and last character cannot be a dash. Max length is 64 characters.

## MoveAssignmentRequest

The request for `  ReservationService.MoveAssignment  ` .

**Note** : "bigquery.reservationAssignments.create" permission is required on the destination\_id.

**Note** : "bigquery.reservationAssignments.create" and "bigquery.reservationAssignments.delete" permission are required on the related assignee.

Fields

`  name  `

`  string  `

Required. The resource name of the assignment, e.g. `  projects/myproject/locations/US/reservations/team1-prod/assignments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.reservationAssignments.delete  `

`  destination_id  `

`  string  `

The new reservation ID, e.g.: `  projects/myotherproject/locations/US/reservations/team2-prod  `

`  assignment_id  `

`  string  `

The optional assignment ID. A new assignment name is generated if this field is empty.

This field can contain only lowercase alphanumeric characters or dashes. Max length is 64 characters.

## Reservation

A reservation is a mechanism used to guarantee slots to users.

Fields

`  name  `

`  string  `

Identifier. The resource name of the reservation, e.g., `  projects/*/locations/*/reservations/team1-prod  ` . The reservation\_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.

`  slot_capacity  `

`  int64  `

Optional. Baseline slots available to this reservation. A slot is a unit of computational power in BigQuery, and serves as the unit of parallelism.

Queries using this reservation might use more slots during runtime if ignore\_idle\_slots is set to false, or autoscaling is enabled.

The total slot\_capacity of the reservation and its siblings may exceed the total slot\_count of capacity commitments. In that case, the exceeding slots will be charged with the autoscale SKU. You can increase the number of baseline slots in a reservation every few minutes. If you want to decrease your baseline slots, you are limited to once an hour if you have recently changed your baseline slot capacity and your baseline slots exceed your committed slots. Otherwise, you can decrease your baseline slots every few minutes.

`  ignore_idle_slots  `

`  bool  `

Optional. If false, any query or pipeline job using this reservation will use idle slots from other reservations within the same admin project. If true, a query or pipeline job using this reservation will execute with the slot capacity specified in the slot\_capacity field at most.

`  autoscale  `

`  Autoscale  `

Optional. The configuration parameters for the auto scaling feature.

`  concurrency  `

`  int64  `

Optional. Job concurrency target which sets a soft upper bound on the number of jobs that can run concurrently in this reservation. This is a soft target due to asynchronous nature of the system and various optimizations for small queries. Default value is 0 which means that concurrency target will be automatically computed by the system. NOTE: this field is exposed as target job concurrency in the Information Schema, DDL and BigQuery CLI.

`  creation_time  `

`  Timestamp  `

Output only. Creation time of the reservation.

`  update_time  `

`  Timestamp  `

Output only. Last update time of the reservation.

`  edition  `

`  Edition  `

Optional. Edition of the reservation.

`  primary_location  `

`  string  `

Output only. The current location of the reservation's primary replica. This field is only set for reservations using the managed disaster recovery feature.

`  secondary_location  `

`  string  `

Optional. The current location of the reservation's secondary replica. This field is only set for reservations using the managed disaster recovery feature. Users can set this in create reservation calls to create a failover reservation or in update reservation calls to convert a non-failover reservation to a failover reservation(or vice versa).

`  original_primary_location  `

`  string  `

Output only. The location where the reservation was originally created. This is set only during the failover reservation's creation. All billing charges for the failover reservation will be applied to this location.

`  scaling_mode  `

`  ScalingMode  `

Optional. The scaling mode for the reservation. If the field is present but max\_slots is not present, requests will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

`  reservation_group  `

`  string  `

Optional. The reservation group that this reservation belongs to. You can set this property when you create or update a reservation. Reservations do not need to belong to a reservation group. Format: projects/{project}/locations/{location}/reservationGroups/{reservation\_group} or just {reservation\_group}

`  replication_status  `

`  ReplicationStatus  `

Output only. The Disaster Recovery(DR) replication status of the reservation. This is only available for the primary replicas of DR/failover reservations and provides information about the both the staleness of the secondary and the last error encountered while trying to replicate changes from the primary to the secondary. If this field is blank, it means that the reservation is either not a DR reservation or the reservation is a DR secondary or that any replication operations on the reservation have succeeded.

`  max_slots  `

`  int64  `

Optional. The overall max slots for the reservation, covering slot\_capacity (baseline), idle slots (if ignore\_idle\_slots is false) and scaled slots. If present, the reservation won't use more than the specified number of slots, even if there is demand and supply (from idle slots). NOTE: capping a reservation's idle slot usage is best effort and its usage may exceed the max\_slots value. However, in terms of autoscale.current\_slots (which accounts for the additional added slots), it will never exceed the max\_slots - baseline.

This field must be set together with the scaling\_mode enum value, otherwise the request will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

If the max\_slots and scaling\_mode are set, the autoscale or autoscale.max\_slots field must be unset. Otherwise the request will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` . However, the autoscale field may still be in the output. The autopscale.max\_slots will always show as 0 and the autoscaler.current\_slots will represent the current slots from autoscaler excluding idle slots. For example, if the max\_slots is 1000 and scaling\_mode is AUTOSCALE\_ONLY, then in the output, the autoscaler.max\_slots will be 0 and the autoscaler.current\_slots may be any value between 0 and 1000.

If the max\_slots is 1000, scaling\_mode is ALL\_SLOTS, the baseline is 100 and idle slots usage is 200, then in the output, the autoscaler.max\_slots will be 0 and the autoscaler.current\_slots will not be higher than 700.

If the max\_slots is 1000, scaling\_mode is IDLE\_SLOTS\_ONLY, then in the output, the autoscaler field will be null.

If the max\_slots and scaling\_mode are set, then the ignore\_idle\_slots field must be aligned with the scaling\_mode enum value.(See details in ScalingMode comments). Otherwise the request will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

Please note, the max\_slots is for user to manage the part of slots greater than the baseline. Therefore, we don't allow users to set max\_slots smaller or equal to the baseline as it will not be meaningful. If the field is present and slot\_capacity\>=max\_slots, requests will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

Please note that if max\_slots is set to 0, we will treat it as unset. Customers can set max\_slots to 0 and set scaling\_mode to SCALING\_MODE\_UNSPECIFIED to disable the max\_slots feature.

## Autoscale

Auto scaling settings.

Fields

`  current_slots  `

`  int64  `

Output only. The slot capacity added to this reservation when autoscale happens. Will be between \[0, max\_slots\]. Note: after users reduce max\_slots, it may take a while before it can be propagated, so current\_slots may stay in the original value and could be larger than max\_slots for that brief period (less than one minute)

`  max_slots  `

`  int64  `

Optional. Number of slots to be scaled when needed.

## ReplicationStatus

Disaster Recovery(DR) replication status of the reservation.

Fields

`  error  `

`  Status  `

Output only. The last error encountered while trying to replicate changes from the primary to the secondary. This field is only available if the replication has not succeeded since.

`  last_error_time  `

`  Timestamp  `

Output only. The time at which the last error was encountered while trying to replicate changes from the primary to the secondary. This field is only available if the replication has not succeeded since.

`  last_replication_time  `

`  Timestamp  `

Output only. A timestamp corresponding to the last change on the primary that was successfully replicated to the secondary.

`  soft_failover_start_time  `

`  Timestamp  `

Output only. The time at which a soft failover for the reservation and its associated datasets was initiated. After this field is set, all subsequent changes to the reservation will be rejected unless a hard failover overrides this operation. This field will be cleared once the failover is complete.

## ScalingMode

The scaling mode for the reservation. This enum determines how the reservation scales up and down.

Enums

`  SCALING_MODE_UNSPECIFIED  `

Default value of ScalingMode.

`  AUTOSCALE_ONLY  `

The reservation will scale up only using slots from autoscaling. It will not use any idle slots even if there may be some available. The upper limit that autoscaling can scale up to will be max\_slots - baseline. For example, if max\_slots is 1000, baseline is 200 and customer sets ScalingMode to AUTOSCALE\_ONLY, then autoscalerg will scale up to 800 slots and no idle slots will be used.

Please note, in this mode, the ignore\_idle\_slots field must be set to true. Otherwise the request will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

`  IDLE_SLOTS_ONLY  `

The reservation will scale up using only idle slots contributed by other reservations or from unassigned commitments. If no idle slots are available it will not scale up further. If the idle slots which it is using are reclaimed by the contributing reservation(s) it may be forced to scale down. The max idle slots the reservation can be max\_slots - baseline capacity. For example, if max\_slots is 1000, baseline is 200 and customer sets ScalingMode to IDLE\_SLOTS\_ONLY, 1. if there are 1000 idle slots available in other reservations, the reservation will scale up to 1000 slots with 200 baseline and 800 idle slots. 2. if there are 500 idle slots available in other reservations, the reservation will scale up to 700 slots with 200 baseline and 300 idle slots. Please note, in this mode, the reservation might not be able to scale up to max\_slots.

Please note, in this mode, the ignore\_idle\_slots field must be set to false. Otherwise the request will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

`  ALL_SLOTS  `

The reservation will scale up using all slots available to it. It will use idle slots contributed by other reservations or from unassigned commitments first. If no idle slots are available it will scale up using autoscaling. For example, if max\_slots is 1000, baseline is 200 and customer sets ScalingMode to ALL\_SLOTS, 1. if there are 800 idle slots available in other reservations, the reservation will scale up to 1000 slots with 200 baseline and 800 idle slots. 2. if there are 500 idle slots available in other reservations, the reservation will scale up to 1000 slots with 200 baseline, 500 idle slots and 300 autoscaling slots. 3. if there are no idle slots available in other reservations, it will scale up to 1000 slots with 200 baseline and 800 autoscaling slots.

Please note, in this mode, the ignore\_idle\_slots field must be set to false. Otherwise the request will be rejected with error code `  google.rpc.Code.INVALID_ARGUMENT  ` .

## ReservationGroup

A reservation group is a container for reservations.

Fields

`  name  `

`  string  `

Identifier. The resource name of the reservation group, e.g., `  projects/*/locations/*/reservationGroups/team1-prod  ` . The reservation\_group\_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.

## SearchAllAssignmentsRequest

The request for `  ReservationService.SearchAllAssignments  ` . Note: "bigquery.reservationAssignments.search" permission is required on the related assignee.

Fields

`  parent  `

`  string  `

Required. The resource name with location (project name could be the wildcard '-'), e.g.: `  projects/-/locations/US  ` .

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservationAssignments.search  `

`  query  `

`  string  `

Please specify resource name as assignee in the query.

Examples:

  - `  assignee=projects/myproject  `
  - `  assignee=folders/123  `
  - `  assignee=organizations/456  `

`  page_size  `

`  int32  `

The maximum number of items to return per page.

`  page_token  `

`  string  `

The next\_page\_token value returned from a previous List request, if any.

## SearchAllAssignmentsResponse

The response for `  ReservationService.SearchAllAssignments  ` .

Fields

`  assignments[]  `

`  Assignment  `

List of assignments visible to the user.

`  next_page_token  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

## SearchAssignmentsRequest

The request for `  ReservationService.SearchAssignments  ` . Note: "bigquery.reservationAssignments.search" permission is required on the related assignee.

Fields

`  parent  `

`  string  `

Required. The resource name of the admin project(containing project and location), e.g.: `  projects/myproject/locations/US  ` .

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.reservationAssignments.search  `

`  query  `

`  string  `

Please specify resource name as assignee in the query.

Examples:

  - `  assignee=projects/myproject  `
  - `  assignee=folders/123  `
  - `  assignee=organizations/456  `

`  page_size  `

`  int32  `

The maximum number of items to return per page.

`  page_token  `

`  string  `

The next\_page\_token value returned from a previous List request, if any.

## SearchAssignmentsResponse

The response for `  ReservationService.SearchAssignments  ` .

Fields

`  assignments[]  `

`  Assignment  `

List of assignments visible to the user.

`  next_page_token  `

`  string  `

Token to retrieve the next page of results, or empty if there are no more results in the list.

## SplitCapacityCommitmentRequest

The request for `  ReservationService.SplitCapacityCommitment  ` .

Fields

`  name  `

`  string  `

Required. The resource name e.g.,: `  projects/myproject/locations/US/capacityCommitments/123  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.capacityCommitments.update  `

`  slot_count  `

`  int64  `

Number of slots in the capacity commitment after the split.

## SplitCapacityCommitmentResponse

The response for `  ReservationService.SplitCapacityCommitment  ` .

Fields

`  first  `

`  CapacityCommitment  `

First capacity commitment, result of a split.

`  second  `

`  CapacityCommitment  `

Second capacity commitment, result of a split.

## TableReference

Fully qualified reference to BigQuery table. Internally stored as google.cloud.bi.v1.BqTableReference.

Fields

`  project_id  `

`  string  `

Optional. The assigned project ID of the project.

`  dataset_id  `

`  string  `

Optional. The ID of the dataset in the above project.

`  table_id  `

`  string  `

Optional. The ID of the table in the above dataset.

## UpdateAssignmentRequest

The request for `  ReservationService.UpdateAssignment  ` .

Fields

`  assignment  `

`  Assignment  `

Content of the assignment to update.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  assignment  ` :

  - `  bigquery.reservationassignments.update  `

`  update_mask  `

`  FieldMask  `

Standard field mask for the set of fields to be updated.

## UpdateBiReservationRequest

A request to update a BI reservation.

Fields

`  bi_reservation  `

`  BiReservation  `

A reservation to update.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  biReservation  ` :

  - `  bigquery.bireservations.update  `

`  update_mask  `

`  FieldMask  `

A list of fields to be updated in this request.

## UpdateCapacityCommitmentRequest

The request for `  ReservationService.UpdateCapacityCommitment  ` .

Fields

`  capacity_commitment  `

`  CapacityCommitment  `

Content of the capacity commitment to update.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  capacityCommitment  ` :

  - `  bigquery.capacityCommitments.update  `

`  update_mask  `

`  FieldMask  `

Standard field mask for the set of fields to be updated.

## UpdateReservationRequest

The request for `  ReservationService.UpdateReservation  ` .

Fields

`  reservation  `

`  Reservation  `

Content of the reservation to update.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  reservation  ` :

  - `  bigquery.reservations.update  `

`  update_mask  `

`  FieldMask  `

Standard field mask for the set of fields to be updated.

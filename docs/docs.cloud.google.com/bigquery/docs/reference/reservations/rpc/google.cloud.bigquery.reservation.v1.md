---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1
title: Package google.cloud.bigquery.reservation.v1
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

- [`ReservationService`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService) (interface)
- [`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment) (message)
- [`Assignment.JobType`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment.JobType) (enum)
- [`Assignment.State`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment.State) (enum)
- [`BiReservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.BiReservation) (message)
- [`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment) (message)
- [`CapacityCommitment.CommitmentPlan`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment.CommitmentPlan) (enum)
- [`CapacityCommitment.State`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment.State) (enum)
- [`CreateAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateAssignmentRequest) (message)
- [`CreateCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateCapacityCommitmentRequest) (message)
- [`CreateReservationGroupRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateReservationGroupRequest) (message)
- [`CreateReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateReservationRequest) (message)
- [`DeleteAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteAssignmentRequest) (message)
- [`DeleteCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteCapacityCommitmentRequest) (message)
- [`DeleteReservationGroupRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteReservationGroupRequest) (message)
- [`DeleteReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteReservationRequest) (message)
- [`Edition`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Edition) (enum)
- [`FailoverMode`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.FailoverMode) (enum)
- [`FailoverReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.FailoverReservationRequest) (message)
- [`GetBiReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetBiReservationRequest) (message)
- [`GetCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetCapacityCommitmentRequest) (message)
- [`GetReservationGroupRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetReservationGroupRequest) (message)
- [`GetReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetReservationRequest) (message)
- [`ListAssignmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListAssignmentsRequest) (message)
- [`ListAssignmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListAssignmentsResponse) (message)
- [`ListCapacityCommitmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListCapacityCommitmentsRequest) (message)
- [`ListCapacityCommitmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListCapacityCommitmentsResponse) (message)
- [`ListReservationGroupsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationGroupsRequest) (message)
- [`ListReservationGroupsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationGroupsResponse) (message)
- [`ListReservationsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationsRequest) (message)
- [`ListReservationsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationsResponse) (message)
- [`MergeCapacityCommitmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.MergeCapacityCommitmentsRequest) (message)
- [`MoveAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.MoveAssignmentRequest) (message)
- [`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation) (message)
- [`Reservation.Autoscale`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation.Autoscale) (message)
- [`Reservation.ReplicationStatus`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation.ReplicationStatus) (message)
- [`Reservation.ScalingMode`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation.ScalingMode) (enum)
- [`ReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationGroup) (message)
- [`SchedulingPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SchedulingPolicy) (message)
- [`SearchAllAssignmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAllAssignmentsRequest) (message)
- [`SearchAllAssignmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAllAssignmentsResponse) (message)
- [`SearchAssignmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAssignmentsRequest) (message)
- [`SearchAssignmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAssignmentsResponse) (message)
- [`SplitCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SplitCapacityCommitmentRequest) (message)
- [`SplitCapacityCommitmentResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SplitCapacityCommitmentResponse) (message)
- [`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.TableReference) (message)
- [`UpdateAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateAssignmentRequest) (message)
- [`UpdateBiReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateBiReservationRequest) (message)
- [`UpdateCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateCapacityCommitmentRequest) (message)
- [`UpdateReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateReservationRequest) (message)

## ReservationService

This API allows users to manage their BigQuery reservations.

A reservation provides computational resource guarantees, in the form of [slots](https://cloud.google.com/bigquery/docs/slots) , to users. A slot is a unit of computational power in BigQuery, and serves as the basic unit of parallelism. In a scan of a multi-partitioned table, a single slot operates on a single partition of the table. A reservation resource exists as a child resource of the admin project and location, e.g.: `projects/myproject/locations/US/reservations/reservationName` .

A capacity commitment is a way to purchase compute capacity for BigQuery jobs (in the form of slots) with some committed period of usage. A capacity commitment resource exists as a child resource of the admin project and location, e.g.: `projects/myproject/locations/US/capacityCommitments/id` .

**CreateAssignment**

`rpc CreateAssignment( `[`CreateAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateAssignmentRequest)` ) returns ( `[`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment)` )`

Creates an assignment object which allows the given project to submit jobs of a certain type using slots from the specified reservation.

Currently a resource (project, folder, organization) can only have one assignment per each (job_type, location) combination, and that reservation will be used for all jobs of the matching type.

Different assignments can be created on different levels of the projects, folders or organization hierarchy. During query execution, the assignment is looked up at the project, folder and organization levels in that order. The first assignment found is applied to the query.

When creating assignments, it does not matter if other assignments exist at higher levels.

Example:

- The organization `organizationA` contains two projects, `project1` and `project2` .
- Assignments for all three entities ( `organizationA` , `project1` , and `project2` ) could all be created and mapped to the same or different reservations.

"None" assignments represent an absence of the assignment. Projects assigned to None use on-demand pricing. To create a "None" assignment, use "none" as a reservation_id in the parent. Example parent: `projects/myproject/locations/US/reservations/none` .

Returns `google.rpc.Code.PERMISSION_DENIED` if user does not have 'bigquery.admin' permissions on the project using the reservation and the project that owns this reservation.

Returns `google.rpc.Code.INVALID_ARGUMENT` when location of the assignment does not match location of the reservation.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateCapacityCommitment**

`rpc CreateCapacityCommitment( `[`CreateCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateCapacityCommitmentRequest)` ) returns ( `[`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment)` )`

Creates a new capacity commitment resource.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateReservation**

`rpc CreateReservation( `[`CreateReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateReservationRequest)` ) returns ( `[`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation)` )`

Creates a new reservation resource.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateReservationGroup**

`rpc CreateReservationGroup( `[`CreateReservationGroupRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CreateReservationGroupRequest)` ) returns ( `[`ReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationGroup)` )`

Creates a new reservation group.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteAssignment**

`rpc DeleteAssignment( `[`DeleteAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteAssignmentRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a assignment. No expansion will happen.

Example:

- Organization `organizationA` contains two projects, `project1` and `project2` .
- Reservation `res1` exists and was created previously.
- CreateAssignment was used previously to define the following associations between entities and reservations: `<organizationA, res1>` and `<project1, res1>`

In this example, deletion of the `<organizationA, res1>` assignment won't affect the other assignment `<project1, res1>` . After said deletion, queries from `project1` will still use `res1` while queries from `project2` will switch to use on-demand mode.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteCapacityCommitment**

`rpc DeleteCapacityCommitment( `[`DeleteCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteCapacityCommitmentRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a capacity commitment. Attempting to delete capacity commitment before its commitment_end_time will fail with the error code `google.rpc.Code.FAILED_PRECONDITION` .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteReservation**

`rpc DeleteReservation( `[`DeleteReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteReservationRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a reservation. Returns `google.rpc.Code.FAILED_PRECONDITION` when reservation has assignments.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteReservationGroup**

`rpc DeleteReservationGroup( `[`DeleteReservationGroupRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.DeleteReservationGroupRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a reservation. Returns `google.rpc.Code.FAILED_PRECONDITION` when reservation has assignments.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**FailoverReservation**

`rpc FailoverReservation( `[`FailoverReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.FailoverReservationRequest)` ) returns ( `[`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation)` )`

Fail over a reservation to the secondary location. The operation should be done in the current secondary location, which will be promoted to the new primary location for the reservation. Attempting to failover a reservation in the current primary location will fail with the error code `google.rpc.Code.FAILED_PRECONDITION` .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetBiReservation**

`rpc GetBiReservation( `[`GetBiReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetBiReservationRequest)` ) returns ( `[`BiReservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.BiReservation)` )`

Retrieves a BI reservation.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetCapacityCommitment**

`rpc GetCapacityCommitment( `[`GetCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetCapacityCommitmentRequest)` ) returns ( `[`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment)` )`

Returns information about the capacity commitment.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetIamPolicy**

`rpc GetIamPolicy( `[`GetIamPolicyRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.GetIamPolicyRequest)` ) returns ( `[`Policy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.Policy)` )`

Gets the access control policy for a resource. May return:

- A `NOT_FOUND` error if the resource doesn't exist or you don't have the permission to view it.
- An empty policy if the resource exists but doesn't have a set policy.

Supported resources are: - Reservations - ReservationAssignments

To call this method, you must have the following Google IAM permissions:

- `bigqueryreservation.reservations.getIamPolicy` to get policies on reservations.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetReservation**

`rpc GetReservation( `[`GetReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetReservationRequest)` ) returns ( `[`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation)` )`

Returns information about the reservation.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetReservationGroup**

`rpc GetReservationGroup( `[`GetReservationGroupRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.GetReservationGroupRequest)` ) returns ( `[`ReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationGroup)` )`

Returns information about the reservation group.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListAssignments**

`rpc ListAssignments( `[`ListAssignmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListAssignmentsRequest)` ) returns ( `[`ListAssignmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListAssignmentsResponse)` )`

Lists assignments.

Only explicitly created assignments will be returned.

Example:

- Organization `organizationA` contains two projects, `project1` and `project2` .
- Reservation `res1` exists and was created previously.
- CreateAssignment was used previously to define the following associations between entities and reservations: `<organizationA, res1>` and `<project1, res1>`

In this example, ListAssignments will just return the above two assignments for reservation `res1` , and no expansion/merge will happen.

The wildcard "-" can be used for reservations in the request. In that case all assignments belongs to the specified project and location will be listed.

**Note** "-" cannot be used for projects nor locations.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListCapacityCommitments**

`rpc ListCapacityCommitments( `[`ListCapacityCommitmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListCapacityCommitmentsRequest)` ) returns ( `[`ListCapacityCommitmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListCapacityCommitmentsResponse)` )`

Lists all the capacity commitments for the admin project.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListReservationGroups**

`rpc ListReservationGroups( `[`ListReservationGroupsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationGroupsRequest)` ) returns ( `[`ListReservationGroupsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationGroupsResponse)` )`

Lists all the reservation groups for the project in the specified location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListReservations**

`rpc ListReservations( `[`ListReservationsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationsRequest)` ) returns ( `[`ListReservationsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ListReservationsResponse)` )`

Lists all the reservations for the project in the specified location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**MergeCapacityCommitments**

`rpc MergeCapacityCommitments( `[`MergeCapacityCommitmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.MergeCapacityCommitmentsRequest)` ) returns ( `[`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment)` )`

Merges capacity commitments of the same plan into a single commitment.

The resulting capacity commitment has the greater commitment_end_time out of the to-be-merged capacity commitments.

Attempting to merge capacity commitments of different plan will fail with the error code `google.rpc.Code.FAILED_PRECONDITION` .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**MoveAssignment**

`rpc MoveAssignment( `[`MoveAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.MoveAssignmentRequest)` ) returns ( `[`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment)` )`

Moves an assignment under a new reservation.

This differs from removing an existing assignment and recreating a new one by providing a transactional change that ensures an assignee always has an associated reservation.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SearchAllAssignments**

`rpc SearchAllAssignments( `[`SearchAllAssignmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAllAssignmentsRequest)` ) returns ( `[`SearchAllAssignmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAllAssignmentsResponse)` )`

Looks up assignments for a specified resource for a particular region. If the request is about a project:

1.  Assignments created on the project will be returned if they exist.
2.  Otherwise assignments created on the closest ancestor will be returned.
3.  Assignments for different JobTypes will all be returned.

The same logic applies if the request is about a folder.

If the request is about an organization, then assignments created on the organization will be returned (organization doesn't have ancestors).

Comparing to ListAssignments, there are some behavior differences:

1.  permission on the assignee will be verified in this API.
2.  Hierarchy lookup (project-\>folder-\>organization) happens in this API.
3.  Parent here is `projects/*/locations/*` , instead of `projects/*/locations/*reservations/*` .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SearchAssignments**

> This item is deprecated!

`rpc SearchAssignments( `[`SearchAssignmentsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAssignmentsRequest)` ) returns ( `[`SearchAssignmentsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SearchAssignmentsResponse)` )`

Deprecated: Looks up assignments for a specified resource for a particular region. If the request is about a project:

1.  Assignments created on the project will be returned if they exist.
2.  Otherwise assignments created on the closest ancestor will be returned.
3.  Assignments for different JobTypes will all be returned.

The same logic applies if the request is about a folder.

If the request is about an organization, then assignments created on the organization will be returned (organization doesn't have ancestors).

Comparing to ListAssignments, there are some behavior differences:

1.  permission on the assignee will be verified in this API.
2.  Hierarchy lookup (project-\>folder-\>organization) happens in this API.
3.  Parent here is `projects/*/locations/*` , instead of `projects/*/locations/*reservations/*` .

**Note** "-" cannot be used for projects nor locations.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SetIamPolicy**

`rpc SetIamPolicy( `[`SetIamPolicyRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.SetIamPolicyRequest)` ) returns ( `[`Policy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.Policy)` )`

Sets an access control policy for a resource. Replaces any existing policy.

Supported resources are: - Reservations

To call this method, you must have the following Google IAM permissions:

- `bigqueryreservation.reservations.setIamPolicy` to set policies on reservations.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SplitCapacityCommitment**

`rpc SplitCapacityCommitment( `[`SplitCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SplitCapacityCommitmentRequest)` ) returns ( `[`SplitCapacityCommitmentResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SplitCapacityCommitmentResponse)` )`

Splits capacity commitment to two commitments of the same plan and `commitment_end_time` .

A common use case is to enable downgrading commitments.

For example, in order to downgrade from 10000 slots to 8000, you might split a 10000 capacity commitment into commitments of 2000 and 8000. Then, you delete the first one after the commitment end time passes.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**TestIamPermissions**

`rpc TestIamPermissions( `[`TestIamPermissionsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.TestIamPermissionsRequest)` ) returns ( `[`TestIamPermissionsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.TestIamPermissionsResponse)` )`

Gets your permissions on a resource. Returns an empty set of permissions if the resource doesn't exist.

Supported resources are: - Reservations

No Google IAM permissions are required to call this method.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateAssignment**

`rpc UpdateAssignment( `[`UpdateAssignmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateAssignmentRequest)` ) returns ( `[`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment)` )`

Updates an existing assignment.

Only the `priority` field can be updated.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateBiReservation**

`rpc UpdateBiReservation( `[`UpdateBiReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateBiReservationRequest)` ) returns ( `[`BiReservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.BiReservation)` )`

Updates a BI reservation.

Only fields specified in the `field_mask` are updated.

A singleton BI reservation always exists with default size 0. In order to reserve BI capacity it needs to be updated to an amount greater than 0. In order to release BI capacity reservation size must be set to 0.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateCapacityCommitment**

`rpc UpdateCapacityCommitment( `[`UpdateCapacityCommitmentRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateCapacityCommitmentRequest)` ) returns ( `[`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment)` )`

Updates an existing capacity commitment.

Only `plan` and `renewal_plan` fields can be updated.

Plan can only be changed to a plan of a longer commitment period. Attempting to change to a plan with shorter commitment period will fail with the error code `google.rpc.Code.FAILED_PRECONDITION` .

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateReservation**

`rpc UpdateReservation( `[`UpdateReservationRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.UpdateReservationRequest)` ) returns ( `[`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation)` )`

Updates an existing reservation resource.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## Assignment

An assignment allows a project to submit jobs of a certain type using slots from the specified reservation.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Output only. Name of the resource. E.g.: <code>projects/myproject/locations/US/reservations/team1-prod/assignments/123</code> . The assignment_id must only contain lower case alphanumeric characters or dashes and the max length is 64 characters.</p></td>
</tr>
<tr class="even">
<td><code>assignee</code></td>
<td><p><code>string</code></p>
<p>Optional. The resource which will use the reservation. E.g. <code>projects/myproject</code> , <code>folders/123</code> , or <code>organizations/456</code> .</p></td>
</tr>
<tr class="odd">
<td><code>job_type</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment.JobType"><code>JobType</code></a></p>
<p>Optional. Which type of jobs will use the reservation.</p></td>
</tr>
<tr class="even">
<td><code>state</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment.State"><code>State</code></a></p>
<p>Output only. State of the assignment.</p></td>
</tr>
<tr class="odd">
<td><code>scheduling_policy</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SchedulingPolicy"><code>SchedulingPolicy</code></a></p>
<p>Optional. The scheduling policy to use for jobs and queries of this assignee when running under the associated reservation. The scheduling policy controls how the reservation's resources are distributed. This overrides the default scheduling policy specified on the reservation.</p>
<p>This feature is not yet generally available.</p></td>
</tr>
<tr class="even">
<td><code>principal</code></td>
<td><p><code>string</code></p>
<p>Optional. Represents the principal for this assignment. If not empty, jobs run by this principal utilize the associated reservation. Otherwise, jobs fall back to using the reservation assigned to the project, folder, or organization, in that order. If no reservation is assigned at any of these levels, on-demand capacity is used.</p>
<p>The supported formats are:</p>
<ul>
<li><code>principal://goog/subject/USER_EMAIL_ADDRESS</code> for users,</li>
<li><code>principal://iam.googleapis.com/projects/-/serviceAccounts/SA_EMAIL_ADDRESS</code> for service accounts,</li>
<li><code>principal://iam.googleapis.com/projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/POOL_ID/subject/SUBJECT_ID</code> for workload identity pool identities.</li>
<li>The special value <code>unknown_or_deleted_user</code> represents principals which cannot be read from the user info service, for example, deleted users.</li>
</ul></td>
</tr>
</tbody>
</table>

## JobType

Types of job, which could be specified when using the reservation.

| Enums                                 |                                                                                                                                                                                                                               |
|---------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_TYPE_UNSPECIFIED`                | Invalid type. Requests with this value will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` .                                                                                                                  |
| `PIPELINE`                            | Pipeline (load/export) jobs from the project will use the reservation.                                                                                                                                                        |
| `QUERY`                               | Query jobs from the project will use the reservation.                                                                                                                                                                         |
| `ML_EXTERNAL`                         | BigQuery ML jobs that use services external to BigQuery for model training. These jobs will not utilize idle slots from other reservations.                                                                                   |
| `BACKGROUND`                          | Background jobs that BigQuery runs for the customers in the background.                                                                                                                                                       |
| `CONTINUOUS`                          | Continuous SQL jobs will use this reservation. Reservations with continuous assignments cannot be mixed with non-continuous assignments.                                                                                      |
| `BACKGROUND_CHANGE_DATA_CAPTURE`      | Finer granularity background jobs for capturing changes in a source database and streaming them into BigQuery. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists). |
| `BACKGROUND_COLUMN_METADATA_INDEX`    | Finer granularity background jobs for refreshing cached metadata for BigQuery tables. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists).                          |
| `BACKGROUND_SEARCH_INDEX_REFRESH`     | Finer granularity background jobs for refreshing search indexes upon BigQuery table columns. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists).                   |
| `AUTOMATIC_MATERIALIZED_VIEW_REFRESH` | Automated materialized view refresh jobs will use the reservation. Reservations with this job type will take priority over a default QUERY reservation assignment (if it exists).                                             |

## State

Assignment will remain in PENDING state if no active capacity commitment is present. It will become ACTIVE when some capacity commitment becomes active.

| Enums               |                                                                                        |
|---------------------|----------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Invalid state value.                                                                   |
| `PENDING`           | Queries from assignee will be executed as on-demand, if related assignment is pending. |
| `ACTIVE`            | Assignment is ready.                                                                   |

## BiReservation

Represents a BI Reservation.

| Fields               |                                                                                                                                                                                                                                        |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`               | `string` Identifier. The resource name of the singleton BI reservation. Reservation names have the form `projects/{project_id}/locations/{location_id}/biReservation` .                                                                |
| `update_time`        | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The last update timestamp of a reservation.                                                                                             |
| `size`               | `int64` Optional. Size of a reservation, in bytes.                                                                                                                                                                                     |
| `preferred_tables[]` | [`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.TableReference) Optional. Preferred tables to use BI capacity for. |

## CapacityCommitment

Capacity commitment is a way to purchase compute capacity for BigQuery jobs (in the form of slots) with some committed period of usage. Annual commitments renew by default. Commitments can be removed after their commitment end time passes.

In order to remove annual commitment, its plan needs to be changed to monthly or flex first.

A capacity commitment resource exists as a child resource of the admin project.

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                  | `string` Output only. The resource name of the capacity commitment, e.g., `projects/myproject/locations/US/capacityCommitments/123` The commitment_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.                                                                                                                        |
| `slot_count`            | `int64` Optional. Number of slots in this commitment.                                                                                                                                                                                                                                                                                                                                                                                       |
| `plan`                  | [`CommitmentPlan`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment.CommitmentPlan) Optional. Capacity commitment commitment plan.                                                                                                                                                                                       |
| `state`                 | [`State`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment.State) Output only. State of the commitment.                                                                                                                                                                                                                  |
| `commitment_start_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The start of the current commitment period. It is applicable only for ACTIVE capacity commitments. Note after the commitment is renewed, commitment_start_time won't be changed. It refers to the start time of the original commitment.                                                                                                     |
| `commitment_end_time`   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The end of the current commitment period. It is applicable only for ACTIVE capacity commitments. Note after renewal, commitment_end_time is the time the renewed commitment expires. So itwould be at a time after commitment_start_time + committed period, because we don't change commitment_start_time ,                                 |
| `failure_status`        | [`Status`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.rpc#google.rpc.Status) Output only. For FAILED commitment plan, provides the reason of failure.                                                                                                                                                                                                                                                    |
| `renewal_plan`          | [`CommitmentPlan`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment.CommitmentPlan) Optional. The plan this capacity commitment is converted to after commitment_end_time passes. Once the plan is changed, committed period is extended according to commitment plan. Only applicable for ANNUAL and TRIAL commitments. |
| `edition`               | [`Edition`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Edition) Optional. Edition of the capacity commitment.                                                                                                                                                                                                                         |
| `is_flat_rate`          | `bool` Output only. If true, the commitment is a flat-rate commitment, otherwise, it's an edition commitment.                                                                                                                                                                                                                                                                                                                               |

## CommitmentPlan

Commitment plan defines the current committed period. Capacity commitment cannot be deleted during it's committed period.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>COMMITMENT_PLAN_UNSPECIFIED</code></td>
<td>Invalid plan value. Requests with this value will be rejected with error code <code>google.rpc.Code.INVALID_ARGUMENT</code> .</td>
</tr>
<tr class="even">
<td><code>FLEX</code></td>
<td><p>Deprecated: Flex commitments are deprecated. Please use Edition-based capacity commitments. Flex commitments have committed period of 1 minute after becoming ACTIVE. After that, they are not in a committed period anymore and can be removed any time.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>FLEX_FLAT_RATE</code></td>
<td><p>Same as FLEX, should only be used if flat-rate commitments are still available.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="even">
<td><code>TRIAL</code></td>
<td><p>Trial commitments have a committed period of 182 days after becoming ACTIVE. After that, they are converted to a new commitment based on the <code>renewal_plan</code> . Default <code>renewal_plan</code> for Trial commitment is Flex so that it can be deleted right after committed period ends.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>MONTHLY</code></td>
<td>Monthly commitments have a committed period of 30 days after becoming ACTIVE. After that, they are not in a committed period anymore and can be removed any time.</td>
</tr>
<tr class="even">
<td><code>MONTHLY_FLAT_RATE</code></td>
<td><p>Same as MONTHLY, should only be used if flat-rate commitments are still available.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>ANNUAL</code></td>
<td>Annual commitments have a committed period of 365 days after becoming ACTIVE. After that they are converted to a new commitment based on the renewal_plan.</td>
</tr>
<tr class="even">
<td><code>ANNUAL_FLAT_RATE</code></td>
<td><p>Same as ANNUAL, should only be used if flat-rate commitments are still available.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>THREE_YEAR</code></td>
<td>3-year commitments have a committed period of 1095(3 * 365) days after becoming ACTIVE. After that they are converted to a new commitment based on the renewal_plan.</td>
</tr>
<tr class="even">
<td><code>NONE</code></td>
<td>Should only be used for <code>renewal_plan</code> and is only meaningful if edition is specified to values other than EDITION_UNSPECIFIED. Otherwise CreateCapacityCommitmentRequest or UpdateCapacityCommitmentRequest will be rejected with error code <code>google.rpc.Code.INVALID_ARGUMENT</code> . If the renewal_plan is NONE, capacity commitment will be removed at the end of its commitment period.</td>
</tr>
</tbody>
</table>

## State

Capacity commitment can either become ACTIVE right away or transition from PENDING to ACTIVE or FAILED.

| Enums               |                                                                                                                              |
|---------------------|------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Invalid state value.                                                                                                         |
| `PENDING`           | Capacity commitment is pending provisioning. Pending capacity commitment does not contribute to the project's slot_capacity. |
| `ACTIVE`            | Once slots are provisioned, capacity commitment becomes active. slot_count is added to the project's slot_capacity.          |
| `FAILED`            | Capacity commitment is failed to be activated by the backend.                                                                |

## CreateAssignmentRequest

The request for [`ReservationService.CreateAssignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.CreateAssignment) . Note: "bigquery.reservationAssignments.create" permission is required on the related assignee.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The parent resource name of the assignment E.g. <code>projects/myproject/locations/US/reservations/team1-prod</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>assignment</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment"><code>Assignment</code></a></p>
<p>Assignment resource to create.</p></td>
</tr>
<tr class="odd">
<td><code>assignment_id</code></td>
<td><p><code>string</code></p>
<p>The optional assignment ID. Assignment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. Max length is 64 characters.</p></td>
</tr>
</tbody>
</table>

## CreateCapacityCommitmentRequest

The request for [`ReservationService.CreateCapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.CreateCapacityCommitment) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the parent reservation. E.g., <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>capacity_commitment</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment"><code>CapacityCommitment</code></a></p>
<p>Content of the capacity commitment to create.</p></td>
</tr>
<tr class="odd">
<td><code>enforce_single_admin_project_per_org</code></td>
<td><p><code>bool</code></p>
<p>If true, fail the request if another project in the organization has a capacity commitment.</p></td>
</tr>
<tr class="even">
<td><code>capacity_commitment_id</code></td>
<td><p><code>string</code></p>
<p>The optional capacity commitment ID. Capacity commitment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. The first and last character cannot be a dash. Max length is 64 characters. NOTE: this ID won't be kept if the capacity commitment is split or merged.</p></td>
</tr>
</tbody>
</table>

## CreateReservationGroupRequest

The request for [`ReservationService.CreateReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.CreateReservationGroup) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Project, location. E.g., <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationGroups.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>reservation_group_id</code></td>
<td><p><code>string</code></p>
<p>Required. The reservation group ID. It must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.</p></td>
</tr>
<tr class="odd">
<td><code>reservation_group</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationGroup"><code>ReservationGroup</code></a></p>
<p>Required. New Reservation Group to create.</p></td>
</tr>
</tbody>
</table>

## CreateReservationRequest

The request for [`ReservationService.CreateReservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.CreateReservation) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Project, location. E.g., <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservations.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>reservation_id</code></td>
<td><p><code>string</code></p>
<p>The reservation ID. It must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.</p></td>
</tr>
<tr class="odd">
<td><code>reservation</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation"><code>Reservation</code></a></p>
<p>Definition of the new reservation to create.</p></td>
</tr>
</tbody>
</table>

## DeleteAssignmentRequest

The request for [`ReservationService.DeleteAssignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.DeleteAssignment) . Note: "bigquery.reservationAssignments.delete" permission is required on the related assignee.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the resource, e.g. <code>projects/myproject/locations/US/reservations/team1-prod/assignments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DeleteCapacityCommitmentRequest

The request for [`ReservationService.DeleteCapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.DeleteCapacityCommitment) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the capacity commitment to delete. E.g., <code>projects/myproject/locations/US/capacityCommitments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.delete</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>force</code></td>
<td><p><code>bool</code></p>
<p>Can be used to force delete commitments even if assignments exist. Deleting commitments with assignments may cause queries to fail if they no longer have access to slots.</p></td>
</tr>
</tbody>
</table>

## DeleteReservationGroupRequest

The request for [`ReservationService.DeleteReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.DeleteReservationGroup) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the reservation group to retrieve. E.g., <code>projects/myproject/locations/US/reservationGroups/team1-prod</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservationGroups.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DeleteReservationRequest

The request for [`ReservationService.DeleteReservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.DeleteReservation) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the reservation to retrieve. E.g., <code>projects/myproject/locations/US/reservations/team1-prod</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservations.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Edition

The type of editions. Different features and behaviors are provided to different editions Capacity commitments and reservations are linked to editions.

| Enums                 |                                                     |
|-----------------------|-----------------------------------------------------|
| `EDITION_UNSPECIFIED` | Default value, which will be treated as ENTERPRISE. |
| `STANDARD`            | Standard edition.                                   |
| `ENTERPRISE`          | Enterprise edition.                                 |
| `ENTERPRISE_PLUS`     | Enterprise Plus edition.                            |

## FailoverMode

The failover mode when a user initiates a failover on a reservation determines how writes that are pending replication are handled after the failover is initiated.

| Enums                       |                                                                                                                                                                                                                             |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `FAILOVER_MODE_UNSPECIFIED` | Invalid value.                                                                                                                                                                                                              |
| `SOFT`                      | When customers initiate a soft failover, BigQuery will wait until all committed writes are replicated to the secondary. This mode requires both regions to be available for the failover to succeed and prevents data loss. |
| `HARD`                      | When customers initiate a hard failover, BigQuery will not wait until all committed writes are replicated to the secondary. There can be data loss for hard failover.                                                       |

## FailoverReservationRequest

The request for ReservationService.FailoverReservation.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the reservation to failover. E.g., <code>projects/myproject/locations/US/reservations/team1-prod</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservations.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>failover_mode</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.FailoverMode"><code>FailoverMode</code></a></p>
<p>Optional. A parameter that determines how writes that are pending replication are handled after a failover is initiated. If not specified, HARD failover mode is used by default.</p></td>
</tr>
</tbody>
</table>

## GetBiReservationRequest

A request to get a singleton BI reservation.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the requested reservation, for example: <code>projects/{project_id}/locations/{location_id}/biReservation</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.bireservations.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetCapacityCommitmentRequest

The request for [`ReservationService.GetCapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.GetCapacityCommitment) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the capacity commitment to retrieve. E.g., <code>projects/myproject/locations/US/capacityCommitments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetReservationGroupRequest

The request for [`ReservationService.GetReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.GetReservationGroup) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the reservation group to retrieve. E.g., <code>projects/myproject/locations/US/reservationGroups/team1-prod</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservationGroups.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetReservationRequest

The request for [`ReservationService.GetReservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.GetReservation) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the reservation to retrieve. E.g., <code>projects/myproject/locations/US/reservations/team1-prod</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservations.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## ListAssignmentsRequest

The request for [`ReservationService.ListAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListAssignments) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The parent resource name e.g.:</p>
<p><code>projects/myproject/locations/US/reservations/team1-prod</code></p>
<p>Or:</p>
<p><code>projects/myproject/locations/US/reservations/-</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of items to return per page.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>The next_page_token value returned from a previous List request, if any.</p></td>
</tr>
</tbody>
</table>

## ListAssignmentsResponse

The response for [`ReservationService.ListAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListAssignments) .

| Fields            |                                                                                                                                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `assignments[]`   | [`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment) List of assignments visible to the user. |
| `next_page_token` | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                              |

## ListCapacityCommitmentsRequest

The request for [`ReservationService.ListCapacityCommitments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListCapacityCommitments) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Resource name of the parent reservation. E.g., <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of items to return.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>The next_page_token value returned from a previous List request, if any.</p></td>
</tr>
</tbody>
</table>

## ListCapacityCommitmentsResponse

The response for [`ReservationService.ListCapacityCommitments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListCapacityCommitments) .

| Fields                   |                                                                                                                                                                                                                                               |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `capacity_commitments[]` | [`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment) List of capacity commitments visible to the user. |
| `next_page_token`        | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                                                       |

## ListReservationGroupsRequest

The request for [`ReservationService.ListReservationGroups`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListReservationGroups) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The parent resource name containing project and location, e.g.: <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationGroups.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of items to return per page.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>The next_page_token value returned from a previous List request, if any.</p></td>
</tr>
</tbody>
</table>

## ListReservationGroupsResponse

The response for [`ReservationService.ListReservationGroups`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListReservationGroups) .

| Fields                 |                                                                                                                                                                                                                                   |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservation_groups[]` | [`ReservationGroup`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationGroup) List of reservations visible to the user. |
| `next_page_token`      | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                                           |

## ListReservationsRequest

The request for [`ReservationService.ListReservations`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListReservations) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The parent resource name containing project and location, e.g.: <code>projects/myproject/locations/US</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservations.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of items to return per page.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>The next_page_token value returned from a previous List request, if any.</p></td>
</tr>
</tbody>
</table>

## ListReservationsResponse

The response for [`ReservationService.ListReservations`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.ListReservations) .

| Fields            |                                                                                                                                                                                                                         |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservations[]`  | [`Reservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation) List of reservations visible to the user. |
| `next_page_token` | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                                 |

## MergeCapacityCommitmentsRequest

The request for [`ReservationService.MergeCapacityCommitments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.MergeCapacityCommitments) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Parent resource that identifies admin project and location e.g., <code>projects/myproject/locations/us</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>capacity_commitment_ids[]</code></td>
<td><p><code>string</code></p>
<p>Ids of capacity commitments to merge. These capacity commitments must exist under admin project and location specified in the parent. ID is the last portion of capacity commitment name e.g., 'abc' for projects/myproject/locations/US/capacityCommitments/abc</p></td>
</tr>
<tr class="odd">
<td><code>capacity_commitment_id</code></td>
<td><p><code>string</code></p>
<p>Optional. The optional resulting capacity commitment ID. Capacity commitment name will be generated automatically if this field is empty. This field must only contain lower case alphanumeric characters or dashes. The first and last character cannot be a dash. Max length is 64 characters.</p></td>
</tr>
</tbody>
</table>

## MoveAssignmentRequest

The request for [`ReservationService.MoveAssignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.MoveAssignment) .

**Note** : "bigquery.reservationAssignments.create" permission is required on the destination_id.

**Note** : "bigquery.reservationAssignments.create" and "bigquery.reservationAssignments.delete" permission are required on the related assignee.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The resource name of the assignment, e.g. <code>projects/myproject/locations/US/reservations/team1-prod/assignments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.delete</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>destination_id</code></td>
<td><p><code>string</code></p>
<p>The new reservation ID, e.g.: <code>projects/myotherproject/locations/US/reservations/team2-prod</code></p></td>
</tr>
<tr class="odd">
<td><code>assignment_id</code></td>
<td><p><code>string</code></p>
<p>The optional assignment ID. A new assignment name is generated if this field is empty.</p>
<p>This field can contain only lowercase alphanumeric characters or dashes. Max length is 64 characters.</p></td>
</tr>
</tbody>
</table>

## Reservation

A reservation is a mechanism used to guarantee slots to users.

| Fields                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                      | `string` Identifier. The resource name of the reservation, e.g., `projects/*/locations/*/reservations/team1-prod` . The reservation_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `slot_capacity`             | `int64` Optional. Baseline slots available to this reservation. A slot is a unit of computational power in BigQuery, and serves as the unit of parallelism. Queries using this reservation might use more slots during runtime if ignore_idle_slots is set to false, or autoscaling is enabled. The total slot_capacity of the reservation and its siblings may exceed the total slot_count of capacity commitments. In that case, the exceeding slots will be charged with the autoscale SKU. You can increase the number of baseline slots in a reservation every few minutes. If you want to decrease your baseline slots, you are limited to once an hour if you have recently changed your baseline slot capacity and your baseline slots exceed your committed slots. Otherwise, you can decrease your baseline slots every few minutes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `ignore_idle_slots`         | `bool` Optional. If false, any query or pipeline job using this reservation will use idle slots from other reservations within the same admin project. If true, a query or pipeline job using this reservation will execute with the slot capacity specified in the slot_capacity field at most.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `autoscale`                 | [`Autoscale`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation.Autoscale) Optional. The configuration parameters for the auto scaling feature.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `concurrency`               | `int64` Optional. Job concurrency target which sets a soft upper bound on the number of jobs that can run concurrently in this reservation. This is a soft target due to asynchronous nature of the system and various optimizations for small queries. Default value is 0 which means that concurrency target will be automatically computed by the system. NOTE: this field is exposed as target job concurrency in the Information Schema, DDL and BigQuery CLI.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `creation_time`             | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Creation time of the reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `update_time`               | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Last update time of the reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `edition`                   | [`Edition`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Edition) Optional. Edition of the reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `primary_location`          | `string` Output only. The current location of the reservation's primary replica. This field is only set for reservations using the managed disaster recovery feature.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `secondary_location`        | `string` Optional. The current location of the reservation's secondary replica. This field is only set for reservations using the managed disaster recovery feature. Users can set this in create reservation calls to create a failover reservation or in update reservation calls to convert a non-failover reservation to a failover reservation(or vice versa).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `original_primary_location` | `string` Output only. The location where the reservation was originally created. This is set only during the failover reservation's creation. All billing charges for the failover reservation will be applied to this location.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `scaling_mode`              | [`ScalingMode`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation.ScalingMode) Optional. The scaling mode for the reservation. If the field is present but max_slots is not present, requests will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `reservation_group`         | `string` Optional. The reservation group that this reservation belongs to. You can set this property when you create or update a reservation. Reservations do not need to belong to a reservation group. Format: projects/{project}/locations/{location}/reservationGroups/{reservation_group} or just {reservation_group}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `replication_status`        | [`ReplicationStatus`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation.ReplicationStatus) Output only. The Disaster Recovery(DR) replication status of the reservation. This is only available for the primary replicas of DR/failover reservations and provides information about the both the staleness of the secondary and the last error encountered while trying to replicate changes from the primary to the secondary. If this field is blank, it means that the reservation is either not a DR reservation or the reservation is a DR secondary or that any replication operations on the reservation have succeeded.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `scheduling_policy`         | [`SchedulingPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.SchedulingPolicy) Optional. The scheduling policy to use for jobs and queries running under this reservation. The scheduling policy controls how the reservation's resources are distributed. This feature is not yet generally available.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `max_slots`                 | `int64` Optional. The overall max slots for the reservation, covering slot_capacity (baseline), idle slots (if ignore_idle_slots is false) and scaled slots. If present, the reservation won't use more than the specified number of slots, even if there is demand and supply (from idle slots). NOTE: capping a reservation's idle slot usage is best effort and its usage may exceed the max_slots value. However, in terms of autoscale.current_slots (which accounts for the additional added slots), it will never exceed the max_slots - baseline. This field must be set together with the scaling_mode enum value, otherwise the request will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` . If the max_slots and scaling_mode are set, the autoscale or autoscale.max_slots field must be unset. Otherwise the request will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` . However, the autoscale field may still be in the output. The autopscale.max_slots will always show as 0 and the autoscaler.current_slots will represent the current slots from autoscaler excluding idle slots. For example, if the max_slots is 1000 and scaling_mode is AUTOSCALE_ONLY, then in the output, the autoscaler.max_slots will be 0 and the autoscaler.current_slots may be any value between 0 and 1000. If the max_slots is 1000, scaling_mode is ALL_SLOTS, the baseline is 100 and idle slots usage is 200, then in the output, the autoscaler.max_slots will be 0 and the autoscaler.current_slots will not be higher than 700. If the max_slots is 1000, scaling_mode is IDLE_SLOTS_ONLY, then in the output, the autoscaler field will be null. If the max_slots and scaling_mode are set, then the ignore_idle_slots field must be aligned with the scaling_mode enum value.(See details in ScalingMode comments). Otherwise the request will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` . Please note, the max_slots is for user to manage the part of slots greater than the baseline. Therefore, we don't allow users to set max_slots smaller or equal to the baseline as it will not be meaningful. If the field is present and slot_capacity\>=max_slots, requests will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` . Please note that if max_slots is set to 0, we will treat it as unset. Customers can set max_slots to 0 and set scaling_mode to SCALING_MODE_UNSPECIFIED to disable the max_slots feature. |

## Autoscale

Auto scaling settings.

| Fields          |                                                                                                                                                                                                                                                                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `current_slots` | `int64` Output only. The slot capacity added to this reservation when autoscale happens. Will be between \[0, max_slots\]. Note: after users reduce max_slots, it may take a while before it can be propagated, so current_slots may stay in the original value and could be larger than max_slots for that brief period (less than one minute) |
| `max_slots`     | `int64` Optional. Number of slots to be scaled when needed.                                                                                                                                                                                                                                                                                     |

## ReplicationStatus

Disaster Recovery(DR) replication status of the reservation.

| Fields                     |                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `error`                    | [`Status`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.rpc#google.rpc.Status) Output only. The last error encountered while trying to replicate changes from the primary to the secondary. This field is only available if the replication has not succeeded since.                                                                                          |
| `last_error_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The time at which the last error was encountered while trying to replicate changes from the primary to the secondary. This field is only available if the replication has not succeeded since.                                                                                                  |
| `last_replication_time`    | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. A timestamp corresponding to the last change on the primary that was successfully replicated to the secondary.                                                                                                                                                                                  |
| `soft_failover_start_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The time at which a soft failover for the reservation and its associated datasets was initiated. After this field is set, all subsequent changes to the reservation will be rejected unless a hard failover overrides this operation. This field will be cleared once the failover is complete. |

## ScalingMode

The scaling mode for the reservation. This enum determines how the reservation scales up and down.

| Enums                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SCALING_MODE_UNSPECIFIED` | Default value of ScalingMode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `AUTOSCALE_ONLY`           | The reservation will scale up only using slots from autoscaling. It will not use any idle slots even if there may be some available. The upper limit that autoscaling can scale up to will be max_slots - baseline. For example, if max_slots is 1000, baseline is 200 and customer sets ScalingMode to AUTOSCALE_ONLY, then autoscalerg will scale up to 800 slots and no idle slots will be used. Please note, in this mode, the ignore_idle_slots field must be set to true. Otherwise the request will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `IDLE_SLOTS_ONLY`          | The reservation will scale up using only idle slots contributed by other reservations or from unassigned commitments. If no idle slots are available it will not scale up further. If the idle slots which it is using are reclaimed by the contributing reservation(s) it may be forced to scale down. The max idle slots the reservation can be max_slots - baseline capacity. For example, if max_slots is 1000, baseline is 200 and customer sets ScalingMode to IDLE_SLOTS_ONLY, 1. if there are 1000 idle slots available in other reservations, the reservation will scale up to 1000 slots with 200 baseline and 800 idle slots. 2. if there are 500 idle slots available in other reservations, the reservation will scale up to 700 slots with 200 baseline and 500 idle slots. Please note, in this mode, the reservation might not be able to scale up to max_slots. Please note, in this mode, the ignore_idle_slots field must be set to false. Otherwise the request will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` . |
| `ALL_SLOTS`                | The reservation will scale up using all slots available to it. It will use idle slots contributed by other reservations or from unassigned commitments first. If no idle slots are available it will scale up using autoscaling. For example, if max_slots is 1000, baseline is 200 and customer sets ScalingMode to ALL_SLOTS, 1. if there are 800 idle slots available in other reservations, the reservation will scale up to 1000 slots with 200 baseline and 800 idle slots. 2. if there are 500 idle slots available in other reservations, the reservation will scale up to 1000 slots with 200 baseline, 500 idle slots and 300 autoscaling slots. 3. if there are no idle slots available in other reservations, it will scale up to 1000 slots with 200 baseline and 800 autoscaling slots. Please note, in this mode, the ignore_idle_slots field must be set to false. Otherwise the request will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` .                                                                            |

## ReservationGroup

A reservation group is a container for reservations.

| Fields          |                                                                                                                                                                                                                                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`          | `string` Identifier. The resource name of the reservation group, e.g., `projects/*/locations/*/reservationGroups/team1-prod` . The reservation_group_id must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.                                     |
| `creation_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Creation time of the reservation group.                                                                                                                                                                                                                     |
| `update_time`   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Last update time of the reservation group via a user operation. This timestamp is updated only when an update operation explicitly targets this reservation group directly. It is not updated when parent or child groups are created, updated, or deleted. |

## SchedulingPolicy

The scheduling policy controls how a reservation's resources are distributed.

| Fields        |                                                                                                                                                                                                                            |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `concurrency` | `int64` Optional. If present and \> 0, the reservation will attempt to limit the concurrency of jobs running for any particular project within it to the given value. This feature is not yet generally available.         |
| `max_slots`   | `int64` Optional. If present and \> 0, the reservation will attempt to limit the slot consumption of queries running for any particular project within it to the given value. This feature is not yet generally available. |

## SearchAllAssignmentsRequest

The request for [`ReservationService.SearchAllAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.SearchAllAssignments) . Note: "bigquery.reservationAssignments.search" permission is required on the related assignee.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The resource name with location (project name could be the wildcard '-'), e.g.: <code>projects/-/locations/US</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.search</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>Please specify resource name as assignee in the query.</p>
<p>Examples:</p>
<ul>
<li><code>assignee=projects/myproject</code></li>
<li><code>assignee=folders/123</code></li>
<li><code>assignee=organizations/456</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of items to return per page.</p></td>
</tr>
<tr class="even">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>The next_page_token value returned from a previous List request, if any.</p></td>
</tr>
</tbody>
</table>

## SearchAllAssignmentsResponse

The response for [`ReservationService.SearchAllAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.SearchAllAssignments) .

| Fields            |                                                                                                                                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `assignments[]`   | [`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment) List of assignments visible to the user. |
| `next_page_token` | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                              |

## SearchAssignmentsRequest

The request for [`ReservationService.SearchAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.SearchAssignments) . Note: "bigquery.reservationAssignments.search" permission is required on the related assignee.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The resource name of the admin project(containing project and location), e.g.: <code>projects/myproject/locations/US</code> .</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.reservationAssignments.search</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>Please specify resource name as assignee in the query.</p>
<p>Examples:</p>
<ul>
<li><code>assignee=projects/myproject</code></li>
<li><code>assignee=folders/123</code></li>
<li><code>assignee=organizations/456</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of items to return per page.</p></td>
</tr>
<tr class="even">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>The next_page_token value returned from a previous List request, if any.</p></td>
</tr>
</tbody>
</table>

## SearchAssignmentsResponse

The response for [`ReservationService.SearchAssignments`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.SearchAssignments) .

| Fields            |                                                                                                                                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `assignments[]`   | [`Assignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment) List of assignments visible to the user. |
| `next_page_token` | `string` Token to retrieve the next page of results, or empty if there are no more results in the list.                                                                                                              |

## SplitCapacityCommitmentRequest

The request for [`ReservationService.SplitCapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.SplitCapacityCommitment) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The resource name e.g.,: <code>projects/myproject/locations/US/capacityCommitments/123</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>slot_count</code></td>
<td><p><code>int64</code></p>
<p>Number of slots in the capacity commitment after the split.</p></td>
</tr>
</tbody>
</table>

## SplitCapacityCommitmentResponse

The response for [`ReservationService.SplitCapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.SplitCapacityCommitment) .

| Fields   |                                                                                                                                                                                                                                            |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `first`  | [`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment) First capacity commitment, result of a split.  |
| `second` | [`CapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment) Second capacity commitment, result of a split. |

## TableReference

Fully qualified reference to BigQuery table. Internally stored as google.cloud.bi.v1.BqTableReference.

| Fields       |                                                                |
|--------------|----------------------------------------------------------------|
| `project_id` | `string` Optional. The assigned project ID of the project.     |
| `dataset_id` | `string` Optional. The ID of the dataset in the above project. |
| `table_id`   | `string` Optional. The ID of the table in the above dataset.   |

## UpdateAssignmentRequest

The request for [`ReservationService.UpdateAssignment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.UpdateAssignment) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>assignment</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Assignment"><code>Assignment</code></a></p>
<p>Content of the assignment to update.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>assignment</code> :</p>
<ul>
<li><code>bigquery.reservationassignments.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>Standard field mask for the set of fields to be updated.</p></td>
</tr>
</tbody>
</table>

## UpdateBiReservationRequest

A request to update a BI reservation.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>bi_reservation</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.BiReservation"><code>BiReservation</code></a></p>
<p>A reservation to update.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>biReservation</code> :</p>
<ul>
<li><code>bigquery.bireservations.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>A list of fields to be updated in this request.</p></td>
</tr>
</tbody>
</table>

## UpdateCapacityCommitmentRequest

The request for [`ReservationService.UpdateCapacityCommitment`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.UpdateCapacityCommitment) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>capacity_commitment</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.CapacityCommitment"><code>CapacityCommitment</code></a></p>
<p>Content of the capacity commitment to update.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>capacityCommitment</code> :</p>
<ul>
<li><code>bigquery.capacityCommitments.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>Standard field mask for the set of fields to be updated.</p></td>
</tr>
</tbody>
</table>

## UpdateReservationRequest

The request for [`ReservationService.UpdateReservation`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.ReservationService.UpdateReservation) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>reservation</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.cloud.bigquery.reservation.v1#google.cloud.bigquery.reservation.v1.Reservation"><code>Reservation</code></a></p>
<p>Content of the reservation to update.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>reservation</code> :</p>
<ul>
<li><code>bigquery.reservations.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>Standard field mask for the set of fields to be updated.</p></td>
</tr>
</tbody>
</table>

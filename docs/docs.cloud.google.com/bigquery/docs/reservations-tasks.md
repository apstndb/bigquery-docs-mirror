# Manage workload reservations

The BigQuery Reservation API lets you purchase dedicated slots (called [*commitments*](/bigquery/docs/reservations-workload-management#slot_commitments) ), create pools of slots (called [*reservations*](/bigquery/docs/reservations-intro#reservations) ), and assign projects, folders, and organizations to those reservations.

Reservations allow you to assign a dedicated number of slots to a workload. For example, you might not want a production workload to compete with test workloads for slots. You could create a reservation named `  prod  ` and assign your production workloads to this reservation. For more information, see [Understand reservations](/bigquery/docs/reservations-workload-management) .

## Create reservations

### Required permissions

To create a reservation, you need the following Identity and Access Management (IAM) permission:

  - `  bigquery.reservations.create  ` on the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that maintains ownership of the commitments.

Each of the following predefined IAM roles includes this permission:

  - `  BigQuery Resource Editor  `
  - `  BigQuery Resource Admin  `

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Create a reservation with dedicated slots

Select one of the following options:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Click **Create reservation** .

4.  In the **Reservation name** field, enter a name for the reservation.

5.  In the **Location** list, select the location. If you select a [BigQuery Omni location](/bigquery/docs/omni-introduction#locations) , your edition option is limited to the Enterprise edition.

6.  In the **Edition** list, select the edition. BigQuery edition features such as autoscaling are only available within an edition. For more information, see [Introduction to BigQuery editions](/bigquery/docs/editions-intro) .

7.  In the **Max reservation size selector** list, select the maximum reservation size.

8.  Optional: In the **Baseline slots** field, enter the number of baseline slots for the reservation.
    
    The number of available autoscaling slots is determined by subtracting the **Baseline slots** value from the **Max reservation size** . For example, if you create a reservation with 100 baseline slots and a max reservation size of 400, your reservation has 300 autoscaling slots. For more information about baseline slots, see [Using reservations with baseline and autoscaling slots](/bigquery/docs/slots-autoscaling-intro#using_reservations_with_baseline_and_autoscaling_slots) .

9.  To disable [idle slot sharing](/bigquery/docs/slots#idle_slots) and use only the specified slot capacity, click the **Ignore idle slots** toggle.

10. To expand the **Advanced settings** section, click the expand\_more expander arrow.

11. Optional: To set the target job concurrency, click the **Override automatic target job concurrency** toggle to on and enter the **Target Job Concurrency** .

12. The breakdown of slots is displayed in the **Cost estimate** table. A summary of the reservation is displayed in the **Capacity summary** table.

13. Click **Save** .

The new reservation is visible in the **Slot reservations** tab.

### SQL

To create a reservation, use the [`  CREATE RESERVATION  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_reservation_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE RESERVATION
      `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME`
    OPTIONS (
      slot_capacity = NUMBER_OF_BASELINE_SLOTS,
      edition = EDITION,
      autoscale_max_slots = NUMBER_OF_AUTOSCALING_SLOTS);
    ```
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
    
      - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation. If you select a [BigQuery Omni location](/bigquery/docs/omni-introduction#locations) , your edition option is limited to the Enterprise edition.
    
      - `  RESERVATION_NAME  ` : the name of the reservation
        
        The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.
    
      - `  NUMBER_OF_BASELINE_SLOTS  ` : the number baseline of slots to allocate to the reservation. You cannot set the `  slot_capacity  ` option and the `  standard  ` edition option in the same reservation.
    
      - `  EDITION  ` : the edition of the reservation. Assigning a reservation to an edition comes with feature and pricing changes. For more information, see [Introduction to BigQuery editions](/bigquery/docs/editions-intro) .
    
      - `  NUMBER_OF_AUTOSCALING_SLOTS  ` : the number of autoscaling slots assigned to the reservation. This is equal to the value of the max reservation size minus the number of baseline slots.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To create a reservation, use the `  bq mk  ` command with the `  --reservation  ` flag:

``` text
bq mk \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --reservation \
    --slots=NUMBER_OF_BASELINE_SLOTS \
    --ignore_idle_slots=false \
    --edition=EDITION \
    --autoscale_max_slots=NUMBER_OF_AUTOSCALING_SLOTS \
    --max_slots=MAXIMUM_NUMBER_OF_SLOTS
    --scaling_mode=SCALING_MODE
    RESERVATION_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID

  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation. If you select a [BigQuery Omni location](/bigquery/docs/omni-introduction#locations) , your edition option is limited to the Enterprise edition.

  - `  NUMBER_OF_BASELINE_SLOTS  ` : the number of baseline slots to allocate to the reservation

  - `  RESERVATION_NAME  ` : the name of the reservation. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.

  - `  EDITION  ` : the edition of the reservation. Assigning a reservation to an edition comes with feature and pricing changes. For more information, see [Introduction to BigQuery editions](/bigquery/docs/editions-intro) .

  - `  NUMBER_OF_AUTOSCALING_SLOTS  ` : the number of autoscaling slots assigned to the reservation. This is equal to the value of the max reservation size minus the number of baseline slots. This can't be configured with either the `  --max_slots  ` or `  --scaling_mode  ` flags.

  - `  MAXIMUM_NUMBER_OF_SLOTS  ` : the maximum number of slots the reservation can consume. This value must be configured with the `  --scaling_mode  ` flag ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).

  - `  SCALING_MODE  ` : the scaling mode of the reservation. The options are `  ALL_SLOTS  ` , `  IDLE_SLOTS_ONLY  ` , or `  AUTOSCALE_ONLY  ` . This value must be configured with the `  --scaling_mode  ` flag ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).

For information about the `  --ignore_idle_slots  ` flag, see [Idle slots](/bigquery/docs/slots#idle_slots) . The default value is `  false  ` .

### Terraform

Use the [`  google_bigquery_reservation  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_reservation) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example creates a reservation named `  my-reservation  ` :

``` terraform
resource "google_bigquery_reservation" "default" {
  name              = "my-reservation"
  location          = "us-central1"
  slot_capacity     = 100
  edition           = "ENTERPRISE"
  ignore_idle_slots = false # Use idle slots from other reservations
  concurrency       = 0     # Automatically adjust query concurrency based on available resources
  autoscale {
    max_slots = 200 # Allow the reservation to scale up to 300 slots (slot_capacity + max_slots) if needed
  }
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.
    
    You only need to run this command once per project, and you can run it in any directory.
    
    ``` text
    export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    ```
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `  .tf  ` extension—for example `  main.tf  ` . In this tutorial, the file is referred to as `  main.tf  ` .
    
    ``` text
    mkdir DIRECTORY && cd DIRECTORY && touch main.tf
    ```

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `  main.tf  ` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
    ``` text
    terraform init
    ```
    
    Optionally, to use the latest Google provider version, include the `  -upgrade  ` option:
    
    ``` text
    terraform init -upgrade
    ```

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
    ``` text
    terraform plan
    ```
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `  yes  ` at the prompt:
    
    ``` text
    terraform apply
    ```
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

**Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

### Python

Install the [google-cloud-bigquery-reservation package](/python/docs/reference/bigqueryreservation/latest) before using this code sample. Construct a [ReservationServiceClient](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.services.reservation_service.ReservationServiceClient#google_cloud_bigquery_reservation_v1_services_reservation_service_ReservationServiceClient) . Describe the reservation you'd like to create with a [Reservation](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.types.Reservation) . Create the reservation with the [create\_reservation](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.services.reservation_service.ReservationServiceClient#google_cloud_bigquery_reservation_v1_services_reservation_service_ReservationServiceClient_create_reservation) method.

``` python
# TODO(developer): Set project_id to the project ID containing the
# reservation.
project_id = "your-project-id"

# TODO(developer): Set location to the location of the reservation.
# See: https://cloud.google.com/bigquery/docs/locations for a list of
# available locations.
location = "US"

# TODO(developer): Set reservation_id to a unique ID of the reservation.
reservation_id = "sample-reservation"

# TODO(developer): Set slot_capicity to the number of slots in the
# reservation.
slot_capacity = 100

# TODO(developer): Choose a transport to use. Either 'grpc' or 'rest'
transport = "grpc"

# ...

from google.cloud.bigquery_reservation_v1.services import reservation_service
from google.cloud.bigquery_reservation_v1.types import (
    reservation as reservation_types,
)

reservation_client = reservation_service.ReservationServiceClient(
    transport=transport
)

parent = reservation_client.common_location_path(project_id, location)

reservation = reservation_types.Reservation(slot_capacity=slot_capacity)
reservation = reservation_client.create_reservation(
    parent=parent,
    reservation=reservation,
    reservation_id=reservation_id,
)

print(f"Created reservation: {reservation.name}")
```

### Create a predictable reservation

Before you create a reservation with a [maximum number of slots](/bigquery/docs/reservations-workload-management#predictable) , you must first enable [reservation-based fairness](/bigquery/docs/slots#fairness) .

#### Enable reservation-based fairness

To enable reservation-based fairness, set the [`  enable_reservation_based_fairness  ` flag](/bigquery/docs/default-configuration) to `  true  ` .

To update the reservation-based fairness on a project, you need the `  bigquery.config.update  ` permission on the [project](/bigquery/docs/reservations-workload-management#admin-project) that maintains ownership of the reservations. The predefined `  BigQuery Admin  ` role includes this permission.

For more information about updating the default configuration of a project, see [Manage configuration settings](/bigquery/docs/default-configuration#required_permissions) .

``` text
ALTER PROJECT `PROJECT_NAME` SET OPTIONS (
    `region-LOCATION.enable_reservation_based_fairness`= true);
```

Replace the following:

  - PROJECT\_NAME : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project)
  - LOCATION : the [location](/bigquery/docs/locations) of the reservation

#### Create a predictable reservation

To create a predictable reservation with a maximum number of slots, select one of the following options:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation panel, go to the **Capacity management** section, and then click **Create reservation** .

3.  In the **Reservation name** field, enter a name for the reservation.

4.  In the **Location** list, select the location. If you select a [BigQuery Omni location](/bigquery/docs/omni-introduction#locations) , your edition option is limited to the Enterprise edition.

5.  In the **Edition** list, select the edition. For more information, see [Understand BigQuery editions](/bigquery/docs/editions-intro) .

6.  In the **Max reservation size selector** list, select the maximum reservation size.

7.  Optional: In the **Baseline slots** field, enter the number of baseline slots for the reservation.
    
    The number of available autoscaling slots is determined by subtracting the **Baseline slots** value from the **Max reservation size** . For example, if you create a reservation with 100 baseline slots and a max reservation size of 400, your reservation has 300 autoscaling slots. For more information about baseline slots, see [Using reservations with baseline and autoscaling slots](/bigquery/docs/slots-autoscaling-intro#using_reservations_with_baseline_and_autoscaling_slots) .

8.  To disable [idle slot sharing](/bigquery/docs/slots#idle_slots) and use only the specified slot capacity, click the **Ignore idle slots** toggle.

9.  To expand the **Advanced settings** section, click the expand\_more expander arrow.
    
    1.  In the **How to use idle slots?** list, select the configuration option.

10. The breakdown of slots is displayed in the **Cost estimate** table. A summary of the reservation is displayed in the **Capacity summary** table.

11. Click **Save** .

The new reservation is visible in the **Slot reservations** tab.

### bq

To create a predictable reservation, use the `  bq mk  ` command with the `  --reservation  ` flag and set the value of `  max_slots  ` and `  scaling_mode  ` :

``` text
bq mk \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --reservation \
    --slots=NUMBER_OF_BASELINE_SLOTS \
    --ignore_idle_slots=false \
    --edition=EDITION \
    --max_slots=MAXIMUM_NUMBER_OF_SLOTS \
    --scaling_mode=SCALING_MODE
    RESERVATION_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID

  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation. If you select a [BigQuery Omni location](/bigquery/docs/omni-introduction#locations) , your edition option is limited to the Enterprise edition.

  - `  NUMBER_OF_BASELINE_SLOTS  ` : the number of baseline slots to allocate to the reservation

  - `  RESERVATION_NAME  ` : the name of the reservation

  - `  EDITION  ` : the edition of the reservation. Assigning a reservation to an edition comes with feature and pricing changes. For more information, see [Introduction to BigQuery editions](/bigquery/docs/editions-intro) .

  - `  MAXIMUM_NUMBER_OF_SLOTS  ` : the maximum number of slots the reservation can consume. This value must be configured with the `  --scaling_mode  ` flag.

  - `  SCALING_MODE  ` : `  SCALING_MODE  ` : the scaling mode of the reservation. The options are `  ALL_SLOTS  ` , `  IDLE_SLOTS_ONLY  ` , or `  AUTOSCALE_ONLY  ` . This value must be configured with the `  max_slots  ` flag. This value must be aligned with `  ignore_idle_slots  ` flag. For details, see [Reservation predictability](/bigquery/docs/reservations-workload-management#predictable) .

For information about the `  --ignore_idle_slots  ` flag, see [Idle slots](/bigquery/docs/slots#idle_slots) . The default value is `  false  ` .

### SQL

To create a predictable reservation, use the [`  CREATE RESERVATION  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_reservation_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE RESERVATION
      `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME`
    OPTIONS (
      slot_capacity = NUMBER_OF_BASELINE_SLOTS,
      edition = EDITION,
      ignore_idle_slots=IGNORE_IDLE_SLOTS
      max_slots = MAX_NUMBER_OF_SLOTS,
      scaling_mode = SCALING_MODE);
    ```
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource.
    
      - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation. If you select a [BigQuery Omni location](/bigquery/docs/omni-introduction#locations) , your edition option is limited to the Enterprise edition.
    
      - `  RESERVATION_NAME  ` : the name of the reservation.The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.
    
      - `  NUMBER_OF_BASELINE_SLOTS  ` : the number baseline of slots to allocate to the reservation. You cannot set the `  slot_capacity  ` option and the `  standard  ` edition option in the same reservation.
    
      - `  EDITION  ` : the edition of the reservation. Assigning a reservation to an edition comes with feature and pricing changes. For more information, see [Introduction to BigQuery editions](/bigquery/docs/editions-intro) .
    
      - `  IGNORE_IDLE_SLOTS  ` : whether the reservation uses [Idle slots](/bigquery/docs/slots#idle_slots) or not. The default value is `  false  ` .
    
      - `  MAX_NUMBER_OF_SLOTS  ` : the maximum number of slots the reservation can consume. This value must be configured with `  scaling_mode  ` option.
    
      - `  SCALING_MODE  ` : the scaling mode of the reservation. The options are `  ALL_SLOTS  ` , `  IDLE_SLOTS_ONLY  ` , or `  AUTOSCALE_ONLY  ` . This value must be configured with the `  max_slots  ` option. This value must be aligned with `  ignore_idle_slots  ` option. For details, see [Reservation predictability](/bigquery/docs/reservations-workload-management#predictable) .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

To learn more about predictable reservations, see [Predictable reservations](/bigquery/docs/reservations-workload-management#predictable) .

## Update reservations

You can make the following updates to a reservation:

  - Change the reservation size by adding or removing slots.
  - Configure whether queries in this reservation use idle slots.
  - Change the amount of baseline or autoscaling slots allocated to a reservation.
  - Set the target job concurrency.

To change the edition of a reservation, first [delete](#delete_reservations) the reservation, then [create](#create_reservations) a reservation with the updated edition.

### Required permissions

To update a reservation, you need the following Identity and Access Management (IAM) permission:

  - `  bigquery.reservations.update  ` on the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that maintains ownership of the commitments.

Each of the following predefined IAM roles includes this permission:

  - `  BigQuery Admin  `
  - `  BigQuery Resource Admin  `
  - `  BigQuery Resource Editor  `

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

### Change the size of a reservation

You can add or remove slots from an existing reservation.

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Click the **Slot reservations** tab.

4.  Find the reservation you want to update.

5.  Expand the more\_vert **Actions** option.

6.  Click **Edit** .

7.  In the **Max reservation size selector** dialog, enter the max reservation size.

8.  In the **Baseline slots** field, enter the number of baseline slots.

9.  To expand the **Advanced settings** section, click the expand\_more expander arrow.

10. Optional: To set the target job concurrency, click the **Override automatic target job concurrency** toggle to on and enter the **Target Job Concurrency** .

11. Click **Save** .

### SQL

To change the size of a reservation, use the [`  ALTER RESERVATION SET OPTIONS  ` data definition language (DDL) statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_reservation_set_options_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    ALTER RESERVATION
      `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME`
    SET OPTIONS (
      slot_capacity = NUMBER_OF_BASELINE_SLOTS,
      autoscale_max_slots = NUMBER_OF_AUTOSCALING_SLOTS);
    ```
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
    
      - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation, for example `  europe-west9  ` .
    
      - `  RESERVATION_NAME  ` : the name of the reservation. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.
    
      - `  NUMBER_OF_BASELINE_SLOTS  ` : the number of baseline slots to allocate to the reservation.
    
      - `  NUMBER_OF_AUTOSCALING_SLOTS  ` : the number of autoscaling slots assigned to the reservation. This is equal to the value of the max reservation size minus the number of baseline slots.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To update the size of a reservation, use the `  bq update  ` command with the `  --reservation  ` flag:

``` text
bq update \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --slots=NUMBER_OF_BASELINE_SLOTS \
    --autoscale_max_slots=NUMBER_OF_AUTOSCALING_SLOTS \
    --reservation RESERVATION_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation
  - `  NUMBER_OF_BASELINE_SLOTS  ` : the number of baseline slots to allocate to the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.
  - `  NUMBER_OF_AUTOSCALING_SLOTS  ` : the number of autoscaling slots assigned to the reservation. This is equal to the value of the max reservation size minus the number of baseline slots.

### Python

Install the [google-cloud-bigquery-reservation package](/python/docs/reference/bigqueryreservation/latest) before using this code sample. Construct a [ReservationServiceClient](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.services.reservation_service.ReservationServiceClient#google_cloud_bigquery_reservation_v1_services_reservation_service_ReservationServiceClient) . Describe the updated properties with a [Reservation](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.types.Reservation) and the [FieldMask.paths](https://googleapis.dev/python/protobuf/latest/google/protobuf/field_mask_pb2.html#google.protobuf.field_mask_pb2.FieldMask.paths) property. Update the reservation with the [update\_reservation](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.services.reservation_service.ReservationServiceClient#google_cloud_bigquery_reservation_v1_services_reservation_service_ReservationServiceClient_update_reservation) method.

``` python
# TODO(developer): Set project_id to the project ID containing the
# reservation.
project_id = "your-project-id"

# TODO(developer): Set location to the location of the reservation.
# See: https://cloud.google.com/bigquery/docs/locations for a list of
# available locations.
location = "US"

# TODO(developer): Set reservation_id to a unique ID of the reservation.
reservation_id = "sample-reservation"

# TODO(developer): Set slot_capicity to the new number of slots in the
# reservation.
slot_capacity = 50

# TODO(developer): Choose a transport to use. Either 'grpc' or 'rest'
transport = "grpc"

# ...

from google.cloud.bigquery_reservation_v1.services import reservation_service
from google.cloud.bigquery_reservation_v1.types import (
    reservation as reservation_types,
)
from google.protobuf import field_mask_pb2

reservation_client = reservation_service.ReservationServiceClient(
    transport=transport
)

reservation_name = reservation_client.reservation_path(
    project_id, location, reservation_id
)
reservation = reservation_types.Reservation(
    name=reservation_name,
    slot_capacity=slot_capacity,
)
field_mask = field_mask_pb2.FieldMask(paths=["slot_capacity"])
reservation = reservation_client.update_reservation(
    reservation=reservation, update_mask=field_mask
)

print(f"Updated reservation: {reservation.name}")
print(f"\tslot_capacity: {reservation.slot_capacity}")
```

### Configure whether queries use idle slots

The `  --ignore_idle_slots  ` flag controls whether queries running in a reservation can use idle slots from other reservations. For more information, see [Idle slots](/bigquery/docs/slots#idle_slots) . You can update this configuration on an existing reservation.

To update a reservation, use the `  bq update  ` command with the `  --reservation  ` flag . The following example sets `  --ignore_idle_slots  ` to `  true  ` , meaning the reservation will only use slots allocated to the reservation.

``` text
bq update \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --ignore_idle_slots=true \
    --reservation RESERVATION_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.

### List the idle slot configuration

To list the [idle slots](/bigquery/docs/slots#idle_slots) setting for a reservation, do the following:

### SQL

Query the `  ignore_idle_slots  ` column of the [`  INFORMATION_SCHEMA.RESERVATIONS_BY_PROJECT  ` view](/bigquery/docs/information-schema-reservations#schema) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    SELECT
      reservation_name,
      ignore_idle_slots
    FROM
      `ADMIN_PROJECT_ID.region-LOCATION`.INFORMATION_SCHEMA.RESERVATIONS_BY_PROJECT;
    ```
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resources
      - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservations

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

Use the `  bq ls  ` command with the `  --reservation  ` flag:

``` text
bq ls --reservation \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resources
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservations

The `  ignoreIdleSlots  ` field contains the configuration setting.

## Delete reservations

If you delete a reservation, any running jobs that use slots from that reservation fail. To prevent errors, allow running jobs to complete before you delete the reservation.

### Required permissions

To delete a reservation, you need the following Identity and Access Management (IAM) permission:

  - `  bigquery.reservations.delete  ` on the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that maintains ownership of the commitments.

Each of the following predefined IAM roles includes this permission:

  - `  BigQuery Admin  `
  - `  BigQuery Resource Admin  `
  - `  BigQuery Resource Editor  `

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

**Caution:** You can delete a reservation with active commitments, but you are still charged for the remaining duration of the commitment. Deleting the reservation or switching associated projects to on-demand pricing doesn't stop these charges. For more information about commitment expiration, see [commitment expiration](/bigquery/docs/reservations-commitments#commitment_expiration) . For additional help with reservations, commitments, or costs, contact [Google Cloud Support](/bigquery/docs/getting-support) .

### Delete a reservation

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Click the **Reservations** tab.

4.  Find the reservation you want to delete.

5.  Expand the more\_vert **Actions** option.

6.  Click **Delete** .

7.  In the **Delete reservation** dialog, click **Delete** .

### SQL

To delete a reservation, use the [`  DROP RESERVATION  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#drop_reservation_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    DROP RESERVATION
      `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME`;
    ```
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
      - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation
      - `  RESERVATION_NAME  ` : the ID of the reservation

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### bq

To delete a reservation, use the `  bq rm  ` command with the `  --reservation  ` flag:

``` text
bq rm \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --reservation RESERVATION_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.

### Python

Install the [google-cloud-bigquery-reservation package](/python/docs/reference/bigqueryreservation/latest) before using this code sample. Construct a [ReservationServiceClient](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.services.reservation_service.ReservationServiceClient#google_cloud_bigquery_reservation_v1_services_reservation_service_ReservationServiceClient) . Delete the reservation with the [delete\_reservation](/python/docs/reference/bigqueryreservation/latest/google.cloud.bigquery_reservation_v1.services.reservation_service.ReservationServiceClient#google_cloud_bigquery_reservation_v1_services_reservation_service_ReservationServiceClient_delete_reservation) method.

``` python
# TODO(developer): Set project_id to the project ID containing the
# reservation.
project_id = "your-project-id"

# TODO(developer): Set location to the location of the reservation.
# See: https://cloud.google.com/bigquery/docs/locations for a list of
# available locations.
location = "US"

# TODO(developer): Set reservation_id to a unique ID of the reservation.
reservation_id = "sample-reservation"

# TODO(developer): Choose a transport to use. Either 'grpc' or 'rest'
transport = "grpc"

# ...

from google.cloud.bigquery_reservation_v1.services import reservation_service

reservation_client = reservation_service.ReservationServiceClient(
    transport=transport
)
reservation_name = reservation_client.reservation_path(
    project_id, location, reservation_id
)
reservation_client.delete_reservation(name=reservation_name)

print(f"Deleted reservation: {reservation_name}")
```

## Control access to reservations

You can control which users have access to specific reservations. For a user to override a reservation on their query, they must have the `  reservations.use  ` permission on that reservation.

### Required permissions

To get the permission that you need to specify a particular reservation for your job, ask your administrator to grant you the [Resource Editor](/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor) ( `  roles/bigquery.resourceEditor  ` ) IAM role on the reservation resource. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  reservations.use  ` permission, which is required to specify a particular reservation for your job.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Control access to a reservation

To manage access to a specific reservation resource, use the [`  bq set-iam-policy  `](/bigquery/docs/reference/bq-cli-reference#bq_set-iam-policy) command.

To manage access to multiple reservation resources, use the Google Cloud console to grant the BigQuery Resource Editor role on the project, folder, or organization. When you grant the role, use an [IAM condition](/bigquery/docs/conditions) to allow access to the reservation resources when the specified conditions are met.

To control access to reservations, do one of the following:

### Console

In the Google Cloud console, you can allow access to multiple reservation resources by using a condition.

1.  In the Google Cloud console, go to the **IAM** page.

2.  Select a project, folder, or organization.

3.  To grant the `  bigquery.resourceEditor  ` role to a principal who has a role on the reservation resources:
    
    1.  On the **View by principals** tab, navigate to the appropriate principal or use the **Filter** option to find the principal.
    
    2.  Click edit **Edit principal** .
    
    3.  On the **Assign roles** page, click add **Add roles** .
    
    4.  In the **Search for roles** field, enter `  bigquery.resourceEditor  ` .
    
    5.  Check the **BigQuery Resource Editor** option in the search results and then click **Apply.**
    
    6.  Click **Save** .

4.  Alternatively, to grant the `  bigquery.resourceEditor  ` role to a principal who doesn't have a role on the reservation resources:
    
    1.  Click person\_add **Grant Access** .
    
    2.  On the **Add principals** page, in the **New principals** field, enter the principal's identifier — for example, `  my-user@example.com  ` .
    
    3.  Click add **Add roles** .
    
    4.  In the **Search for roles** field, enter `  bigquery.resourceEditor  ` .
    
    5.  Check the **BigQuery Resource Editor** option in the search results and then click **Apply.**
    
    6.  In the **BigQuery Resource Editor** box, click **Add condition** .
    
    7.  On the **Add condition** page:
        
        1.  Enter values in the **Title** and **Description** fields.
        
        2.  In the **Condition builder** , add your condition. For example, to add a condition that grants the role to all reservation names that end with `  /reservation1  ` , for **Condition type** , choose **Name** , for **Operator** , choose **Ends with** , and for **Value** , enter `  /reservation1  ` .
        
        3.  Click **Save** .

5.  Click **Save** .

### bq

In the bq command-line tool, you can grant access to an individual reservation resource.

To grant access to a reservation, use the [`  bq set-iam-policy  `](/bigquery/docs/reference/bq-cli-reference#bq_set-iam-policy) command:

``` bash
bq set-iam-policy --reservation RESOURCE FILE_NAME
```

Replace the following:

  - `  RESOURCE  ` : the reservation identifier. For example, `  project1:US.reservation1  ` .

  - `  FILE_NAME  ` : the file that contains the policy in JSON format. The format should follow the [IAM policy structure](/iam/docs/allow-policies#structure) for allow policies. For example:
    
    ``` text
    {
      "bindings": [
        {
          "members": [
            "user:my-user@example.com"
          ],
          "role": "roles/bigquery.resourceEditor"
        }
      ],
      "etag": "BwUjMhCsNvY=",
      "version": 1
    }
    ```

For more information about IAM, see [Manage access to other resources](/iam/docs/manage-access-other-resources) .

## Prioritize idle slots with reservation groups

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To request support or provide feedback for this feature, contact <bigquery-wlm-feedback@google.com> .

You can control which reservations get priority access to idle slots by creating a reservation group. Reservations within a reservation group will share idle slots with each other before they are available to other reservations in the project.

Before you create a reservation group, you must first enable [reservation-based fairness](/bigquery/docs/slots#fairness) .

### Required permissions

To get the permissions that you need to update a particular reservation to set the reservation group, ask your administrator to grant you the [Reservation Editor](/iam/docs/roles-permissions/bigquery#bigquery.reservationEditor) ( `  roles/bigquery.reservationEditor  ` ) IAM role on the reservation resource. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Create reservation group

To create a reservation group:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Select the checkbox next to the reservation that you want to add to a group.

4.  Click **Create reservation group** button in the table header.

5.  In the **Create reservation group** pane, enter your group name in **Group name** field.

6.  Optional: In the **Reservations** field, select additional reservations to be added to the group. Click **OK** .

7.  Click **Create** .

The new reservation group is visible in the **Slot reservations** tab.

### bq

To create a reservation, use the `  bq mk  ` command with the `  --reservation  ` flag:

``` text
bq mk \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --alpha=reservation_groups \
    --reservation_group \
    RESERVATION_GROUP_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation.
  - `  RESERVATION_GROUP_NAME  ` : the name of the reservation group. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.

### Add a reservation to a reservation group

To add a reservation to a reservation group, update the `  reservation_group  ` property of the reservation:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Expand the more\_vert **Actions** option.

4.  Click **Edit** .

5.  In the **Edit reservation group** pane, select the reservations to be added in the **Reservations** field. Click **OK** .

6.  Click **Save** .

The reservation group is updated with the latest member reservations.

### bq

To update the reservation and set the reservation group, use the `  bq update  ` command with the `  --reservation  ` flag:

``` text
bq update \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --alpha=reservation_groups \
    --reservation_group_name=RESERVATION_GROUP_NAME \
    --reservation RESERVATION_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation
  - `  RESERVATION_GROUP_NAME  ` : the name of the reservation group. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.
  - `  RESERVATION_NAME  ` : the name of the reservation. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.

### Listing the reservations that have a reservation group

To list the reservation group information for your reservations, do the following:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  In the **Slot reservations** tab, you can see both reservation groups and reservations (without a parent group) in the table.

4.  Click the expansion button next to a reservation group, the reservation group row is expanded to show the member reservations in the following rows.

### bq

To list the reservations and include the reservation group information, use the `  bq ls  ` command with the `  --reservation  ` and `  --alpha=reservation_groups  ` flags:

``` text
bq ls \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --alpha=reservation_groups \
    --reservation
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation

### Remove a reservation from a reservation group

To remove a reservation from a reservation group, update the `  reservation_group  ` property of the reservation to be the empty string:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Expand the more\_vert **Actions** option.

4.  Click **Edit** .

5.  In the **Edit reservation group** pane, select the reservations to be removed in the **Reservations** field. Click **OK** .

6.  Click **Save** .

The reservation group is updated with the latest member reservations.

If the reservation to be removed is the last one in the group:

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Capacity management** .

3.  Expand the more\_vert **Actions** option.

4.  Click **Edit** .

5.  Click **Ungroup** in the **Edit reservation group** pane.

The reservation group is deleted.

### bq

To remove the reservation from the reservation group, use the `  bq update  ` command with the `  --reservation  ` flag:

``` text
bq update \
    --project_id=ADMIN_PROJECT_ID \
    --location=LOCATION \
    --alpha=reservation_groups \
    --reservation_group_name="" \
    --reservation RESERVATION_NAME
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID
  - `  LOCATION  ` : the [location](/bigquery/docs/locations) of the reservation
  - `  NUMBER_OF_BASELINE_SLOTS  ` : the number of baseline slots to allocate to the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation. The name can contain only lowercase alphanumeric characters or dashes, must start with a letter and must not end with a dash, and the maximum length is 64 characters.

To learn more about reservation groups, see [Reservation groups](/bigquery/docs/reservations-workload-management#groups) .

## Troubleshoot

You might encounter the following errors when creating or updating a reservation:

  - Error: `  Max reservation size can only be configured in multiples of 50, except when covered by excess commitments.  `  
    Error: `  Baseline slots can only be configured in multiples of 50, except when covered by excess commitments.  `  
    Slots always autoscale to a multiple of 50. Scaling up is based on actual usage, and is rounded up to the nearest 50 slot increment. When there is no commitment or if the commitment cannot cover the increases, the baseline and autoscaling slots can only be increased in multiples of 50.
    If `  reservation size - baseline slots  ` isn't a multiple of 50, then the reservation can't scale up to the maximum reservations size, resulting in this error.
    **Resolution:**
      - Purchase more capacity commitments to cover the slot increases.
      - Choose baseline and max slots that are increments of 50.

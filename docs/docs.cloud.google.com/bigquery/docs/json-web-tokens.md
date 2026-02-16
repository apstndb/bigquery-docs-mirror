# Authenticate with JWTs

The BigQuery API accepts [JSON Web Tokens (JWTs)](https://datatracker.ietf.org/doc/rfc7519/) to authenticate requests.

As a best practice, you should use [Application Default Credentials (ADC) to authenticate to BigQuery](/bigquery/docs/authentication) . If you can't use ADC and you're using a service account for authentication, then you can [use a signed JWT](https://developers.google.com/identity/protocols/oauth2/service-account#jwt-auth) instead. JWTs let you make an API call without a network request to Google's authorization server.

You can use JWTs to authenticate in the following ways:

  - For service account keys created in Google Cloud console or by using the gcloud CLI, [use a client library](#client-libraries) that provides JWT signing.
  - For system-managed service accounts, [use the REST API or the gcloud CLI](#rest-gcloud) .

### Scope and Audience

Use [scopes](https://developers.google.com/identity/protocols/oauth2/scopes) with service account when possible. If not possible, you can use an [audience claim](https://datatracker.ietf.org/doc/html/rfc7519#section-4.1.3) . For the BigQuery APIs, set the audience value to `  https://bigquery.googleapis.com/  ` .

### Create JWTs with client libraries

For service account keys created in Google Cloud console or by using the gcloud CLI, use a client library that provides JWT signing. The following list provides some appropriate options for popular programming languages:

  - Go: [func JWTAccessTokenSourceFromJSON](https://pkg.go.dev/golang.org/x/oauth2/google#JWTAccessTokenSourceFromJSON)
  - Java: [Class ServiceAccountCredentials](/java/docs/reference/google-auth-library/latest/com.google.auth.oauth2.ServiceAccountCredentials)
  - Node.js: [Class JWTAccess](/nodejs/docs/reference/google-auth-library/latest/google-auth-library/jwtaccess)
  - PHP: [ServiceAccountJwtAccessCredentials](/php/docs/reference/cloud-bigquery/latest#authentication)
  - Python: [google.auth.jwt module](https://googleapis.dev/python/google-auth/latest/reference/google.auth.jwt.html)
  - Ruby: [Class: Google::Auth::ServiceAccountJwtHeaderCredentials](https://www.rubydoc.info/gems/googleauth/Google/Auth/ServiceAccountJwtHeaderCredentials)

#### Java example

The following example uses the [BigQuery client library for Java](/bigquery/docs/quickstarts/quickstart-client-libraries) to create and sign a JWT. The default scope for BigQuery API is set to `  https://www.googleapis.com/auth/bigquery  ` in the client library.

``` text
import com.google.auth.oauth2.ServiceAccountCredentials;
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.common.collect.ImmutableList;

import java.io.FileInputStream;
import java.io.IOException;
import java.net.URI;

public class Example {
    public static void main(String... args) throws IOException {
        String projectId = "myproject";
        // Load JSON file that contains service account keys and create ServiceAccountCredentials object.
        String credentialsPath = "/path/to/key.json";
        ServiceAccountCredentials credentials = null;
        try (FileInputStream is = new FileInputStream(credentialsPath)) {
          credentials =  ServiceAccountCredentials.fromStream(is);
          // The default scope for BigQuery is used.
          // Alternatively, use `.setScopes()` to set custom scopes.
          credentials = credentials.toBuilder()
              .setUseJwtAccessWithScope(true)
              .build();
        }
        // Instantiate BigQuery client with the credentials object.
        BigQuery bigquery =
                BigQueryOptions.newBuilder().setCredentials(credentials).build().getService();
        // Use the client to list BigQuery datasets.
        System.out.println("Datasets:");
        bigquery
            .listDatasets(projectId)
            .iterateAll()
            .forEach(dataset -> System.out.printf("%s%n", dataset.getDatasetId().getDataset()));
    }
}
```

### Create JWTs with REST or the gcloud CLI

For system-managed service accounts, you must manually assemble the JWT, then use the REST method [`  projects.serviceAccounts.signJwt  `](/iam/docs/reference/credentials/rest/v1/projects.serviceAccounts/signJwt) or the Google Cloud CLI command [`  gcloud beta iam service-accounts sign-jwt  `](https://cloud.google.com/sdk/gcloud/reference/beta/iam/service-accounts/sign-jwt) to sign the JWT. To use either of these approaches, you must be a member of the [Service Account Token Creator](/iam/docs/roles-permissions/iam#iam.serviceAccountTokenCreator) Identity and Access Management role.

#### gcloud CLI example

The following example shows a bash script that assembles a JWT and then uses the `  gcloud beta iam service-accounts sign-jwt  ` command to sign it.

``` text
#!/bin/bash

SA_EMAIL_ADDRESS="myserviceaccount@myproject.iam.gserviceaccount.com"

TMP_DIR=$(mktemp -d /tmp/sa_signed_jwt.XXXXX)
trap "rm -rf ${TMP_DIR}" EXIT
JWT_FILE="${TMP_DIR}/jwt-claim-set.json"
SIGNED_JWT_FILE="${TMP_DIR}/output.jwt"

IAT=$(date '+%s')
EXP=$((IAT+3600))

cat <<EOF > $JWT_FILE
{
  "aud": "https://bigquery.googleapis.com/",
  "iat": $IAT,
  "exp": $EXP,
  "iss": "$SA_EMAIL_ADDRESS",
  "sub": "$SA_EMAIL_ADDRESS"
}
EOF

gcloud beta iam service-accounts sign-jwt --iam-account $SA_EMAIL_ADDRESS $JWT_FILE $SIGNED_JWT_FILE

echo "Datasets:"
curl -L -H "Authorization: Bearer $(cat $SIGNED_JWT_FILE)" \
-X GET \
"https://bigquery.googleapis.com/bigquery/v2/projects/myproject/datasets?alt=json"
```

## What's next

  - Learn more about [BigQuery authentication](/bigquery/docs/authentication) .
  - Learn how to [authenticate with end-user credentials](/bigquery/docs/authentication/end-user-installed) .

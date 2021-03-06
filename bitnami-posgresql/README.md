# Tanzu Service Manager with Postgresql

This example uses the [Bitnami Postgresql Chart](https://github.com/bitnami/charts/tree/master/bitnami/postgresql)
to provision an instance.

The `overrides-postgresql.yaml` file changes the service type to add a load-balancer, as the default
chart uses ClusterIP. This example also sets the name of the database and uses that in `bind.yaml`.


#### Chart Notes

For the root user's password, this chart by default uses Helm's `randAlphaNum` helper for the password.
This means that any upgrade or other change that re-deploys the chart will result
in a password change, and thus require binding the service instance again. To mitigate this and
control when the password changes at the end user level, use
`create-service` configuration parameters:

```bash
cf create-service postgresql default my-postgresql -c '{"postgresqlPostgresPassword": "some-secure-string"}'
```

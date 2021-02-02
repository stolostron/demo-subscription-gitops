# Creating a Service Now keep-alive using a ticket
## Modify the YAML
1. Update the `snow-keepalive-cronjob.yaml` update the `env` variables with the approriate, token, URL, job name, namespace and adjust the time to run, once every 24hrs
2. Do the same for `snow-keepalive-job.yaml` if you want to run the independent job
3. Apply the cronjob `oc -n NAMESPACE apply -k ansible/keepalive` where NAMESPACE is going to host your cronjob
4. Check on the cronjob `oc get cronjob`, this also creates an ansible job that is referenced for the `spec.extra_vars` values.


## env variables that you need to fill
```yaml
TOWER_OAUTH_TOKEN       # This is the token for accessing Ansible Tower
TOWER_HOST              # URL to the Ansible Tower
TOWER_JOB_TEMPLATE_NAME # The name of the job template to use
ANSIBLEJOB_NAMESPACE    # Namespace where this cronjob is being created/run

# Change these settings in snow-keepalive-cronjob.yaml and snow-keepalive-job.yaml
```
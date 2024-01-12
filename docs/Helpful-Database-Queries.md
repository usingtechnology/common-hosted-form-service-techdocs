[Home](index) > [Developer](Developer) > [DevOps](DevOps) > **Helpful Database Queries**
***

Sometimes it's necessary to run queries against the database to help solve a problem. Be sure to port-forward from a replica (read-only) database pod so that:
1. You don't accidentally change data
1. Your queries don't add CPU/memory load to the primary database pod that CHEFS uses

```bash
oc -n [NAMESPACE] port-forward svc/patroni-master-readonly 54321:5432
```

Some helpful queries are:

#### The form permissions for a user

When a user has a problem with a form, they often don't mention which form it is. The following query will tell you which forms that a user has access to. If the user only has one form, it saves asking them for the form name or id.

```sql
SELECT * FROM user_form_access_vw WHERE "userId" = '${USER_ID}';
```

#### The number of submissions for a form

Gets the number of non-draft and non-deleted submissions and groups them by version. This is useful when someone says they did an export but it was empty - there may be no submissions for the version they're exporting!

```sql
SELECT version, count(*) FROM form_submission JOIN form_version ON form_submission."formVersionId" = form_version.id
    WHERE form_version."formId" = '${formId}'
    AND form_submission.draft = false AND form_submission.deleted = false
    GROUP BY version ORDER BY version;
```

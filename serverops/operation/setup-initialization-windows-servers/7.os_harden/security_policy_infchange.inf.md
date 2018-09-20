# security\_policy\_infchange.inf

{% code-tabs %}
{% code-tabs-item title="security\_policy\_infchange.inf" %}
```text
[Unicode]
[System Access]
ClearTextPassword = 0
PasswordComplexity = 1
LSAAnonymousNameLookup = 0
[Event Audit]
[Registry Values]
[Privilege Rights]
SeRemoteShutdownPrivilege = *S-1-5-32-544
SeShutdownPrivilege = *S-1-5-32-544
[Version]
signature="$CHICAGO$"
Revision=1
```
{% endcode-tabs-item %}
{% endcode-tabs %}


# Notes

## [iRules after 14.1](https://support.f5.com/csp/article/K23237429)

- new Bigip versions such as v14.1.x and v15.x have an improvement fix for iRules ID737252 where the Bigip would send RST to client if one iRule already sent an HTTP::respond event in HTTP_REQUEST, while another iRule assigned to the same virtual tries to access HTTP context (i.e set HTTP::host)
- support article: [K23237429](https://support.f5.com/csp/article/K23237429)
- We provided many workarounds for the customer as below:
  1. return to previous behavior as they initially requested: #tmsh modify sys db tmm.http.tcl.validation value disable.
  2. check for var Has_Responded before trying to modify an HTTP context if conflicting iRules are assigned to the same virtual.
  3. once an iRule sends a HTTP::respond/redirect make sure to disable event all after that line so that other iRules dont attempt to change anything on the context.
  4. Adjust priorities of execution on iRules (needs good understanding of customer requirements as they seem to have different iRules that needs to be priorities first and this indicates the lack of original design in their iRules implementation).


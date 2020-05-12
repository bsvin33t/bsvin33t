`default_scope` bring some degrees of convenience, however, most of the DB queries are application logic. Applying `default_scope` may payoff when filtering out soft deleted object, but most of cases are rarely justified. Even you could identifid the `where` clause from SQL log, the situation quickly becomes ugly and turns into a horror movie when joining multiple tables with `default_scope`. Modifying those queries with `unscope` is risky and query specs of such are likely to be not fully covered to provide the safety net.


By my colleague Tony. 

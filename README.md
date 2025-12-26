UPDATE T_AUDIT_TRAIL_AT at
SET at.AT_ACTION = 'CREATE'
WHERE at.AT_ID IN (
    SELECT at2.AT_ID
    FROM T_AUDIT_TRAIL_AT at2
    JOIN T_EVENT_DETAIL_ED ed
      ON ed.ED_AUDIT_TRAIL_ID = at2.AT_ID
    WHERE at2.AT_ACTION = 'UPDATE'
      AND at2.AT_TARGET = 'INSURANCE_CONTRACT'
      AND ed.ED_EVENT_DETAIL_VALUE = 'BULK_RENEW'
);
-----++++++++--

databaseChangeLog:
  - changeSet:
      id: E2ECC-88071-update-audit-action-bulk-renew
      author: c25661
      changes:
        - sql:
            comment: >
              Update audit action from UPDATE to CREATE for bulk renew insurance contracts
            sql: |
              UPDATE T_AUDIT_TRAIL_AT at
              SET at.AT_ACTION = 'CREATE'
              WHERE at.AT_ID IN (
                  SELECT at2.AT_ID
                  FROM T_AUDIT_TRAIL_AT at2
                  JOIN T_EVENT_DETAIL_ED ed
                    ON ed.ED_AUDIT_TRAIL_ID = at2.AT_ID
                  WHERE at2.AT_ACTION = 'UPDATE'
                    AND at2.AT_TARGET = 'INSURANCE_CONTRACT'
                    AND ed.ED_EVENT_DETAIL_VALUE = 'BULK_RENEW'
              );



    _+++++------++-+-+-+


    databaseChangeLog:
  - changeSet:
      id: E2ECC-88071-update-audit-action-bulk-renew
      author: h59959
      changes:
        - sql:
            comment: Fix audit action for bulk renew insurance contracts
            sql: |
              UPDATE T_AUDIT_TRAIL_AT
              SET AT_ACTION = 'CREATE'
              WHERE AT_ID IN (
                  SELECT at2.AT_ID
                  FROM T_AUDIT_TRAIL_AT at2
                  JOIN T_EVENT_DETAIL_ED ed
                    ON ed.ED_AUDIT_TRAIL_ID = at2.AT_ID
                  WHERE at2.AT_ACTION = 'UPDATE'
                    AND at2.AT_TARGET = 'INSURANCE_CONTRACT'
                    AND ed.ED_EVENT_DETAIL_VALUE = 'BULK_RENEW'
              );

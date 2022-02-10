# Postgres tricks

## Foreign check and BEFORE INSERT trigger

So, if you want to automaticall fill a foreign key refence table with a trigger use the DEFERRABLE option:

ref: https://dba.stackexchange.com/questions/164474/foreign-key-violation-within-trigger-on-insert-of-new-id-in-other-table-as-for

```sql
ALTER TABLE table_a
    ADD CONSTRAINT table_a_col_name_table_b_fk FOREIGN KEY (col_name)
    REFERENCES table_b (col_name)
    ON UPDATE NO ACTION   /* or whichever action is deemed appropriate */
    ON DELETE NO ACTION   /* or whichever action is deemed appropriate */
    DEFERRABLE INITIALLY DEFERRED;
```

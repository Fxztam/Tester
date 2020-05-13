```pl/sql
BEGIN
   EXECUTE IMMEDIATE '
            CREATE or REPLACE PROCEDURE drop_object (p_type VARCHAR2, p_name VARCHAR2) IS
                BEGIN
                    EXECUTE IMMEDIATE ''drop ''||p_type||''  ''||p_name;
                EXCEPTION WHEN OTHERS THEN NULL;
            END drop_object;
    ';
EXCEPTION WHEN OTHERS THEN NULL;
END;
/

BEGIN
   FOR ct in (select Table_name tabname from user_tables) 
   LOOP
      BEGIN
	  dbms_output.put_line(ct.tabname);
          drop_object('table', upper(ct.tabname));
      EXCEPTION WHEN OTHERS THEN NULL;
      END;
   END LOOP;
END drop_tables;
/
```

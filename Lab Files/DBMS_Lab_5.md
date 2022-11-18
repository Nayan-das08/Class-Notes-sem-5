%%[[_Lab Files]]%%
%%#lab/dbms%% 
# Experiment 5
Oct 28, 2022

## Objective
To explore procedures and functions in **PL/SQL**.

---
## Theory
### `PROCEDURE`
A `PROCEDURE` is a subprogram or a PL/SQL program module that does not return a value directly and are mainly used to perform an action..

### `FUNCTION`
A `FUNCTION` is a subprogram or a PL/SQL program module that returns a single value and are mainly used to compute and return a value.

---
## **Code and Output:**

### Source Code
```
-- FUNCTION AND PROCEDURE TO TEST ODD OR EVEN
DECLARE
    X NUMBER;

FUNCTION ODD_EVEN_FUNC ( X IN NUMBER )
RETURN BOOLEAN
IS
BEGIN
    IF MOD ( X, 2 ) = 0 THEN
        RETURN TRUE;
    ELSE
        RETURN FALSE;
    END IF;
END;

PROCEDURE ODD_EVEN_PROC ( X IN NUMBER )
IS
BEGIN
    IF MOD ( X, 2 ) = 0 THEN
        DBMS_OUTPUT.PUT_LINE ( X || ' is even (procedure)' );
    ELSE
        DBMS_OUTPUT.PUT_LINE ( X || ' is odd (procedure)' );
    END IF;
END;

BEGIN
    X := &X;

    ODD_EVEN_PROC ( X => X );

    IF ODD_EVEN_FUNC ( X => X ) = TRUE THEN
        DBMS_OUTPUT.PUT_LINE ( X || ' is even (function)' );
    ELSE
        DBMS_OUTPUT.PUT_LINE ( X || ' is odd (function)' );
    END IF;
END;

/
```

Output:
```
SQL> @oddeven
Enter value for x: 5
old  26:     X := &X;
new  26:     X := 5;
5 is odd (procedure)
5 is odd (function)

PL/SQL procedure successfully completed.
```

---
### Source Code
```
-- FUNCTION AND PROCEDURE TO GET CUBE
DECLARE
    X NUMBER;
    Y NUMBER;

FUNCTION CUBE_FUNC ( X IN NUMBER )
RETURN INTEGER
IS
BEGIN
    RETURN X * X * X;
END;

PROCEDURE CUBE_PROC ( X IN OUT NUMBER )
IS
BEGIN
    X := X * X * X;
END;

BEGIN
    X := &X;
    Y := X;

    DBMS_OUTPUT.PUT_LINE (
        X ||
        ' ^ 3 = ' ||
        CUBE_FUNC ( X => X ) ||
        ' (function)'
    );

    CUBE_PROC ( X => Y );

    DBMS_OUTPUT.PUT_LINE ( X || ' ^ 3 = ' || Y || ' (procedure)' );
END;

/
```

Output
```
SQL> @cube
Enter value for x: 6
old  19:     X := &X;
new  19:     X := 6;
6 ^ 3 = 216 (function)
6 ^ 3 = 216 (procedure)

PL/SQL procedure successfully completed.
```

---
### Source Code
```
-- FUNCTION AND PROCEDURE TO FIND GREATER NUMBER
DECLARE
    X NUMBER;
    Y NUMBER;
    Z NUMBER;

FUNCTION GREATER_FUNC ( X IN NUMBER, Y IN NUMBER )
RETURN NUMBER
IS
BEGIN
    IF X >= Y THEN
        RETURN X;
    ELSE
        RETURN Y;
    END IF;
END;

PROCEDURE GREATER_PROC ( X IN NUMBER, Y IN NUMBER, Z OUT NUMBER )
IS
BEGIN
    IF X >= Y THEN
        Z := X;
    ELSE
        Z := Y;
    END IF;
END;

BEGIN
    X := &X;
    Y := &Y;

    GREATER_PROC ( X => X, Y => Y, Z => Z );

    DBMS_OUTPUT.PUT_LINE (
        GREATER_FUNC ( X => X, Y => Y ) ||
        ' is the greater of ' ||
        X ||
        ' and ' ||
        Y ||
        ' (function)'
    );

    DBMS_OUTPUT.PUT_LINE (
        Z ||
        ' is the greater of ' ||
        X ||
        ' and ' ||
        Y ||
        ' (procedure)'
    );
END;

/
```

Output
```
SQL> @greaterthan
Enter value for x: 5
old  28:     X := &X;
new  28:     X := 5;
Enter value for y: 20
old  29:     Y := &Y;
new  29:     Y := 20;
20 is the greater of 5 and 20 (function)
20 is the greater of 5 and 20 (procedure)       

PL/SQL procedure successfully completed.
```

---
### Source Code
```
-- FUNCTION TO FIND FACTORIAL
DECLARE
    X INTEGER;
    Y INTEGER;

FUNCTION FACTORIAL ( X IN INTEGER )
RETURN INTEGER
IS
BEGIN
    IF X = 1 THEN
        RETURN 1;
    ELSE
        RETURN X * FACTORIAL ( X - 1 );
    END IF;
END;

BEGIN
    X := &X;
    Y := FACTORIAL( X );

    DBMS_OUTPUT.PUT_LINE ( X || '! = ' || Y );
END;

/
```

Output
```
SQL> @factorial
Enter value for x: 15
old  17:     X := &X;
new  17:     X := 15;
15! = 1307674368000

PL/SQL procedure successfully completed.
```

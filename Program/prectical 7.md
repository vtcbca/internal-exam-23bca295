## practical 7


```python
import sqlite3 as sq
```


```python
con=sq.connect("D:/23BCA295/sqlite2/database/contect.db")
```


```python
c=con.cursor()
```

## create table


```python
c.execute("create table if not exists contect(fname,lname,contact,email,city)")
```




    <sqlite3.Cursor at 0x234754717c0>




```python
c.execute("insert into contect values('ammar','tai',2255886644,'ammar123@gmail.com','portugal'), ('aadil','hafeji',1313131331,'aadil@gmail.com','rome'), ('parth','patel','2525252255','parth@gmail.com','lisbon'),  ('jeet','patel',131232132,'jeet@gmail.com','birlin'),('jenish','patel',213546546,'jenish@gmail.com','poland'), ('harsh','patel',1231231123,'jenish@gmail.com','mumbai'), ('raj','patel',21321321,'raj@gmail.com','surat'), ('om','patel',55751054895,'om@gmail.com','bardoli')")

```




    <sqlite3.Cursor at 0x234754717c0>




```python
c.execute(" CREATE TABLE logtable ( operation_name VARCHAR(50),datetime TIMESTAMP DEFAULT CURRENT_TIMESTAMP, fname VARCHAR(50),  lname VARCHAR(50),contact VARCHAR(20),old_contact VARCHAR(20), new_contact VARCHAR(20))")
```




    <sqlite3.Cursor at 0x234754717c0>




```python
c.executemany('''INSERT INTO contect (fname, lname, contact, email, city)VALUES (?, ?, ?, ?, ?)''', records)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[8], line 1
    ----> 1 c.executemany('''INSERT INTO contect (fname, lname, contact, email, city)VALUES (?, ?, ?, ?, ?)''', records)
    

    NameError: name 'records' is not defined


## create trigger


```python
c.execute(''' create trigger if not exists check_trigger
            BEFORE DELETE ON contect
            FOR EACH ROW
            WHEN OLD.fname = 'aadil'
            BEGIN
       DELETE FROM contact WHERE fname = 'aadil';
END;
''')
```




    <sqlite3.Cursor at 0x234754717c0>




```python
c.execute(" DELETE FROM contect WHERE fname = 'aadil' AND lname = 'hafeji'")
```


    ---------------------------------------------------------------------------

    OperationalError                          Traceback (most recent call last)

    Cell In[11], line 1
    ----> 1 c.execute(" DELETE FROM contect WHERE fname = 'aadil' AND lname = 'hafeji'")
    

    OperationalError: no such table: main.contact



```python
c.execute('SELECT * FROM contect')
```




    <sqlite3.Cursor at 0x234754717c0>




```python
rows = c.fetchall()
for row in rows:
    print(row)
```

    ('ammar', 'tai', 2255886644, 'ammar123@gmail.com', 'portugal')
    ('aadil', 'hafeji', 1313131331, 'aadil@gmail.com', 'rome')
    ('parth', 'patel', '2525252255', 'parth@gmail.com', 'lisbon')
    ('jeet', 'patel', 131232132, 'jeet@gmail.com', 'birlin')
    ('jenish', 'patel', 213546546, 'jenish@gmail.com', 'poland')
    ('harsh', 'patel', 1231231123, 'jenish@gmail.com', 'mumbai')
    ('raj', 'patel', 21321321, 'raj@gmail.com', 'surat')
    ('om', 'patel', 55751054895, 'om@gmail.com', 'bardoli')
    

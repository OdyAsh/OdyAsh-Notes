old function using SQLite:
```python
def create_Db():
    '''
    Create a new Database to store Job Details
    '''

    file = filedialog.asksaveasfilename()
    print(file)
    if file == "":
        return
    index = len(file) - file[::-1].index("/")
    path=file[:index]
    fileName = file[index:] + ".sqlite" ^8x-w-


    global conn,cur
    conn = sqlite3.connect(path+fileName, detect_types=sqlite3.PARSE_DECLTYPES | sqlite3.PARSE_COLNAMES)
    conn.execute('pragma foreign_keys=ON')
    cur = conn.cursor()

    cur.execute('''CREATE TABLE if NOT EXISTS Job (
                    ID INTEGER PRIMARY KEY AUTOINCREMENT,
                    jobNo TEXT,
                    name TEXT,
                    surveyDate DATE,
                    timePeriod1 TEXT,
                    timePeriod2 TEXT,
                    timePeriod3 TEXT,
                    timePeriod4 TEXT,
                    noOfCameras INTEGER,
                    interval INTEGER,
                    OVTemplate DATE,
                    OVCounts DATE,
                    unclassed DATE,
                    classed DATE,
                    comparison DATE,
                    completed DATE,
                    createdBy TEXT,
                    createdDate DATE,
                    classification TEXT,
                    folder TEXT,
                    selectedDuplicates INTEGER,
                    plateRestriction INTEGER
                    )''')

    cur.execute('''CREATE TABLE IF NOT EXISTS Site (
                    id	INTEGER PRIMARY KEY AUTOINCREMENT,
                    siteNo INTEGER,
                    jobNo INTEGER,
                    FOREIGN KEY(JobNo) REFERENCES Job(ID)
                )''')

    cur.execute('''CREATE TABLE IF NOT EXISTS Movement (
                    id	INTEGER PRIMARY KEY AUTOINCREMENT,
                    siteID INTEGER,
                    cameraNo TEXT,
                    originalMovementNum INTEGER,
                    combinedMovementNum INTEGER,
                    dir INTEGER,
                    comment TEXT,
                    FOREIGN KEY(siteID) REFERENCES Site(ID)
                )''')
    conn.commit()
    #messagebox.askyesno(message="Do you want to set this new database as the working database?")
    return path+fileName
```

new function using pyodbc:
``` Python
def create_Db():
    '''
    Create a new Database to store Job Details
    '''

    file = filedialog.asksaveasfilename()

    print('file:', file)
    if file == "":
        return
    index = len(file) - file[::-1].index("/")
    path=file[:index]
    fileName = file[index:] # + ".sqlite"
    filePath = os.path.abspath(os.path.join(path, fileName)) 
    print('filePath:', filePath)
    global conn,cur
    conn = pyodbc.connect('Driver={ODBC Driver 17 for SQL Server};Server=<your_data, in my case: LAPTOP-xx>;UID=<your_data>;PWD=<your_data>;'+'FILEDSN=<your_db_name>.dsn')
    # conn = sqlite3.connect(path+fileName, detect_types=sqlite3.PARSE_DECLTYPES | sqlite3.PARSE_COLNAMES)
    print('conn:', conn)
    # conn.execute('pragma foreign_keys=ON')
    cur = conn.cursor()
    conn.autocommit = True
    try:
        cur.execute(f'''CREATE DATABASE {fileName} 
                        ON PRIMARY (NAME={fileName}, FILENAME="{filePath}.mdf") 
                        LOG ON (NAME={fileName}_log, FILENAME="{filePath}.ldf")
                    ''')
    except pyodbc.ProgrammingError as e:
        if ('access is denied' in e.args[1].lower()):
            print('access is denied, will store db files in root directory of local disk D instead')
            filePath = os.path.abspath(os.path.join('D:/', fileName)) 
            cur.execute(f'''CREATE DATABASE {fileName} 
                        ON PRIMARY (NAME={fileName}, FILENAME="{filePath}.mdf") 
                        LOG ON (NAME={fileName}_log, FILENAME="{filePath}.ldf")
                        ''')
        else:
            print(e.args[1])
            return

    conn.autocommit = False

    cur.execute(f'''USE {fileName}''')

    if not cur.tables(table='Job', tableType='TABLE').fetchone():
        cur.execute('''CREATE TABLE Job (
                        ID INT IDENTITY(1,1) PRIMARY KEY,
                        jobNo NVARCHAR(3000),
                        name NVARCHAR(3000),
                        surveyDate DATE,
                        timePeriod1 NVARCHAR(3000),
                        timePeriod2 NVARCHAR(3000),
                        timePeriod3 NVARCHAR(3000),
                        timePeriod4 NVARCHAR(3000),
                        noOfCameras INT,
                        interval INT,
                        OVTemplate DATE,
                        OVCounts DATE,
                        unclassed DATE,
                        classed DATE,
                        comparison DATE,
                        completed DATE,
                        createdBy NVARCHAR(3000),
                        createdDate DATE,
                        classification NVARCHAR(3000),
                        folder NVARCHAR(3000),
                        selectedDuplicates INT,
                        plateRestriction INT
                    )''')
    if not cur.tables(table='Site', tableType='TABLE').fetchone():
        cur.execute('''CREATE TABLE Site (
                        id	INT IDENTITY(1,1) PRIMARY KEY,
                        siteNo INTEGER,
                        jobNo INTEGER,
                        FOREIGN KEY(JobNo) REFERENCES Job(ID)
                    )''')

    if not cur.tables(table='Movement', tableType='TABLE').fetchone():
        cur.execute('''CREATE TABLE Movement (
                        id	INT IDENTITY(1,1) PRIMARY KEY,
                        siteID INTEGER,
                        cameraNo NVARCHAR(3000),
                        originalMovementNum INTEGER,
                        combinedMovementNum INTEGER,
                        dir INTEGER,
                        comment NVARCHAR(3000),
                        FOREIGN KEY(siteID) REFERENCES Site(ID)
                    )''')

    conn.commit()
    #messagebox.askyesno(message="Do you want to set this new database as the working database?")

    return filePath + '.mdf' ^0zvia
```


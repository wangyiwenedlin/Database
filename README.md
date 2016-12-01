# Database
/*
mysql -uroot
mysql> create database spds;
mysql> create user siemens;
mysql> grant all on spds.* to 'siemens'@'localhost' identified by 'JIsiemens2016';
mysql> alter database spds default character set utf8 collate utf8_bin;
mysql -usiemens spds -pJIsiemens2016 < sql/tbl_create.sql
*/

DROP TABLE IF EXISTS Tooling;
DROP TABLE IF EXISTS Equipment;
DROP TABLE IF EXISTS RecordFormInfo;
DROP TABLE IF EXISTS RecordForm;
DROP TABLE IF EXISTS WorkInstructionInfo;
DROP TABLE IF EXISTS WorkInstruction;
DROP TABLE IF EXISTS MQCPInfo;
DROP TABLE IF EXISTS MQCP;
DROP TABLE IF EXISTS ProcessCardInfo;
DROP TABLE IF EXISTS ProcessCard;
DROP TABLE IF EXISTS Product;
DROP TABLE IF EXISTS User;
DROP TABLE IF EXISTS WeldingRecord;
DROP TABLE IF EXISTS WeldingRecordInfo;
DROP TABLE IF EXISTS DimensionRecord;
DROP TABLE IF EXISTS DimensionRecordInfo;
DROP TABLE IF EXISTS PieceInfo;


CREATE TABLE User(	
username VARCHAR(255) PRIMARY KEY,
password VARCHAR(255),
email VARCHAR(255),
phone VARCHAR(20),
company VARCHAR(255)
);

CREATE TABLE Product(
productid INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50),
created TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
creator VARCHAR(20)
);

CREATE TABLE Tooling(
productid INT,
toolingid INT,
id VARCHAR(255),
name VARCHAR(255),
specification VARCHAR(255),
PRIMARY KEY (productid,toolingid),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE Equipment(
productid INT,
equipid INT,
id VARCHAR(255),
name VARCHAR(255),
specification VARCHAR(255),
PRIMARY KEY (productid,equipid),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE ProcessCard(
productid INT,
version TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
current Boolean DEFAULT 0,
released Boolean DEFAULT 0,
filename VARCHAR(255),
PRIMARY KEY (productid,version),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE ProcessCardInfo(
id INT PRIMARY KEY AUTO_INCREMENT,
docid VARCHAR(255),
dept VARCHAR(255),
step INT,
operation TEXT,
spec TEXT,
vgbmkb TEXT,
equipment TEXT,
program TEXT,
material TEXT,
wi TEXT,
result Boolean,
operator VARCHAR(255),
comment TEXT,
other TEXT,
productid INT,
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE MQCP(
productid INT,
version TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
current Boolean DEFAULT 0,
released Boolean DEFAULT 0,
filename VARCHAR(255),
PRIMARY KEY (productid,version),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE MQCPInfo(
id INT PRIMARY KEY AUTO_INCREMENT,
docid VARCHAR(255),
no INT,
multi INT,
operations text,
referencedoc text,
no2 INT,
setuptime VARCHAR(255),
optime VARCHAR(255),
characteristics VARCHAR(255),
ctq VARCHAR(255),
location VARCHAR(255),
dim VARCHAR(255),
lowertol VARCHAR(255),
uppertol VARCHAR(255),
equipment text,
samplesize VARCHAR(255),
docmethod VARCHAR(255),
remark text,
productid INT,
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE WorkInstruction(
productid INT,
version TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
current Boolean DEFAULT 0,
released Boolean DEFAULT 0,
filename VARCHAR(255),
PRIMARY KEY (productid,version),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE WorkInstructionInfo(
id INT PRIMARY KEY AUTO_INCREMENT,
docid VARCHAR(255),
no VARCHAR(255),
content VARCHAR(255),
drawing VARCHAR(255),
data VARCHAR(255),
others VARCHAR(255),
productid INT,
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE RecordForm(
productid INT,
version TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
current Boolean DEFAULT 0,
released Boolean DEFAULT 0,
filename VARCHAR(255),
PRIMARY KEY (productid,version),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE RecordFormInfo(
id INT PRIMARY KEY AUTO_INCREMENT,
docid VARCHAR(255),
serialno INT,
partid VARCHAR(255),
tableno VARCHAR(255),
fixture VARCHAR(255),
depthnominal VARCHAR(255),
depthactual VARCHAR(255),
widthmin Boolean,
widthmax Boolean,
go Boolean,
nogo Boolean,
cutterchange Boolean,
offset Boolean,
operator VARCHAR(255),
opdate VARCHAR(255),
remark VARCHAR(255),
outerinner Boolean,
productid INT,
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);
CREATE TABLE WeldingRecord(
productid INT,
version TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
current Boolean DEFAULT 0,
released Boolean DEFAULT 0,
filename VARCHAR(255),
PRIMARY KEY (productid,version),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE WeldingRecordInfo(
id INT PRIMARY KEY AUTO_INCREMENT,
docid VARCHAR(255),
num INT,
part VARCHAR(255),
welder VARCHAR(255),
material VARCHAR(255),
preparation Boolean,
curr INT,
voltage INT,
speed INT,
height VARCHAR(255),
result Boolean,
productid INT,
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE DimensionalRecord(
productid INT,
version TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
current Boolean DEFAULT 0,
released Boolean DEFAULT 0,
filename VARCHAR(255),
PRIMARY KEY (productid,version),
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE DimensionalRecordInfo(
id INT PRIMARY KEY AUTO_INCREMENT,
docid VARCHAR(255),
proname VARCHAR(255),
componame VARCHAR(255),
unit VARCHAR(255),
componum VARCHAR(255),
drawingmun VARCHAR(255),
standard VARCHAR(255),
qty INT,
rev CHAR(255),
sketch VARCHAR(255),
devalue1 INT,devalue2 INT,devalue3 INT,devalue4 INT,devalue5 INT,
devalue6 INT,devalue7 INT,devalue8 INT,devalue9 INT,devalue10 INT,
deviation1 INT,deviation2 INT,deviation3 INT,deviation4 INT,deviation5 INT,
deviation6 INT,deviation7 INT,deviation8 INT,deviation9 INT,deviation10 INT,
cutst Boolean,
wequality Boolean,
viquality Boolean,
evaluation Boolean,
inspector VARCHAR(255),
qc VARCHAR(255),
date1 DATE,
date2 DATE,
productid INT,
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);

CREATE TABLE PieceInfo(
id INT PRIMARY KEY AUTO_INCREMENT,
docid VARCHAR(255),
piecenum VARCHAR(255),
mevalue1 INT,mevalue2 INT,mevalue3 INT,mevalue4 INT,mevalue5 INT,
mevalue6 INT,mevalue7 INT,mevalue8 INT,mevalue9 INT,mevalue10 INT,
productid INT,
FOREIGN KEY (productid) REFERENCES Product(productid) ON DELETE CASCADE
);


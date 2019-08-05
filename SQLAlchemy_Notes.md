# Advanced SQL / SQL Alchemy Notes (Class #1)

## Connecting to SQLite DB

```
from sqlalchemy import create_engine

database_path = "../Resources/Census_Data.sqlite" 

# Census data is example, replace it with the DB you are working with.

engine = create_engine(f"sqlite:///{database_path}")
```
Now you can query the database by using engine.execute

You can query like in SQL

```
data = engine.execute("SELECT * FROM  Census_Data")
```

Print each record in the database

```
for record in data:
    print(record)
```

## Using Pandas to import Database

```
import pandas as pd
from sqlalchemy import create_engine

database_path = "(set path to your DB)"

# Create Engine

engine = create_engine(f"sqlite:///{database_path}) # This is a MUST
conn = engine.connect()
```
You can import your query into a DB by:

``` 
data = pd.read_sql("SELECT * FROM Census_Data, conn) 

# conn is the connection to the engine
```

Now you can perform pandas functions on the DataFrame "data

## SQL Alchemy

### Setting classes

```
# Dependencies

from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

from sqlalchemy import Column, Integer, String, Float
```

Now create class "Dog" with the table name and then corresponding columns within the table. 

```
class Dog(Base):
        __tablename__ = 'dog'
        id = Column(Integer, primary_key=True)
        name = Column(String(255))
        color = Column(String(255))
        age = Column(Integer)
```
You can then add instances you create to the database. First make the instances:

```
dog = Dog(name="Fido", color='Brown', age=4)
cat = Cat(name="Whiskers", color="Gray", age=7)
```

Then make a connetion to the DB
```
database_path = "pets_db"
engine = create_engine(f"sqlite:///{database_path}")
conn = engine.connect()
```

Create the metadata from the DB. From SQL Alchemy Documentation:

"The declarative_base() base class contains a MetaData object where newly defined Table objects are collected. This object is intended to be accessed directly for MetaData-specific operations. Such as, to issue CREATE statements for all tables:"

```
Base.metadata.create_all(engine)
```
Need to import Session in order to perform CRUD (Create, Read, Update, Delete)

```
from sqlalchemy.orm import Session
session = Session(bind=engine)
```
Now you can add the instances to the DB
```
session.add(dog)
session.add(cat)
session.commit()
```
With Session, you can also query the DB
```
dog_list = session.query(Dog)
for doggy in dog_list:
    print(doggy.name)
```

# Advanced SQL / SQL Alchemy Notes (Class #2)

## Querying a DB using the Sharks example

Import Dependencies
```
from sqlalchemy import create_engine
from sqlalchemy.ext.delcrative import delclarative_base
Base = declraative_base()

from sqlalchemy import Column, Integer, String, Float
```

Create the engine to be able to talk to the DB and also create the metadata so we can extract the info
```
from sqlalchemy import create_engine
database_path = "../Resources/sharks.sqlite"
engine = create_engine(f"sqlite:///{database_path}")
Base.metadata.create_all(engine)
```

Import Session to be able to CRUD later:
```
from sqlalchemy.orm import Session
session = Session(bind=engine)
```

Create the Sharks class to match the database. The class definitions should match the schema of the Database:

```
class Sharks(Base):
    __tablename__ = 'sharks'
    id = Column(Integer, primary_key=True)
    case_number = Column(String)
    date = Column(String)
    year = Column(Integer)
    type = Column(String)
    country = Column(String)
    area = Column(String)
    location= Column(String)
    activity = Column(String)
    name = Column(String)
    sex = Column(String)
    age = Column(Integer)
    injury = Column(String)
    fatal_y_n = Column(String)
    time = Column(String)
    species = Column(String)
    investigator_or_source = Column(String)
    pdf = Column(String)
    original_order = Column(Integer)
```
Now you can query the Sharks DB. For example:
```
attacks = session.query(Sharks) 
for attack in attacks:
    print(attack.location)
```
You are querying the whol database. The for loop is specifically looking for the Location column of each row. 

You can then run more queries on the DB using python-based code:
```
provoked = session.query(Sharks).filter_by(type='Provoked').count()
print(provoked)
```
More examples of queries:
```
usa = session.query(Sharks).filter_by(country='USA').count()
print(usa)

year_2017 = session.query(Sharks).filter_by(year="2017").count()
print(year_2017)

surfing = session.query(Sharks).filter_by(activity='Surfing').count()
print(surfing)

fatal_surfing = session.query(Sharks).\
    filter_by(fatal_y_n='Y').\
    filter(Sharks.area == "Eastern Cape Province").count()
print(fatal_surfing)

fatal_surfing = session.query(Sharks).\
    filter_by(fatal_y_n='Y').\
    filter(Sharks.country == "MOZAMBIQUE").\
    filter(Sharks.activity == 'Spearfishing').count()
print(fatal_surfing)
```
## Creating,Updating and Deleting in DB using Session
### Example using the Pet DB From Class 2, Activity 3
Build the Pet Class
```
 # Define our pet table
class Pet(Base):
    __tablename__ = 'pet'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    type = Column(String)
    age = Column(Integer)
```
Then create the engine, the tables and Session for engine. This must be done in order to perform CRUD operations
```
engine = create_engine('sqlite:///pets.sqlite') 
## This creates tables in the DB
Base.metadata.create_all(engine)

from sqlalchemy.orm import Session
session = Session(engine)
```
## Create Data
All we did above was create the Pets DB and the tables above when we created the engine to talk to SQLite. This part adds the data. 
```
session.add(Pet(name='Justin Timbersnake', type='snek', age=2))
session.add(Pet(name='Pawtrick Stewart', type='good boy', age=10))
session.add(Pet(name='Godzilla', type='iguana', age=1))
session.add(Pet(name='Marshmallow', type='polar bear', age=4)) 
```
Then you have to add the data. This is where Javier says its like Git. You can check by doing:
```
engine.execute('select * from pet').fetchall()
```
Now you have to use .new, .commit() attributes to add the data. 
```
# Use .new attribute to see the queue of data ready to go into the database
session.new
# commit() flushes whatever remaining changes remain to the database, and commits the transaction. 
session.commit()
```
Probably good idea to make sure theres nothing new to add
```
session.new
```
Now you can query the DB to see if the info got added
```
session.query(Pet.name, Pet.type, Pet.age).all()
```
So you have to .add the data, then .new to set them to be pushed to DB, then .commit() to actually push the data
## Update Data

Create a query to the data you want to change
```
pet = session.query(Pet).filter_by(name="Marshmallow").first()
pet.age += 1
```
The variable pet should be a list for the row where the pet's name is Marshmallow, so it should have its Name, type and age. That's what you can just do pet.age to add 1 to the age of Marshmallow

You then have to .dirty instead of .new to make modifications to data
```
session.dirty
# then commit the changes
session.commit()
# check for new things to update by doing .dirty again
session.dirty
# then query the DB to see if changes were made. 

session.query(Pet.id, Pet.name, Pet.type, Pet.age).all()
```
### To delete, you run a query for what you want to delete
``` 
pet = session.query(Pet).filter_by(id=4).delete()
## Then commit the changes
session.commit()
## check for changes made by query
session.query(Pet.id, Pet.name, Pet.type, Pet.age).all()
```
## Reflection

```
# Dependencies are the same for reflection, only diff is the automap_base instead of declrative_base
import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine

# Create engine is a must like always
engine = create_engine("sqlite:///../Resources/dow.sqlite")

# Set Base to automap_base instead of delcrative_base
Base = automap_base()

# Use the Base class to reflect the database tables
Base.prepare(engine, reflect=True)
```
This is the difference between Reflection is Declrative
```
# Print all of the classes mapped to the Base
# This would show the different classes built using the delcrative_base
Base.classes.keys()

# Assign the dow class to a variable called `Dow`
Dow = Base.classes.dow
```
Assigning it to a variable allows us to query the class/table using Session
```
session = Session(engine)

# Display the row's columns and data in dictionary format
first_row = session.query(Dow).first()
first_row.__dict__
```
Example of running a specific query in Reflection
```
# Use the session to query Dow table and display the first 5 trade volumes
for row in session.query(Dow.stock, Dow.volume).limit(15).all():
    print(row)
```
## Inspection
Pretty much the same setup as reflection except you use inspect the engine. You can then get table names and get column names and types

```
import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine, inspect

# Create the connection engine
engine = create_engine("sqlite:///../Resources/dow.sqlite")

# Create the inspector and connect it to the engine
inspector = inspect(engine)

# Collect the names of tables within the database
inspector.get_table_names()

# Using the inspector to print the column names within the 'dow' table and its types
columns = inspector.get_columns('dow')
for column in columns:
    print(column["name"], column["type"])
```


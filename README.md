# mongomodel

A orm type library for mongoDB wrapped arround pymongo library
provides schema definition , validation and APIs to interact with the mongoDB.

## Requirement

```
python
pymongo
mongoDB
```

## Installation
```bash
git clone https://github.com/hazra1991/mongomodel.git
pip install pymongo
```

## Usage and API implemented
### General usage.
```
from mongomodel.models import DocumentModel
from mongomodel.datatypes import Email,StringField,EmbeddedDocumentList,NumberField,DateTime,Boolean

class Ex_schema(DocumentModel):
    __database__ ="test_DB"
    __collection__="user_info_col"
    __schema__ ={
        "email_id":Email(unique=True),
        "first_name":StringField(),
        "password":StringField(),
        "phone":NumberField(minimum=10,maximum=12),
        "location":StringField(optional=True),
        "verified":Boolean(default=False),
        "DOB":{
            "year":NumberField(),
            "month":NumberField(),
            "day":NumberField()
        }
    }
```
### API
     ~params:: insert(self,*addtodoc) 
        :- usesage::- doc.insert() or doc.insert({"appened":"info to the main doc and save"})
    
    ~params:: connect(cls,dburi="mongodb://localhost:27017/",username=None,password=None))
        :- usesage .classmethod to connect to the db .Should be called before any oporattions
    
    ~params::  findone(self,filterkey=None)
        :- usesage doc.db.collection.findone(filterkey={"email":"example@eg.com"})
        :- returns a dictionary object or None if not present
           we can also use the schema Document model object to navigate the returned info
           EX:
                doc = schema(Documentmodel)
                doc.findone({"email":"w@ww.com"})
                doc.get("email") = "new@mail.com"
            and directly can be saved like
                doc.insert() 
    ~params::  findall
        :- usesage doc.findall(filterkey={"email":"example@eg.com"})
        :- returns a list
    ~params::  updatedoc
        :- usesage doc.updatedoc(filterkey={"email":"example@eg.com"})
    ~params::  deletedoc
        :- usesage doc.deletedoc(filterkey={"email":"example@eg.com"})
#### Note:-  "__database__" , "__collection__" ,"__schema__" are mandatory variables


## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to add and update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)

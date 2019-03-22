# APP with API formed with XML and XSD

An API and a client which send XML data.

This repository contain 2 directories: app and api.

the directory app contain the client on Ionic.
the directory api contain the xml and xsd-schema-validator.

this app is simple:

* Create surveys with your data(XML).
````
<surveys xmlns="https://www.APP_Suresh.com/APP"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://www.APP_Suresh.com/APP validator.xsd">
    <survey>
        <age>18</age>
        <country>Germany</country>
        <email>banana@gmail.com</email>
        <name>Banana</name>
        <lastName>Man</lastName>
        <points>9</points>
        <user_survey>BananaMan96</user_survey>
    </survey>
</surveys>
````
* Surveys XML file that stored in the Server.
````
<?xml version="1.0" encoding="UTF-8"?>
<surveys xmlns="https://www.APP_Suresh.com/APP"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://www.APP_Suresh.com/APP validator.xsd">
    <survey>
        <age>18</age>
        <country>Germany</country>
        <email>banana@gmail.com</email>
        <name>Banana</name>
        <lastName>Man</lastName>
        <points>9</points>
        <user_survey>BananaMan96</user_survey>
    </survey>
    <survey>
        <age>21</age>
        <country>Italy</country>
        <email>pepedestroyer@gmail.com</email>
        <name>Pepe</name>
        <lastName>Juan</lastName>
        <note>esto es una nota</note>
        <points>6</points>
        <user_survey>xXPepeXx</user_survey>
    </survey>
</surveys>
````
* Create lists with your user and have title, number and done.
````
<?xml version="1.0" encoding="UTF-8"?>
<lists xmlns="https://www.APP_Suresh.com/APP"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://www.APP_Suresh.com/APP validator.xsd">
    <user id="1">
        <list>
            <title>Papaya</title>
            <number>4</number>
            <done>True</done>
        </list>
    </user>
</list>
````
* Lists XML file that stored in the Server.
````
<?xml version="1.0" encoding="UTF-8"?>
<lists xmlns="https://www.APP_Suresh.com/APP"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://www.APP_Suresh.com/APP validator.xsd">
    <user id="1">
        <list>
            <title>Papaya</title>
            <number>4</number>
            <done>True</done>
        </list>
        <list>
            <title>Melón</title>
            <number>1</number>
            <done>False</done>
        </list>
    </user>
    <user id="2">
        <list>
            <title>Bananas</title>
            <number>9</number>
            <done>True</done>
        </list>
        <list>
            <title>Naranjas</title>
            <number>4</number>
            <done>False</done>
        </list>
    </user>
</lists>
````
* XSD file in server.
````
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           targetNamespace="https://www.APP_Suresh.com/APP"
           xmlns="https://www.APP_Suresh.com/APP"
           elementFormDefault="qualified">
    
    <!--Elements-->
    
    <!--Surveys-->
    <xs:element name="surveys" type="surveys"/>
    <xs:element name="survey" type="survey"/>
    <xs:element name="age" type="ageValidator"/>
    <xs:element name="country" type="countryValidator"/>
    <xs:element name="email" type="emailValidator"/>
    <xs:element name="name" type="nameValidator"/>
    <xs:element name="lastName" type="nameValidator"/>
    <xs:element name="note" type="xs:string"/>
    <xs:element name="points" type="pointsValidator"/>
    <xs:element name="user_survey" type="xs:string"/>
    <!--Surveys-->
    
    <!--Lists-->
    <xs:element name="lists" type="lists"/>
    <xs:element name="user" type="user"/>
    <xs:element name="list" type="list"/>
    <xs:element name="title" type="xs:string"/>
    <xs:element name="number" type="xs:int"/>
    <xs:element name="done" type="doneValidator"/>
    <!--Lists-->
    
    <!--Complex-->
    
    <!--Surveys-->
    <xs:complexType name="surveys">
        <xs:sequence>
            <xs:element ref = "survey" maxOccurs="unbounded"/>
        </xs:sequence>
    </xs:complexType>
    
    <xs:complexType name="survey">
        <xs:sequence>
            <xs:element ref="age"/>
            <xs:element ref="country"/>
            <xs:element ref="email"/>
            <xs:element ref="name"/>
            <xs:element ref="lastName"/>
            <xs:element ref="note" minOccurs="0"/>
            <xs:element ref="points"/>
            <xs:element ref="user_survey"/>
        </xs:sequence>
    </xs:complexType>
    <!--Surveys-->
    
    <!--Lists-->
    <xs:complexType name="lists">
        <xs:sequence>
            <xs:element ref="user" maxOccurs="unbounded"/>
        </xs:sequence> 
    </xs:complexType>
    
    <xs:complexType name="user">
        <xs:sequence>
            <xs:element ref="list" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id">
            <xs:simpleType>
                <xs:restriction base="xs:int">
                    <xs:minInclusive value="1"/>
                </xs:restriction>
            </xs:simpleType>
        </xs:attribute>
    </xs:complexType>
    
    <xs:complexType name="list">
        <xs:sequence>
            <xs:element ref="title"/>
            <xs:element ref="number"/>
            <xs:element ref="done"/>
        </xs:sequence>
    </xs:complexType>
    
    <!--Lists-->
    
    <!--Restriction-->
    
    <!--Surveys-->
    <xs:simpleType name="ageValidator">
        <xs:restriction base="xs:int">
            <xs:minInclusive value="18"/>
            <xs:maxInclusive value="99"/>
        </xs:restriction>
    </xs:simpleType>
    
    <xs:simpleType name="countryValidator">
        <xs:restriction base="xs:string">
            <xs:enumeration value="Spain"/>
            <xs:enumeration value="Germany"/>
            <xs:enumeration value="France"/>
            <xs:enumeration value="Italy"/>
        </xs:restriction>
    </xs:simpleType>
    
    <xs:simpleType name="emailValidator">
        <xs:restriction base="xs:string">
            <xs:pattern value="[^@]+@[^\.]+\..+"/>
        </xs:restriction>
    </xs:simpleType>
    
    <xs:simpleType name="nameValidator">
        <xs:restriction base="xs:string">
            <xs:pattern value="[A-Z]{1}[a-z]*"/>
        </xs:restriction>
    </xs:simpleType>
    
    <xs:simpleType name="pointsValidator">
        <xs:restriction base="xs:int">
            <xs:minInclusive value="1"/>
            <xs:maxInclusive value="9"/>
        </xs:restriction>
    </xs:simpleType>
    <!--Surveys-->
    
    <!--Lists-->
    <xs:simpleType name="doneValidator">
        <xs:restriction base="xs:string">
            <xs:enumeration value="True"/>
            <xs:enumeration value="False"/>
        </xs:restriction>
    </xs:simpleType>
    <!--Lists-->
</xs:schema>
````

### Screenshots

* Check XML Surveys and Lists.
(photo)
* And now, validate XML Survey and Lists
(photo)
### Acknowledgments
* https://github.com/tcrurav/XmlRESTfulNodeJSfromJS This github is very good, you always find the solution to your problems. In this case, I use this project like a model.
https://gist.github.com/PurpleBooth/109311bb0361f32d87a2#file-readme-template-md It's a good README.md template.
* https://www.w3schools.com/xml/ This is good to start learn XML.
https://www.w3schools.com/xml/schema_intro.asp You can learn XSD with this link, W3School is GOD.
https://netbeans.org/ It's a good framework to do XML and XSD.

### Is the markup language a markup language?
Markdown is a lightweight markup language.
### Does it comply with the basic syntax of markup languages?

**Extensible Markup Language (XML)**

XML is a commonly used method to transport and store data in a structured format that humans and machines can easily understand. Consider a scenario where two computers need to communicate and share data. Both devices need to agree on a common format for exchanging information. This agreement (format) is known as `XML`. You can think of XML as a digital filing cabinet. Just as a filing cabinet has folders with labelled documents inside, XML uses `tags` to label and organise information. These tags are like folders that define the type of data stored. This is what an XML looks like, a simple piece of text information organised in a structured manner: 

```javascript
<people>
   <name>Glitch</name>
   <address>Wareville</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

In this case, the tags **<people>**, **<name>**, **<address>**, etc are like folders in a filing cabinet, but now they store data about Glitch. The content inside the tags, like "`Glitch`," "`Wareville`," and "`123-4567`" represents the actual data being stored. Like before, the key benefit of XML is that it is easily shareable and customisable, allowing you to create your own tags. 

**Document Type Definition (DTD)**

Now that the two computers have agreed to share data in a common format, what about the structure of the format? Here is when the DTD comes into play. A DTD is a set of **rules** that defines the structure of an XML document. Just like a database scheme, it acts like a blueprint, telling you what elements (tags) and attributes are allowed in the XML file. Think of it as a guideline that ensures the XML document follows a specific structure.

For example, if we want to ensure that an XML document about `people` will always include a `name`, `address`, `email`, and `phone number`, we would define those rules through a DTD as shown below:  

```javascript
<!DOCTYPE people [
   <!ELEMENT people(name, address, email, phone)>
   <!ELEMENT name (#PCDATA)>
   <!ELEMENT address (#PCDATA)>
   <!ELEMENT email (#PCDATA)>
   <!ELEMENT phone (#PCDATA)>
]>
```

In the above DTD, **<!ELEMENT>**  defines the elements (tags) that are allowed, like name, address, email, and phone, whereas `#PCDATA` stands for parsed `people` data, meaning it will consist of just plain text.  

**Entities**

So far, both computers have agreed on the format, the structure of data, and the type of data they will share. Entities in XML are placeholders that allow the insertion of large chunks of data or referencing internal or external files. They assist in making the XML file easy to manage, especially when the same data is repeated multiple times. Entities can be defined internally within the XML document or externally, referencing data from an outside source. 

For example, an external entity references data from an external file or resource. In the following code, the entity `&ext;` could refer to an external file located at "`http://tryhackme.com/robots.txt`", which would be loaded into the XML, if allowed by the system:

```javascript
<!DOCTYPE people [
   <!ENTITY ext SYSTEM "http://tryhackme.com/robots.txt">
]>
<people>
   <name>Glitch</name>
   <address>&ext;</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

We are specifically discussing external entities because it is one of the main reasons that XXE is introduced if it is not properly managed.

**XML External Entity (XXE)**

After understanding XML and how entities work, we can now explore the XXE vulnerability. XXE is an attack that takes advantage of **how** **XML parsers handle external entities**. When a web application processes an XML file that contains an external entity, the parser attempts to load or execute whatever resource the entity points to. If necessary sanitisation is not in place, the attacker may point the entity to any malicious source/code causing the undesired behaviour of the web app.

For example, if a vulnerable XML parser processes this external entity definition:

```javascript
<!DOCTYPE people[
   <!ENTITY thmFile SYSTEM "file:///etc/passwd">
]>
<people>
   <name>Glitch</name>
   <address>&thmFile;</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

Here, the entity `&thmFile;` refers to the sensitive file `/etc/passwd` on a system. When the XML is processed, the parser will try to load and display the contents of that file, exposing sensitive information to the attacker.
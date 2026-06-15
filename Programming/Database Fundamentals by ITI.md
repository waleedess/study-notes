## Database System Components

1. Application Programs
2. DBMS (Software to process Queries and to access stored data)
3. DB & its Metadata (Definition)
- Metadata examples
    1. Table/Column Name
    2. Column data types
    3. DB objects structure
    4. Constraints
    5. Access Privileges
    6. Usernames & Passwords & User privileges
    7. Log Files of interactions

|  | DBMS Pros | DBMS Cons |
| --- | --- | --- |
| 1 | Redundancy Control | Needs Expertise |
| 2 | Authorized Access | Expensive (Software and Infra) |
| 3 | Integrity Constraints Enforcement | May not be compatible with other DBMS but can use 3rd-party tools |
| 4 | Avoiding Inconsistency |  |
| 5 | Backups |  |

---

### DBMS Archi

#### External Schema

- Concerned what data user will see and how it is presented
- Multiple (different) across one system

#### Conceptual Schema

- Concerned with what is represented

#### Physical Schema

- How are the data represented in DB and how is it implemented
- Physical Hardware Info about the Disk

---

Different types of schemas → apply agility to change one without missing with the other

---

### Data Models

- Logical/Conceptual Model → Concepts to how users perceive data
- Physical Model → Concepts about how is data stored and the paths need to access or search for it

### Mappings

- Mappings is the process of transforming requests and results between levels

Request → External Schema → Conceptual → Physical → Disk → Result → Physical → Conceptual → Same External

---

### DBMS other functions

First it supported only numbers and characters, then it started to support:

1. Images/Videos/Audios
2. Spatial Data (ex. GPS)
3. Time Series (time vs data ex. el borsa)
4. Data mining → Analysis of data and Clustering to give better Info (Can be built-in but with limitations)

---

### DBMS Environments

#### Centralized

- Mainframe (Oldest): Processing Depends only on one server → single point of failure for both Application and Database and slow performance
- Client/Server: 2-Tier Environment: 
1-Database Server → still single point of failure 
2-Thick Client : Application is locally installed not connected like Mainframe → no                                               Application single point of failure
→Overall High cost for support and updates
- Internet Computing: 3-Tier Environment:
1-Database Server  → Single point of failure
2-Application Server → Application server is single point of failure. but, lower support and                                               maintenance cost
3-Thin Client
- Internet Computing: N-Tier Environment:
1-Database Server  → Still Single point of failure
2-Many application Servers (Diff/Alike) → no Application server single point of failure
3-Thin Client

#### Distributed

Gaining High availability → NO Single Point of Failure
                                                   But with High Cost

- Replication (copy&paste)
    - Partial Replica → 2 Servers installed (one copies only a part of the other)
    - Full Replica → 2 servers (exact full copies) installed working back2back using a heartbeat like indication of status so when the main is down the other start working and all the traffic will be routed to it
- Fragmentation (cut&paste)
    
    Data is Fragmented to be undergo this operation, Can Be horizontal → Records or Vertical → Columns or Hybrid
    
    - Each part gets installed to a server and all of them are on a same network of specific type

## ERD: Entity Relationship Modeling (Conceptual Design)

Identifies info required by business by displaying the relevant entities and relationships betn them

---

#### Modeling Guideline Questions

1. What Entities need to be described 
2. What Characteristics or Attributes -of described Entities- needs to be recorded
3. Can an Attribute -or more- Uniquely identify one specific occurrence of its Entity
4. What Relationships exist between Entities

---

### Entity

- It is each object that have independent (Physical or Conceptual) existence and have its own Characteristics or Attributes
- Rectangle-Shaped

#### Types of Entities

| Strong Entity | Weak Entity |
| --- | --- |
| Single Rectangle | Double Rectangle |
| Have a Unique Attribute |   Must be both of:
  • Can’t have a Unique Attribute
  • Fully Dependent on another Entity |

---

### Attributes

- Oval-Shaped
- Unique Attributes will have an Underline under their name inside the Oval

#### Types of Attributes

| Single/Simple Attribute | Multi-Valued Attribute  | Composite Attribute | Derived Attribute |
| --- | --- | --- | --- |
| Single Oval | Double Oval | Single Ovals Connected | Dotted Oval |
| not divisible and have a single value for a particular Entity instance | Have set of values for a same Entity | Divided into smaller subparts | Calculated from another attribute |

---

### Relationships

#### Degree

- Rhombus-Shaped

Relationship Degrees

| Binary | Unary (Recursive) | Ternary  |
| --- | --- | --- |
| Connects 2 Entities  | Between an Entity with Itself | Connects 3 Entities  |

---

#### Car**dinality** Ratio

- Indicates maximum number of relationship and its indicator put in a circle on the end of the relationship, ex.:
Emp(M)------(1)Dept
 → an employee can work only in one department
 but a department contains more than one employee

Ratios:

| 1 | any letter(M) |
| --- | --- |
| Only one | Many |
- Ternary Relationships will have their ratios put as 3 binary relationships 
ex. : 
Emp (M)---(M) | (M) --- (M) Proj
                            |
                          (M)
                            |
                          (M)
                         Skill
→ On each Binary relationship side the ratio must me the same
if i cant → divide that Entity and make loops

---

#### Participation

- Indicates minimum number of relationship

Participations

| Must | May |
| --- | --- |
| Double lined relationship x==y | Single lined relationship x—x |
| All Should participate | Not all or Not at all should participate |

---

## Mapping and Relation Database (Logical Design)

- Relations is subjected in Tables of: Tuples (Rows) & Columns & the intersection betn. them is called Domain of single value

### Mapping Entities

#### Mapping Strong Entities

- Primary key is like an info domain at 1st column of an Relationship and should agree with the 2 of:
    - Containing a unique value for each Domain
    - Not having a Domain with Null
- Primary key can be chosen in the shortest Unique Combination is single so it is according to
    - Have less storage ex. (number>Letter)
- `EntityName (singleAtt.1,singleAtt.2,CompositeAtt.subpart1,CompositeAtt.subpart2)` → Chosen Primary key will have its name underlined as in example
- Multi-Valued Attributes can’t be in the same Map as single as it will result in null Domains → it will be in a other Map with the same Primary key but named as Foreign Key that will reference
- `EntityName - MultiAtt. (singleAtt.2, MultiAtt.)` → Foreign Key should have an dotted-underline
- `EntityName - MultiAtt. (singleAtt.2, MultiAtt.)` → Primary key Combination && Foreign key idea
- Derived Attributes Usually not even stored in the database to oppose headaches but if it has high traffic it can be stored as an exception

#### Mapping Weak Entities

- A other Entity’s Primary key should correspond to it in a form of foreign key to be companied with a Unique Weak Entity’s attribute (Partial Primary key)

---

## Mapping Relationship Types
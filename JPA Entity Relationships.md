# JPA Entity Relationships

### Why these relationships exist?
- Because as we know the realtional DB we are using stores data across multiple tables examples :
  - One Employee belongs to one department
  - One Department can have multiple Employees
  - One Employee can work on many projects
  - Each project can have multiple Employees
- So we need a way to map Object->Tables annd Object Relations->Foreign Keys
> In the backend JPA does all this mapping

### Primary Relationships Types
- @OnetoOne
- @OnetoMany
- @ManytoOne
- @ManytoMany
> These Annotations DO NOT create SQL relationships  
> These Descibe the realtionships so the Hibernate Generate the SQL for us
- What these Annotations internally do is :
```
// When you write
@ManyToMany
private Department dept;
```
- Hibernate :
    - Reads MetaData through reflection
    - Builds internal mapping model
    - Decides b/w JoinTable and JoinColumn
 
#### Full Flow of the Hibernate
**1. Hibernate Starts and Scan all @Entity Clases**
```
  @Entity
  class Employee{...}
  ```  
  - scanning all the project packages and finds all clases with Annotations (@Entity, @Embeddable, @MapSuperClass).  
  > Uses **JAVA reflection**
  
**2. Hibernate Reads all Fields and Anootations**  
    example if you define like    
```
@Entity
public class Employee{  
  @Id  
  @GeneratedValue  
  private Long id;  
}
```  
  - what hibernate interprets is that you have an ID field which is the Primary Key and has Auto Generation  
  > This is what we call metadata extraction

**3.Builds an internal Mapping Model**
- Hibernate creates a mapping model (EntityPersister, ClassMetadata, PropertyMapping) which contains :-
  - table name = employee
  - columns = id, name, department_id
  - key column = id
  - foreign key column = department_id
  - relationship type = ManyToOne
  - fetch type = LAZY by default
  - cascade = none
- it stores the above in the MetaData Registery inside the **Session Factory**

**4. Hibernate decides the SQL Schema based on the MetaData**
- for instance lets take an example :
```
@ManyToOne
@JoinColumn(name="department_id")
private Department department;
```
- Hibernate genrates an SQL for this :
```
department_id BIGINT,
CONTRAINT fk_dept FOREIGN KEY(department_id) REFERENCES department(id)
```
- The Flow is like Annotations -> MetaData -> Actual SQL
 
### @ManyToOne
- Many Employees -> One Department
> Employees is the owning side as the foreign key sits there
```
@ManytoOne(fetch = FetchType.LAZY)
@JoinColumn(name="department_id")
private Department department;
```
- under the hood Hibernate generates a column **(department_id)**

### Internal Flow of every Relationship
1. Parse Annotations
2. Build Metadata
3. Create Proxies for Lazy Fields
4. Create SQL Schema
5. Manage PersistenceContext
6. Track Changes via Dirty Checking
7. Generate SQL dynamically at Flush
8. Maintain first level cache
9. Handle Cascades
10. Commit Transaction

### Common Exceptions 
- LazyInitializationException
- DataIntegrityViolationException
- TransientObjectException
- DetachedEntityPassedToPersistException
- ConstraintViolationException

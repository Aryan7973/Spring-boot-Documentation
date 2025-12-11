# Different Annotation in Spring Boot

## @Transient
- It is applied on fields/methods which will tell the Hibernate to ignore this field.
- Fields/Methods having Trasnient are not stored in DB.
> Tells Hibernate this field exists in my Java Entity but NEVER touch the DB with it.  
> **Would I ever query/store this?? if no then Transient it.**
- Example :   
        - you use a fullName field in the entity and have a setter which concatenates.  
        - so setting this field and setter @Transient will not store this in DB as this is just for computation.

```
@Entity
@Table(name = "users")
@Getter @Setter
public class User{
        private String firstName;
        private String lastName;

        @Transient
        private String fullName;

        public String getFullName() {
                return firstName + " " + lastName;
        }
}
```
- Alternatives for Transient :

| Objective | Use this |
| ---- | --- |
| read only column in DB | @Column(insertable = false, updatable = false) + getter | 
| Just hiding from JSON serialize/deserialize | @JsonIgnore on getter | 
| hide from both JPA and JSON | @JsonIgnore + @Transient |


## @Access

        

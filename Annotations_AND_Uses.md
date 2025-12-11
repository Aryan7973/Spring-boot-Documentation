# Different Annotation in Spring Boot

## @Transient:
- It is applied on fields/methods which will tell the Hibernate to ignore this field.
- Fields/Methods having Trasnient are not stored in DB.
> Tells Hibernate this field exists in my Java Entity but NEVER touch the DB with it.
- Example :   
        - you use a fullName field in the entity and have a setter which concatenates.
        - so setting this field and setter @Transient will not store this in DB as this is just for computation.

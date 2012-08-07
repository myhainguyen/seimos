Seimos
======

Hibernate Criteria Encapsulation

Seimos is not a Hibernate substitute but an extension. It encapsulates repetitives issues when programming through 
Criteria. Here you are some examples:

1. Full list
------------
  1.1. Criteria
    Criteria criteria = session.createCriteria(Route.class);
    List routes = criteria.list();

  1.2. Seimos
    dao.list();
    
2. Adding restrictions
  1.1. Criteria
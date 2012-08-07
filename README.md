Seimos
======

Hibernate Criteria Encapsulation

Seimos is not a Hibernate substitute but an extension. It encapsulates repetitives issues when programming through 
Criteria. Here you are some examples:

1. Full list
------------
  1.1. Criteria

    Criteria criteria = session.createCriteria(Cat.class);    
    List cats = criteria.list();

  1.2. Seimos
  
    List cats = dao.list();
    
2. Adding restrictions
----------------------
  2.1. Criteria

    Criteria criteria = session.createCriteria(Cat.class);
    criteria.add(Restrictions.eq(“id”, 10000));
    List cats = criteria.list();
    
  2.2. Seimos
  
    Filters filters = new Filters();
    filters.add(new Filter(“id”, 10000));
    List cats = dao.find(filters);
    
    Of course both Criteria and Seimos have a lot of restrictions type. For Seimos each new Filter added to filters could use a specific condition for filtering. For example, new Filter's could be used as follows:
    filters.add(new Filter("description", "Pap"));
    filters.add(new Filter("birth", new Date()));
    filters.add(new Filter("serial", 10000, Condition.GREATER);  // Serial for cats? It's just an example :)
    
    And Condition could be any of 
    
    * EQUALS
    * NOT_EQUALS
    * STARTS_WITH
    * NOT_STARTS_WITH
    * ENDS_WITH
    * NOT_ENDS_WITH
    * EQUALS_CASE_INSENSITIVE
    * STARTS_WITH_CASE_SENSITIVE
    * NOT_STARTS_WITH_CASE_SENSITIVE
    * ENDS_WITH_CASE_SENSITIVE
    * NOT_ENDS_WITH_CASE_SENSITIVE
    * GREATER
    * GREATER_OR_EQUALS
    * LESS
    * LESS_OR_EQUALS
    * NULL
    * NOT_NULL
    * BETWEEN
    * OR
    * AND
    * IN
    * NOT_IN
    * EQ_PROPERTY
    * LESS_THAN_PROPERTY
    * LESS_OR_EQUALS_THAN_PROPERTY
    * GREATER_THAN_PROPERTY
    * GREATER_OR_EQUALS_THAN_PROPERTY
    
    Condition it's extensible too.
    
    For default, any search for an attribute of String type use MatchMode.START and 'like' clausule when Condition is supressed, i.e., new Filter("description", "Pap") it's the same of new Filter("description", "Pap", Condition.STARTS_WITH). For any other type, default condition is EQUALS, that means, new Filter("id", 10000) it's the same of new Filter("id", 10000, Condition.EQUALS).
    
    Filter's can be nested when Condition allows. Condition.AND and Condition.OR use constructor
    * new Filter(Condition.AND, filter01, filter02)
    * new Filter(Condition.OR, filter01, filter02)
    filter01 and filter02 are new Filter(...) of any type, including with Condition.AND or Condition.OR
    
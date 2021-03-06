# Summary of FAIKR module 2 

## Knowledge Representation Languages

### First Order Logic (*FOL*)

Also known as Predicate Calculus, it can be considered a standard for knowledge representation.

Syntax:

- An infinite set of object constants.
- An infinite set of variables.
- An infinite set of functional symbols of all arities.
- An infinite set of predicates symbols of all arities.
- Connectives: <img src="svgs/f4ac2a9bfb464ea0f19dccc459ef546c.svg?invert_in_darkmode" align=middle width=71.23287434999999pt height=18.264896099999987pt/>
- Quantifiers: <img src="svgs/58948550348485a5775e8d8a05ac742b.svg?invert_in_darkmode" align=middle width=25.57077929999999pt height=22.831056599999986pt/>

### Description Logic (*DL*)

Notations that are designed to describe definitions and properties of categories, formalizing what a semantic network means and studying the reasoning mechanisms.

A DL knowledge base is composed by a ***TBox*** (a set of "schema" axioms) and an ***ABox*** (a set of "data" axioms, or ground facts).

#### Attributive Language (*AL*)

It does not support disjunction and provides limited forms of negation and existential quantifier only.
The syntax is composed by

- Atomic concepts
- Roles (relationships)
- Individuals (nominals)
- Boolean operators
  - Conjunction <img src="svgs/134e7ad74c723bdf3141c457e55a5e35.svg?invert_in_darkmode" align=middle width=10.95894029999999pt height=18.264896099999987pt/>
  - Disjunction <img src="svgs/2cfa3b62e25c55e1f2b62ff472d5fd09.svg?invert_in_darkmode" align=middle width=10.95894029999999pt height=18.264896099999987pt/>
  - Negation <img src="svgs/23bf728170c10d0449b90561f827623a.svg?invert_in_darkmode" align=middle width=10.95894029999999pt height=14.15524440000002pt/>, applicable only to atomic concepts
- Restricted quantifiers: <img src="svgs/b4c5b626a225ce855a9e41a4287d3cc5.svg?invert_in_darkmode" align=middle width=25.57077929999999pt height=22.831056599999986pt/>
- Universal and bottom concepts (<img src="svgs/b37a16d4b12caeff164d04ba28599132.svg?invert_in_darkmode" align=middle width=32.87674994999999pt height=22.831056599999986pt/>)
- Value restriction
  - Universal restriction <img src="svgs/0b93210f16164ffe472977e912f17b2a.svg?invert_in_darkmode" align=middle width=39.231785999999985pt height=22.831056599999986pt/>
  - Existential restriction <img src="svgs/fdcbe66a0740c16f07076e237ac8972d.svg?invert_in_darkmode" align=middle width=39.231785999999985pt height=22.831056599999986pt/>
- Concept subsumption (<img src="svgs/425e4da138ab8b67e31ea86f4f9a6c1e.svg?invert_in_darkmode" align=middle width=73.05938309999999pt height=20.908638300000003pt/>)
- Concept equivalence (<img src="svgs/ebf45b23c8b2fe7cb8bf20cb8bbd565d.svg?invert_in_darkmode" align=middle width=12.785434199999989pt height=15.24650820000002pt/>)

##### AL extensions

- Attributive Language with Complements (***ALC***): AL extension where, unlike AL, the complement of any concept is allowed (e.g. <img src="svgs/d184cf6de77c954877a47f3cc17341e2.svg?invert_in_darkmode" align=middle width=172.08909794999997pt height=24.65753399999998pt/> ), not only the complement of atomic concepts.
- Attributive Language with role Hierarchy (***ALH***): AL extension where it is possible to have role hierarchy (e.g. <img src="svgs/bedfb6c564d5211692298539902d1c50.svg?invert_in_darkmode" align=middle width=175.79928794999998pt height=22.831056599999986pt/> ).
- Attributive Language with Inverse roles (***ALI***): AL extension where it is possible to use qualified number restrictions (e.g. <img src="svgs/cc9f5d5fba7b996cdc9223e0852fba14.svg?invert_in_darkmode" align=middle width=194.70088934999998pt height=24.65753399999998pt/> ).
- Attributive Language with Number restrictions (***ALN***): AL extension where it is possible to use qualified number restrictions (e.g. <img src="svgs/eeab7c292febcd99f3d4e292b80e73f6.svg?invert_in_darkmode" align=middle width=110.61089159999999pt height=22.831056599999986pt/> ).

Extensions can be combined, for example creating ***ALCN***, but each extension increases computational cost.

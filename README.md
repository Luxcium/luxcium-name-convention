# Luxcium Projects Naming Conventions

In order to document my preferences for names of variable tokens and such, I
decided to create this document to structure my naming conventions pcincipally
in JavaScript / TypeScript projects and in Bash, ShellScript, ZSH projects.

## TypeScript and JavaScript projects

### IInterfaces vs Interfaces

In my projects I aim at using the `IInterface` notation only for *interfaces*
that represent the *contract* for the shape of an *object* to others (other
parts of the same project internaly, or to other users and consumers external
to the project).

Normally theses should be
[POJOs](https://en.wikipedia.org/wiki/Plain_old_Java_object), ordinary
JavaScript *object*, easely serializable, which dose not contain methods. Such
*objects* should not be bound by any *other* special restrictions.

This definition of a contract is for now somehow subjective and should be
defined more formally later, I decided **not** to use a `IInterface` notation
for other *interfaces* that represent an *object* type. *Interfaces* always
begin with an upper case letter but as of now I decided to use the `xInterface`
notation for *interfaces* that have a name that starts with capital leter
**'I'** but are not consider `IInterface`s. For type definitions other than
`IInterface`s and *objects*, type aliases should alway be used.

*Objects* respecting the `IInterface` notation should be considered as *[value
objects](https://en.wikipedia.org/wiki/Value_object)* object that contains
attributes but has no conceptual identity, they should be immutable: this is
required for the implicit contract that two value objects created equal,
should remain equal. They should be treated as immutable, it is useful for the
value object described with an `IInterface` to be immutable, as client code
cannot put the value object in an invalid state or introduce buggy behaviour
after creation. Example: When people exchange business cards, they generally
do not distinguish between each unique card; they are only concerned about the
information printed on the card. In this context, business cards are value
objects.

### Classes

*Objects* that are not conforming to the `IInterface` notation specified above
should follow the normal `Interface` or `xInterface` notation specified above
unless an *object* contain the `this` *keyword*, require the usage of the
`new` *keyword* to be instantiated, or need to have methods added to its
prototype. If an *object* does not only consist of fields, or of fields and
static methods, such *object* shoud be defined with the `class` *keyword* and
therefor must be intantatiated from the *keyword* `new` or from a static
method of that *object* returning an instance of that *object*, or from other
code that use these mechanisme to resolve to an instance of such *object*.

### Functions


In most, if not all cases, a function should always be defined with the
`function` *keyword* if it is defined at the *global* or *module* scope
level, unless a type needs to be assigned which would resuld in the use of the
`const` *keyword* *i.e.*:
```typescript
   const functionName: FunctionType = (parameter)=> parameter &&
   'someFunctionDefinition'
```
In all other cases (i.e. function defined whithin an other function), the arow
function should be used except in the cases where its behaviour differ with a
function defined using the `function` *keyword*.

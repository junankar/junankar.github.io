---
title: "Koenig Lookup"
permalink: /cpp/koenig_lookup/
excerpt: "Koenig Lookup"
last_modified_at: 2020-07-27
---

## Argument-Dependent Lookup (ADL)
  
ADL defines rules lookup for an unqualified function names.

## Example Use Case

```
namespace nsp
{
   class TestClass
   {
   };

   void PrintTestClass(const TestClass&)
   {
   }
}

int main()
{
    nsp::TestClass a;

    // Qualifying PrintTestClass with namespace is not needed
    // e.g. nsp::PrintTestClass(a);
    PrintTestClass(a);

    return 0;
}
```

## Special Use Cases

[C++ Core Guidelines: Surprises with Argument-Dependent Lookup](https://www.modernescpp.com/index.php/c-core-guidelines-argument-dependent-lookup-or-koenig-lookup) mentions interesting cases with ADL.

## References
* <small>[Argument-Dependent Name (Koenig) Lookup on Functions](https://docs.microsoft.com/en-us/cpp/cpp/argument-dependent-name-koenig-lookup-on-functions?view=vs-2019)</small>
* [A Personal Note About Argument-Dependent Lookup](https://www.drdobbs.com/cpp/a-personal-note-about-argument-dependent/232901443)
* [C++ Core Guidelines: Surprises with Argument-Dependent Lookup](https://www.modernescpp.com/index.php/c-core-guidelines-argument-dependent-lookup-or-koenig-lookup)
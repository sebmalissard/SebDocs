# CPP

* https://cpp.developpez.com/cours/cppavance
* https://cpp.developpez.com/cours/

## Contructeur

https://en.cppreference.com/w/cpp/language/member_functions#Special_member_functions

Contructeur par copie.
S'il n'est pas défini, le compilateur effectue une simple copie des membres (sans gérer la mémoire allouée dynamiquement).
```cpp
class X {
public:
    X(const X& x); // contructeur par copie
    X& operator =(const X& x) // operatuer de copie
};
```

Interdire le contructeur par copie:
```cpp
class X {
public:
    X(const X& s) = delete; // interdit le contructeur par copie
};
```

User declared copy constructor (either user-provided, deleted or defaulted)  prevents the implicit generation of a default constructor.

```cpp
struct G
{
    G(const G&) {}
    // G::G() is implicitly defined as deleted
};

struct H
{
    H(const H&) = delete;
    // H::H() is implicitly defined as deleted
};
 
struct I
{
    I(const I&) = default; // utilise l'implementation par default de ce constructeur
    // I::I() is implicitly defined as deleted
};
```

## Keyword

### Explicit

Specifies that a constructor or conversion function(since C++11) is explicit, that is, it cannot be used for implicit conversions and copy-initialization.

```cpp
struct A
{
    A(int) { }      // converting constructor
    A(int, int) { } // converting constructor (C++11)
    operator bool() const { return true; }
};
 
struct B
{
    explicit B(int) { }
    explicit B(int, int) { }
    explicit operator bool() const { return true; }
};
 
int main()
{
    A a1 = 1;      // OK: copy-initialization selects A::A(int)
    A a2(2);       // OK: direct-initialization selects A::A(int)
    A a3 {4, 5};   // OK: direct-list-initialization selects A::A(int, int)
    A a4 = {4, 5}; // OK: copy-list-initialization selects A::A(int, int)
    A a5 = (A)1;   // OK: explicit cast performs static_cast
    if (a1) { }    // OK: A::operator bool()
    bool na1 = a1; // OK: copy-initialization selects A::operator bool()
    bool na2 = static_cast<bool>(a1); // OK: static_cast performs direct-initialization
 
//  B b1 = 1;      // error: copy-initialization does not consider B::B(int)
    B b2(2);       // OK: direct-initialization selects B::B(int)
    B b3 {4, 5};   // OK: direct-list-initialization selects B::B(int, int)
//  B b4 = {4, 5}; // error: copy-list-initialization does not consider B::B(int, int)
    B b5 = (B)1;   // OK: explicit cast performs static_cast
    if (b2) { }    // OK: B::operator bool()
//  bool nb1 = b2; // error: copy-initialization does not consider B::operator bool()
    bool nb2 = static_cast<bool>(b2); // OK: static_cast performs direct-initialization
 
    [](...){}(a4, a5, na1, na2, b5, nb2); // may suppress "unused variable" warnings
}
```

### Implicit conversions

Implicit conversions are performed whenever an expression of some type T1 is used in context that does not accept that type, but accepts some other type T2.

### Mutable

En C++ une méthode suffixée const peut néanmoins changer la valeur d’un membre en utilisant le mot clé mutable.

```cpp
class X {
private:
    int _i;
    mutable int _flag;
public:
    int getI() const {
        _flag = 1; // OK
        return _i;
    }
};
```

## vtable

https://www.irif.fr/~carton/Enseignement/ObjetsAvances/Cours/vtable.html

Example un object B sans methode virtuel en mémoire:

    B
    +-------------+
    |      u      |
    +-------------+
    |      v      |
    +-------------+

Avec 2 méthodes virtuel

                                    Vtable de B
                                  +-------------+
                             +--->|      0      |      // Top-offset
                             |    +-------------+
    B                        +----|     RTTI    |      // Run-time type information
    +-------------+               +-------------+
    |    vptr     |-------------->|    B::x()   |
    +-------------+               +-------------+
    |      u      |               |    B::y()   |
    +-------------+               +-------------+
    |      v      |
    +-------------+

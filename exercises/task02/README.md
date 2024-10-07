## vec.cpp

### Vec3 v0; 

    |-DeclStmt 0x7fab0e047120 <line:14:2, col:9>
         -VarDecl 0x7fab0e03dc50 <col:2, col:7> col:7 v0 'Vec3':'Vec3' callinit
            -CXXConstructExpr 0x7fab0e0470f8 <col:7> 'Vec3':'Vec3' 'void () noexcept'

### Vec3 v1();

    |-DeclStmt 0x7fab0e047270 <line:15:2, col:11>
        -FunctionDecl 0x7fab0e0471b8 parent 0x7fab0d837808 <col:2, col:10> col:7 v1 'Vec3 ()'


As we can see in the **Abstract Syntax Tree** line 15 *Vec3 v1();* is treated as a function declaration, even it does like a correct object instantiation. Even inside the function there is no **VarDecl** happening.

### Vec3 v2(1, 2, 3);

    |-DeclStmt 0x7fab0e0473d0 <line:16:2, col:18>
        `-VarDecl 0x7fab0e047298 <col:2, col:17> col:7 v2 'Vec3':'Vec3' callinit
           `-CXXConstructExpr 0x7fab0e047390 <col:7, col:17> 'Vec3':'Vec3' 'void (int, int, int)'
             |-IntegerLiteral 0x7fab0e047300 <col:10> 'int' 1
             |-IntegerLiteral 0x7fab0e047320 <col:13> 'int' 2
             `-IntegerLiteral 0x7fab0e047340 <col:16> 'int' 3

### Vec3 v3{1, 2, 3};

    |-DeclStmt 0x7fab0e047558 <line:17:2, col:18>
    | `-VarDecl 0x7fab0e0473f8 <col:2, col:17> col:7 v3 'Vec3':'Vec3' listinit
    |   `-CXXConstructExpr 0x7fab0e047518 <col:7, col:17> 'Vec3':'Vec3' 'void (int, int, int)' list
    |     |-IntegerLiteral 0x7fab0e047460 <col:10> 'int' 1
    |     |-IntegerLiteral 0x7fab0e047480 <col:13> 'int' 2
    |     `-IntegerLiteral 0x7fab0e0474a0 <col:16> 'int' 3    

### Vec3 v4 = {1, 2, 3};

    |-DeclStmt 0x7fab0e0476e0 <line:18:2, col:21>
    | `-VarDecl 0x7fab0e047580 <col:2, col:20> col:7 v4 'Vec3':'Vec3' cinit
    |   `-CXXConstructExpr 0x7fab0e0476a0 <col:12, col:20> 'Vec3':'Vec3' 'void (int, int, int)' list
    |     |-IntegerLiteral 0x7fab0e0475e8 <col:13> 'int' 1
    |     |-IntegerLiteral 0x7fab0e047608 <col:16> 'int' 2
    |     `-IntegerLiteral 0x7fab0e047628 <col:19> 'int' 3

## Temporary Object Declarations    

### auto v5 = Vec3{}; 

    |-DeclStmt 0x7fab0e047a60 <line:20:2, col:18>
    | `-VarDecl 0x7fab0e047770 <col:2, col:17> col:7 v5 'Vec3':'Vec3' cinit
    |   `-CXXTemporaryObjectExpr 0x7fab0e047828 <col:12, col:17> 'Vec3':'Vec3' 'void () noexcept' list zeroing


### auto v6 = Vec3(1, 2, 3);

    |-DeclStmt 0x7fab0e047c90 <line:21:2, col:25>
    | `-VarDecl 0x7fab0e047ab8 <col:2, col:24> col:7 v6 'Vec3':'Vec3' cinit
    |   `-CXXTemporaryObjectExpr 0x7fab0e047b90 <col:12, col:24> 'Vec3':'Vec3' 'void (int, int, int)'
    |     |-IntegerLiteral 0x7fab0e047b30 <col:17> 'int' 1
    |     |-IntegerLiteral 0x7fab0e047b50 <col:20> 'int' 2
    |     `-IntegerLiteral 0x7fab0e047b70 <col:23> 'int' 3

### auto v7 = Vec3{1, 2, 3};

    `-DeclStmt 0x7fab0c00fd20 <line:22:2, col:25>
      `-VarDecl 0x7fab0e047ce8 <col:2, col:24> col:7 v7 'Vec3':'Vec3' cinit
        `-CXXTemporaryObjectExpr 0x7fab0c00fc18 <col:12, col:24> 'Vec3':'Vec3' 'void (int, int, int)' list
          |-IntegerLiteral 0x7fab0e047d60 <col:17> 'int' 1
          |-IntegerLiteral 0x7fab0e047d80 <col:20> 'int' 2
          `-IntegerLiteral 0x7fab0e047da0 <col:23> 'int' 3


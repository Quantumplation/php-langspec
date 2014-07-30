#Specification for PHP
Facebook has dedicated all copyright to this specification to the public
domain worldwide under the CC0 Public Domain Dedication located at
<http://creativecommons.org/publicdomain/zero/1.0/>. This specification
is distributed without any warranty.

(Initially written in 2014 by Facebook, Inc., July 2014)


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Introduction](#introduction)
- [Conformance](#conformance)
- [Terms and Definitions](#terms-and-definitions)
- [Basic Concepts](#basic-concepts)
  - [Program Structure](#program-structure)
  - [Program Start-Up](#program-start-up)
  - [Program Termination](#program-termination)
  - [The Memory Model](#the-memory-model)
    - [General](#general)
    - [Reclamation and Automatic Memory Management](#reclamation-and-automatic-memory-management)
    - [Assignment](#assignment)
      - [General](#general-1)
      - [Value Assignment of Scalar Types to a Local Variable](#value-assignment-of-scalar-types-to-a-local-variable)
      - [Value Assignment of Object and Resource Types to a Local Variable](#value-assignment-of-object-and-resource-types-to-a-local-variable)
      - [ByRef Assignment for Scalar Types with Local Variables](#byref-assignment-for-scalar-types-with-local-variables)
      - [Byref Assignment of Non-Scalar Types with Local Variables](#byref-assignment-of-non-scalar-types-with-local-variables)
      - [Value Assignment of Array Types to Local Variables](#value-assignment-of-array-types-to-local-variables)
      - [Deferred Array Copying](#deferred-array-copying)
      - [General Value Assignment](#general-value-assignment)
      - [General ByRef Assignment](#general-byref-assignment)
    - [Argument Passing](#argument-passing)
    - [Value Returning](#value-returning)
    - [Cloning objects](#cloning-objects)
  - [Scope](#scope)
  - [Storage Duration](#storage-duration)
- [Types](#types)
  - [General](#general-2)
  - [Scalar Types](#scalar-types)
    - [General](#general-3)
    - [The Boolean Type](#the-boolean-type)
    - [The Integer Type](#the-integer-type)
    - [The Floating-Point Type](#the-floating-point-type)
    - [The String Type](#the-string-type)
    - [The Null Type](#the-null-type)
  - [Composite Types](#composite-types)
    - [Array Types](#array-types)
    - [Object Types](#object-types)
    - [Resource Types](#resource-types)
- [Constants](#constants)
  - [General](#general-4)
  - [Context-Dependent Constants](#context-dependent-constants)
  - [Core Predefined Constants](#core-predefined-constants)
  - [User-Defined Constants](#user-defined-constants)
- [Variables](#variables)
  - [General](#general-5)
  - [Kinds of Variables](#kinds-of-variables)
    - [Constants](#constants-1)
    - [Local Variables](#local-variables)
    - [Array Elements](#array-elements)
    - [Function Statics](#function-statics)
    - [Global Variables](#global-variables)
    - [Instance Properties](#instance-properties)
    - [Static Properties](#static-properties)
    - [Class and Interface Constants](#class-and-interface-constants)
  - [Predefined Variables](#predefined-variables)
- [Conversions](#conversions)
  - [General](#general-6)
  - [Converting to Boolean Type](#converting-to-boolean-type)
  - [Converting to Integer Type](#converting-to-integer-type)
  - [Converting to Floating-Point Type](#converting-to-floating-point-type)
  - [Converting to String Type](#converting-to-string-type)
  - [Converting to Array Type](#converting-to-array-type)
  - [Converting to Object Type](#converting-to-object-type)
- [Lexical Structure](#lexical-structure)
  - [Scripts](#scripts)
  - [Grammars](#grammars)
  - [Lexical analysis](#lexical-analysis)
  - [General](#general-7)
  - [Comments](#comments)
    - [White Space](#white-space)
    - [Tokens](#tokens)
      - [General](#general-8)
      - [Names](#names)
      - [Keywords](#keywords)
      - [Literals](#literals)
        - [General](#general-9)
        - [Boolean Literals](#boolean-literals)
        - [Integer Literals](#integer-literals)
        - [Floating-Point Literals](#floating-point-literals)
        - [String Literals](#string-literals)
          - [Single-Quoted String Literals](#single-quoted-string-literals)
          - [Double-Quoted String Literals](#double-quoted-string-literals)
          - [Heredoc String Literals](#heredoc-string-literals)
          - [Nowdoc String Literals](#nowdoc-string-literals)
        - [The Null Literal](#the-null-literal)
      - [Operators and Punctuators](#operators-and-punctuators)
- [Expressions](#expressions)
  - [General](#general-10)
  - [Primary Expressions](#primary-expressions)
    - [General](#general-11)
    - [Intrinsics](#intrinsics)
      - [General](#general-12)
      - [array](#array)
      - [echo](#echo)
      - [empty](#empty)
      - [eval](#eval)
      - [exit/die](#exitdie)
      - [isset](#isset)
      - [list](#list)
      - [print](#print)
      - [unset](#unset)
    - [Anonymous Function-Creation](#anonymous-function-creation)
  - [Postfix Operators](#postfix-operators)
    - [General](#general-13)
    - [The `clone` Operator](#the-clone-operator)
    - [The `new` Operator](#the-new-operator)
    - [Array Creation Operator](#array-creation-operator)
    - [Subscript Operator](#subscript-operator)
    - [Function Call Operator](#function-call-operator)
    - [Member-Selection Operator](#member-selection-operator)
    - [Postfix Increment and Decrement Operators](#postfix-increment-and-decrement-operators)
    - [Scope-Resolution Operator](#scope-resolution-operator)
    - [Exponentiation Operator](#exponentiation-operator)
  - [Unary Operators](#unary-operators)
    - [General](#general-14)
    - [Prefix Increment and Decrement Operators](#prefix-increment-and-decrement-operators)
    - [Unary Arithmetic Operators](#unary-arithmetic-operators)
    - [Error Control Operator](#error-control-operator)
    - [Shell Command Operator](#shell-command-operator)
    - [Cast Operator](#cast-operator)
    - [Variable-Name Creation Operator](#variable-name-creation-operator)
  - [`instanceof` Operator](#instanceof-operator)
  - [Multiplicative Operators](#multiplicative-operators)
  - [Additive Operators](#additive-operators)
  - [Bitwise Shift Operators](#bitwise-shift-operators)
  - [Relational Operators](#relational-operators)
  - [Equality Operators](#equality-operators)
  - [Bitwise AND Operator](#bitwise-and-operator)
  - [Bitwise Exclusive OR Operator](#bitwise-exclusive-or-operator)
  - [Bitwise Inclusive OR Operator](#bitwise-inclusive-or-operator)
  - [Logical AND Operator (form 1)](#logical-and-operator-form-1)
  - [Logical Inclusive OR Operator (form 1)](#logical-inclusive-or-operator-form-1)
  - [Conditional Operator](#conditional-operator)
  - [Assignment Operators](#assignment-operators)
    - [General](#general-15)
    - [Simple Assignment](#simple-assignment)
    - [byRef Assignment](#byref-assignment)
  - [Compound Assignment](#compound-assignment)
  - [Logical AND Operator (form 2)](#logical-and-operator-form-2)
  - [Logical Exclusive OR Operator](#logical-exclusive-or-operator)
  - [Logical Inclusive OR Operator (form 2)](#logical-inclusive-or-operator-form-2)
  - [`yield` Operator](#yield-operator)
  - [Script Inclusion Operators](#script-inclusion-operators)
    - [General](#general-16)
    - [The `include` Operator](#the-include-operator)
    - [The `include_once` Operator](#the-include_once-operator)
    - [The `require` Operator](#the-require-operator)
    - [The `require_once` Operator](#the-require_once-operator)
  - [Constant Expressions](#constant-expressions)
- [Statements](#statements)
  - [General](#general-17)
  - [Compound Statements](#compound-statements)
  - [Labeled Statements](#labeled-statements)
  - [Expression Statements](#expression-statements)
  - [Selection Statements](#selection-statements)
    - [General](#general-18)
    - [The `if` Statement](#the-if-statement)
    - [The `switch` Statement](#the-switch-statement)
  - [Iteration Statements](#iteration-statements)
    - [General](#general-19)
  - [The `while` Statement](#the-while-statement)
  - [The `do` Statement](#the-do-statement)
  - [The `for` Statement](#the-for-statement)
  - [The `foreach` Statement](#the-foreach-statement)
  - [Jump Statements](#jump-statements)
    - [General](#general-20)
    - [The `goto` Statement](#the-goto-statement)
    - [The `continue` Statement](#the-continue-statement)
  - [The `break` Statement](#the-break-statement)
    - [The `return` Statement](#the-return-statement)
    - [The `throw` Statement](#the-throw-statement)
  - [The `try` Statement](#the-try-statement)
  - [The `declare` Statement](#the-declare-statement)
- [Arrays](#arrays)
  - [General](#general-21)
  - [Array Creation and Initialization](#array-creation-and-initialization)
  - [Element Access and Insertion](#element-access-and-insertion)
- [Functions](#functions)
  - [General](#general-22)
  - [Function Calls](#function-calls)
  - [Function Definitions](#function-definitions)
  - [Variable Functions](#variable-functions)
  - [Anonymous Functions](#anonymous-functions)
- [Classes](#classes)
  - [General](#general-23)
  - [Class Declarations](#class-declarations)
  - [Class Members](#class-members)
  - [Dynamic Members](#dynamic-members)
  - [Constants](#constants-2)
  - [Properties](#properties)
  - [Methods](#methods)
  - [Constructors](#constructors)
  - [Destructors](#destructors)
  - [Methods with Special Semantics](#methods-with-special-semantics)
    - [General](#general-24)
    - [Method `__call`](#method-__call)
    - [Method `__callStatic`](#method-__callstatic)
    - [Method `__clone`](#method-__clone)
    - [Method `__get`](#method-__get)
    - [Method `__invoke`](#method-__invoke)
    - [Method `__isset`](#method-__isset)
    - [Method `__set`](#method-__set)
    - [Method `__set_state`](#method-__set_state)
    - [Method `__sleep`](#method-__sleep)
    - [Method `__toString`](#method-__tostring)
    - [Method `__unset`](#method-__unset)
    - [Method `__wakeup`](#method-__wakeup)
  - [Serialization](#serialization)
  - [Predefined Classes](#predefined-classes)
    - [Class `Closure`](#class-closure)
    - [Class `Generator`](#class-generator)
    - [Class `__PHP_Incomplete_Class`](#class-__php_incomplete_class)
    - [Class `stdClass`](#class-stdclass)
- [Interfaces](#interfaces)
  - [General](#general-25)
  - [Interface Declarations](#interface-declarations)
  - [Interface Members](#interface-members)
  - [Constants](#constants-3)
  - [Methods](#methods-1)
  - [Predefined Interfaces](#predefined-interfaces)
    - [Interface `ArrayAccess`](#interface-arrayaccess)
    - [Interface `Iterator`](#interface-iterator)
    - [Interface `IteratorAggregate`](#interface-iteratoraggregate)
    - [Interface `Traversable`](#interface-traversable)
    - [Interface  `Serializable`](#interface--serializable)
- [Traits](#traits)
  - [General](#general-26)
  - [Trait Declarations](#trait-declarations)
  - [Trait Members](#trait-members)
- [Exception Handling](#exception-handling)
  - [General](#general-27)
  - [Class `Exception`](#class-exception)
  - [Tracing Exceptions](#tracing-exceptions)
  - [User-Defined Exception Classes](#user-defined-exception-classes)
- [Namespaces](#namespaces)
  - [General](#general-28)
  - [Name Lookup](#name-lookup)
  - [Defining Namespaces](#defining-namespaces)
  - [Namespace Use Declarations**](#namespace-use-declarations)
- [Grammar](#grammar)
  - [General](#general-29)
  - [Lexical Grammar](#lexical-grammar)
    - [General](#general-30)
    - [Comments](#comments-1)
    - [White Space](#white-space-1)
    - [Tokens](#tokens-1)
      - [General](#general-31)
      - [Names](#names-1)
    - [Keywords](#keywords-1)
    - [Literals](#literals-1)
      - [General](#general-32)
      - [Boolean Literals](#boolean-literals-1)
      - [Integer Literals](#integer-literals-1)
      - [Floating-Point Literals](#floating-point-literals-1)
      - [String Literals](#string-literals-1)
      - [The Null Literal](#the-null-literal-1)
    - [Operators and Punctuators](#operators-and-punctuators-1)
  - [Syntactic Grammar](#syntactic-grammar)
    - [Program Structure](#program-structure-1)
    - [Variables](#variables-1)
    - [Expressions](#expressions-1)
      - [Primary Expressions](#primary-expressions-1)
      - [Postfix Operators](#postfix-operators-1)
      - [Unary Operators](#unary-operators-1)
      - [instanceof Operator](#instanceof-operator)
      - [Multiplicative Operators](#multiplicative-operators-1)
      - [Additive Operators](#additive-operators-1)
      - [Bitwise Shift Operators](#bitwise-shift-operators-1)
      - [Relational Operators](#relational-operators-1)
      - [Equality Operators](#equality-operators-1)
      - [Bitwise Logical Operators](#bitwise-logical-operators)
      - [Logical Operators (form 1)](#logical-operators-form-1)
      - [Conditional Operator](#conditional-operator-1)
      - [Assignment Operators](#assignment-operators-1)
      - [Logical Operators (form 2)](#logical-operators-form-2)
      - [yield Operator](#yield-operator)
      - [Script Inclusion Operators](#script-inclusion-operators-1)
      - [Constant Expressions](#constant-expressions-1)
    - [Statements](#statements-1)
      - [General](#general-33)
      - [Compound Statements](#compound-statements-1)
      - [Labeled Statements](#labeled-statements-1)
      - [Expression Statements](#expression-statements-1)
      - [Iteration Statements](#iteration-statements-1)
      - [Jump Statements](#jump-statements-1)
      - [The try Statement](#the-try-statement)
      - [The declare Statement](#the-declare-statement)
    - [Functions](#functions-1)
    - [Classes](#classes-1)
    - [Interfaces](#interfaces-1)
    - [Traits](#traits-1)
    - [Namespaces](#namespaces-1)
- [Bibliography](#bibliography)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
#Introduction
¯\\\_(ツ)_/¯
#Conformance
¯\\\_(ツ)_/¯
#Terms and Definitions
¯\\\_(ツ)_/¯
#Basic Concepts
##Program Structure
¯\\\_(ツ)_/¯
##Program Start-Up
¯\\\_(ツ)_/¯
##Program Termination
¯\\\_(ツ)_/¯
##The Memory Model
###General
¯\\\_(ツ)_/¯
###Reclamation and Automatic Memory Management
¯\\\_(ツ)_/¯
###Assignment
####General
¯\\\_(ツ)_/¯
####Value Assignment of Scalar Types to a Local Variable
¯\\\_(ツ)_/¯
####Value Assignment of Object and Resource Types to a Local Variable
¯\\\_(ツ)_/¯
####ByRef Assignment for Scalar Types with Local Variables
¯\\\_(ツ)_/¯
####Byref Assignment of Non-Scalar Types with Local Variables
¯\\\_(ツ)_/¯
####Value Assignment of Array Types to Local Variables
¯\\\_(ツ)_/¯
####Deferred Array Copying
¯\\\_(ツ)_/¯
####General Value Assignment
¯\\\_(ツ)_/¯
####General ByRef Assignment
¯\\\_(ツ)_/¯
###Argument Passing
¯\\\_(ツ)_/¯
###Value Returning
¯\\\_(ツ)_/¯
###Cloning objects
¯\\\_(ツ)_/¯
##Scope
¯\\\_(ツ)_/¯
##Storage Duration
¯\\\_(ツ)_/¯
#Types
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Scalar Types
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###The Boolean Type
¯\\\_(ツ)_/¯
###The Integer Type
¯\\\_(ツ)_/¯
###The Floating-Point Type
¯\\\_(ツ)_/¯
###The String Type
¯\\\_(ツ)_/¯
###The Null Type
¯\\\_(ツ)_/¯
##Composite Types
¯\\\_(ツ)_/¯
###Array Types
¯\\\_(ツ)_/¯
###Object Types
¯\\\_(ツ)_/¯
###Resource Types
¯\\\_(ツ)_/¯
#Constants
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Context-Dependent Constants
¯\\\_(ツ)_/¯
##Core Predefined Constants
¯\\\_(ツ)_/¯
##User-Defined Constants
¯\\\_(ツ)_/¯
#Variables
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Kinds of Variables
¯\\\_(ツ)_/¯
###Constants
¯\\\_(ツ)_/¯
###Local Variables
¯\\\_(ツ)_/¯
###Array Elements
¯\\\_(ツ)_/¯
###Function Statics
¯\\\_(ツ)_/¯
###Global Variables
¯\\\_(ツ)_/¯
###Instance Properties
¯\\\_(ツ)_/¯
###Static Properties
¯\\\_(ツ)_/¯
###Class and Interface Constants
¯\\\_(ツ)_/¯
##Predefined Variables
¯\\\_(ツ)_/¯
#Conversions
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Converting to Boolean Type
¯\\\_(ツ)_/¯
##Converting to Integer Type
¯\\\_(ツ)_/¯
##Converting to Floating-Point Type
¯\\\_(ツ)_/¯
##Converting to String Type
¯\\\_(ツ)_/¯
##Converting to Array Type
¯\\\_(ツ)_/¯
##Converting to Object Type
¯\\\_(ツ)_/¯
#Lexical Structure
¯\\\_(ツ)_/¯
##Scripts
¯\\\_(ツ)_/¯
##Grammars
¯\\\_(ツ)_/¯
##Lexical analysis
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Comments
¯\\\_(ツ)_/¯
###White Space
¯\\\_(ツ)_/¯
###Tokens
¯\\\_(ツ)_/¯
####General
¯\\\_(ツ)_/¯
####Names
¯\\\_(ツ)_/¯
####Keywords
¯\\\_(ツ)_/¯
####Literals
¯\\\_(ツ)_/¯
#####General
¯\\\_(ツ)_/¯
#####Boolean Literals
¯\\\_(ツ)_/¯
#####Integer Literals
¯\\\_(ツ)_/¯
#####Floating-Point Literals
¯\\\_(ツ)_/¯
#####String Literals
¯\\\_(ツ)_/¯
######Single-Quoted String Literals
¯\\\_(ツ)_/¯
######Double-Quoted String Literals
¯\\\_(ツ)_/¯
######Heredoc String Literals
¯\\\_(ツ)_/¯
######Nowdoc String Literals
¯\\\_(ツ)_/¯
#####The Null Literal
¯\\\_(ツ)_/¯
####Operators and Punctuators
¯\\\_(ツ)_/¯
#Expressions
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Primary Expressions
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###Intrinsics
¯\\\_(ツ)_/¯
####General
¯\\\_(ツ)_/¯
####array
¯\\\_(ツ)_/¯
####echo
¯\\\_(ツ)_/¯
####empty
¯\\\_(ツ)_/¯
####eval
¯\\\_(ツ)_/¯
####exit/die
¯\\\_(ツ)_/¯
####isset
¯\\\_(ツ)_/¯
####list
¯\\\_(ツ)_/¯
####print
¯\\\_(ツ)_/¯
####unset
¯\\\_(ツ)_/¯
###Anonymous Function-Creation
¯\\\_(ツ)_/¯
##Postfix Operators
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###The `clone` Operator
¯\\\_(ツ)_/¯
###The `new` Operator
¯\\\_(ツ)_/¯
###Array Creation Operator
¯\\\_(ツ)_/¯
###Subscript Operator
¯\\\_(ツ)_/¯
###Function Call Operator
¯\\\_(ツ)_/¯
strlen($lastName) // returns the # of bytes in the string
¯\\\_(ツ)_/¯
###Member-Selection Operator
¯\\\_(ツ)_/¯
###Postfix Increment and Decrement Operators
¯\\\_(ツ)_/¯
###Scope-Resolution Operator
¯\\\_(ツ)_/¯
###Exponentiation Operator
¯\\\_(ツ)_/¯
##Unary Operators
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###Prefix Increment and Decrement Operators
¯\\\_(ツ)_/¯
###Unary Arithmetic Operators
¯\\\_(ツ)_/¯
###Error Control Operator
¯\\\_(ツ)_/¯
###Shell Command Operator
¯\\\_(ツ)_/¯
###Cast Operator
¯\\\_(ツ)_/¯
###Variable-Name Creation Operator
¯\\\_(ツ)_/¯
##`instanceof` Operator
¯\\\_(ツ)_/¯
##Multiplicative Operators
¯\\\_(ツ)_/¯
##Additive Operators
¯\\\_(ツ)_/¯
##Bitwise Shift Operators
¯\\\_(ツ)_/¯
##Relational Operators
¯\\\_(ツ)_/¯
##Equality Operators
¯\\\_(ツ)_/¯
## Bitwise AND Operator
¯\\\_(ツ)_/¯
##Bitwise Exclusive OR Operator
¯\\\_(ツ)_/¯
##Bitwise Inclusive OR Operator
¯\\\_(ツ)_/¯
##Logical AND Operator (form 1)
¯\\\_(ツ)_/¯
##Logical Inclusive OR Operator (form 1)
¯\\\_(ツ)_/¯
##Conditional Operator
¯\\\_(ツ)_/¯
##Assignment Operators
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###Simple Assignment
¯\\\_(ツ)_/¯
###byRef Assignment
¯\\\_(ツ)_/¯
##Compound Assignment
¯\\\_(ツ)_/¯
##Logical AND Operator (form 2)
¯\\\_(ツ)_/¯
##Logical Exclusive OR Operator
¯\\\_(ツ)_/¯
##Logical Inclusive OR Operator (form 2)
¯\\\_(ツ)_/¯
## `yield` Operator
¯\\\_(ツ)_/¯
##Script Inclusion Operators
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###The `include` Operator
¯\\\_(ツ)_/¯
###The `include_once` Operator
¯\\\_(ツ)_/¯
###The `require` Operator
¯\\\_(ツ)_/¯
###The `require_once` Operator
¯\\\_(ツ)_/¯
##Constant Expressions
¯\\\_(ツ)_/¯
#Statements
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Compound Statements
¯\\\_(ツ)_/¯
##Labeled Statements
¯\\\_(ツ)_/¯
##Expression Statements
¯\\\_(ツ)_/¯
##Selection Statements
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###The `if` Statement
¯\\\_(ツ)_/¯
###The `switch` Statement
¯\\\_(ツ)_/¯
##Iteration Statements
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
##The `while` Statement
¯\\\_(ツ)_/¯
##The `do` Statement
¯\\\_(ツ)_/¯
##The `for` Statement
¯\\\_(ツ)_/¯
##The `foreach` Statement
¯\\\_(ツ)_/¯
##Jump Statements
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###The `goto` Statement
¯\\\_(ツ)_/¯
###The `continue` Statement
¯\\\_(ツ)_/¯
##The `break` Statement
¯\\\_(ツ)_/¯
###The `return` Statement
¯\\\_(ツ)_/¯
###The `throw` Statement
¯\\\_(ツ)_/¯
##The `try` Statement
¯\\\_(ツ)_/¯
##The `declare` Statement
¯\\\_(ツ)_/¯
#Arrays
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Array Creation and Initialization
¯\\\_(ツ)_/¯
##Element Access and Insertion
¯\\\_(ツ)_/¯
#Functions
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Function Calls
¯\\\_(ツ)_/¯
##Function Definitions
¯\\\_(ツ)_/¯
##Variable Functions
¯\\\_(ツ)_/¯
##Anonymous Functions
¯\\\_(ツ)_/¯
#Classes
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Class Declarations
¯\\\_(ツ)_/¯
##Class Members
¯\\\_(ツ)_/¯
##Dynamic Members
¯\\\_(ツ)_/¯
##Constants
¯\\\_(ツ)_/¯
##Properties
¯\\\_(ツ)_/¯
##Methods
¯\\\_(ツ)_/¯
##Constructors
¯\\\_(ツ)_/¯
##Destructors
¯\\\_(ツ)_/¯
##Methods with Special Semantics
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###Method `__call`
¯\\\_(ツ)_/¯
###Method `__callStatic`
¯\\\_(ツ)_/¯
###Method `__clone`
¯\\\_(ツ)_/¯
###Method `__get`
¯\\\_(ツ)_/¯
###Method `__invoke`
¯\\\_(ツ)_/¯
###Method `__isset`
¯\\\_(ツ)_/¯
###Method `__set`
¯\\\_(ツ)_/¯
###Method `__set_state`
¯\\\_(ツ)_/¯
###Method `__sleep`
¯\\\_(ツ)_/¯
###Method `__toString`
¯\\\_(ツ)_/¯
###Method `__unset`
¯\\\_(ツ)_/¯
###Method `__wakeup`
¯\\\_(ツ)_/¯
##Serialization
¯\\\_(ツ)_/¯
##Predefined Classes
¯\\\_(ツ)_/¯
### Class `Closure`
¯\\\_(ツ)_/¯
###Class `Generator`
¯\\\_(ツ)_/¯
###Class `__PHP_Incomplete_Class`
¯\\\_(ツ)_/¯
###Class `stdClass`
¯\\\_(ツ)_/¯
#Interfaces
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Interface Declarations
¯\\\_(ツ)_/¯
##Interface Members
¯\\\_(ツ)_/¯
##Constants
¯\\\_(ツ)_/¯
##Methods
¯\\\_(ツ)_/¯
##Predefined Interfaces
¯\\\_(ツ)_/¯
###Interface `ArrayAccess`
¯\\\_(ツ)_/¯
###Interface `Iterator`
¯\\\_(ツ)_/¯
###Interface `IteratorAggregate`
¯\\\_(ツ)_/¯
###Interface `Traversable`
¯\\\_(ツ)_/¯
###Interface  `Serializable`
¯\\\_(ツ)_/¯
#Traits
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Trait Declarations
¯\\\_(ツ)_/¯
##Trait Members
¯\\\_(ツ)_/¯
#Exception Handling
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Class `Exception`
¯\\\_(ツ)_/¯
##Tracing Exceptions
¯\\\_(ツ)_/¯
##User-Defined Exception Classes
¯\\\_(ツ)_/¯
#Namespaces
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Name Lookup
¯\\\_(ツ)_/¯
##Defining Namespaces
¯\\\_(ツ)_/¯
##Namespace Use Declarations**
¯\\\_(ツ)_/¯
#Grammar
¯\\\_(ツ)_/¯
##General
¯\\\_(ツ)_/¯
##Lexical Grammar
¯\\\_(ツ)_/¯
###General
¯\\\_(ツ)_/¯
###Comments
¯\\\_(ツ)_/¯
###White Space
¯\\\_(ツ)_/¯
###Tokens
¯\\\_(ツ)_/¯
####General
¯\\\_(ツ)_/¯
####Names
¯\\\_(ツ)_/¯
###Keywords
¯\\\_(ツ)_/¯
###Literals
¯\\\_(ツ)_/¯
####General
¯\\\_(ツ)_/¯
####Boolean Literals
¯\\\_(ツ)_/¯
####Integer Literals
¯\\\_(ツ)_/¯
####Floating-Point Literals
¯\\\_(ツ)_/¯
####String Literals
¯\\\_(ツ)_/¯
####The Null Literal
¯\\\_(ツ)_/¯
###Operators and Punctuators
¯\\\_(ツ)_/¯
##Syntactic Grammar
¯\\\_(ツ)_/¯
###Program Structure
¯\\\_(ツ)_/¯
###Variables
¯\\\_(ツ)_/¯
###Expressions
¯\\\_(ツ)_/¯
####Primary Expressions
¯\\\_(ツ)_/¯
####Postfix Operators
¯\\\_(ツ)_/¯
####Unary Operators
¯\\\_(ツ)_/¯
####instanceof Operator
¯\\\_(ツ)_/¯
####Multiplicative Operators
¯\\\_(ツ)_/¯
####Additive Operators
¯\\\_(ツ)_/¯
####Bitwise Shift Operators
¯\\\_(ツ)_/¯
####Relational Operators
¯\\\_(ツ)_/¯
####Equality Operators
¯\\\_(ツ)_/¯
####Bitwise Logical Operators
¯\\\_(ツ)_/¯
####Logical Operators (form 1)
¯\\\_(ツ)_/¯
####Conditional Operator
¯\\\_(ツ)_/¯
####Assignment Operators
¯\\\_(ツ)_/¯
####Logical Operators (form 2)
¯\\\_(ツ)_/¯
####yield Operator
¯\\\_(ツ)_/¯
####Script Inclusion Operators
¯\\\_(ツ)_/¯
####Constant Expressions
¯\\\_(ツ)_/¯
###Statements
¯\\\_(ツ)_/¯
####General
¯\\\_(ツ)_/¯
####Compound Statements
¯\\\_(ツ)_/¯
####Labeled Statements
¯\\\_(ツ)_/¯
####Expression Statements
¯\\\_(ツ)_/¯
####Iteration Statements
¯\\\_(ツ)_/¯
####Jump Statements
¯\\\_(ツ)_/¯
####The try Statement
¯\\\_(ツ)_/¯
####The declare Statement
¯\\\_(ツ)_/¯
###Functions
¯\\\_(ツ)_/¯
###Classes
¯\\\_(ツ)_/¯
###Interfaces
¯\\\_(ツ)_/¯
###Traits
¯\\\_(ツ)_/¯
###Namespaces
¯\\\_(ツ)_/¯
#Bibliography
¯\\\_(ツ)_/¯

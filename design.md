# 🧠 ZARA Interpreter Design Document

## 📌 Project Overview

This project implements a **mini scripting language interpreter** for the ZARA language (Zero-ceremony Arithmetic and Reasoning Assembler) using Java.

The interpreter allows users to write `.zara` programs and execute them via a command-line interface.

---

## 🎯 Objectives

- Build a working interpreter using **pure Java**
- Apply **Object-Oriented Design principles**
- Implement a **3-stage execution pipeline**:
  - Tokenization
  - Parsing
  - Evaluation
- Support variables, arithmetic, conditions, and loops

---

## 🏗️ System Architecture

The interpreter follows a pipeline-based architecture:

```
Source Code (.zara)
        ↓
   Tokenizer
        ↓
   List<Token>
        ↓
     Parser
        ↓
 List<Instruction> (AST)
        ↓
   Interpreter
        ↓
     Output
```

---

## ⚙️ Core Components

### 1. Tokenizer

**Responsibility:**
Convert raw source code into tokens.

**Key Classes:**
- `TokenType` (enum)
- `Token`
- `Tokenizer`

**Supported Tokens:**
- Keywords: `set`, `show`, `when`, `loop`
- Identifiers
- Numbers
- Strings
- Operators: `+`, `-`, `*`, `/`, `>`, `<`, `=`
- Special: NEWLINE, EOF

---

### 2. Parser

**Responsibility:**
Convert tokens into a structured representation (AST).

**Key Class:**
- `Parser`

**Parsing Strategy:**
- Recursive descent parsing
- Operator precedence handled via:
  - `parseExpression()` → +, -
  - `parseTerm()` → *, /
  - `parsePrimary()` → literals & variables

---

### 3. Abstract Syntax Tree (AST)

**Purpose:**
Represent expressions in a hierarchical structure.

**Interface:**
```java
public interface Expression {
    Object evaluate(Environment env);
}
```

**Node Types:**
- `NumberNode`
- `StringNode`
- `VariableNode`
- `BinaryOpNode`

---

### 4. Environment

**Responsibility:**
Store variable values during execution.

**Implementation:**
```java
Map<String, Object>
```

**Operations:**
- `set(name, value)`
- `get(name)`

---

### 5. Instructions

**Purpose:**
Represent executable statements.

**Interface:**
```java
public interface Instruction {
    void execute(Environment env);
}
```

**Instruction Types:**
- `AssignInstruction`
- `PrintInstruction`
- `IfInstruction`
- `RepeatInstruction`

---

### 6. Interpreter

**Responsibility:**
Connect all components and execute the program.

**Steps:**
1. Tokenize input
2. Parse tokens
3. Execute instructions

---

### 7. CLI Interface

- Accept `.zara` file as input
- Read file content
- Pass to interpreter

---

## 🔁 Execution Flow Example

**Input:**
```
set x = 10
set y = 3
show x + y * 2
```

**Execution Steps:**
1. Tokenizer → generates tokens
2. Parser → builds AST
3. Evaluator:
   - Computes `y * 2`
   - Adds to `x`
   - Prints result

---

## 👥 Team Members

- Bhaskar Mahato  
- Dilip Vaishnav  
- Rohit Kumar  

---

## 👥 Team Responsibilities

| Name | Responsibility |
|------|----------------|
| Bhaskar Mahato | Tokenizer + Integration |
| Dilip Vaishnav | Parser + AST |
| Rohit Kumar | Execution + Interpreter |

All members are responsible for understanding the complete system for the viva.

---

## 📂 Project Structure

```
project/
├── tokenizer/
├── parser/
├── ast/
├── instruction/
├── runtime/
├── interpreter/
└── Main.java
```

---

## 🧪 Testing Plan

Test cases include:
- Arithmetic operations
- String printing
- Conditional execution
- Loop execution

---

## ⚠️ Error Handling

- Undefined variable → RuntimeException
- Invalid syntax → Parser error
- Invalid tokens → Tokenizer error

---

## 🚀 Future Enhancements

- Else block support
- Equality operator (`==`)
- Nested loops and conditions
- Better error messages with line numbers

---

## 📚 Design Principles Used

- Single Responsibility Principle
- Separation of Concerns
- Modular Design
- Extensibility

---

## ✅ Conclusion

This project demonstrates how programming languages work internally by building a complete interpreter from scratch using object-oriented design principles.
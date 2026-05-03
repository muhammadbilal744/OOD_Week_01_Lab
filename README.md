#  Object-Oriented Design (OOD) — Week 1 Lab

&gt; **Course:** Object-Oriented Design  

---

##  Table of Contents
1. [OOP vs OOD: The Fundamental Difference](#-oop-vs-ood-the-fundamental-difference)
2. [The 4 Design Smells](#-the-4-design-smells)
3. [The 4-Step OOD Process](#-the-4-step-ood-process)
4. [UML Relationships Explained](#-uml-relationships-explained)
5. [Project: Restaurant System](#-project-restaurant-system)
   - [Requirements Analysis](#requirements-analysis)
   - [CRC Cards](#crc-cards)
   - [UML Diagram](#uml-diagram)
   - [Relationship Decisions](#relationship-decisions)
   - [Code Implementation](#code-implementation)
   - [Lifetime Proof](#lifetime-proof)
6. [Key Takeaways](#-key-takeaways)

---

##  OOP vs OOD: The Fundamental Difference

| Aspect | **OOP (Object-Oriented Programming)** | **OOD (Object-Oriented Design)** |
|--------|--------------------------------------|----------------------------------|
| **Analogy** | The *tool* — knowing how to use a hammer | The *blueprint* — knowing where to place the walls |
| **Focus** | Syntax, classes, methods, inheritance, polymorphism | Assigning responsibilities, managing dependencies, maintainability |
| **Question it answers** | *"How do I write this code in Python?"* | *"What code should I write, and where does it belong?"* |
| **Output** | Working code | Robust, flexible architecture |

&gt; **Key Insight:** Knowing Python syntax doesn't mean you know how to *structure* a system. OOD is the **planning phase** before you write code.

---

##  The 4 Design Smells

Symptoms that your class structure needs refactoring:

| Smell | Meaning | Example |
|-------|---------|---------|
| ** Rigidity** | System is hard to change. One modification causes cascading changes. | *"I just wanted to add a new payment method, but now I have to update 14 different files."* |
| ** Immobility** | System is hard to reuse. Useful logic is tangled with irrelevant details. | *"I need the discount logic for the mobile app, but it's deeply embedded in the web UI class."* |
| ** Fragility** | System is easy to break. Changes cause unexpected bugs. | *"I fixed the email template, and somehow the tax calculation stopped working."* |
| **🌫️ Opacity** | System is hard to understand. Classes have misleading names. | *"Why is the 'UserSession' class responsible for generating PDF invoices?"* |

---

##  The 4-Step OOD Process

A repeatable framework for moving from plain English to working code:


---


---

## 🔗 UML Relationships Explained

### The Golden Rule
> **"If A is destroyed, does B also cease to exist?"**

| Answer | Relationship | Symbol | Keyword | Example |
|--------|-------------|--------|---------|---------|
| **YES** → B dies too | **Composition** | `◆──` | "owns" | Ride owns Payment |
| **NO** → B survives, A owns B | **Aggregation** | `◇──` | "has-a" | Fleet has Vehicle |
| **NO** → B survives, no ownership | **Association** | `───` | "uses" | Driver uses RideRequest |

### Code Patterns

| Relationship | Object Created Where? | Code Pattern |
|-------------|----------------------|--------------|
| **Composition** | Inside the owner class | `self.part = Part(...)` in `__init__` |
| **Aggregation** | Outside, passed in | `self.part = part` (parameter) |
| **Association** | Outside, passed in | `self.partner = partner` (parameter) |

---

## 🍽️ Project: Restaurant System

### Requirements Analysis

> *"A Restaurant has multiple Menus (e.g., Breakfast, Dinner). A Menu has multiple MenuItems. A Customer places an Order. An Order contains multiple OrderItems."*

### Step 1: Nouns → Classes, Verbs → Methods

| Noun | Class? | Why? |
|------|--------|------|
| Restaurant | ✅ Class | Main entity, owns menus |
| Menu | ✅ Class | Sub-entity, owns items |
| MenuItem | ✅ Class | Individual food item |
| Customer | ✅ Class | Actor, places orders |
| Order | ✅ Class | Transaction entity |
| OrderItem | ✅ Class | Part of order |

| Verb | Method | Class |
|------|--------|-------|
| has (menus) | `create_menu()` | Restaurant |
| has (items) | `add_item()` | Menu |
| places | `place_order()` | Customer |
| contains | `add_item()` | Order |

---

### CRC Cards

#### Restaurant

┌──────────────────────────────────────────────┐
│  Restaurant                                  │
├─────────────────────┬────────────────────────┤
│ Responsibilities    │  Collaborators         │
│ • Own menus         │  • Menu                │
│ • Receive orders    │  • Order               │
│ • Display menus     │                        │
└─────────────────────┴────────────────────────┘


#### Menu
┌──────────────────────────────────────────────┐
│  Menu                                        │
├─────────────────────┬────────────────────────┤
│ Responsibilities    │  Collaborators         │
│ • Own menu items    │  • MenuItem            │
│ • Add/remove items  │  • Restaurant          │
│ • Display items     │                        │
└─────────────────────┴────────────────────────┘

#### Customer
┌──────────────────────────────────────────────┐
│  Order                                       │
├─────────────────────┬────────────────────────┤
│ Responsibilities    │  Collaborators         │
│ • Own order items   │  • OrderItem           │
│ • Calculate total   │  • MenuItem            │
│ • Track status      │  • Customer            │
│ • Show receipt      │                        │
└─────────────────────┴────────────────────────┘

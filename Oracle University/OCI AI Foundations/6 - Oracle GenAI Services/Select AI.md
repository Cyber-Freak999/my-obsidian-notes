# What Is Select AI?

**Select AI** is a feature of Oracle Autonomous Database that lets users query data using **natural language (NL)** instead of traditional SQL.

You can ask questions in plain English, like:

> “What are the top 10 streamed movies?”

Select AI then:
- Translates the NL query into a **SQL statement** using a **large language model (LLM)**.
- Executes it.
- Returns the result set, SQL query, or a narrative summary.

You don’t need to:
- Know SQL syntax.
- Know the schema or table/column names.
# Where It Fits in the Oracle AI Stack

Oracle delivers AI at **every layer** of the stack:

- **Infrastructure (OCI Gen AI)**
- **Data layer (Select AI in Autonomous DB)**
- **App layer (APEX, REST, etc.)**

**Select AI** sits in the **data layer**, helping enterprises use LLMs to get insights from **private organizational data**, which is not known to public LLMs.

---

## 🧪 Demo Highlights: Select AI in Action

An APEX app connects to Autonomous Database. With Select AI:

1. The user types:
    
    > “Show top 10 streamed movies”
    
    - ✅ Returns a result set (no need to know table or column names)
1. The user follows up with:
    
    > “Who are the actors in these movies?”
    
2. Then:
    
    > “What is the total number of movies streamed?”
    

You can also:

- Use **APEX interactive reports** to explore data visually (filters, charts).
- View the **generated SQL** using `SELECT AI SHOWSQL`.

---

#  How It Works Under the Hood

Select AI is powered by a **multi-step LLM integration process**:

1. **User submits a question** (natural language).    
2. Oracle **engineers a prompt**, optimized for DB context.
3. A selected **LLM** interprets the question and returns SQL.
4. The **database runs the SQL**.
5. Results are returned to:
    - SQL Developer
    - APEX app
    - REST API
    - Other clients
# Custom AI Profiles

Oracle allows pluggable configuration of different AI providers and models through **AI Profiles**.
You can:
- Choose the LLM provider: **OCI Gen AI, OpenAI, Cohere, LLaMA**, etc.    
- Specify:
    - Which **schemas, tables, or views** are included.
    - Which **model** is best suited for the workload.

## Enterprise-Grade Security

- Your **data never leaves** your **tenancy** when using **OCI Gen AI**.
- The **LLMs have no access** to your private data—queries are constructed using metadata only.
- Strong Oracle DB security guarantees are preserved at every step.

---

## 🧱 SQL Developer Integration

You can interact with Select AI via **SQL Developer**: 
```sql
    SELECT AI 'your natural language question';
    ```

To view the SQL that was generated:    
```sql
    SELECT AI SHOWSQL;
    ```

Refine the questions iteratively to get more accurate or detailed answers.
🚀 Stage 2 Task: Intelligence Query Engine Assessment

An advanced demographic query engine designed for growth analysts and marketing teams. This API supports multi-dimensional filtering, strict pagination, and a custom-built Natural Language Query (NLQ) engine to translate human intentions into database operations.

🧠 Natural Language Parsing (NLQ) Approach

Our search engine uses a deterministic, rule-based parsing architecture. To ensure zero-latency and high reliability (no LLM hallucination), it processes plain English strings through a multi-stage extraction pipeline.

🛠️ How it Works

    Normalization: The input query is lowercased and stripped of extra whitespace to ensure case-insensitive matching.

    Keyword Mapping: The engine scans for reserved keywords defined in our parser.js dictionary.

    Conflict Resolution: If "female" is detected, it overrides "male" detection (preventing the "male-in-female" string overlap bug).

        If both "male" and "female" appear (e.g., "male and female teenagers"), the gender filter is safely omitted to show all results.

    Parameter Extraction:

        Age Groups: Direct mapping for child, teenager, adult, and senior.

        Dynamic Ranges: Uses Regex (/above (\d+)/) to extract numeric constraints.

        "Young" Definition: Explicitly mapped to a 16-24 age range as per system requirements.

    Geographic Detection: Matches against an ISO-3166-1 mapped dictionary of 50+ major countries.

📖 Supported Keywords
Category Keywords Resulting Filter
Gender male, female, men, women, guy gender
Age Group child, teenager, adult, senior age_group
"Young" young, youth min_age: 16, max_age: 24
Comparison above, older than, under, younger than gte or lte on age
Country nigeria, kenya, uk, usa, etc. country_id

⚠️ Limitations & Edge Cases

While robust, the current rule-based parser has the following limitations:

    Negation: Does not currently support negative queries (e.g., "people not from Nigeria").

    Compound Logic: Does not support OR logic in a single query (e.g., "teenagers or seniors").

    Complex Syntax: "People between 20 and 30" will only capture "30" as a max_age filter; it expects "above X" or "under Y" syntax.

    Ambiguity: In queries like "adult teenagers," the logic follows a "Last-Match-Wins" rule for the age_group field.

🛠️ Technical Stack

    Runtime: Node.js

    Framework: Express.js

    Database: Supabase (PostgreSQL)

    ID Standard: UUID v7

    Date Standard: ISO 8601 (UTC)

🚀 Deployment

The API is optimized for serverless environments.

    Ensure .env contains SUPABASE_URL and SUPABASE_ANON_KEY.

    Run npm install.

    Run node seed.js to populate the 2026 required profiles.

    Start with npm start.

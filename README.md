## Natural Language Parsing Approach

My system uses a rule-based RegEx parser to transform plain English queries into structured database filters.

### Supported Keywords & Mappings

- **Genders:** "male", "female", "men", "women" -> maps to `gender`
- **Age Groups:** "child", "teenager", "adult", "senior" -> maps to `age_group`
- **Young:** "young" -> maps to `min_age=16` and `max_age=24`
- **Comparison:** "above [X]", "older than [X]" -> maps to `gte.age`
- **Countries:** Detects 50+ country names (e.g., "nigeria", "kenya") -> maps to `country_id`

### Limitations

- Does not support complex intent like "everyone except males".
- Multiple conflicting age groups (e.g., "adult teenager") will default to the last keyword found.
- If both "male" and "female" are mentioned in the same query, the gender filter is ignored to show all results.

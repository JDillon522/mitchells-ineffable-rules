# IR-paren-same-op

Unnecessary parentheses around homogeneous logical conditions should be removed, while required CHECK constraint parentheses are preserved.

- **Auto-Fixable**: Yes
- **Enabled by Default**: Yes
- **Category**: Query Structure Rules
- **Commit Profile**: Yes
- **Intentional Semantic Rewrite**: Yes
- **MyBatis Safe**: Yes
- **Trellis Safe**: No
- **Configuration Options**:
  - `enabled`: `true`

#### ❌ Violating Example
```sql
SELECT id FROM users WHERE (active = true AND type = 'admin' AND age > 21);
```

####  Correct Example
```sql
SELECT id FROM users WHERE active = true AND type = 'admin' AND age > 21;
```

#### Additional Validations
```sql
SELECT id FROM users WHERE (active = true AND type = 'admin') OR age > 21;
```

```sql
SELECT id FROM users WHERE active = true AND (type = 'admin' OR age > 21);
```

```sql
SELECT id FROM users WHERE (active = true);
```

```sql
SELECT count(*) FILTER (WHERE active AND visible) FROM users;
```

```sql
SELECT id FROM users WHERE NOT (active AND visible);
```

```sql
CREATE TABLE sample_item (amount NUMERIC CHECK (amount >= 0 AND amount < 100));
```

```sql
CREATE TABLE sample_item (CHECK (enabled OR visible));
```

```sql
ALTER TABLE sample_item ADD CONSTRAINT valid_amount CHECK (amount > 0 AND amount < 100) NOT VALID;
```

```sql
CREATE DOMAIN positive_amount AS NUMERIC CHECK (VALUE > 0 AND VALUE < 100);
```

```sql
CREATE TABLE sample_item (CHECK /* retain */ (NOT empty(shape) AND valid(shape)));
```

```sql
CREATE TABLE sample_item (CHECK ((kind = 'point' AND is_point) OR (kind = 'area' AND is_area)));
```

# IR-line-length

Lines must not exceed the configured maximum length. Overlong keyword-owned IN, VALUES, and TABLE lists wrap one item per line, OPTIONS and LIMIT TO lists expand, and long constraints and indexes wrap at schema-clause boundaries. Large INSERT data dumps remain compact, including multi-row VALUES lists. Unrelated SQL and comments remain checked and formatted. Literal data that cannot be wrapped without changing its value is reported as nonfixable.

- **Auto-Fixable**: Sometimes
- **Enabled by Default**: Yes
- **Category**: General Rules
- **Commit Profile**: Yes
- **MyBatis Safe**: Yes
- **Trellis Safe**: No
- **Configuration Options**:
  - `enabled` (Default: `true`): Enable or disable this rule.
  - `max_length` (Default: `120`): Maximum line length limit.
  - `base_indent` (Default: `0`): Base indentation offset (in spaces or leading space string) to subtract before checking line lengths. *Note: Value dynamically inherited from rule [`IR-indent`](../general/IR-indent.md) -> `base_indent` if not configured.*
  - `bulk_insert_threshold` (Default: `100`): Number of inserted VALUES rows across statements that marks a file as a bulk data dump; use 0 to disable the exemption.

#### ❌ Violating Example
```sql
-- This is a very long comment line that exceeds the maximum line length limit of 120 characters to demonstrate how the comment wrapping works.
```

####  Correct Example
```sql
-- This is a very long comment line that exceeds the maximum line length limit of 120 characters to demonstrate how the
-- comment wrapping works.
```

#### Additional Validations
```sql
INSERT INTO sample_item (item_id, name) VALUES (1, 'first'), (2, 'second');
```

Rather than adding `sys.path.insert` to every script you write, add this to `pyproject.toml`:

toml

```toml
[tool.uv]
package = true
```

Then reinstall:

bash

```bash
uv sync
```



import sys
from pathlib import Path
sys.path.insert(0, str(Path(__file__).resolve().parents[1]))

from backend.core.database import SessionLocal
from backend.models.category import Category

DEFAULT_CATEGORIES = [
    "Food & Dining",
    "Transport",
    "Housing & Utilities",
    "Entertainment",
    "Healthcare",
    "Shopping",
    "Savings & Investment",
    "Income",
    "Other",
]

def seed(db=None):
    close_after = False
    if db is None:
        db = SessionLocal()
        close_after = True

    for name in DEFAULT_CATEGORIES:
        exists = db.query(Category).filter_by(name=name).first()
        if not exists:
            db.add(Category(name=name, is_system=True))
    db.commit()

    if close_after:
        db.close()
        print("Categories seeded.")


if __name__ == "__main__":
    seed()
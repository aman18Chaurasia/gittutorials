# 🧠 ToDo
# 🧠 Flask CRUD API – Developer Notes

This README summarizes key concepts, corrections, and best practices learned while building a Flask-based CRUD (To-Do) API. Ideal for revision, interviews, or quick reference.

---

## 📦 CRUD Endpoints Overview

| Method   | Route              | Action    | Description                      |
|----------|--------------------|-----------|----------------------------------|
| `GET`    | `/items` or `/items/<id>` | Read      | Get all items or specific item   |
| `POST`   | `/items`           | Create    | Add a new item (JSON body)       |
| `PUT`    | `/items/<id>`      | Update    | Update an existing item          |
| `DELETE` | `/items/<id>`      | Delete    | Remove an item by ID             |

---

## ❌ Common Mistakes & ✅ Corrections

| ❌ Mistake                             | ✅ Correction                        |
|----------------------------------------|--------------------------------------|
| `/items<int:item_id>` (missing `/`)    | Use `/items/<int:item_id>`           |
| `.get('aman', ...)`                    | Use `.get('name', item['name'])`     |
| Confused left/right in update          | Left = field to update, Right = value |
| List comprehension confusion           | It creates and replaces `items`      |
| JSON objects side-by-side              | Wrap in a list: `[ {...}, {...} ]`   |

---

## 🔧 Sample Code Patterns

### Safe Update (PUT)

```python
item['name'] = request.json.get('name', item['name'])
```

### Safe Delete (Without `next()`)

```python
items = [item for item in items if item['id'] != item_id]
```

### POST Item Creation

```python
if not request.json or 'name' not in request.json:
    return jsonify({"error": "Missing fields"}), 400

new_item = {
    "id": items[-1]['id'] + 1 if items else 1,
    "name": request.json['name'],
    "description": request.json['description']
}
items.append(new_item)
```

---

## ⚙️ Status Codes Reference

| Code | Meaning       | Use Case                    |
|------|---------------|-----------------------------|
| 200  | OK            | GET, PUT, DELETE success     |
| 201  | Created       | After successful POST        |
| 400  | Bad Request   | Missing/invalid data         |
| 404  | Not Found     | Item not found               |

---

## 🔮 Good Practices

- ✅ Validate `request.json` before using it.
- ✅ Use `.get()` to handle missing keys safely.
- ✅ Always return correct HTTP status codes.
- ✅ Use `next()` or filtering to find items.
- ✅ Avoid overwriting lists unless intended.

---

## 🚀 Next Steps

- Add `completed: bool` field for real To-Do logic
- Add `created_at`, `updated_at` timestamps
- Replace in-memory list with SQLite or TinyDB
- Deploy using Render, Railway, or PythonAnywhere
- Add a frontend using HTML or React

---

# 06 — Tables

---

## 📌 What are Tables?

HTML tables display **structured data** in rows and columns — like a spreadsheet.

> ⚠️ **Important:** Tables are for **data only**, not for page layouts! In the past, developers used tables for layout, but now we use CSS Flexbox and Grid.

---

## 🏗️ Basic Table Structure

```html
<table>
    <tr>
        <th>Column 1 Header</th>
        <th>Column 2 Header</th>
    </tr>
    <tr>
        <td>Row 1, Cell 1</td>
        <td>Row 1, Cell 2</td>
    </tr>
</table>
```

### Tags Explained:

| Tag | Name | Purpose |
|-----|------|---------|
| `<table>` | Table | The container for the entire table |
| `<tr>` | Table Row | A horizontal row of cells |
| `<th>` | Table Header | A header cell — **bold and centered** by default |
| `<td>` | Table Data | A regular data cell |
| `<thead>` | Table Head | Groups the header row(s) |
| `<tbody>` | Table Body | Groups the main data rows |
| `<tfoot>` | Table Footer | Groups the footer row(s) |

---

## 📊 A Complete Table Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Student Marks Table</title>
    <style>
        /* Basic table styling with CSS */
        table {
            border-collapse: collapse; /* Removes double borders */
            width: 100%;
        }
        th, td {
            border: 1px solid #ccc;   /* Adds borders to all cells */
            padding: 10px;            /* Adds space inside cells */
            text-align: left;
        }
        th {
            background-color: #4a90d9; /* Blue header */
            color: white;
        }
        tr:nth-child(even) {
            background-color: #f2f2f2; /* Alternating row colors */
        }
    </style>
</head>
<body>

    <h1>Student Results</h1>

    <table>
        <!-- Table Header Section -->
        <thead>
            <tr>
                <th>Student Name</th>
                <th>Subject</th>
                <th>Marks</th>
                <th>Grade</th>
            </tr>
        </thead>

        <!-- Table Body Section -->
        <tbody>
            <tr>
                <td>Aarav Shah</td>
                <td>Mathematics</td>
                <td>95</td>
                <td>A+</td>
            </tr>
            <tr>
                <td>Priya Thapa</td>
                <td>Science</td>
                <td>87</td>
                <td>A</td>
            </tr>
            <tr>
                <td>Rohan Karki</td>
                <td>English</td>
                <td>72</td>
                <td>B+</td>
            </tr>
        </tbody>

        <!-- Table Footer Section -->
        <tfoot>
            <tr>
                <td colspan="2"><strong>Class Average</strong></td>
                <td>84.7</td>
                <td>A</td>
            </tr>
        </tfoot>
    </table>

</body>
</html>
```

---

## 🔀 Spanning Columns and Rows

### `colspan` — Merge cells **horizontally**

```html
<tr>
    <!-- This cell spans across 3 columns -->
    <td colspan="3">This cell takes up 3 columns</td>
</tr>
```

### `rowspan` — Merge cells **vertically**

```html
<tr>
    <!-- This cell spans across 2 rows -->
    <td rowspan="2">I cover 2 rows</td>
    <td>Row 1, Col 2</td>
</tr>
<tr>
    <!-- No first cell here — it's covered by the rowspan above -->
    <td>Row 2, Col 2</td>
</tr>
```

---

## 🎨 Table Styling Tips

```css
/* Remove double borders */
table { border-collapse: collapse; }

/* Full width */
table { width: 100%; }

/* Cell spacing */
th, td { padding: 12px 15px; }

/* Striped rows for readability */
tr:nth-child(even) { background-color: #f9f9f9; }

/* Hover effect on rows */
tr:hover { background-color: #eef6ff; }
```

---

## ✅ Key Takeaways

- `<table>` contains `<tr>` rows, which contain `<th>` or `<td>` cells.
- Use `<thead>`, `<tbody>`, `<tfoot>` to organize sections.
- Use `colspan` to span columns, `rowspan` to span rows.
- Always style tables with CSS — default tables look plain.
- **Tables are for data, not layouts!**

---

> ➡️ **Next:** `07-forms.md` — Forms and input types (the most important topic for real websites).

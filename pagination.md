# Pagination

A comprehensive pagination system with navigation controls, page input, and rows-per-page selection for data tables and list views.

---

## 1. Quick start

```tsx
import {
  PaginationRoot,
  PaginationRowsPerPage,
  PaginationPageInput,
  PaginationNavigation,
} from "gends";

function Example() {
  const [currentPage, setCurrentPage] = useState(1);
  const [rowsPerPage, setRowsPerPage] = useState(10);
  const totalPages = Math.ceil(totalItems / rowsPerPage);

  return (
    <PaginationRoot>
      <PaginationRowsPerPage value={rowsPerPage} onChange={setRowsPerPage} />
      <PaginationPageInput
        currentPage={currentPage}
        totalPages={totalPages}
        onPageChange={setCurrentPage}
      />
      <PaginationNavigation
        currentPage={currentPage}
        totalPages={totalPages}
        onPageChange={setCurrentPage}
      />
    </PaginationRoot>
  );
}
```

---

## 2. Component structure

The pagination system consists of four composable components:

| Component               | Purpose                   | Features                      |
| ----------------------- | ------------------------- | ----------------------------- |
| `PaginationRoot`        | Container wrapper         | Layout and spacing            |
| `PaginationRowsPerPage` | Items per page selector   | Dropdown with preset options  |
| `PaginationPageInput`   | Page number input/display | Input field or simple display |
| `PaginationNavigation`  | Previous/next navigation  | Icon buttons with states      |

---

## 3. Rows per page selector

```tsx
// Default options (5, 10, 20, 50, 100)
<PaginationRowsPerPage
  value={rowsPerPage}
  onChange={setRowsPerPage}
/>

// Custom options
<PaginationRowsPerPage
  value={rowsPerPage}
  onChange={setRowsPerPage}
  options={[10, 25, 50, 100]}
/>
```

---

## 4. Page input variants

The page input supports two display modes:

```tsx
// Default input mode - editable input field
<PaginationPageInput
  currentPage={currentPage}
  totalPages={totalPages}
  onPageChange={setCurrentPage}
  variant="default"
/>

// Simple display mode - read-only text
<PaginationPageInput
  currentPage={currentPage}
  totalPages={totalPages}
  onPageChange={setCurrentPage}
  variant="simple"
/>
```

---

## 5. Navigation controls

```tsx
// Navigation with previous/next buttons
<PaginationNavigation
  currentPage={currentPage}
  totalPages={totalPages}
  onPageChange={setCurrentPage}
/>

// Buttons automatically disable at boundaries
// - Previous disabled when currentPage <= 1
// - Next disabled when currentPage >= totalPages
```

---

## 6. Advanced page input features

The page input includes several smart features:

```tsx
// Keyboard navigation
// - Arrow Up: Increment page
// - Arrow Down: Decrement page
// - Enter: Confirm input
// - Escape: Reset to current page

// Input validation
// - Only numeric input allowed
// - Auto-clamps to valid range (1 to totalPages)
// - Handles empty input gracefully
```

---

## 7. Full prop reference

### PaginationRoot Props

| Prop        | Type     | Description            |
| ----------- | -------- | ---------------------- |
| `className` | `string` | Additional CSS classes |

### PaginationRowsPerPage Props

| Prop       | Type                      | Default            | Description                 |
| ---------- | ------------------------- | ------------------ | --------------------------- |
| `value`    | `number`                  | -                  | Current rows per page value |
| `onChange` | `(value: number) => void` | -                  | Value change handler        |
| `options`  | `number[]`                | `[5,10,20,50,100]` | Available options           |

### PaginationPageInput Props

| Prop           | Type                     | Default     | Description           |
| -------------- | ------------------------ | ----------- | --------------------- |
| `currentPage`  | `number`                 | -           | Current active page   |
| `totalPages`   | `number`                 | -           | Total number of pages |
| `onPageChange` | `(page: number) => void` | -           | Page change handler   |
| `variant`      | `'default' \| 'simple'`  | `'default'` | Display mode          |

### PaginationNavigation Props

| Prop           | Type                     | Description           |
| -------------- | ------------------------ | --------------------- |
| `currentPage`  | `number`                 | Current active page   |
| `totalPages`   | `number`                 | Total number of pages |
| `onPageChange` | `(page: number) => void` | Page change handler   |

---

## 8. Recipes

### Basic table pagination

```tsx
function DataTable() {
  const [currentPage, setCurrentPage] = useState(1);
  const [rowsPerPage, setRowsPerPage] = useState(10);

  const totalPages = Math.ceil(data.length / rowsPerPage);
  const startIndex = (currentPage - 1) * rowsPerPage;
  const paginatedData = data.slice(startIndex, startIndex + rowsPerPage);

  return (
    <div>
      <Table data={paginatedData} />
      <PaginationRoot>
        <PaginationRowsPerPage value={rowsPerPage} onChange={setRowsPerPage} />
        <PaginationPageInput
          currentPage={currentPage}
          totalPages={totalPages}
          onPageChange={setCurrentPage}
        />
        <PaginationNavigation
          currentPage={currentPage}
          totalPages={totalPages}
          onPageChange={setCurrentPage}
        />
      </PaginationRoot>
    </div>
  );
}
```

### Simple pagination (no rows selector)

```tsx
<PaginationRoot>
  <PaginationPageInput
    currentPage={currentPage}
    totalPages={totalPages}
    onPageChange={setCurrentPage}
    variant="simple"
  />
  <PaginationNavigation
    currentPage={currentPage}
    totalPages={totalPages}
    onPageChange={setCurrentPage}
  />
</PaginationRoot>
```

### Server-side pagination

```tsx
function ServerPaginatedTable() {
  const [currentPage, setCurrentPage] = useState(1);
  const [rowsPerPage, setRowsPerPage] = useState(10);
  const { data, totalCount } = useServerData(currentPage, rowsPerPage);

  const totalPages = Math.ceil(totalCount / rowsPerPage);

  const handlePageChange = page => {
    setCurrentPage(page);
    // Server request happens automatically via useServerData
  };

  const handleRowsChange = rows => {
    setRowsPerPage(rows);
    setCurrentPage(1); // Reset to first page
  };

  return (
    <div>
      <Table data={data} />
      <PaginationRoot>
        <PaginationRowsPerPage
          value={rowsPerPage}
          onChange={handleRowsChange}
          options={[10, 25, 50]}
        />
        <PaginationPageInput
          currentPage={currentPage}
          totalPages={totalPages}
          onPageChange={handlePageChange}
        />
        <PaginationNavigation
          currentPage={currentPage}
          totalPages={totalPages}
          onPageChange={handlePageChange}
        />
      </PaginationRoot>
    </div>
  );
}
```

### Custom styled pagination

```tsx
<PaginationRoot className="bg-gray-50 p-4 rounded-lg">
  <PaginationRowsPerPage value={rowsPerPage} onChange={setRowsPerPage} className="text-sm" />
  <PaginationPageInput
    currentPage={currentPage}
    totalPages={totalPages}
    onPageChange={setCurrentPage}
    className="mx-4"
  />
  <PaginationNavigation
    currentPage={currentPage}
    totalPages={totalPages}
    onPageChange={setCurrentPage}
    className="gap-2"
  />
</PaginationRoot>
```

---

## 9. Accessibility

The Pagination components include comprehensive accessibility features:

- Keyboard navigation support for all interactive elements
- Proper ARIA labels and roles
- Focus management and visible focus indicators
- Screen reader announcements for page changes
- Disabled state handling

```tsx
// Accessibility is built-in, but you can enhance it:
<PaginationNavigation
  currentPage={currentPage}
  totalPages={totalPages}
  onPageChange={setCurrentPage}
  aria-label="Table pagination navigation"
/>
```

---

## 10. Design Tokens

The Pagination components use the following design system tokens:

**Layout:**

- Container: `flex items-center justify-between gap-4`
- Navigation gap: `gap-gd-8`
- Button size: `w-gd-24 h-gd-24`

**Typography:**

- Labels: `text-sm font-400 text-color-neutral-grey-80`
- Page input: Center-aligned text

**Form Elements:**

- Dropdown width: `w-gd-64`
- Dropdown height: `h-gd-32`
- Input width: `w-16`

**Colors:**

- Text: `text-color-neutral-grey-80`
- Borders: Based on component defaults
- Focus states: Primary color theme

**Spacing:**

- Container padding: `gap-4 whitespace-nowrap`
- Element gaps: `gap-gd-12`, `gap-2`

---

Consider using Pagination with:

- **Table** — For data tables
- **Dropdown** — For rows per page selection
- **Input** — For page number entry
- **IconButton** — For navigation controls
- **Typography** — For labels and text

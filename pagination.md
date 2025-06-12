# Pagination Component

## Overview

The Pagination component is a flexible and accessible navigation system built with Genesis Design System tokens. It provides a comprehensive set of features for navigating through paginated content with support for both top and bottom positioning, customizable page sizes, and responsive design. The component is designed for various use cases such as data tables, lists, and content pagination with complete accessibility support.

## Component API

### Pagination Props

| Prop             | Type                         | Default                | Description                                  |
| ---------------- | ---------------------------- | ---------------------- | -------------------------------------------- |
| currentPage      | `number`                     | Required               | The current page number                      |
| totalPages       | `number`                     | Required               | Total number of pages to display             |
| pageSize         | `number`                     | Required               | Number of items per page                     |
| onPageChange     | `(page: number) => void`     | Required               | Function called when page changes            |
| onPageSizeChange | `(pageSize: number) => void` | Required               | Function called when page size changes       |
| variant          | `"top" \| "bottom"`          | `"bottom"`             | Position variant of the pagination component |
| pageSizeOptions  | `number[]`                   | `[5, 10, 20, 50, 100]` | Available options for page size selection    |
| isLoading        | `boolean`                    | `false`                | Whether the component is in loading state    |
| isEmpty          | `boolean`                    | `false`                | Whether there is no data to paginate         |
| className        | `string`                     | `undefined`            | Additional CSS classes for the component     |

### Import Statement

```typescript
import { Pagination } from "gends";
```

## Basic Usage

### Default Pagination

```tsx
import { Pagination } from "gends";

function MyComponent() {
  const [currentPage, setCurrentPage] = useState(1);
  const [pageSize, setPageSize] = useState(10);
  const totalPages = 25;

  return (
    <Pagination
      currentPage={currentPage}
      totalPages={totalPages}
      pageSize={pageSize}
      onPageChange={setCurrentPage}
      onPageSizeChange={setPageSize}
    />
  );
}
```

## Variants

### Bottom Variant (Default)

```tsx
<Pagination
  variant="bottom"
  currentPage={1}
  totalPages={25}
  pageSize={10}
  onPageChange={handlePageChange}
  onPageSizeChange={handlePageSizeChange}
/>
```

The bottom variant is the default and provides:

- Full page size selector
- Page input field (desktop) or text display (mobile)
- Navigation controls
- Responsive layout adjustments

### Top Variant

```tsx
<Pagination
  variant="top"
  currentPage={1}
  totalPages={25}
  pageSize={10}
  onPageChange={handlePageChange}
  onPageSizeChange={handlePageSizeChange}
/>
```

The top variant is more streamlined and:

- Maintains page input on mobile
- Hides "Rows per page" text on mobile
- Optimized for table headers
- Compact layout

## Advanced Features

### Custom Page Size Options

```tsx
<Pagination
  currentPage={1}
  totalPages={25}
  pageSize={15}
  pageSizeOptions={[15, 30, 50, 100]}
  onPageChange={handlePageChange}
  onPageSizeChange={handlePageSizeChange}
/>
```

### Interactive State Management

```tsx
function InteractivePagination() {
  const [page, setPage] = useState(1);
  const [pageSize, setPageSize] = useState(20);
  const totalItems = 500;
  const totalPages = Math.ceil(totalItems / pageSize);

  const handlePageChange = useCallback((newPage: number) => {
    setPage(newPage);
  }, []);

  const handlePageSizeChange = useCallback((newSize: number) => {
    setPageSize(newSize);
    setPage(1); // Reset to first page when changing page size
  }, []);

  return (
    <Pagination
      currentPage={page}
      totalPages={totalPages}
      pageSize={pageSize}
      onPageChange={handlePageChange}
      onPageSizeChange={handlePageSizeChange}
    />
  );
}
```

### Loading State

```tsx
<Pagination
  currentPage={1}
  totalPages={25}
  pageSize={10}
  onPageChange={handlePageChange}
  onPageSizeChange={handlePageSizeChange}
  isLoading={true}
/>
```

### Empty State

```tsx
<Pagination
  currentPage={1}
  totalPages={0}
  pageSize={10}
  onPageChange={handlePageChange}
  onPageSizeChange={handlePageSizeChange}
  isEmpty={true}
/>
```

## Real-World Usage Examples

### Data Table Integration

```tsx
function DataTable() {
  const [page, setPage] = useState(1);
  const [pageSize, setPageSize] = useState(10);
  const [data, setData] = useState([]);
  const [totalItems, setTotalItems] = useState(0);

  useEffect(() => {
    fetchData(page, pageSize).then(response => {
      setData(response.items);
      setTotalItems(response.total);
    });
  }, [page, pageSize]);

  const totalPages = Math.ceil(totalItems / pageSize);

  return (
    <div>
      <Pagination
        variant="top"
        currentPage={page}
        totalPages={totalPages}
        pageSize={pageSize}
        onPageChange={setPage}
        onPageSizeChange={setPageSize}
      />
      <Table data={data} />
      <Pagination
        variant="bottom"
        currentPage={page}
        totalPages={totalPages}
        pageSize={pageSize}
        onPageChange={setPage}
        onPageSizeChange={setPageSize}
      />
    </div>
  );
}
```

### List View with Custom Page Sizes

```tsx
function ListView() {
  const [page, setPage] = useState(1);
  const [pageSize, setPageSize] = useState(15);
  const totalItems = 150;
  const totalPages = Math.ceil(totalItems / pageSize);

  return (
    <div>
      <List items={items.slice((page - 1) * pageSize, page * pageSize)} />
      <Pagination
        currentPage={page}
        totalPages={totalPages}
        pageSize={pageSize}
        pageSizeOptions={[15, 30, 50, 100]}
        onPageChange={setPage}
        onPageSizeChange={setPageSize}
      />
    </div>
  );
}
```

## Accessibility Features

### Keyboard Navigation

- **Focus Management**: All interactive elements are keyboard accessible
- **ARIA Attributes**: Proper roles and labels for screen readers
- **Navigation**: Arrow keys for page navigation
- **Input**: Direct page number entry with validation

### Screen Reader Support

- **ARIA Labels**: Clear identification of pagination purpose
- **Status Updates**: Dynamic updates for page changes
- **Page Information**: Clear indication of current page and total pages

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Focus Indicators**: Clear visual feedback for keyboard focus
- **Responsive Design**: Adapts to different screen sizes and zoom levels

## Design System Integration

### Genesis Design Tokens

**Typography:**

- Page Numbers: `text-en-desktop-body-s`
- Page Size Label: `text-en-desktop-body-s`

**Spacing:**

- Container: `gap-4`
- Navigation: `gap-2`
- Mobile Adjustments: `sm:gap-4`

**Layout:**

- Desktop: `flex-row items-center`
- Mobile: `flex-col items-start`

## Best Practices

### Performance

- Use debounced page changes for input fields
- Optimize page size options based on data volume
- Handle loading states appropriately

### User Experience

- Keep page size options reasonable
- Provide clear feedback for invalid inputs
- Maintain consistent positioning in the UI
- Consider mobile-first design

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Handle edge cases (empty state, loading)
- Consider data fetching patterns

## Troubleshooting

### Common Issues

**Page Number Validation:**

- Check current page bounds
- Handle invalid input gracefully
- Reset to valid page when needed

**Page Size Changes:**

- Reset to first page on size change
- Validate new page size
- Update total pages calculation

**Mobile Responsiveness:**

- Test different screen sizes
- Verify touch targets
- Check layout adjustments

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Pagination component provides a flexible and accessible way to navigate through paginated content. Choose the appropriate configuration based on your specific use case and requirements.

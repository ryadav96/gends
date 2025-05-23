# Data Table

The DataTable component is a powerful and flexible table component that supports features like sorting, pagination, row selection, column management, filtering, and more.

## Features

- Row selection with action bar
- Column management (show/hide columns)
- Sorting
- Pagination
- Header rows customization (top, middle, bottom)
- Filtering with pills
- Truncation and wrapping of cell content
- Loading state with shimmer effect
- Expandable rows with sub-tables
- Customizable row actions
- Fixed columns
- Table borders customization

## Installation

The DataTable component is part of the GenDS library. Make sure you have the required dependencies installed:

```bash
npm install @tanstack/react-table
```

## Basic Usage

Here's a basic example of how to use the DataTable component:

```tsx
import { DataTable, useDataTable } from 'gends';
import { ColumnDef } from '@tanstack/react-table';

interface TableData {
  id: number;
  name: string;
  age: number;
  email: string;
}

const columns: ColumnDef<TableData>[] = [
  { accessorKey: "id", header: "ID" },
  { accessorKey: "name", header: "Name" },
  { accessorKey: "age", header: "Age" },
  { accessorKey: "email", header: "Email" }
];

const data = [
  { id: 1, name: "John Doe", age: 30, email: "john@example.com" },
  { id: 2, name: "Jane Smith", age: 25, email: "jane@example.com" }
];

function MyTable() {
  const { table } = useDataTable<TableData>({
    data,
    columns,
    enableRowSelection: true
  });

  return <DataTable table={table} />;
}
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| table | Table<TData> | required | Table instance from useDataTable hook |
| enableRowSelection | boolean | false | Enable row selection functionality |
| showColumnDivider | boolean | false | Show vertical dividers between columns |
| showOuterBorder | boolean | false | Show outer border of the table |
| tableHeight | string | undefined | Set a fixed height for the table with scrolling |
| emptyStateHeight | string | "200px" | Height of empty state message |
| stickyFooter | boolean | true | Make the footer sticky |
| showTableFooter | boolean | false | Show the table footer |
| truncateAll | boolean | false | Truncate content in all columns |
| truncateColumns | string[] | [] | Array of column IDs to truncate |
| wrapAll | boolean | true | Enable text wrapping for all columns |
| wrapColumns | string[] | [] | Array of column IDs to enable text wrapping |
| isLoading | boolean | false | Show loading state with shimmer effect |
| shimmerRowCount | number | 5 | Number of shimmer rows to show while loading |

## Advanced Usage

### 1. Row Selection with Action Bar

```tsx
function AdvancedTable() {
  const { table } = useDataTable<TableData>({
    data,
    columns,
    enableRowSelection: true
  });

  return (
    <DataTable table={table}>
      <DataTableActionBar table={table}>
        <DataTableActionBarSelection table={table} />
        <DataTableActionBarAction
          tooltip="Delete rows"
          onClick={() => console.log("Delete", selectedRows)}
        >
          <TrashIcon />
          <span>Delete</span>
        </DataTableActionBarAction>
        <DataTableActionBarOverflow
          items={[
            {
              label: "Export CSV",
              onClick: () => console.log("Export CSV")
            },
            {
              label: "Mark as Read",
              onClick: () => console.log("Mark as Read")
            }
          ]}
        />
      </DataTableActionBar>
    </DataTable>
  );
}
```

### 2. Custom Header Rows with Tabs and Filters

```tsx
<DataTable
  table={table}
  headerTopRow={
    <div className="border-b bg-white px-4">
      <div className="flex justify-between items-center">
        <div className="w-[60%]">
          <TabsRow table={table} items={mainTabItems} size="l" />
        </div>
        <div className="w-[30%] min-w-[200px] flex items-center justify-end gap-3">
          <SearchBar size="s" hideDropdown />
          <ColumnManagerDropdown table={table} />
        </div>
      </div>
    </div>
  }
  showHeaderTopRow
  headerMiddleRow={
    <div className="border-b bg-white">
      <FilterPills
        options={filterOptions}
        onChange={onFilterPillChange}
        onClearAll={onClearAll}
        onMoreOptionChange={onMoreOptionChange}
        moreFilterOptions={moreFilterOptions}
      />
    </div>
  }
  showHeaderMiddleRow
/>
```

### 3. Pagination

```tsx
<DataTable
  table={table}
  showTableFooter
  tableFooter={
    <Pagination
      currentPage={currentPage}
      totalPages={totalPages}
      pageSize={pageSize}
      onPageChange={setPage}
      onPageSizeChange={setPageSize}
      className="w-full"
    />
  }
/>
```

### 4. Content Truncation and Wrapping

```tsx
<DataTable
  table={table}
  // Truncate specific columns
  truncateColumns={["description", "longText"]}
  // Or truncate all columns
  truncateAll={true}
  // Enable wrapping for specific columns
  wrapColumns={["content"]}
  // Or enable wrapping for all columns
  wrapAll={true}
/>
```

### 5. Loading State

```tsx
<DataTable
  table={table}
  isLoading={isLoading}
  shimmerRowCount={10}
/>
```

## Action Bar Customization

The DataTableActionBar provides a flexible way to add actions for selected rows. It appears at the bottom of the screen when rows are selected.

### Available Action Bar Components

1. `DataTableActionBarSelection`: Shows selection count and clear selection button
2. `DataTableActionBarAction`: Individual action buttons with tooltips
3. `DataTableActionBarOverflow`: Dropdown menu for additional actions
4. `ActionBarRowMovementControls`: Controls for moving rows up/down

### Example with All Action Bar Features

```tsx
<DataTable table={table}>
  <DataTableActionBar table={table}>
    {/* Selection info and clear button */}
    <DataTableActionBarSelection table={table} />
    
    {/* Row movement controls */}
    <ActionBarRowMovementControls table={table} />
    
    {/* Primary actions */}
    <DataTableActionBarAction
      tooltip="Archive selected items"
      onClick={handleArchive}
      isPending={isArchiving}
    >
      <ArchiveIcon className="w-gd-18 h-gd-18" />
      <span>Archive</span>
    </DataTableActionBarAction>
    
    <DataTableActionBarAction
      tooltip="Delete selected items"
      onClick={handleDelete}
      isPending={isDeleting}
    >
      <TrashIcon className="w-gd-18 h-gd-18" />
      <span>Delete</span>
    </DataTableActionBarAction>
    
    {/* Overflow menu for additional actions */}
    <DataTableActionBarOverflow
      items={[
        {
          label: "Export as CSV",
          onClick: handleExport,
          icon: <ExportIcon />
        },
        {
          label: "Print selected",
          onClick: handlePrint,
          icon: <PrintIcon />
        }
      ]}
    />
  </DataTableActionBar>
</DataTable>
```

## Events and Callbacks

The DataTable component exposes several events through the table instance:

| Event | Description |
|-------|-------------|
| onSortingChange | Called when column sorting changes |
| onPaginationChange | Called when page or page size changes |
| onColumnVisibilityChange | Called when columns are shown/hidden |
| onRowSelectionChange | Called when row selection changes |
| onExpandedChange | Called when rows are expanded/collapsed |

Example of handling events:

```tsx
const { table } = useDataTable<TableData>({
  data,
  columns,
  onSortingChange: (sorting) => {
    console.log('New sorting:', sorting);
  },
  onPaginationChange: (pagination) => {
    console.log('New pagination:', pagination);
  },
  onRowSelectionChange: (selectedRows) => {
    console.log('Selected rows:', selectedRows);
  }
});
```

## Best Practices

1. Always provide a unique `localStorageKey` when using `ColumnManagerDropdown` to avoid conflicts between different table instances.
2. Use the reserved keys `ROW_SELECT` and `ROW_EXPAND` properly for row selection and expansion columns.
3. The `COLUMN_ACTIONS` key is reserved for fixed column actions.
4. Implement proper error handling and loading states.
5. Consider mobile responsiveness when designing table layouts.
6. Use appropriate truncation and wrapping strategies for different types of content.

## Customization

The DataTable component can be customized using CSS classes and through various prop combinations. The component uses Tailwind CSS for styling, making it easy to override styles when needed.

## Accessibility

The DataTable component follows accessibility best practices:
- Proper ARIA attributes for interactive elements
- Keyboard navigation support
- Screen reader-friendly markup
- Clear focus indicators